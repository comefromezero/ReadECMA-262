# 流程控制语句

js代码的执行是自上而下的，但是js也提供了很多控制语句来控制程序流的执行。

## if语句

if语句有四种形式：

if ...

if ...
else ...

if ...
else if ...

if ... 
else if ...
else ...

注意点：else总是跟距离他最近的之前的if语句组成if ... else ...语句对。

## do-while循环语句(es3)

do-while 语句是一种后测试循环语句，即循环体中的代码执行后才会对退出条件进行求值。换句话说，循环体内的代码至少执行一次。

语法如下：
``` Javascript
do { 
 statement 
} while (expression);
```
## while循环语句

while 语句是一种先测试循环语句，即先检测退出条件，再执行循环体内的代码。因此，while 循环体内的代码有可能不会执行。

语法如下：
``` Javascript
while(expression) statement
```
## for循环语句

for 语句也是先测试语句，只不过增加了进入循环之前的初始化代码，以及循环执行后要执行的表达式。

语法如下：
``` Javascript
for (initialization; expression; post-loop-expression) statement
```
例子：

``` Javascript
for(let index=0;index<100;index++){}

//这里index是一个局部变量，作用域是for循环的参数列表以及for循环内部。
```

## for-in迭代器循环语句

for-in 语句是一种严格的迭代语句，用于枚举对象中的非符号键属性。

语法如下：

``` Javascript
for (property in expression) statement
```
例子：

``` Javascript
for (const propName in window) { 
 document.write(propName); 
}
//这里propName是一个局部变量，其作用域是每一次迭代过程。
//也就是说，上一次迭代与这一次迭代之间的propName实际是处于两个不同作用域的同名变量。
//这里为啥使用const而不使用let？这是为了防止在这一次迭代处理过程中意外改变propName的值。当然，这里也可以使用let，但是const更好。
```

## for-of迭代器循环语句

for-of 语句是一种严格的迭代语句，用于遍历可迭代对象的元素。(es6新增)

语句如下：

``` Javascript
for (property of expression) statement
```
例子：

``` Javascript
for (const el of [2,4,6,8]) { 
 document.write(el); 
}
// 这里的el也是一个局部变量，其作用域是每一次迭代过程。
//也就是说，上一次迭代与这一次迭代之间的el实际是处于两个不同作用域的同名变量。
//这里为啥使用const而不使用let？这是为了防止在这一次迭代处理过程中意外改变el的值。当然，这里也可以使用let，但是const更好。
```

## label标签语句

label标签语句的作用是给跳转语句设置一个跳转点。（慎用，这会影响程序的可维护性。）

语法如下：

``` Javascript
label: statement
```
例子：

``` Javascript
start: for (let i = 0; i < count; i++) { 
 console.log(i); 
}
```

## break和continue语句

break和continue语句用来退出循环，break是退出整个循环，而continue是中断此次循环。

它们都可以在后面附带标签，从而中断循环执行之后，从标签位置重新开始执行。(慎用，这会影响程序的可维护性。)


例子：

``` Javascript
let num = 0; 
for (let i = 1; i < 10; i++) { 
 if (i % 5 == 0) { 
 break; //循环执行到第五次的时候，执行break，然后整个for循环执行结束，转到consolo.log(num)执行，此时num为4。
 } 
 num++; 
} 
console.log(num); // 4

let num = 0; 
for (let i = 1; i < 10; i++) { 
 if (i % 5 == 0) { 
 continue; // 执行到第五次直接中断执行，num少加一次，所以最后的结果是num=8。
 } 
 num++; 
} 
console.log(num); // 8
```

标签跳转的例子就不举了，这个特性慎用。

## with语句

with 语句的用途是将代码作用域设置为特定的对象。

语法如下：

``` Javascript
with (expression) statement;
```

由于with语句很难调试，而且会影响程序性能，目前已经不太推荐使用with语句了。

## switch语句

switch语句常常用于多个分支跳转的情况，另外相关的关键字case和default。

语法通常如下：

``` Javascript
switch (expression) { 
 case value1: 
    statement 
    break; 
 case value2: 
    statement 
    break; 
 case value3: 
    statement 
    break; 
 case value4: 
    statement 
    break; 
 default: //default可以不写
    statement 
}
```

## return语句

该语句用于结束function的code的执行结束，我也把它放在这里吧，好像现在除了变量定义语句其它的语句都在这里有所说明了。

流程控制语句也没有太多的东西可说，就这样吧。