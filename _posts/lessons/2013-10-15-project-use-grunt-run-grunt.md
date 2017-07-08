---
layout: post
category: lessons
title: 使用grunt-run-grunt插件组织团队的开发
tagline: 使用grunt-run-grunt插件组织团队的开发
tags : [Grunt插件, 项目组织]
---
{% include JB/setup %}

## 项目构建的需求 ##

在组织项目的开发工作时，如果构建工具选型是Grunt，那么常常有以下几个需求：

1. Gruntfile文件随着项目复杂性的增加，会变的越来越庞大。为了便于开发团队的分工协作，需要在某种程度上分拆Gruntfile，让不同的团队、不同的开发者关注不同的部分。
2. 把Gruntfile分拆成不同的文件后，既要有统一的入口执行整体的构建，又要能够使分拆后的Gruntfile不依赖于其他部分独立构建，以确保团队分工的互不干扰。
3. 在整个项目中，package.json和node_modules要能够共用。确保每一部分的开发者，只关注Gruntfile的编写，不需要关注全局共性的package.json和node_modules。

不同的团队、 不同的项目因为细化需求的不同，都会各自选择不同的解决方案。

## Gruntfile的分拆方案 ##

### Gruntfile文件内的逻辑分组 ###

使用任务的目标名称，在逻辑上分组构建任务。这是大多数项目最初会用到的方法，如[grunt中文文档项目(https://github.com/basestyle/grunt-cn)](https://github.com/basestyle/grunt-cn)。

在传递给grunt.initConfig方法的对象中，使用如下类似的不同任务目标名称区分webapp和pc两类任务：

	jshint:{
		webapp: ['app/www/js/main.js'],
		pc: ['js/chart.js','js/common.js','js/demand.js','js/dialog.js','js/formbeautify.js','js/jquery.autopagination.js',
			'js/jquery.cascadeselect.js','js/jquery.datepicker.js','js/jquery.formvalid.js','js/jquery.memberinput.js',
			'js/jquery.multiupload.js','js/jquery.tabs.js','js/pmstation.js','js/project.js','js/setting.js','js/tasktable.js','js/work.js']
	},

在自定义的别名任务中，把两类任务分组成webapp和pc两个单任务：

	grunt.registerTask('webapp', ['htmlhint:webapp','jshint:webapp','uglify:webapp','cssmin:webapp','copy:webapp','replace:webapp']);
	grunt.registerTask('pc', ['jshint:pc','uglify:pc','cssmin:pc','copy:pc','replace:pc']);

如果两类任务调用的任务都相同，也可以使用动态别名任务的方法来处理。

代码示例如下：

	grunt.registerTask('build', 'Run all my build tasks.', function(n) {
	  if (n == null) {
	    grunt.warn('Build num must be specified, like build:001.');
	  }
	  grunt.task.run('foo:' + n, 'bar:' + n, 'baz:' + n);
	});

参见Grunt文档的《常见问题-"动态"别名任务》([中文](http://www.gruntjs.org/article/frequently_asked_questions.html)/[英文](http://gruntjs.com/frequently-asked-questions))。


### Grunt配置编程处理在不同的文件中 ###

将配置对象分拆出来，然后在Gruntfile.js中require进来，再将这些不同任务的对象组合成一个对象传递给grunt.initConfig。

上述方案是在我提出问题（[有没有分拆Gruntfile.js的方案？(https://github.com/basestyle/grunt-cn/issues/34)](https://github.com/basestyle/grunt-cn/issues/34)）后，[TooBug](http://www.toobug.net)[[GitHub](https://github.com/TooBug)]和[Vincent Hou](https://github.com/qivhou)给出的解决方案。

因为没有进一步展开，所以没有示例代码。

### 使用自定义任务把构建任务分解在不同的文件中 ###

我在知乎上提出问题《[有什么方案可以把较为庞大的gruntfile分拆？(http://www.zhihu.com/question/21766711)](http://www.zhihu.com/question/21766711)》后,[墨磊](http://morlay.tla42.org/)[[GitHub](https://github.com/morlay)]给出的解决方案，基本上就是使用自定义任务把构建任务分解在不同的文件中的。

比如，在[gruntjs.com(https://github.com/gruntjs/gruntjs.com)](https://github.com/gruntjs/gruntjs.com)项目中，也是通过把blog、docs等任务从Gruntfile中分拆出来的。

代码示例如下：

	// Load local tasks
	grunt.loadTasks('tasks'); // getWiki, docs tasks
	
	grunt.registerTask('build', ['clean', 'copy', 'jade', 'docs', 'blog', 'plugins', 'concat']);

上例中的docs、blog任务就是放在tasks目录下，使用grunt.loadTasks方法统一加载的。

## 选择grunt-run-grunt插件 ##

前文的所述的几个方案，用于分拆Gruntfile虽然很不错，但是并不能解决最初提出的后两个需求：

- 分拆后的Gruntfile，能够不依赖于其他部分的独立构建。
- package.json和node_modules要能够共用。

我发现[grunt-run-grunt(https://github.com/Bartvds/grunt-run-grunt)](https://github.com/Bartvds/grunt-run-grunt)插件可以同时满足这三个需求。

很遗憾的是，这个插件关注的人不多，Fork的人也不多。或许其他的开发团队有更高明的方案也说不一定，还需要继续跟进。

## 项目的组织方案 ##

在选型定案使用grunt-run-grunt插件以后，项目的组织就确定了。

入口Gruntfile的代码示例：

    run_grunt:{
      options: {
        'base': require('path').resolve('.')
      },
      main:{
        src: ['src/pro/a.Gruntfile.js', 'src/frameworks/b.lib.Gruntfile.js', 'src/frameworks/c.lib.Gruntfile.js']        
      }
    }

需要特别注意的是，options中的base配置是指整个项目所有的Gruntfile都是以这个入口Gruntfile所在的目录为base目录的。

这个扩展机制可以在options中配置最终传递给grunt的命令行参数，属性名是命令行参数名，属性值是命令行参数的值。

上例配置的意义是要求执行类似如下样式的Grunt命令：

	grunt --base e:/dev/

各部分的Gruntfile与正常的Gruntfile没有什么区别。唯一的区别就是，这个方案把所有的Gruntfile的base目录设定为入口Gruntfile所在的目录。

比如，src/pro/a.Gruntfile.js中的代码示例如下：

    concat: {
      "pro: {
        src: [
          "src/frameworks/b.lib.js",
          "src/frameworks/c.lib.js",
          "src/pro/a.js"
        ],
        dest: "dist/pro/a.js"
      }
	}

示例中，不管是src目录，还是dest目录，都是以入口Gruntfile目录为基准的。

当然，base目录不这样安排是最简单的，在入口Gruntfile的run_grunt任务中不配置base就可以了。如此以来，所有的Gruntfile中的目录都是以本Gruntfile所在目录为base目录的。