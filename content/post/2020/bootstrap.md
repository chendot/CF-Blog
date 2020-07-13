---
title: "Bootstrap"
date: 2020-03-02
thumbnail: "img/twitter-bootstrap.jpg"
sidebar: false
tags:
  - "IT"
categories:
  - "技术文档"
---

Bootstrap是Twitter开源的基于HTML、CSS、JavaScript的前端框架。它是为实现快速开发Web应用程序而设计的一套前端工具包。支持响应式布局，并且在V3版本之后坚持移动设备优先。就是复制黏贴一把梭，html\css\js代码的封装组合。Bootstrap将会根据你的屏幕的大小来调整HTML元素的大小 —— 强调 响应式设计的概念。通过响应式设计，你无需再为你的网站设计一个手机版的。它在任何尺寸的屏幕上看起来都会不错。<!--more-->

你仅需要通过添加下列代码到你的HTML开头来将Bootstrap添加到任意应用中：
```html
<link rel="stylesheet" href="//cdn.bootcss.com/bootstrap/3.3.1/css/bootstrap.min.css"/>
```

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