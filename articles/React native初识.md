> 出处：[Learning React native](http://shop.oreilly.com/product/0636920041511.do)  
> 时间：2016.04.27

# 前言
最近开始学习React native，本来还是菜鸟，所以不敢讲太多技术上的东西。但是对于学习一门新技术，我觉得需要了解她的优缺点和工作方式。这篇文章也是基于这个出发点，翻译了[Learning React native](http://shop.oreilly.com/product/0636920041511.do)的前两章的主要内容，若有表述的有错误或者偏差，希望你能及时留言给我。

# React native初识

## React native是什么
React native是一个可以写iOS、Android应用程序的JS框架。她基于facebook的React框架，不过React面对是浏览器，而React native面对的是客户端。换句话说，web开发者现在可以用他们最熟悉的JS来写“原生”的APP应用了。而且，由于你写的大部分代码是被不同的平台所共享，所以React native可以同时开发并调试iOS和Android。  

和web端的React框架一样，React native是用到了JS与XML相结合的方式来作为markup，我们称之为JSX。在这个基础之下，React native搭建了一座访问APP原生API的桥梁（iOS中的Object-C与Android的Java）。所以，当用React native搭建的App的组件，表现形式和原生的是一样的，而不像以前我们通常使用的的webview是一个网页。同时，React native也提供了终端平台API的JS接口，这样你的React native应用也可以调用摄像机或者GPS了。  

目前，React native支持包括iOS和Android的设备，未来也可能扩展到其他的应用平台。国内外已有一部分的React native的APP上线了，你可以到React native官网上查看一些。  

### React native的优势

### 给开发人员的建议

### 代码复用与经验分享

### 可能存在的问题与风险

## React native的工作原理
