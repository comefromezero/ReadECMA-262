# 扩展运算符(...,Spread Syntax)

用于将数组或者字符串展开，或者将对象以键值对的形式展开。

## 语法

函数调用：

myFunction(...iterableObj);


字面量数组构造或字符串：

[...iterableObj, '4', ...'hello', 6];


构造字面量对象时,进行克隆或者属性拷贝（ECMAScript 2018规范新增特性）：

let objClone = { ...obj };

## 作用于对象

对象中的扩展运算符(...)用于取出参数对象中的所有可遍历属性，拷贝到当前对象之中。

``` Javascript
let bar = { a: 1, b: 2 };
let baz = { ...bar }; // { a: 1, b: 2 }

//等价于
let bar = { a: 1, b: 2 };
let baz = Object.assign({}, bar); // { a: 1, b: 2 }
```

Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。(如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性)。

同样，如果用户自定义的属性，放在扩展运算符后面，则扩展运算符内部的同名属性会被覆盖掉。

``` Javascript
let bar = {a: 1, b: 2};
let baz = {...bar, ...{a:2, b: 4}};  // {a: 2, b: 4}
```

扩展运算符对对象实例的拷贝属于一种浅拷贝。

``` Javascript
let obj1 = { a: 1, b: 2};
let obj2 = { ...obj1, b: '2-edited'};
console.log(obj1); // {a: 1, b: 2}
console.log(obj2); //  {a: 1, b: "2-edited"}

let obj1 = { a: 1, b: 2, c: {nickName: 'd'}};
let obj2 = { ...obj1};
obj2.c.nickName = 'd-edited';
console.log(obj1); // {a: 1, b: 2, c: {nickName: 'd-edited'}}
console.log(obj2); // {a: 1, b: 2, c: {nickName: 'd-edited'}}
```