---
layout: post
title: "Gulp使用教程"
date: 2017-03-16   
tag: 前端学习 
---

### **1 介绍**
       
	Gulp 是前端开发过程中对代码进行构建的工具。

	Gulp 是基于 Nodejs 的自动任务运行器， 她能自动化地完成 JavaScript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。在实现上，她借鉴了 Unix 操作系统的管道（pipe）思想，前一级的输出，直接变成后一级的输入，使得在操作上非常简单。 

[参考Gulp中文网](http://www.gulpjs.com.cn/)         

Gulp使用流程：安装 Nodejs -> 全局安装 Gulp -> 项目安装 Gulp 以及 Gulp 插件 -> 配置 gulpfile.js -> 运行任务

### **2.1 安装NodeJs**

Gulp是基于Nodejs的，所以先安装Nodejs。
[Nodejs官网下载](https://nodejs.org/en/) 

下载后根据向导安装即可。

安装完毕 **Nodejs** 后即可测试是否安装成功。在命令提示符下（通常 windows 系统是 cmd，mac 系统是终端）输入 `node -v` 即可查看安装的 Nodejs 版本。

常用命令说明：

`node -v`：查看安装的 Nodejs 版本，出现版本号，说明已正确安装nodejs。

`npm -v`：查看npm的版本号，npm是在安装 Nodejs 时一同安装的 Nodejs 包管理器。

### **2.2 npm 简介**

npm 是 node package manager 的简称，它是 Nodejs 的包管理器，用于 node 插件的管理，如安装、卸载、依赖管理等。

**安装插件**

`npm install <name> [-g] [--save-dev]`

	<name> 表示插件名称，如 gulp。

-g 表示全局安装。全局安装可以通过命令行在任何地方调用它，本地安装（非全局安装）将安装在定位目录的 node_modules 文件夹下，通过 require() 调用。

--save 表示将保存配置信息至 package.json 文件，package.json 是 Nodejs 项目配置文件。之所以要保存至 package.json，是因为 Nodejs 插件包相对来说非常庞大，将配置信息写入 package.json 并将其加入版本管理，其他开发者对应下载即可（命令提示符执行 `npm install`，则会根据 package.json 下载所有需要的包，`npm install --production` 只下载 dependencies 节点的包）。

-dev 表示保存至 package.json 的 devDependencies 节点，不指定 -dev 将保存至 dependencies 节点；一般保存在 dependencies 的像这些：express/ejs/body-parser 等。

**卸载插件**

`npm uninstall <name> [-g] [--save-dev]`

要卸载插件，不要直接删除本地插件包，需要使用上述命令来卸载。

**更新插件**

`npm update <name> [-g] [--save-dev]`

要更新全部插件，可使用 `npm update [--save-dev]`。

### **2.3 cnpm**
	npm 安装插件是从国外服务器下载资源，受网络影响大，可能出现异常，可以使用[淘宝镜像](http://npm.taobao.org/)，淘宝镜像是一个完整 npmjs.org 镜像，可以用它代替官方版本，其同步频率目前为 10 分钟一次以保证尽量与官方服务同步。

	为保证安装能够正常进行，推荐使用淘宝镜像。cnpm 安装命令为：`npm install -g cnpm --registry=https://registry.npm.taobao.org`。

	cnpm 的用法与 npm 完全一致，只需要将执行 npm 命令的地方替换为 cnpm 即可。

###	**2.4 全局安装 Gulp**
	为了在任何地方都可以使用到 Gulp 命令来执行任务，我们全局安装 Gulp，可以在命令提示符下使用 `npm install gulp -g 或 cnpm install gulp -g` 来实现安装。

	等待安装结束，可使用 `gulp -v` 命令测试 Gulp 版本，如果看到版本号出现，则说明安装成功。本文 Gulp 版本为 3.9.1。

###	**2.5 生成 package.json**
	package.json 是基于 Nodejs 项目必不可少的配置文件，它是存放在项目根目录的 json 文件。

	package.json 用来存放即将安装的插件 name 和 version，这个文件有什么用呢？当我们把项目拷贝给别人的时候不需要拷贝插件，只需要把项目文件、package.json 和 gulpfile.js 拷贝过去就可以，接收人 cd 到项目文件目录直接输入 `npm install` 即可安装上我们拷贝前安装的各种插件。

	package.json 文件格式如下：

>	{
>	  "name": "demo", // 项目名称
>	  "version": "1.0.0", // 项目版本
>	  "description": "test page", // 项目描述
>	  "main": "example.js", // 入口文件
>	  "scripts": { // 运行脚本命令的 npm 命令行缩写
>	    "test": "echo \"Error: no test specified\" && exit 1"
>	  },
>	  "author": "xiaoming", // 作者
>	  "license": "ISC" // 项目许可协议
>	}`


可直接复制上述文本后修改，要注意的是 json 文件中不允许使用注释内容，所以如果是复制修改还需要将注释去掉。或在命令提示符下使用 `npm init` 命令来初始化自动生成 package.json 文件：


>	$ npm init
>	This utility will walk you through creating a package.json file.
>	It only covers the most common items, and tries to guess >sensible defaults.
>
>	See `npm help json` for definitive documentation on these fields
>	and exactly what they do.
>
>	Use `npm install <pkg> --save` afterwards to install a package >and
>	save it as a dependency in the package.json file.
>
>	Press ^C at any time to quit.
>	name: (demo) 
>	version: (1.0.0) 
>	description: test page
>	entry point: (example.js) 
>	test command: 
>	git repository: 
>	keywords: 
>	author: xiaoming
>	license: (ISC) 
>	About to write to /Users/isaac/Documents/HTML5/projects/demo/>package.json:
>
>	{
>	  "name": "demo",
>	  "version": "1.0.0",
>	  "description": "test page",
>	  "main": "example.js",
>	  "scripts": {
>	    "test": "echo \"Error: no test specified\" && exit 1"
>	  },
>	  "author": "xiaoming",
>	  "license": "ISC"
>	}
>
>
>	Is this ok? (yes) yes>

`npm init`执行后会提示输入项目名称、版本、描述等信息，按提示输入即可，也可以留空。