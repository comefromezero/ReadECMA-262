# typeof运算符

该运算符主要用于判断一个变量是什么类型。typeof运算符的结果是返回一个字符串，用来表示具体类型：

"undefined"表示值未定义

"boolean"表示值为布尔值

"string"表示值为字符串

"number"表示值为数值

"object"表示值为对象（而不是函数）或 null

"function"表示值为函数

"symbol"表示值为符号

> 类型主要分为两种:primitive type和reference type。ES定义了6种基本的primitive type：null,undefined，boolean，string,number，symbol。reference type则是由多个值构成的对象。

``` Javascript

//用于判断一个变量是什么类型

function ESTypeFunc(VarValue){

    VarType = typeof(VarValue);
    if("object"=== VarType){
        return null===VarValue?"null":"object";
    }else{
        return VarType;
    }
}

```

# Instanceof运算符


![原型链](https://github.com/comefromezero/ReadECMA-262/blob/main/img/%E5%8E%9F%E5%9E%8B%E9%93%BE.png)

[原型链与对象](https://blog.csdn.net/lengye7/article/details/118155220)

instanceof 操作符可以用来确定一个实例的原型链上是否有某个原型。

``` Javascript

function Foo() {} 
let f = new Foo(); 
console.log(f instanceof Foo); // true

console.log(f instanceof String); //false

console.log(f instanceof Object); //true,参考上面原型链，可以知道，Object在任何实例的原型链上。

```