---
layout: post
title: "《你不知道的JavaScript》"
date: 2020-04-19  
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

  ```javascript
  - Array.prototype.slice.call( arguments );
  - Array.from( arguments );
  ```

- 42.0 === 42;//true

- 对于 . 运算符需要给予特别注
  意，因为它是一个有效的数字字符，会被优先识别为数字常量的一部分，然后才是对象属
  性访问运算符。

  ```javascript
  // 无效语法：
  42.toFixed( 3 ); // SyntaxError
  // 下面的语法都有效：
  (42).toFixed( 3 ); // "42.000"
  0.42.toFixed( 3 ); // "0.420"
  42..toFixed( 3 ); // "42.000"
  ```

  

- 

- 

