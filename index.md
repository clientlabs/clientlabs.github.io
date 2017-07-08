---
layout: page
title: 客户端技术实验室
tagline: 学习和研究互联网客户端javascript方面的技术
---
{% include JB/setup %}

## 常用工具 ##

- [[GitHub](https://github.com/gruntjs/)] Grunt ： 一个自动化的项目构建工具 [[中文文档](http://www.gruntjs.org/)] [[英文文档](http://www.gruntjs.com/)]
- [[GitHub](https://github.com/jquery/qunit)] QUnit ：一个javascript的单元测试框架 [[QUnit官网](http://qunitjs.com/)] [[Grunt插件](https://github.com/gruntjs/grunt-contrib-qunit)]

## 常用教程 ##

- [windows下安装jekyll](http://aotee.com/windows-installation-jekyll) - [阿泉的博客](http://aotee.com/)
- [Jekyll在Windows下面中文编码问题解决方案](http://www.cnblogs.com/aleda/articles/Jekyll-in-Windows-following-Chinese-encoding-problem-solutions.html)
- [windows下本地jekyll博客搭建手记](http://blog.jsfor.com/skill/2013/09/07/jekyll-local-structures-notes/)

## 学习项目 ##

- [[GitHub](https://github.com/clientlab/advertisement)] advertisement ： 学习和研究广告投放系统的前端技术
- [[GitHub](https://github.com/clientlab/analytics)] analytics ： 学习和研究监测分析系统的前端技术

## 工具项目 ##

- [[GitHub](https://github.com/clientlab/grunt-clientlab-filter)] grunt-clientlab-filter ： 执行查找替换指定占位符的GRUNT任务
- [[GitHub](https://github.com/clientlab/grunt-init-gruntfile)] grunt-init-gruntfile ： 使用grunt-init命令创建Client Lab常用的Gruntfile
- [[GitHub](https://github.com/Bartvds/grunt-run-grunt)] [grunt-run-grunt](https://github.com/clientlab/grunt-run-grunt) ： 当前组织首页使用的博客引擎

## 参考项目 ##

- [[GitHub](https://github.com/mojombo/jekyll)] [jekyll](https://github.com/clientlab/jekyll) ： 当前组织首页使用的博客引擎
- [[GitHub](https://github.com/plusjade/jekyll-bootstrap)] [jekyll-bootstrap](https://github.com/clientlab/jekyll-bootstrap) : 当前组织首页使用的博客引擎（使用了bootstrap框架）
- [[GitHub](https://github.com/plusjade/themes.jekyllbootstrap.com)] [themes.jekyllbootstrap.com](https://github.com/clientlab/themes.jekyllbootstrap.com) : 博客引擎的皮肤项目
- [[GitHub](https://github.com/jekyllbootstrap/theme-tom)] [theme-tom](https://github.com/clientlab/theme-tom) : 当前组织首页使用的博客引擎的项目

## 最新文章 ##

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## 团组成员 ##

- [周培公](http://www.peigong.tk) - [GitHub](https://github.com/)
- [听歌](http://tingge.github.io) - [GitHub](https://github.com/TingGe)
- [尘埃](https://github.com/chenai1112)
- [onionyy](https://github.com/onionyy)
