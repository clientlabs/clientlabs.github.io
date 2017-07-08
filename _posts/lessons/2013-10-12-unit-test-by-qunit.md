---
layout: post
category: lessons
title: 在javascript项目中使用QUint进行单元测试
tagline: javascript中的单元测试
tags : [开发工具, 单元测试]
---
{% include JB/setup %}

## QUnit的简介 ##

> 本文只介绍[Qunit](http://qunitjs.com/)的使用，不再介绍单元测试框架的选型过程。

QUnit的官网介绍：

QUnit is a powerful, easy-to-use JavaScript unit testing framework. 

QUnit是一个强大的、简单易用的javascript单元测试框架。

### 下载QUnit ###

可以到[QUnit官网(http://qunitjs.com)](http://qunitjs.com/)上下载qunit.js和qunit.css两个文件。

虽然有[jQuery CDN(http://code.jquery.com/)](http://code.jquery.com/)和[GitHub托管(https://github.com/jquery/qunit)](https://github.com/jquery/qunit)的代码可用，但是为了稳定，还是下载了使用吧。

### QUnit上手应用 ###

> 以下的代码示例直接使用QUnit官网首页的示例。

QUnit单元测试的HTML页面代码示例：

	<!DOCTYPE html>
	<html>
	<head>
	  <meta charset="utf-8">
	  <title>QUnit Example</title>
	  <link rel="stylesheet" href="/resources/qunit.css">
	</head>
	<body>
	  <div id="qunit"></div>
	  <div id="qunit-fixture"></div>
	  <script src="/resources/qunit.js"></script>
	  <script src="/resources/tests.js"></script>
	</body>
	</html>

tests.js中的示例代码：

	test( "hello test", function() {
	  ok( 1 == "1", "Passed!" );
	});

## QUnit的常用API ##

> 断言是单元测试中最常用、最核心的概念，就是在测试的时候，对代码的运行结果作出的一些假设。如果断言成立，就说单元测试通过，反之则视为测试失败。

### 测试方法和模块 ###

最常用的测试代码，示例如下：

	test("该测试用例的主题", function(){/*- 具体的测试断言 -*/});

当测试用例较多时，可以用module()方法进行分组。示例如下：

	module( "测试分组一" );
	test( "测试方法1", function() {});
	test( "测试方法2", function() {});
	 
	module( "测试分组二" );
	test( "测试方法3", function() {});
	test( "测试方法4", function() {});

在测试结果HTML页面上，会以 `测试分组一：测试方法1` 的形式呈现。

### QUnit支持的断言 ###

> 一个测试方法只有一个断言是个好习惯。只是好习惯哦！

一目了然，**ok和equal是最常用的**。

- ok( state, message ) ： 真假断言，state为true则通过。
- equal( actual, expected, message ) ： 相等断言，actual和expected相等（==）则通过。
- notEqual( actual, expected, message ) ： 不等断言，actual和expected不相等（!=）则通过。
- deepEqual( actual, expected, message ) ： 递归相等断言，actual和expected全相等（包括其子元素都相等，适用于基本类型，数组和对象）则通过。
- notDeepEqual( actual, expected, message ) ： 递归不相等断言，actual和expected不全相等（包括其子元素都相等，适用于基本类型，数组和对象）则通过。
- strictEqual( actual, expected, message ) ： 全相等断言，actual和expected全相等（===）则通过。
- notStrictEqual( actual, expected, message ) ： 不全相等断言，actual和expected不全相等（===）则通过。
- raises( block, expected, message ) ： 异常断言，block中抛出异常则通过，expected为可选参数，是所期待抛出异常名的正则表达式。

## 与Grunt构建工具的集成 ##

> Grunt构建工具的安装和使用，关于参考教程[《Grunt的安装和使用》](http://clientlab.github.io/lessons/2013/10/15/installation-and-use-of-grunt/)

### QUnit的Grunt任务 ###

QUnit Grunt任务(grunt-contrib-qunit)的使用，请参见GitHub上的说明[https://github.com/gruntjs/grunt-contrib-qunit](https://github.com/gruntjs/grunt-contrib-qunit)

使用QUint作单元测试，PhantomJS是必须要安装的。

### 安装PhantomJS ###

> [PhantomJS(http://phantomjs.org/)](http://phantomjs.org/) 是一个无界面的WebKit浏览器引擎，还有配套的JavaScript API。它原生支持各种web标准技术：DOM处理，CSS选择器，JSON，Canvas，以及SVG。
。

可以在命令行中使用以下的命令进行安装：

	npm install phantomjs -g

> 参考：[https://npmjs.org/package/phantomjs](https://npmjs.org/package/phantomjs)

## 参考资料 ##

- [JQuery团队打造的javascript单元测试工具QUnit介绍](http://www.cnblogs.com/nuaalfm/archive/2010/02/26/1674235.html)
- [DalekJS – 基于 JavaScript 实现跨浏览器的自动化测试](http://www.tuicool.com/articles/JVRRbq)
- [高效 JavaScript 单元测试](http://www.ibm.com/developerworks/cn/opensource/os-jstesting/)
- [JavaScript的单元测试工具](http://select.yeeyan.org/view/213582/265887)
- [虚拟座谈：JavaScript单元测试现状](http://www.infoq.com/cn/articles/javascript-unit-testing)
- [javascript单元测试](http://www.cnblogs.com/frostbelt/archive/2012/08/03/2622302.html)
- [Node.js 官网(http://nodejs.org)](http://nodejs.org)
- [QUnit 官网](http://qunitjs.com/) - [GitHub](https://github.com/jquery/qunit)
- [Grunt 官网](http://www.gruntjs.com) - [[GitHub](https://github.com/gruntjs/)] [[中文文档](http://www.gruntjs.org/)]
- [PhantomJS官网(http://phantomjs.org)](http://phantomjs.org)
