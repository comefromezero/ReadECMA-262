# Type

## primitive value(原始值) 和 reference value(引用值)

ECMAScript 变量可以包含两种不同类型的数据：原始值和引用值。原始值（primitive value）就是最简单的数据，引用值（reference value）则是由多个值构成的对象。

在把一个值赋给变量时，JavaScript 引擎必须确定这个值是原始值还是引用值。Js中有6种原始值：Undefined、Null、Boolean、Number、String 和 Symbol（ES6中新增）。保存原始值的变量是按值（by value）访问的，因为我们操作的就是存储在变量中的实际值。

引用值是保存在内存中的对象。与其他语言不同，JavaScript 不允许直接访问内存位置，因此也就不能直接操作对象所在的内存空间。在操作对象时，实际上操作的是对该对象的引用（reference）而非实际的对象本身。为此，保存引用值的变量是按引用（by reference）访问的。

### 原始值与引用值的不同之处

* 原始值不能添加、删除、修改属性和方法，引用值可以添加、删除、修改属性和方法

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

 