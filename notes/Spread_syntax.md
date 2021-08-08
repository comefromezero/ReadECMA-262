# 扩展运算符(...,Spread Syntax)

用于将数组或者字符串展开，或者将对象以键值对的形式展开。

任意具有Iterator的对象都可以扩展成为真正的数组。

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

## 函数调用参数

``` Javascript
function add(x,y,z){
    return x+y+z;
}

let arg = [1,2,3,4];

let result = add(...arg);

console.log(result); //6
```

## 作用于数组

* 可以将数组转换为参数序列

``` Javascript
function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers) // 42
```

* 可以复制数组
如果直接通过下列的方式进行数组复制是不可取的：

``` Javascript
const arr1 = [1, 2];
const arr2 = arr1;
arr2[0] = 2;
arr1 // [2, 2]
```

用扩展运算符就很方便：

``` Javascript
const arr1 = [1, 2];
const arr2 = [...arr1];
```

还是记住那句话：扩展运算符(…)用于取出参数对象中的所有可遍历属性，拷贝到当前对象之中，这里参数对象是个数组，数组里面的所有对象都是基础数据类型，将所有基础数据类型重新拷贝到新的数组中。

扩展运算符可以与解构赋值结合起来，用于生成数组
``` Javascript
const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]
```

需要注意的一点是：

如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错。

``` Javascript
const [...rest, last] = [1, 2, 3, 4, 5];
// 报错
const [first, ...rest, last] = [1, 2, 3, 4, 5];
// 报错
```

扩展运算符还可以将字符串转为真正的数组
``` Javascript
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```
任何 Iterator 接口的对象（参阅 Iterator 一章），都可以用扩展运算符转为真正的数组

