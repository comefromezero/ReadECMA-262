# 最新的ECMA-262 

* [TC39](https://tc39.es/ecma262/2021/#sec-grammar-notation) 

TC39是一个Js的发展、实现、学术性的组织。 

--- 

# V8引擎组关于ECMA-262文档的导读备份 

* [part1](https://v8.dev/blog/understanding-ecmascript-part-1) 
* [part2](https://v8.dev/blog/understanding-ecmascript-part-2) 
* [part3](https://v8.dev/blog/understanding-ecmascript-part-3) 
* [part4](https://v8.dev/blog/understanding-ecmascript-part-4) 

# 说明

ECMA-262文档只是对Js的一种标准，其中不少内容都是由各种JS实现自己决定的，所以这也就造成了各种JS实现之间可能存在部分差异。

另外的，ECMA-262文档虽然发布了，浏览器中的JS引擎未必会该ECMA-262文档中的所有特性，所以能够使用何种语法以及何种特性，必须根据实际的JS实现决定。但是由于Babel的出现，我们可以使用一些特别新的语法以及特性，然后利用Babel来进行转换，使这些使用新语法和新特性的代码转换为能够在某些落后于ECMA-262的JS实现上运行。
