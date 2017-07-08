---
layout: post
category: lessons
title: 使用JSDoc3生成javascript项目的API文档
tagline: 使用JSDoc3生成javascript项目的API文档
tags : [开发工具]
---
{% include JB/setup %}

## JSDoc样式的注释 ##

> 选用JSDoc3作为注释规范，文档生成工具使用grunt-jsdoc，本文不再介绍选型过程和原因。对JSDoc3的深入学习使用，可以参考[入口教程http://usejsdoc.org/index.html](http://usejsdoc.org/index.html)。

JSDoc注释的样式如下例，与单行注释 `//` 和多行注释 `/**/` 不同，而是类似于JAVA的JDoc和PHP的PHPDoc。

    /**
    * JSDoc注释。
    */

## JSDoc的常用标签 ##

### 函数注释示例 ###

	/**
	* 函数注释的示例。
	* @param {Integer} augend 被加数。
	* @param {Integer} addend 加数。
	* @return {Integer} 两数之和。
	* @example
	* add(1, 2) => 3
	*/
	function add(augend, addend){
		return augend + addend;
	}


### 参数注释 ###

`@param` 用于对函数、类的方法的参数进行注释，是JSDoc中最常用的注释标签。

`@param` 注释必须指定一个参数名，也可以有一个用大括号括起来的参数类型，以及参数的描述信息。参数类型可以是javascript内置的数据类型，如Array、Boolean、Date、Function、Number Object 、String 等，还可以是其他JSDoc所支持的（英文没看太懂，以后用到再认真学习）。

> The parameter type can be a built-in JavaScript type, such as string or Object, or a JSDoc namepath to another symbol in your code. If you have written documentation for the symbol at that namepath, JSDoc will automatically link to the documentation for that symbol. You can also use a type expression to indicate, for example, that a parameter is not nullable or can accept any type; see the @type documentation for details.

下面直接使用[http://usejsdoc.org/tags-param.html](http://usejsdoc.org/tags-param.html)文档中的例子，说明 `@param` 标签中如何使用参数名、参数类型和参数描述信息。

只有参数名的注释：

	/**
	 * @param somebody
	 */
	function sayHello(somebody) {
	    alert('Hello ' + somebody);
	}

包括参数名和参数类型的注释：

	/**
	 * @param {string} somebody
	 */
	function sayHello(somebody) {
	    alert('Hello ' + somebody);
	}

包括参数名、参数类型和参数描述的注释：

	/**
	 * @param {string} somebody Somebody's name.
	 */
	function sayHello(somebody) {
	    alert('Hello ' + somebody);
	}

### 返回值注释 ###

`@return` 说明函数的返回值。例如：

- `@return {Number}`
- `@return {Number} Sum of a and b`
- `@return {Number|Array} Sum of a and b or an array that contains a, b and the sum of a and b.`

> 参见：[http://usejsdoc.org/tags-returns.html](http://usejsdoc.org/tags-returns.html)

### 模块注释 ###

`@module`标签用于标记当前代码文件属于哪个模块。

在 `@link` 或 `@see` 标签中，使用 `module:moduleName` 可以链接到一个模块。例如，使用 `{@link module:foo/bar}`，可以链接到由 `"@module foo/bar` 定义的模块。

如果没有提供模块名，将使用模块文件所在路径及文件名作模块名。

### 参考引用注释 ###

` @see` 标签可以指向一个相关的引用。示例如下：

	/**
	 * Both of these will link to the bar function.
	 * @see {@link bar}
	 * @see bar
	 */
	function foo() {}
	
	// Use the inline {@link} tag to include a link within a free-form description.
	/**
	 * @see {@link foo} for further information.
	 * @see {@link http://github.com|GitHub}
	 */
	function bar() {}

### 类的注释 ###

- `@name` ：类名称
- `@class` ：类描述
- `@constructor` ：表明这是一个构造函数，非常重要。
- `@extends`	:类继承的父类。
- `@type`	：数据的类型，主要用来注释属性。
- `@default`	：默认值，主要用来注释属性。
- `@abstract` 标明一个成员是抽象的，需要子类去实现。
- `@public`、`@protected`、`@private`：类、方法或属性的访问权限

### 类的注释示例 ###

要把JSDoc3的注释生成API类库文档，`@lends` 是个很要紧的标签。

例如，`@lends Sample.prototype` 表示下面的对象归属于Sample。

较详尽的使用说明参见[http://usejsdoc.org/tags-lends.html](http://usejsdoc.org/tags-lends.html)。

有关类的定义和注释示例，如下：

	/**
	* @name Sample
	* @class 示例类
	* @public
	* @constructor
	*/
	function Sample(){
		this.something = [];
	}

	Sample.prototype = 
	/** @lends Sample.prototype*/
	{
		/**
		* 属性示例。
		* @private
		* @type {Array}
		* @default []
		*/
		something : [],

		/**
		* 方法示例。
		* @public
		* @param {String} arg 跟踪方法插件。
		*/
		doSomething: function(arg){
		}
	};

### 其他常用注释 ###

- `@example`	: 示例代码。
- `@enum [<type>]`	: 一组同样类型的静态属性集合。`switch` 语句中的分支应该只使用枚举。

- `@overview	`	：对当前代码文件的描述。
- `@copyright`	：代码的版权信息。
- `@author <name> [<emailAddress>]`	：代码的作者信息。
- `@version`		：当前代码的版本。

#### README.md 是很好的 ####

如果你有为项目写说明文档的好习惯，碰巧又使用的是MarkDown格式，碰巧文件名又是README.md，那就很好了。

把README.md文件放在代码清单里边，JSDoc工具是自动为你生成API文档的首页，什么系统概况、设计需求、设计方案及版本更新记录等等的内容都可以放进来。

## Grunt自动构建的配置 ##

Grunt的安装使用，请参考教程[《Grunt的安装和使用》](http://clientlab.github.io/lessons/2013/10/15/installation-and-use-of-grunt/)。

JSDoc某些配置有git依赖， 需要在命令行中可以执行git命令。最好先安装一个msysgit(http://msysgit.github.io/)，然后在环境变量中增加git的bin目录。

在Grunt中使用JSDoc3插件的配置参考如下：

    jsdoc: {
      dist : {
          src: ['README.md', 'src/sample.js'], 
          options: {
            destination: 'api',
            template: "libs/jsdoc3/docstrap/template",
            configure: "libs/jsdoc3/docstrap/template/jsdoc.conf.json"            
          }
      }
    }

详细使用方法和参数，参考：[https://github.com/krampstudio/grunt-jsdoc-plugin](https://github.com/krampstudio/grunt-jsdoc-plugin)。

## 参考资料 ##

- [JSDoc 主页](http://usejsdoc.org/index.html) - [GitHub](https://github.com/jsdoc3/jsdoc)
- grunt-jsdoc-plugin Grunt任务插件 [NPM](https://npmjs.org/package/grunt-jsdoc) - [GitHub](https://github.com/krampstudio/grunt-jsdoc-plugin)
- [JSDoc模板docstrap](https://github.com/terryweiss/docstrap)
- [使用jsdoc生成组件API文档—jsdoc实战](http://www.36ria.com/5101)