# Type
ECMAScript 有 6 种简单数据类型（也称为原始类型）：Undefined、Null、Boolean、Number、String 和 Symbol。Symbol（符号）是 ECMAScript 6 新增的。还有一种复杂数据类型叫 Object（对象）。Object 是一种无序名值对的集合。因为在 ECMAScript 中不能定义自己的数据类型，所有值都可以用上述 7 种数据类型之一来表示。

## primitive value(原始值) 和 reference value(引用值)

ECMAScript 变量可以包含两种不同类型的数据：原始值和引用值。原始值（primitive value）就是最简单的数据，引用值（reference value）则是由多个值构成的对象。

在把一个值赋给变量时，JavaScript 引擎必须确定这个值是原始值还是引用值。Js中有6种原始值：Undefined、Null、Boolean、Number、String 和 Symbol（ES6中新增）。保存原始值的变量是按值（by value）访问的，因为我们操作的就是存储在变量中的实际值。

引用值是保存在内存中的对象。与其他语言不同，JavaScript 不允许直接访问内存位置，因此也就不能直接操作对象所在的内存空间。在操作对象时，实际上操作的是对该对象的引用（reference）而非实际的对象本身。为此，保存引用值的变量是按引用（by reference）访问的。

### 原始值与引用值的不同之处

* 原始值不能添加、删除、修改属性和方法，引用值可以添加、删除、修改属性和方法。

对于引用值而言，可以随时添加、修改和删除其属性和方法(这一点应该不用怀疑，我们在操作引用值的时候，实际上就好像在操作其引用的对象一样，我们可以把引用值理解为一个对象的别名，一个对象自然而然能够添加、修改和删除属性与方法。)。比如，看下面的例子：

``` Javascript
let person = new Object(); 
person.name = "Nicholas"; 
console.log(person.name); // "Nicholas"
```

这里，首先创建了一个对象，并把它保存在变量 person 中。然后，给这个对象添加了一个名为name 的属性，并给这个属性赋值了一个字符串"Nicholas"。在此之后，就可以访问这个新属性，直到对象被销毁或属性被显式地删除。

原始值不能有属性，尽管尝试给原始值添加属性不会报错。比如：

``` Javascript
let name = "Nicholas"; 
name.age = 27; 
console.log(name.age); // undefined
```

在此，代码想给字符串 name 定义一个 age 属性并给该属性赋值 27。紧接着在下一行，属性不见了。

* 复制值（值传递）：原始值通过赋值传递给另外一个变量，会将值复制给新的变量；引用值通过赋值传递给另外一个变量，也会将存储在变量中的值复制给新的变量，但是这个值实际上是一个指向对象的指针。

在通过变量把一个原始值赋值到另一个变量时，原始值会被复制到新变量的位置。请看下面的例子：

``` Javascript
let num1 = 5; 
let num2 = num1;
```
这里，num1 包含数值 5。当把 num2 初始化为 num1 时，num2 也会得到数值 5。这个值跟存储在num1 中的 5 是完全独立的，因为它是那个值的副本。

![原始值复制](https://github.com/comefromezero/ReadECMA-262/blob/main/img/%E5%8E%9F%E5%A7%8B%E5%80%BC%E5%A4%8D%E5%88%B6.png)

在把引用值从一个变量赋给另一个变量时，存储在变量中的值也会被复制到新变量所在的位置。区别在于，这里复制的值实际上是一个指针，它指向存储在堆内存中的对象。操作完成后，两个变量实际上指向同一个对象，因此一个对象上面的变化会在另一个对象上反映出来，如下面的例子所示：

``` Javascript
let obj1 = new Object(); 
let obj2 = obj1; 
obj1.name = "Nicholas"; 
console.log(obj2.name); // "Nicholas"
```
在这个例子中，变量 obj1 保存了一个新对象的实例。然后，这个值被复制到 obj2，此时两个变量都指向了同一个对象。在给 obj1 创建属性 name 并赋值后，通过 obj2 也可以访问这个属性，因为它们都指向同一个对象。

![引用值复制](https://github.com/comefromezero/ReadECMA-262/blob/main/img/%E5%BC%95%E7%94%A8%E5%80%BC%E5%A4%8D%E5%88%B6.png)

* 函数参数传递:情况同值复制。

所有函数的参数都是按值传递的。这意味着函数外的值会被复制到函数内部的参数中，就像从一个变量复制到另一个变量一样。如果是原始值，那么就跟原始值变量的复制一样，如果是引用值，那么就跟引用值变量的复制一样。

来看下面这个例子：

``` Javascript
function addTen(num) { 
 num += 10; 
 return num; 
} 
let count = 20;
let result = addTen(count); 
console.log(count); // 20，没有变化
console.log(result); // 30
```

这里，函数 addTen()有一个参数 num，它其实是一个局部变量。在调用时，变量 count 作为参数传入。count 的值是 20，这个值被复制到参数 num 以便在 addTen()内部使用。在函数内部，参数 num的值被加上了 10，但这不会影响函数外部的原始变量 count。参数 num 和变量 count 互不干扰，它们只不过碰巧保存了一样的值。

再看这个例子：

``` Javascript
function setName(obj) { 
 obj.name = "Nicholas"; 
} 
let person = new Object(); 
setName(person); 
console.log(person.name); // "Nicholas"
```

我们创建了一个对象并把它保存在变量 person 中。然后，这个对象被传给 setName()方法，并被复制到参数 obj 中。在函数内部，obj 和 person 都指向同一个对象。结果就是，即使对象是按值传进函数的，obj 也会通过引用访问对象。当函数内部给 obj 设置了 name 属性时，函数外部的对象也会反映这个变化，因为 obj 指向的对象保存在全局作用域的堆内存上。

* 类型操作符：typeof与instanceof。

typeof操作符：typeof variable。

对于字符串、数值、布尔值、Symbol或 undefined，typeof都会返回对应的类型；但是对于null和object，typeof会返回object类型。对于null来说，我们可以认为它是对一个空对象的引用，那么typeof null返回object也就不足为奇了。

tips:typeof作用于函数的时候，其会返回function。ECMA-262 规定，任何实现内部[[Call]]方法的对象都应该在typeof 检测时返回"function"。当在 Safari（直到 Safari 5） 和 Chrome（直到 Chrome 7）中用于检测正则表达式时，由于实现细节的原因，typeof也会返回"function"。在 IE 和 Firefox 中，typeof 对正则表达式返回"object"。

例子：

``` Javascript
let s = "Nicholas"; 
let b = true; 
let i = 22; 
let u; 
let n = null; 
let o = new Object(); 
console.log(typeof s); // string 
console.log(typeof i); // number 
console.log(typeof b); // boolean 
console.log(typeof u); // undefined 
console.log(typeof n); // object 
console.log(typeof o); // object
```

对于原始值来说typeof能够很好的反应类型，但是对于引用值来说，typeof只会返回Object，显然任何引用都是对应某个对象，但是我们更多的是想知道该引用对应的对象是什么类型的对象。

instanceof操作符：variable instanceof constructor。

如果variable是constructor的一个实例，那么就会返回true，否则返回false。

对于原始值来说，使用instanceof总会得到false，因为原始值不可能是某个对象的实例。

对于引用值来说，使用instanceof根据其引用的对象是否为对应的constructor的实例来获得true还是false。

instanceof的计算过程：instanceof会遍历variable的原型链（__proro__属性），如果找到一个对象与constructor是相同的对象，那么就返回true；如果遍历到了variable的原型链尽头，还没有找到一个与constructor相同的对象，那么就返回false。

因此，由原型链可知，任何引用值都是Object对象，此通过 instanceof 操作符检测任何引用值和Object 构造函数都会返回 true。

例子：

``` Javascript
let str = new String();
let nothing = null;
let num = 100;
let ob = new Object();

console.log(str instanceof String); //true
console.log(nothing instanceof Object); //false
console.log(num instanceof Object); //false
console.log(ob instanceof Object); //true
console.log(str instanceof Object); //true
console.log(ob instanceof String); //false
```

## Undefined类型

Undefined 类型只有一个值，就是特殊值 undefined。当使用 var 或 let 声明了变量但没有初始化时，就相当于给变量赋予了 undefined 值。

## Null 类型

Null 类型同样只有一个值，即特殊值 null。逻辑上讲，null 值表示一个空对象指针，这也是给typeof 传一个 null 会返回"object"的原因。

tips:undefined 值是由 null 值派生而来的，因此 ECMA-262 将它们定义为表面上相等，如下面的例子所示：

``` Javascript
console.log(null == undefined); // true
```

## Boolean 类型

Boolean（布尔值）类型是 ECMAScript 中使用最频繁的类型之一，有两个字面值：true 和 false。这两个布尔值不同于数值，因此 true 不等于 1，false 不等于 0。

其他类型与boolean的转换：

|数据类型|转换为true的值|转换为false的值|
|--------|------------|--------------|
|Boolean |true        |  false       |
|String  |非空字符串   | 空字符串      |
|Number  |非零数值（包括无穷值）|0、NaN |
|Object  |任意对象     | null         |
|Undefined|N/A(不存在) |undefined    |




## 包装类型：Boolean、Number、String。