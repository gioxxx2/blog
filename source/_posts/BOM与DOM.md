---
title: JS中的BOM与DOM
date: 2019-02-14 16:25:11
categories: 前端
tags:
    - JavaScript
    - DOM
---

在学习JavaScript中对于BOM与DOM的一些概念比较模糊，所以希望能通过这篇文章梳理自己的理解和认识。

<!--more-->


## BOM(Browser Object Model)，浏览器对象模型

1. BOM和浏览器关系密切。浏览器的很多东西可以通过JavaScript控制的，例如打开新窗口、打开新选项卡（标签页）、关闭页面，把网页设为主页，或加入收藏夹，等等…这些涉及到的对象就是BOM。
2. BOM没有相关标准,不同的浏览器实现同一功能，可以需要不同的实现方式。
3. BOM的最根本对象是window。

##  DOM(Document Object Model),文档对象模型

1. DOM和文档有关，这里的文档指的是网页，也就是HTML文档。网页是由服务器发送给客户端浏览器的，无论用什么浏览器，接收到的HTML都是一样的，所以DOM和浏览器无关，它关注的是网页本身的内容。
2. DOM是W3C的标准。由于和浏览器关系不大，所以标准就好定了。
3. DOM最根本对象是document（实际上是window.document）。


## 关系

两者的关系是BOM包含DOM。

![1355820423_6946](/images/1355820423_6946.jpg)


**DOM 是为了操作文档（网页内容）出现的 API，document 是其的一个对象；
BOM 是为了操作浏览器出现的 API，window 是其的一个对象。**

## DOM

DOM描述了处理网页内容的方法和接口。DOM将整个页面映射为一个由层次节点组成的文件。有1级、2级、3级共3个级别。

```
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
    <head>
            <meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
            <title>DOM</title>
    </head>
    <body>
            <h2><a href="http://www.baidu.com">javascript DOM</a></h2>
            <p>对HTML元素进行操作，可添加、改变或移除css样式等</p>
            <ul>
                    <li>Javascript</li>
                    <li>DOM</li>
                    <li>CSS</li>
            </ul>
    </body>
</html>
```
将HTML代码分解为DOM节点层次图:
![82e6685bd44859146c82709ebd88ea68_articlex](/images/82e6685bd44859146c82709ebd88ea68_articlex.jpeg)

```
 **HTML文档可以说由节点构成的集合，DOM节点有:**
1. 元素节点：上图中<html>、<body>、<p>等都是元素节点，即标签。
2. 文本节点:向用户展示的内容，如<li>...</li>中的JavaScript、DOM、CSS等文本。
3. 属性节点:元素属性，如<a>标签的链接属性href="http://www.baidu.com"。
```
### DOM操作
DOM通过创建树来表示文档，描述了处理网页内容的方法和接口，从而使开发者对文档的内容和结构具有空前的控制力，用DOM API可以轻松地删除、添加和替换节点。

![20161130105804863](/images/20161130105804863.png)


### DOM事件
DOM同时两种事件模型：冒泡型事件和捕获型事件

冒泡型事件：事件按照从最特定的事件目标到最不特定的事件目标的顺序触发  

### BOM的window对象
![20161130105842940](/images/20161130105842940.png)


参考出处
<https://segmentfault.com/a/1190000000654274>
<https://github.com/HarleyWang93/blog/issues/13>


