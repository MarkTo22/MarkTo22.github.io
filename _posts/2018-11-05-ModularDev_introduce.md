---
layout: post
title: "模块化开发"
date: 2018-11-05 
description: "模块化开发入门"
tag: 前端  

---     
## **1. 模块化开发**

### **1.1 模块化**  

	所谓模块化，就是把一个相对独立的功能，单独形成一个文件，可输入指定依赖、输出指定的函数，供外界调用，其它都在内部隐藏实现细节。这样即可方便不同的项目重复使用，也不会对项目造成额外的影响。

前端使用模块化载发主要的作用是：

* 异步加载 js，避免浏览器假死
* 管理模块间依赖关系，便于模块的维护
有了模块，我们就可以更方便地使用别人的代码，想要什么功能，就加载什么模块。

但要使用模块的前提，是必然要形成可遵循的开发规范，使得开发者和使用者都有据可寻，否则你有你的写法，我有我的写法，大家没办法统一，也就不能很好的互用了。

目前通用的规范是，服务器端使用 CommonJS 规范，客户端使用 AMD/CMD 规范。

### **1.2 CommonJS**

	CommonJS 规范出现是在 2009 年，Node.js 就是该规范的实现。CommonJS 规范中是这样加载模块的：

> var gulp = require("gulp");
> gulp.task(/* 任务 */);

模块的加载是同步的，这种写法适合服务器端，因为在服务器读取的模块都是在本地磁盘，加载速度很快，可同步加载完成。但是如果在客户端浏览器中，因为模块是放在服务器端的，模块加载取决于网络环境，以同步的方式加载模块时有可能出现“假死”状况。

本文主要介绍针对浏览器编程，不针对 Node.js 内容，所以在此关于 CommonJS 规范就不作深究，知道 require() 用于加载模块即可。

### **1.3 AMD**
	
	由于在浏览器端，模块使用同步方式加载可能出现假死，那么我们采用异步加载的方式来实现模块加载，这就诞生了 AMD 的规范。

AMD 即 Asynchronous Module Definition 的简称，表示“异步模块定义”的意思。AMD 规范：
[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)。
AMD 采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖所加载模块的语句，都被定义在一个回调函数中，等到模块加载完毕后，回调函数才会执行。
AMD 也采用 require() 来加载模块，语法结构为：

`require([module], callback);`

module 是数组参数，表示所加载模块的名称；callback 是回调函数参数，所有模块加载完毕后执行该回调函数。如：

> require(["jquery"], function($){
> $("#box").text("test");
> });

[RequireJS](http://requirejs.org/) 实现了 AMD 规范,

### **1.4 CMD**
	CMD 即 Common Module Definition 的简称，表示“通用模块定义”的意思。CMD 规范：

[CMD](https://github.com/cmdjs/specification/blob/master/draft/module.md)
CMD 规范明确了模块的基本书写格式和基本交互规则，该规范是在国内发展出来的，由玉伯在推广 SeaJS 过程中规范产出的。

[SeaJS](http://seajs.org/docs/) 实现了 CMD 规范。SeaJS 要解决的问题和 RequireJS 一样，只不过在模块定义方式和模块加载（运行、解析）时机上有所不同。

### **1.5 AMD与CMD的区别**

	AMD 是 RequireJS 在推广过程中对模块定义的规范化产出。
	CMD 是 SeaJS 在推广过程中对模块定义的规范化产出。

二者主要区别如下：
1.对于依赖的模块，AMD 是提前执行，CMD 是延迟执行。
2.CMD 推崇依赖就近，AMD 推崇依赖前置。
3.AMD 的 API 默认是一个当多个用，CMD 的 API 严格区分，推崇职责单一。

当然还有一些其它细节上的区别，具体看规范的定义就好。
参考：[AMD与CMD区别](http://zccst.iteye.com/blog/2215317)
<br>

转载请注明：[博客](https://markto22.github.io) » [点击阅读原文](https://markto22.github.io/2018/11/ModularDev_introduce/)