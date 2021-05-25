---
layout: post
title: "《你不知道的JavaScript》"
date: 2020-04-19  
tag: 书籍推荐
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

- 内部属性 **[[Class]]** 判断 数据类型？

  ```js
  Object.prototype.toString.call([1,2,3])
  //"[object Array]"
  
  var s = new String('123')
  var ss = "123";
  Object.prototype.toString.call(s)
  Object.prototype.toString.call(ss)
  //"[object String]"
  //"[object String]"
  
  Object.prototype.toString.call(true)
  //"[object Boolean]"
  
  Object.prototype.toString.call(null)
  //"[object Null]"
  
  Object.prototype.toString.call(undefined)
  //"[object Undefined]"
  
  Object.prototype.toString.call(1)
  //"[object Number]"
  
  Object.prototype.toString.call({})
  //"[object Object]"
  
  Object.prototype.toString.call(new RegExp())
  //"[object RegExp]"
  
  Object.prototype.toString.call(Symbol("1"))
  //"[object Symbol]"
  
  var fn = function(){};
  Object.prototype.toString.call(fn)
  //"[object Function]"
  
  var wm = new WeakMap();
  Object.prototype.toString.call(wm)
  //"[object WeakMap]"
  
  
  ```

- 常见 **错误** 对象

  ```js
  //创建错误对象（error object）主要是为了获得当前运行栈的上下文。
  
  throw new Error("e1")
  
  throw new EvalError("e2")
  
  throw new RangeError("e3")
  
  throw new ReferenceError("e4")
  
  throw new SyntaxError("e5")
  
  throw new TypeError("e6")
  
  throw new URIError("e7")
  ```

  

- **JSON 字符串化**

  - 所有 `安全`[^1] 的 JSON 值（JSON-safe）都可以使用 JSON.stringify(..) 字符串化
  - JSON.stringify(..) 在**对象**中遇到 **undefined** 、 **function** 和 **symbol** 时会自动将其忽略，在
    数组中则会返回 null （以保证单元位置不变），这些都是 `不安全`[^2]的JSON值。
  - 对包含**循环引用的对象**执行 JSON.stringify(..) 会出错
  - 对象中定义了 **toJSON()**[^3] 方法，JSON 字符串化时会首先调用该方法，然后用它的返回
    值来进行序列化。

  [^1]: 安全的JSON 值是指能够呈现为有效 JSON 格式的值
  [^2]: undefined、function、symbol（ES6+）和包含循环引用的对象
  [^3]: toJSON() 应该“返回一个能够被字符串化的安全的 JSON 值”，而不是“返回一个 JSON 字符串”

  ```js
  //JSON.stringify(...)可传递一个可选参数replacer，它可以是数组或者函数；
  //如果replacer是一个数组，必须是一个字符串数组，其中包含序列化要处理的对象的属性名称，除此之外的其他属性则被忽略
  //如果replacer是一个函数，它会对对象本身调用一次，然后对对象中的每个属性各调用一次，每次传递 2 个参数，键和值。如果要忽略某个键就返回 undefined， 否则返回指定的值
  var a = {
      b: 123,
      c: '321',
      d: [1,2,3]
  };
  JSON.stringify(a, ['b','c']);//"{"b":123,"c":"321"}"
  JSON.stringify(a, function(k, v){
      if(k !== "c") return v;
  });//"{"b":123,"d":[1,2,3]}"
  
  //JSON.string 还有一个可选参数 space，用来指定输出的缩进格式。space 为正整数时是指定每一级缩进的字符数，它还可以是字符串，此时最前面的十个字符被用于每一级的缩进
  var a = {
      b: 123,
      c: '321',
      d: [1,2,3]
  };
  JSON.stringify(a, null, 3);
  JSON.stringify(a, null, "---");
  ```

- `~~` 来截除数字值的小数部分？？？

  > 1.~~ 中的第一个 ~ 执行 ToInt32 并反转字位，然后第二个 ~ 再进行一次字位反转，即将所有
  > 字位反转回原值，最后得到的仍然是 ToInt32 的结果。
  >
  > 2.对 ~~ 我们要多加注意。首先它只适用于 32 位数字，更重要的是它对负数的处理与 Math.
  > floor(..) 不同

  ```js
  Math.floor(-49.6); //-50
  ~~-49.6; //-49
  
  ~~1e20 / 10; //166199296
  1e20 / 10; //1e19
  ```

- `parseInt` 的坑？

  > ES5 之前的 parseInt(..) 有一个坑导致了很多 bug。即如果没有第二个参数来指定转换的
  > 基数（又称为 radix）， parseInt(..) 会根据字符串的第一个字符来自行决定基数。
  > 如果第一个字符是 x 或 X ，则转换为十六进制数字。如果是 0 ，则转换为八进制数字。

  > 从 ES5 开始 parseInt(..) 默认转换为十进制数，除非另外指定。如果你的代码需要在 ES5
  > 之前的环境运行，请记得将第二个参数设置为 10 。

  ```js
  //离奇的例子
  
  parseInt(1/0, 19); //18
  //实际---parseInt("Infinity", 19)
  //第一个字符是“I”，以19为基数时值为18，第二个字符“n”不是一个有效的数字字符，解析到此为止。
  
  parseInt( 0.000008 ); // 0
  parseInt( 0.0000008 ); //8 （“8”来自于“8e-7”）
  parseInt(false, 16); //250 （“fa”来自于“false”）
  parseInt("0x10"); //16
  parseInt("103", 2); //2
  ```

- **宽松相等**和**严格相等**？

  > 正确的解释是：“ == 允许在相等比较中进行强制类型转换，而 === 不允许。”