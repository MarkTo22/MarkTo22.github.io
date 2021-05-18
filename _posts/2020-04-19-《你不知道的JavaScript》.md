---
layout: post
title: "《你不知道的JavaScript》"
date: 2019-05-25  
tag: 书籍阅读
---

##  1. 《你不知道的JavaScript》

​	该书是一本 **JavaScript** 开发人员进阶书籍，让我们知其然，更知其所以然。

- **JavaScript** 有 **7** 种内置类型：

  - 空值（null）

  - 未定义（undefined）

  - 布尔值（boolean）

  - 数字（number）

  - 字符串（string）

  - 对象（object）

  - 符号（symbol，ES6中新增）

    注：除对象之外，其他统称为“基本类型”。

- 通过 **typeof** 的安全防范机制（阻止报错）来检查undeclared 变量

- 如何检测 **null** 值的类型：

  ```javascript
  var a = null;
  (!a && typeof a === "object"); //true
  ```

- 将 **类数组** 转换为真正的 **数组**

  - Array.prototype.slice.call( arguments );
  - Array.from( arguments );

- 42.0 === 42;//true

  

