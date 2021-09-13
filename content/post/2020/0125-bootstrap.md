---
title: "Bootstrap,TypeScript,React,Vue...chaos！"
date: 2020-01-25
thumbnail: "img/twitter-bootstrap.jpg"
sidebar: false
tags:
  - "IT"
categories:
  - "技术文档"
---

Bootstrap：Twitter开源前端框架。号称多终端一把梭，移动设备优先。所谓响应式设计，在任何尺寸的屏幕上看起来都会不错。  
TypeScript：微软爸爸滴超级js，哦～不对，是js的超集
Font Awesome ...
<!--more-->

# 温故而知新

DOM：W3C 文档对象模型
HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法。

平稳退化：确保网页在没有js的情况下也能正常工作
分离js：把网页结构和内容与js脚本动作行为分开
向后兼容性：确保老版本的浏览器不会因为js脚本死掉
性能考虑：确定执行脚本的性能最优

元素节点（elment node），文本节点，属性节点

----

html元素由开始标签和结束标签组成（部分元素只有开始标签）
在开始标签中可以给元素添加属性
标签之间可以嵌套再一起，有些可以作为容器，有些用来显示内容。
我们在网页中的看到的内容，都在body标签之内。
记住常用的八个标签就足够做网页了，没错，前期的学习就用八个标签。
上面都是html最基本的概念，接下来我们看一下要掌握哪八个标签：
```
<h*></h*>：标题标签，h1~h6,我们暂且当做一个标签看待。
<p></p>:段落标签
<ul></ul>：无序列表
<li></li>：列表元素
<a></a>：超链接，href属性可以指定跳转的位置
<img>：图卡，src属性可以设置图片源文件
<div></div>：容器，了解css后在进一步理解容器的概念。
<span></span>：容器，了解css后在进一步理解容器的概念。
```

表单元素-用于提交数据
表格元素-用于显示数据，古老的html用表格布局

## CSS
css的选择器有很多（css2本来就很多，css3又加了很多），参考[css选择器参考手册](https://www.w3school.com.cn/cssref/css_selectors.asp)    
比较常用的选择器：  
类选择器：`.class`  
元素选择器: `element`  
层级选择器: `selector1 selector2`  

一些常用的css属性：   
color
background-color
width
height
font-size
text-align
border


## 表格布局与浮动布局

long long ago, 网页是通过表格元素布局的。现在为了适应不断变化的网页内容，浮动布局（div+css）出现了。这种布局的特点是：
- 把网页内容放到div中，让他变成一个个盒子。
- 通过元素浮动（float属性），让每个盒子摆在他应该在位置上

### 伪元素
在css3版本中，为了区分伪元素与伪类选择器，在伪元素前面用两个冒号（::before,::after）

为一个选择器添加伪元素::before或::after，那么这个选择器找到的所有html标签的前或后方都会新增一个元素，这个元素是伪元素中content属性定义的。

.list::after{ content:"hello";
}

上面的样式中，.list选择器找到的所有元素，其后方都会追加一个"hello"。

在网页的布局中，可以不用定位来实现的布局就不要用定位

## MIME类型
媒体类型（通常称为 Multipurpose Internet Mail Extensions 或 MIME 类型 ）是一种标准，用来表示文档、文件或字节流的性质和格式。它在IETF RFC 6838中进行了定义和标准化。

浏览器通常使用MIME类型（而不是文件扩展名）来确定如何处理URL，因此Web服务器在响应头中添加正确的MIME类型非常重要。如果配置不正确，浏览器可能会曲解文件内容，网站将无法正常工作，并且下载的文件也会被错误处理。

通用结构`type/subtype` ：
```
text/plain
text/html
image/jpeg
image/png
audio/mpeg
audio/ogg
audio/*
video/mp4
application/*
application/json
application/javascript
application/ecmascript
application/octet-stream
…
```


`<meta>` 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。标签位于文档的头部，不包含任何内容。标签的属性定义了与文档相关联的名称/值对。  
在 HTML 中，`<meta>` 标签没有结束标签。在 XHTML 中，`<meta>` 标签必须被正确地关闭。
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```

## React

如何划分组件  
一个组件原则上只能负责一个功能。

最好将渲染 UI 和添加交互这两个过程分开。这是因为，编写一个应用的静态版本时，往往要编写大量代码，而不需要考虑太多交互细节；添加交互功能时则要考虑大量细节，而不需要编写太多代码。所以，将这两个过程分开进行更为合适

props（“properties” 的缩写）和 state 都是普通的 JavaScript 对象。它们都是用来保存信息的，这些信息可以控制组件的渲染输出，而它们的一个重要的不同点就是：props 是传递给组件的（类似于函数的形参），而 state 是在组件内被组件自己管理的（类似于在一个函数内声明的变量）。

为了正确地构建应用，你首先需要找出应用所需的 state 的最小表示，并根据需要计算出其他所有数据。其中的关键正是 DRY: Don’t Repeat Yourself。只保留应用所需的可变 state 的最小集合，其他数据均由它们计算产生。

通过问自己以下三个问题，你可以逐个检查相应数据是否属于 state：
- 该数据是否是由父组件通过 props 传递而来的？如果是，那它应该不是 state。
- 该数据是否随时间的推移而保持不变？如果是，那它应该也不是 state。
- 你能否根据其他 state 或 props 计算出该数据的值？如果是，那它也不是 state。

React 中的数据流是单向的，并顺着组件层级从上往下传递。

### Font Awesome

一个非常方便的图标库。这些图标都是矢量图形，被保存在 .svg 的文件格式中。这些图标就和字体一样，你可以通过像素单位指定它们的大小，它们将会继承其父HTML元素的字体大小。可以将 Font Awesome 图标库增添至任何一个应用中，方法很简单，只需要在 HTML 头部增加下列代码即可：
```html
<link rel="stylesheet" href="//cdn.bootcss.com/font-awesome/4.2.0/css/font-awesome.min.css"/>
```
i 元素起初一般是让其它元素有斜体(italic)的功能，不过现在一般用来指代图标。你可以将 Font Awesome 中的 class 属性添加到 i 元素中，把它变成一个图标，比如：
```html
<i class="fa fa-info-circle"></i>
```
例： 
```html
<button class="btn btn-block btn-primary"><i class="fa fa-thumbs-up"></i>Like</button>
```

## Bootstrap 网格系统

响应式网格系统随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。

<table class="grid" cellspacing="0">
<tbody><tr>
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>		
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>		
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>		
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>
  <td width="8.33%">1</td>		
  <td width="8.33%">1</td>
</tr>
<tr>
  <td colspan="4">4</td>
  <td colspan="4">4</td>		
  <td colspan="4">4</td>
</tr>
<tr>
  <td colspan="4">4</td>
  <td colspan="8">8</td>		
</tr>
<tr>
  <td colspan="6">6</td>
  <td colspan="6">6</td>		
</tr>
<tr>
  <td colspan="12">12</td>
</tr>
</tbody></table>

Bootstrap 包含了一个响应式的、移动设备优先的、不固定的网格系统，可以随着设备或视口大小的增加而适当地扩展到 12 列。它包含了用于简单的布局选项的预定义类，也包含了用于生成更多语义布局的功能强大的混合类。

## Node.js

ES6的模块支持，提供了import，export
Node.js采用的common.js的模块标准
node两大类模块：
- 核心模块：内置
- 文件模块：用户编写的模块，可通过npm安装