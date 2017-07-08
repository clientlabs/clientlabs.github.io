---
layout: post
category: lessons
title: Grunt的安装和使用
tagline: Grunt的安装和使用
tags : [开发工具, Grunt, 自动构建]
---
{% include JB/setup %}

## 安装Grunt前的准备 ##

> 本教程的内容较少原创，多从其他文档上摘录，详见参考资料部分。

Grunt是一个自动化的项目构建工具。Grunt和Grunt的插件都是通过Node.js的包管理器npm来安装和管理的。

如果还没有安装Node.js，需要先从[Node.js网站(http://nodejs.org/)](http://nodejs.org/)下载安装。

> Node.js安装中，以及后继的其他安装中，可能需要系统管理员权限。

> 安装Grunt之前，可以在命令行中运行`node -v`查看你的Node.js版本。0.8.0及以上版本的Node.js才能很好的运行Grunt。


## 安装Grunt的命令行接口 ##

为了方便使用Grunt，你应该在全局范围内安装Grunt的命令行接口(CLI)。

在命令行中，执行如下命令：

	npm install -g grunt-cli

这条命令将会把grunt命令植入到你的系统路径中，这样就允许你从任意目录来运行它(定位到任意目录运行grunt命令)。

## 认识Grunt的两个常用文件 ##

使用Grunt构建的项目中，大多包含有package.json和Gruntfile。

**package.json**：用于存储已经作为npm模块发布的项目元数据(也就是依赖模块，包括Grunt本身)。

**Gruntfile.js**：用于配置或者定义Grunt任务和加载Grunt插件。

## 用一个现有的Grunt项目进行工作 ##

如果已经安装好了Grunt的命令行接口(CLI)，并且项目中已经有了package.json和Gruntfile，使用Grunt进行工作是非常容易的。

### 安装Grunt和相关Grunt插件 ###

1. 进入项目目录(在命令行窗口定位到项目目录；在windows系统下，也可以进入项目文件夹后，按Shift+鼠标右键，打开右键菜单，选择“在此处打开命令窗口(W)”)。
2. 在命令行中，运行 `npm install`，安装项目相关依赖(插件，Grunt内置任务等依赖)。

> 有些Grunt插件，比如JSDoc3插件，需要在命令行中可以执行git命令。最好先安装一个msysgit(http://msysgit.github.io/)，然后在环境变量中增加git的bin目录。

### 执行Grunt构建 ###

在上述的命令行中执行 `grunt`，就可以运行Grunt构建了。

> 至此，通过安装Node.js、在命令行中运行 `npm install -g grunt-cli`、`npm install` 和 `grunt`三个命令，就完成了使用现有的Grunt项目进行工作的所有准备。

## 准备一个新的Grunt项目 ##

### 快速工作的项目脚手架 ###

有很多项目的结构和内容都很类似，人们就设计开发了可以快速工作的模板，能够通过模板迅速的自动创建项目，称为脚手架工具（`grunt-init`）。

在Grunt的GitHub主页（[https://github.com/gruntjs](https://github.com/gruntjs)）上有很多之用的 `grunt-init-*` 脚本架模板工具，比如grunt-init-jquery、grunt-init-gruntplugin等等。

#### 安装grunt-init ####

`grunt-init` 是一个用于自动创建项目的脚手架工具。

先在命令行中进行全局安装：

	npm install -g grunt-init

这样，会把grunt-init命令植入到你的系统路径，从而允许你在任何目录中都可以运行它。

#### 安装和使用grunt-init模板 ####

把需要的模板放在你的 `~/.grunt-init/` 目录中（在Windows平台是%USERPROFILE%/.grunt-init目录）。

> `%USERPROFILE%` 一般是指“C:\Users\你的用户名”这个目录。

建议使用如下的git clone命令把这个模板克隆到该目录：

	git clone https://github.com/clientlab/grunt-init-gruntfile.git ~/.grunt-init/gruntfile

在Windows平台上稍微有些不方便，但是可以在文件浏览器中输入%USERPROFILE%，定义到该目录下，然后执行如下命令：

	git clone https://github.com/clientlab/grunt-init-gruntfile.git ./.grunt-init/gruntfile

> 要想使用上述命令，需要先安装一个msysgit(http://msysgit.github.io/)，然后在环境变量中增加git的bin目录。

最终的文件目录结构，如下：

	.grunt-init/
	.grunt-init/gruntfile/
	.grunt-init/gruntfile/README.md
	.grunt-init/gruntfile/template.js
	.grunt-init/gruntfile/root/

然后进入一个准备开发项目的空目录，按Shift+鼠标右键，打开右键菜单，选择“在此处打开命令窗口(W)”，打开命令行，执行如下程序：

	grunt-init gruntfile

> 请注意，此模板将在当前目录中生成文件，如果你不想覆盖现有文件，一定要使用一个新的空目录。

## 参考资料 ##
- [Node.js 官网(http://nodejs.org)](http://nodejs.org)
- [Grunt 官网](http://www.gruntjs.com) - [[GitHub](https://github.com/gruntjs/)] [[中文文档](http://www.gruntjs.org/)]
- [git工具的安装](http://windows.github.com/)
- [其他常用 grunt-init 模板](https://github.com/gruntjs/)
- [grunt-init 自定义模板开发](http://www.gruntjs.org/article/project_scaffolding.html)