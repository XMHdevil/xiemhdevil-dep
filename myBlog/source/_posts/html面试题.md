---
title: html面试题
categories: 面试题
tags: html
---


## html面试题

### 行内元素

不会独立出现在一行，单独使用的时候后面不会有换行符的元素。

例如：span，strong，img ， a，b，input，select 等等，默认的宽度，总是其内容的高度。并且，margin和padding，只有左右有效。

### 块级元素

独立一行，后面自动带有换行符。

例如： div，p，form，ul，li，ol，dl，h1~h6等

在没有设置宽度的时候，默认宽度时父元素的宽度。

### 常见的空元素：br-换行，hr-水平分割线

### Doctype作用？标准模式和混杂模式如何区分？<!DOCTYPE>

告诉浏览器使用哪个版本的html规范来渲染文档。DOCTYPE不存在或形式不正确会导致html文档以混杂模式呈现。

标准模式（standards mode）以浏览器支持的最高标准运行；混杂模式（Quirks mode）中页面时一种比较宽松的向后兼容的方式显示。

### 引入样式时，link和@import的区别？

链接样式时，link只能和HTML页面中引入外部样式

导入样式表时，@import既可以在HTMl页面中导入外部样式，也可以在css样式文件中导入外部css样式。

### html5有哪些新特性？

HTML5现在已经不是SGML的子集，主要是关于图像，位置，存储，多任务等功能的增加。

（1）、绘画canvas，

（2）、用于媒介回放video和audio元素；

（3）、本地离线存储localStorage长期存储数据，浏览器关闭后数据不丢失；

（4）、sessionStorage的数据在浏览器关闭后自动删除；

（5）、语意化更好的内容元素，如article，footer，header，nav，section；

（6）、表单控件，calendar，date，time，email，url，search；

（7）、新的技术webworker，websocket，Geolocation；

IE8/IE7/IE6支持通过document.createElement方法产生的标签，可以利用这一特性让这些浏览器支持HTML5新标签，浏览器支持新标签后，还需要添加标签的默认样式。当然也可以直接使用成熟的框架、比如html5shim

移除的元素：

1、纯表现的元素：basefont  big  center font s strike  tt u

2、性能较差元素：frame frameset noframes