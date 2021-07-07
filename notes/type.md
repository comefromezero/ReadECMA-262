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
``` Javascript
let message; 
console.log(message == undefined); // true
let message = undefined; 
console.log(message == undefined); // true
```

## Null 类型

Null 类型同样只有一个值，即特殊值 null。逻辑上讲，null 值表示一个空对象指针，这也是给typeof 传一个 null 会返回"object"的原因。

``` Javascript
let car = null; 
console.log(typeof car); // "object"
```

tips:undefined 值是由 null 值派生而来的，因此 ECMA-262 将它们定义为表面上相等，如下面的例子所示：

``` Javascript
console.log(null == undefined); // true
```

## Boolean 类型

Boolean（布尔值）类型是 ECMAScript 中使用最频繁的类型之一，有两个字面值：true 和 false。这两个布尔值不同于数值，因此 true 不等于 1，false 不等于 0。

``` Javascript
let found = true; 
let lost = false;
```

其他类型与boolean的转换：

|数据类型|转换为true的值|转换为false的值|
|--------|------------|--------------|
|Boolean |true        |  false       |
|String  |非空字符串   | 空字符串      |
|Number  |非零数值（包括无穷值）|0、NaN |
|Object  |任意对象     | null         |
|Undefined|N/A(不存在) |undefined    |

## Number 类型
ECMAScript 中最有意思的数据类型或许就是 Number 了。Number 类型使用 IEEE 754 格式表示整数和浮点值（在某些语言中也叫双精度值）。不同的数值类型相应地也有不同的数值字面量格式。

``` Javascript
let intNum = 55; // 整数
let octalNum1 = 070; // 八进制的 56 
let octalNum2 = 079; // 无效的八进制值，当成 79 处理
let octalNum3 = 08; // 无效的八进制值，当成 8 处理
let hexNum1 = 0xA; // 十六进制 10 
let hexNum2 = 0x1f; // 十六进制 31
let floatNum1 = 1.1; 
let floatNum2 = 0.1; 
let floatNum3 = .1; // 有效，但不推荐
let floatNum1 = 1.; // 小数点后面没有数字，当成整数 1 处理
let floatNum2 = 10.0; // 小数点后面是零，当成整数 10 处理
let floatNum = 3.125e7; // 等于 31250000
let floatNum = 3e-17; //等于0.000 000 000 000 000 03 
```

### 值得范围

由于内存的限制，ECMAScript 并不支持表示这个世界上的所有数值。ECMAScript 可以表示的最小数值保存在 Number.MIN_VALUE 中，这个值在多数浏览器中是 5e-324；可以表示的最大数值保存在Number.MAX_VALUE 中，这个值在多数浏览器中是 1.797 693 134 862 315 7e+308。如果某个计算得到的数值结果超出了 JavaScript 可以表示的范围，那么这个数值会被自动转换为一个特殊的 Infinity（无穷）值。任何无法表示的负数以-Infinity（负无穷大）表示，任何无法表示的正数以 Infinity（正无穷大）表示。

如果计算返回正 Infinity 或负 Infinity，则该值将不能再进一步用于任何计算。这是因为Infinity 没有可用于计算的数值表示形式。要确定一个值是不是有限大（即介于JavaScript 能表示的最小值和最大值之间），可以使用 isFinite()函数，如下所示：

``` Javascript
let result = Number.MAX_VALUE + Number.MAX_VALUE; 
console.log(isFinite(result)); // false
```

### 特殊值：NaN

有一个特殊的数值叫 NaN，意思是“不是数值”（Not a Number），用于表示本来要返回数值的操作失败了（而不是抛出错误）。

在 ECMAScript 中，0、+0 或0 相除会返回 NaN：在 ECMAScript 中，0、+0 或-0 相除会返回 NaN：

``` Javascript
console.log(0/0); // NaN 
console.log(-0/+0); // NaN
```

如果分子是非 0 值，分母是有符号 0 或无符号 0，则会返回 Infinity 或-Infinity：

``` Javascript
console.log(5/0); // Infinity 
console.log(5/-0); // -Infinity
```

#### 特性

* 任何涉及 NaN 的操作始终返回 NaN（如 NaN/10，返回NaN）。

* NaN 不等于包括 NaN 在内的任何值。例如，console.log(NaN == NaN); // false。

* isNaN()函数：函数接收一个参数，可以是任意数据类型，然后判断这个参数是否“不是数值”。把一个值传给 isNaN()后，该函数会尝试把它转换为数值。某些非数值的
值可以直接转换成数值，如字符串"10"或布尔值。任何不能转换为数值的值都会导致这个函数返回true。

``` Javascript
console.log(isNaN(NaN)); // true 
console.log(isNaN(10)); // false，10 是数值
console.log(isNaN("10")); // false，可以转换为数值 10 
console.log(isNaN("blue")); // true，不可以转换为数值
console.log(isNaN(true)); // false，可以转换为数值 1
```

### 非数值转换为数值

有 3 个函数可以将非数值转换为数值：Number()、parseInt()和 parseFloat()。Number()是转型函数，可用于任何数据类型。后两个函数主要用于将字符串转换为数值。

Number()转换规则:

* 布尔值，true 转换为 1，false 转换为 0。
* 数值，直接返回。
* null，返回 0。
* undefined，返回 NaN。
* 字符串，应用以下规则。
    * 如果字符串包含数值字符，包括数值字符前面带加、减号的情况，则转换为一个十进制数值。因此，Number("1")返回 1，Number("123")返回 123，Number("011")返回 11（忽略前面的零）。
    * 如果字符串包含有效的浮点值格式如"1.1"，则会转换为相应的浮点值（同样，忽略前面的零）。
    * 如果字符串包含有效的十六进制格式如"0xf"，则会转换为与该十六进制值对应的十进制整数值。
    * 如果是空字符串（不包含字符），则返回 0。
    * 如果字符串包含除上述情况之外的其他字符，则返回 NaN。
* 对象，调用 valueOf()方法，并按照上述规则转换返回的值。如果转换结果是 NaN，则调用toString()方法，再按照转换字符串的规则转换。
``` Javascript
let num1 = Number("Hello world!"); // NaN 
let num2 = Number(""); // 0 
let num3 = Number("000011"); // 11 
let num4 = Number(true); // 1
```

parseInt()函数：将字符串转换为整数。转换规则：

* 字符串最前面的空格会被忽略，从第一个非空格字符开始转换。
* 如果第一个字符不是数值字符、加号或减号，parseInt()立即返回 NaN。
* 空字符串返回 NaN。
* 如果第一个字符是数值字符、加号或减号，则继续依次检测每个字符，直到字符串末尾，或碰到非数值字符。
``` Javascript
let num1 = parseInt("1234blue"); // 1234 
let num2 = parseInt(""); // NaN 
let num3 = parseInt("0xA"); // 10，解释为十六进制整数
let num4 = parseInt(22.5); // 22 
let num5 = parseInt("70"); // 70，解释为十进制值
let num6 = parseInt("0xf"); // 15，解释为十六进制整数
```
tips:parseInt()也接收第二个参数，用于指定底数（进制数）,例如：
``` Javascript
let num = parseInt("0xAF", 16); // 175
let num1 = parseInt("AF", 16); // 175 
let num2 = parseInt("AF"); // NaN
let num1 = parseInt("10", 2); // 2，按二进制解析
let num2 = parseInt("10", 8); // 8，按八进制解析
let num3 = parseInt("10", 10); // 10，按十进制解析
let num4 = parseInt("10", 16); // 16，按十六进制解析
```
因为不传底数参数相当于让 parseInt()自己决定如何解析，所以为避免解析出错，建议始终传给它第二个参数。

parseFloat()函数：将字符串转换为整数或者浮点。转转规则：

* 从位置 0 开始检测每个字符。同样，它也是解析到字符串末尾或者解析到一个无效的浮点数值字符为止。
* 第一次出现的小数点是有效的，但第二次出现的小数点就无效了，此时字符串的剩余字符都会被忽略。因此，"22.34.5"将转换成 22.34。
* 始终忽略字符串开头的零。
* 如果字符串表示整数（没有小数点或者小、数点后面只有一个零），则 parseFloat()返回整数。
* 十六进制数值始终会返回 0。

``` Javascript
let num1 = parseFloat("1234blue"); // 1234，按整数解析
let num2 = parseFloat("0xA"); // 0 
let num3 = parseFloat("22.5"); // 22.5 
let num4 = parseFloat("22.34.5"); // 22.34 
let num5 = parseFloat("0908.5"); // 908.5 
let num6 = parseFloat("3.125e7"); // 31250000
```

tips：

* 严格模式下，禁止使用八进制literal,但是可以使用0o为前缀表示八进制。

* Number在表示浮点数的时候，一定要注意IEEE754的限制，同时，也要注意浮点数的精度问题,浮点值的精确度最高可达 17 位小数，但在算术计算中远不如整数精确。例如，0.1加 0.2得到的不是 0.3，而是 0.300 000 000 000 000 04。由于这种微小的舍入错误，导致很难测试特定的浮点值。

* 正因为浮点精度问题，永远不要用两个浮点数的大小以及相等关系来作为判断条件。

* 浮点数小数点之前的数字可以省略，省略之后，默认为0.

* 在小数点后面没有数字的情况下，数值就会变成整数。如果数值本身就是整数，只是小数点后面跟着 0（如 1.0），那它也会被转换为整数。

* 在计算非常大的数值和非常小的数值的时候都需要特别小心，因为很可能超出Number的表示范围，关注数量级e-324和e308。


## String 类型
String（字符串）数据类型表示零或多个 16 位 Unicode 字符序列。字符串可以使用双引号（"）、单引号（'）标识。

``` Javascript
let firstName = "John"; 
let lastName = 'Jacob';
```

tips：
* 字符串中某些字符可以使用转义序列。
* 字符串是不可变的（immutable），意思是一旦创建，它们的值就不能变了。要修改某个变量中的字符串值，必须先销毁原始的字符串，然后将包含新值的另一个字符串保存到该变量。例如：
``` Javascript
let lang = "Java"; 
lang = lang + "Script";
```

### 其他类型转转为字符串
有两种方式把一个值转换为字符串。一个是toString()方法；另外一个是String()函数。

toString()方法可见于数值、布尔值、对象和字符串值。（没错，字符串值也有 toString()方法，该方法只是简单地返回自身的一个副本。）null 和 undefined 值没有 toString()方法。
``` Javascript
let age = 11; 
let ageAsString = age.toString(); // 字符串"11" 
let found = true; 
let foundAsString = found.toString(); // 字符串"true"
```
对于数值的toString()方法，其可以接收一个底数参数。默认情况下，toString()返回数值的十进制字符串表示。通过传入参数，可以得到数值的二进制、八进制、十六进制，或者其他任何有效基数的字符串表示。
``` Javascript
let num = 10; 
console.log(num.toString()); // "10" 
console.log(num.toString(2)); // "1010" 
console.log(num.toString(8)); // "12" 
console.log(num.toString(10)); // "10" 
console.log(num.toString(16)); // "a"
```

String()转型函数，它始终会返回表示相应类型值的字符串。String()函数遵循如下规则:
* 如果值有 toString()方法，则调用该方法（不传参数）并返回结果。
* 如果值是 null，返回"null"。
* 如果值是 undefined，返回"undefined"。
``` Javascript
let value1 = 10; 
let value2 = true; 
let value3 = null; 
let value4; 
console.log(String(value1)); // "10" 
console.log(String(value2)); // "true" 
console.log(String(value3)); // "null" 
console.log(String(value4)); // "undefined"
```

### 模板字符串（ES6新增）

ECMAScript 6 新增了使用模板字面量定义字符串的能力。其通过``包围定义。
``` Javascript
let lastName = `Jingleheimerschmidt`
```
模板字符串一般用于定义HTML模板，这里我们讨论。

## 包装类型：Boolean、Number、String。

为了方便操作原始值，ECMAScript 提供了 3 种特殊的引用类型：Boolean、Number 和 String。这些类型具有本章介绍的其他引用类型一样的特点，但也具有与各自原始类型对应的特殊行为。每当用到某个原始值的方法或属性时，后台都会创建一个相应原始包装类型的对象，从而暴露出操作原始值的各种方法。

例子：

``` Javascript
let s1 = "some text"; 
let s2 = s1.substring(2);
```
在这里，s1 是一个包含字符串的变量，它是一个原始值。第二行紧接着在 s1 上调用了 substring()方法，并把结果保存在 s2 中。

我们知道，原始值本身不是对象，因此逻辑上不应该有方法。而实际上这个例子又确实按照预期运行了。这是因为后台进行了很多处理，从而实现了上述操作。具体来说，当
第二行访问 s1 时，是以读模式访问的，也就是要从内存中读取变量保存的值。在以读模式访问字符串值的任何时候，后台都会执行以下 3 步：

(1) 创建一个 String 类型的实例；

(2) 调用实例上的特定方法；

(3) 销毁实例。

可以把这 3 步想象成执行了如下 3 行 ECMAScript 代码：

``` Javascript
let s1 = new String("some text"); 
let s2 = s1.substring(2); 
s1 = null;
```

这种行为可以让原始值拥有对象的行为。对布尔值和数值而言，以上 3 步也会在后台发生，只不过使用的是 Boolean 和 Number 包装类型而已。

### 包装类型与引用值类型的不同之处

引用类型与原始值包装类型的主要区别在于对象的生命周期。在通过 new 实例化引用类型后，得到的实例会在离开作用域时被销毁，而自动创建的原始值包装对象则只存在于访问它的那行代码执行期间。

## Symbol 类型

Symbol（符号）是 ECMAScript 6 新增的数据类型。符号是原始值，且符号实例是唯一、不可变的。符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险。

目前没发现什么用途，后续再看。


## Object 类型

ECMAScript 中的对象其实就是一组数据和功能的集合。对象通过 new 操作符后跟对象类型的名称来创建。开发者可以通过创建 Object 类型的实例来创建自己的对象，然后再给对象添加属性和方法：
``` Javascript
let o = new Object();
```

ECMAScript提供了很多Native Object：Date、RegExp、Boolean、Number、String、Global、Math、Object、Array、Map、set等。