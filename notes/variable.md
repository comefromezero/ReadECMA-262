# Variable 

Js的变量松散的类型的，意味着一个变量可以保存任何类型的数据。Js中有3个关键字用于变量声明：var、const(ES6引入)、let（ES6引入）。 

## var声明变量 

格式：var identifiername; 

前面var是关键字，后面identifiername是标识符名，虽然Js支持自动分号插入，但是每一条语句我们都应该带上;。 

``` Javascript
//example1
var message = "hello world"; //声明并初始化一个变量message
``` 
### var声明变量的作用域 

我们知道ES6以前的JS并没有局部作用域，其具备两个作用域：全局作用域和函数作用域，因此，通过var声明的变量，要不就是全局作用域，要不就是函数作用域。 

各位前辈为了获得一个局部作用域，只能通过闭包技术，利用函数作用域来模拟一个局部作用域。 

``` Javascript
//example2
if(1){
    var message = "hello world"; //全局作用域变量
}
consolo.log(message);   //输出结果：hello world
``` 

``` Javascript
//example3
function test1(){
    var message = "hello wolrd"; //函数作用域变量
}

consolo.log(message);   //输出结果:出错
``` 

### 注意点： 

1. 非严格模式下，以下语句是合法的： 
``` Javascript
//example4
message = "hello world"; //不声明一个变量，直接对一个变量赋值
``` 

上面的语句会被解析，解释器会把message当成全局变量来处理，并将其赋值为"hello world"。 

``` Javascript 
//example5
if(1){
    message = "hello world"; //全局作用域变量
}
console.log(message); //输出结果：hellow world
``` 

``` Javascript
//example6
function test2(){
    message = "hello world"; //全局作用域变量
}
``` 

2. 严格模式下，以下语句是不合法的：
``` Javascript 
//example7
message = "hello world"; //语句出错
``` 

3. 严格模式下，以下语句是合法的：
``` Javascript 
//example8
message = "hello world"; //对一个全局作用域变量赋值
var message; //声明一个全局作用域变量
``` 

为什么3中的语句是合法的？这就要提到变量提升了，请往下看。 

### 变量提升 

通过var声明的变量会存在变量提升的情况，从而使得我们可以先使用一个变量，然后再用var声明该变量。例8就是一个典型的变量提升的例子。 

``` Javascript
//exmaple9
var message;
message = "hello world";
//例8就相当于这一段代码,这一段代码在严格模式下当然不会出错了啊，哈哈哈。
``` 

``` Javascript 
//emample10
console.log(message); //输出：undefined,因为还没有对message进行赋值
message = "hello world";
var message;

//相当于如下代码：
var message;
console.log(message);
message = "hello world";
``` 

``` Javascript
//emample11
function test3(){
    console.log(message);
    message = "hello world";
    var message;
}
//相当于如下代码：
function test3(){
    var message;
    console.log(message);
    message = "hello world";
}
test3(); //输出:undefined
``` 

``` Javascript
//exmaple12
var message = "test1";
console.log(message); //输出：test1
var message = "test2";
var message = "test3"
//由于变量提升，多个var声明同一个变量是合法的，上面的代码相当于
var message;
message = "test1";
console.log(message);
message = "test2";
message = "test3";
```

## let声明变量 

格式：let identifiername; 

前面let是关键字，后面identifiername是标识符名，虽然Js支持自动分号插入，但是每一挑语句我们都应该带上。 

``` Javascript
let message = "hello world";
```

* let与var不同的是，let声明的变量是块级作用域，而var声明的是全局作用域或者函数作用域。 

``` Javascript
//example12
if (true) { 
 var name = 'Matt'; 
 console.log(name); // Matt 
} 
console.log(name); // Matt

//对比
if (true) { 
 let age = 26; 
 console.log(age); // 26 age的作用域处于{}之间
} 
console.log(age); // ReferenceError: age 没有定义
``` 

* let不存在变量提升，故不能在同一个块级作用域内对同一个变量声明多次 

``` Javascript
var name; 
var name; //由于变量提升，多个var会在顶部合成一个。
let age; 
let age; // SyntaxError；标识符 age 已经声明过了
``` 

* 同一作用域内let与var声明的变量不能同名 

``` Javascript
var name; 
let name; //由于变量提升，多个var会在顶部合成一个。

let age; 
var age; // SyntaxError；标识符 age 已经声明过了
``` 

* let不存在变量提升 

``` Javascript 
// age 不会被提升
console.log(age); // ReferenceError：age 没有定义
let age = 26;
``` 

* 全局作用域下，var声明的变量会成为global object的property，let声明的变量不会成为global object的property 

``` Javascript
var name = 'Matt'; 
console.log(window.name); // 'Matt' 
let age = 26; 
console.log(window.age); // undefined
``` 

### 利用let给for循环声明一个局限在for内部的索引变量 

let出现以前，我们通过var来为一个for循环声明一个迭代变量，这种方式所声明的索引变量i能够从for循环外部访问，如下： 

``` Javascript 
for (var i = 0; i < 5; ++i) { 
 // 循环逻辑 
} 
console.log(i);   //输出:5
``` 

改用let之后，上面所说的问题就消失了，因为迭代变量的作用域仅限于for循环内部： 

``` Javascript 
for (let i = 0; i < 5; ++i) { 
 // 循环逻辑
} 
console.log(i); // ReferenceError: i 没有定义
``` 

在let以前我们使用var来为for循环声明一个迭代变量，某些时候往往会得到一些奇怪行为： 

``` Javascript
for (var i = 0; i < 5; ++i) { 
 setTimeout(() => console.log(i), 0) 
} 
// 你可能以为会输出 0、1、2、3、4 
// 实际上会输出 5、5、5、5、5
``` 

但是在使用let之后，我们就能得到预期的结果： 

``` Javascript
for (let i = 0; i < 5; ++i) { 
 setTimeout(() => console.log(i), 0) 
} 
// 会输出 0、1、2、3、4
``` 

这是因为在使用 let 声明迭代变量时，JavaScript 引擎在后台会为每个迭代循环声明一个新的迭代变量。每个 setTimeout 引用的都是不同的变量实例，所以 console.log 输出的是我们期望的值，也就是循环执行过程中每个迭代变量的值。 

## const声明变量 

const与let的基本行为一致，声明的变量是块级作用域，不存在变量提升，不能存在同名变量，不能多次声明，全局作用域下声明的变量不会成为global object的property，但是const多了两点不同之处：一、const声明的变量必须在声明的同时初始化；二、const声明的变量在初始化完成之后不能再被修改。换言之，const声明创建常量。 

### const的应用 

虽然const声明的变量的值在初始化之后就不能再修改，但是我们可以修改该变量引用的那个对象。这就非常适合用const来声明一个对特定对象的引用变量，防止在代码运行的过程中，意外的改变该变量的引用指向，这样我们就相当于获得了一个对象的别名。 

``` Javascript
const person = {}; 
person.name = 'Matt'; // ok，我们可以通过persion访问这个对象。
``` 

### 注意点 

不能使用const为for循环声明一个迭代变量。 

``` Javascript
for (const i = 0; i < 10; ++i) {} // TypeError：给常量赋值
``` 

## 总结

在日常使用中，如果一个变量将来需要改变，应该使用let；如果确定一个变量将来不需要改变，应该使用const；不要使用var。