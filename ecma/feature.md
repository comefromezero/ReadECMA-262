# ES2.0的特性（1996）

## source text

起步支持unicode2.0（这里规定了源字符的范围，U0000到U10FFFF的所有字符）

## WhiteSpace

<TAB> //Tab 

<VT>  //Vertical Tab

<FF>  //Form Feed 换页

<SP>  //Space 空格

## LineTerminator

<LF> //Line Feed 换行

<CR> //Carriage Return 回车

## comments

// 单行注释

/* 多行注释 */

## keywords and reserved words

### keywords

break        

for                

new         

var

continue  

function       

return      

void

delete       

if                   

this          

while

else          

in                  

typeof      

with

### future reserved words

abstract

do

import

short

boolean

double

instanceof

static

byte

enum

int

super

case

export

interface

switch

catch

extends

long

synchronized

char

final

native

throw

class

finally

package

throws

const

float

private

transient

debugger

goto

protected

try

default

implements

public

volatile

### other

这三个都是Reserved Words，这是最容易被人忽略的，需要注意。

null

true 

false

## identifier

可以有以下字符组成：

26个大小写字母

$  _  

以及0-9等阿拉伯数字

不能以0-9这几个阿拉伯数字开头

不能是保留字

## punctuator

=                 

\>                   

<                 

==                  

<=                     

\>=

!=                

,                    

!                   

~                   

?:

.                  

&&                

||                 

++                   

--                       

\+

\-                  

\*                    

/                   

&                    

|                        

^

%                

<<                 

\>>               

\>>>                

+=                     

-=

*=                

/=                

&=               

|=                   

^=                     

%=

<<=            

\>>=               

\>>>=           

(  )                         

{ }                  

[ ]                  

;

## literal

### 1、NULL

null

### 2、bool

true

false

### 3、Number

1)、十进制

0

08793

123

-999

+888

2）、浮点值

公式：[ digtals ] [ .digtals ] [ (E|e) [(+|-)] digtals ]

3）、十六进制值

0x和0X开头

例如：0x123e和0Xa68等。

4）、八进制值

0开头+八进制数字

例如：0377//十进制为255。

5）、正负值

前面不加符号或加+号表示正数

前面加-号表示负数

以上所有的值均可在前面加上正负号或者不加。

例如：-0.22，+3.14，-0x123e，-0377等。

### 4、字符串

"双引号字符串"

'单引号字符串'

## Automatic Semicolon Insertion（自动分号插入）

ES规定了其一条语句的结束是;，但是用户在写的时候可以省略一些;，然后ES会自动推导出应该在哪些地方添加;。

具体算法：ES2.0章节7.8

以上部分为ES规定的词法相关要求。

## Types

### primitive type

Null，Undefined，Boolean，String，Number

### reference type

Object

## Type Conversion

ES2.0章节9规定了Types之间的任意转换方法。

## Execution Contexts

这个部分根据文档有所不同，主要定义了执行过程中遇到的各种概念。

而这些概念有些则纯粹用于ES文档中，用于说明各种过程。

### Function Objects

* Declared functions

* Anonymous functions

* Implementation-supplied functions

* Internal functions

### Types of Executable Code

* Global code

* Eval code

* Function code

* Anonymous code

* Implementation-supplied code

### Variable instantiation

这里讲述了声明的不同类型的标识符在程序执行过程中的实例化。

* FunctionDeclaration

* formal parameter

* VariableDeclaration

### Scope Chain and Identifier Resolution

这里直接规定了作用域链以及如何在作用域链中分辨标识符。

### Global Object

program开始执行之前一定会创建一个global object，并初始化一些Properties，在执行的过程中可能也会添加一些Proerties到global object中。在HTML中，这个global object称为windows。

### Activation object

当执行进入declared function code, anonymous code or
implementation-supplied code的执行上下文的时候，一个activation object就会被创建，该activation object与该执行上下文相关联，并且它实例化的时候，会获得arguments这个proeprty。

后续继续执行程序，该activation object会作为variable object（用于变量的实例化）。

当程序执行离开该执行上下文的时候，该activation object被销毁。

### This

这个指向当前上下文，没什么好说的。

### Arguments Object

当程序执行进入declared function code, anonymous code, or
implementation-supplied code的时候，一个arguments对象被创建。

该对象主要用于保存各种参数，以及初始化一些例如callee，length等properties。

### Entering An Execution Context

这里有四类代码，当程序执行进入这些代码的时候，执行上下文的初始化以及一些properties会有所不同。

#### Global Code

#### Eval Code

#### Function and Anonymous Code

#### Implementation-supplied Code

## Statements

* Block 

* Variable statement 

* Empty statement 

* Expression statement 

* The if statement 

* Iteration statements 

    1. The while statement 

    2. The for statement 

    3. The for..in statement 

    4. The continue statement 

* The break statement 

* The return statement 

* The with statement

## Expressions

### Primary Expressions 

* The this keyword 

* Identifier reference 

* Literal reference 

* The Grouping Operator 

### Left-Hand-Side Expressions 

* Property Accessors 

* The new operator 

* Function Calls 

* Argument Lists 

### Postfix expressions 

* Postfix increment operator 

* Postfix decrement operator 

### Unary operators 

* The delete operator 

* The void operator 

* The typeof operator 

* Prefix increment operator 

* Prefix decrement operator 

* Unary + operator 

* Unary - operator 

* The bitwise NOT operator ( ~ ) 

* Logical NOT operator ( ! ) 

### Multiplicative operators 

* Applying the * operator 

* Applying the / operator 

* Applying the % operator 

### Additive operators 

* The addition operator ( + ) 

* The subtraction operator ( - ) 

* Applying the additive operators (+, -) to numbers 

### Bitwise shift operators 

* The left shift operator ( << ) 

* The signed right shift operator ( >> ) 

* The unsigned right shift operator ( >>> ) 

### Relational operators 

* The less-than operator ( < ) 

* The greater-than operator ( > ) 

* The less-than-or-equal operator ( <= ) 

* The greater-than-or-equal operator ( >= ) 

* The in operator ( in )

### Equality operators 

* The equals operator ( == ) 

* The does-not-equals operator ( != ) 

### Binary bitwise operators 

### Binary logical operators 

### Conditional operator ( ?: ) 

### Assignment operators 

* Simple Assignment ( = ) 

* Compound assignment ( op= ) 

### Comma operator ( , )

## Function Definition

* 规定了函数定义的形式。

## Program

* 确定了一个program的基本结构。

一个Program由statements和FunctionDeclaration组成。

## Native ECMAScript Object

The Global Object、Object、Function、Array、String、Boolean、Number、Math、Date

### prototype chain

详细见:章节4.2,该章节详解介绍了原型链，深刻诠释了js对象之间的关系，正是通过原型链，JS实现对象之间的继承。

### The Global Object

全局对象是一个特殊的对象(单例对象)，也是整个JS执行过程中的第一个对象，所有的其他对象或者全局函数以及变量等都是全局对象的property。

### Properties of Global Object

一些平常使用的parseInt()，Math对象等都是它的property。

其他的一些原生对象的构造函数也是它的property。

详细见：ES2.0章节15.1

### Object Objects

一切对象都源于Object.prototype Object这个对象，它处在原型链的最顶端。

一些Object的方法，例如valueof其实在ES2.0就已经实现了。

其他的property详见：章节15.2。

### Function Objects

所有Prototype Object的constructor都是一个函数，所以它们都是一个Function Object Instance。

比较常用的property，Function Object Instance中最有用的一个property，即length，该property表明了该function接收的参数个数。还有一个property，它就是prototype，该属性肯定了Function的双重身份，既是一个function 对象也是一个对象的constructor。

详见：章节15.3

### Array Objects

Prototype Ojbect的toString(),join(),reverse(),sort()等Property都非常有用。

其instance中有用的property：length。

详见：章节15.4

### String Objects

Prototype Object的toString(),valueOf(),charAt(),indexOf(),lastIndexOf(),split(),substring(),toUpperCase(),toLowerCase()等都是非常常用的。

其instance中有用的property：length。

详见：章节15.5

### Booloean objects

Boolean比较简单，其Prototype Object总共就具备两个property:toString()和valueOf()。

详见：章节15.6

### Number objects

Number这个应该是比较有意思的一个Object，在实际使用过程中，很少会用到它以及它的各种properties。

Prototype Object比较有用的properties:toString()和valueOf();

详见：章节15.7

### Math objects

Math这个对象是唯一一个不能实例化的对象(单例对象)，其不能用于new 表达式，其存在的意义就是提供各种数学计算函数以及一些特殊的数学常量。

一些properties:

E：对，就是那个特殊的数学常量e。

PI：对，就是圆周率，π。

abs():绝对值函数。

ceil():不小于参数的最小整数。

floor():不大于参数的最大整数。

max():返回较大的那个数字。

min():返回较小的那个数字。

pow():计算指数值。

random():随机数,正数，其可能等于0，但是绝对小于1的随机数。

详见：章节15.8

### Date objects

这个对象是JS中的时间相关的部分，需要获取当前时间，或者获得一个具体时间的话，都需要用到它。

对于Date对象来说，其构造函数具有多种形式，根据不同的需要使用不同的形式：

 Date(year, month, date, hours, minutes, seconds, ms)

 Date(year, month, date, hours, minutes, seconds)

 Date(year, month, date, hours, minutes)

 Date(year, month, date, hours)

 Date(year, month, day)

 Date(year, month)

 Date(value):value表示1970年1月1日0时之后的毫秒数。

其中需要经常用到的一些properties:

parse():从某一个字符串日期时间获取一个Date对象，返回毫秒数。

UTC():从某个日期生成Date对象，返回毫秒数。

一些Prototype Object的properties:

toString()

valueOf()

getTime():获取当前Date对象中记录的时间距离1970年1月1日之后的毫秒数。

getFullYear():获取当前Date对象中的年份。

getMonth():获取当前Date对象中的月份。

getDay():获取当前Date对象中的时间位于一周的星期几。

toLocaleString()

toUTCString()

toGMTString()

详见：章节15.9

# ES3.0（1999）

## ES3.0新增特性

新增特性主要集中在以下几个方面：

### pwoerful regular expressions

新增正则表达式，增强了语言的字符处理能力。

### better string handling

新增了一些现在经常使用的一些字符串处理的API，例如：concat ( [ string1 [ , string2 [ , … ] ] ] )，replace (searchValue, replaceValue)，search (regexp)，slice (start, end)。

### new control statements

switch/case/default语句

throw语句

try/catch/finally语句

do/while语句

### try/catch exception handling

增加了异常处理机制。

### tighter definition of errors

更严格的错误定义。

下面只是列出了做出改动或者新增的内容，对于没有改动的部分则没有列出来。

## source text

起步支持unicode2.1（这里规定了源字符的范围，U0000到U10FFFF的所有字符）

## White Space

新增：

* <NBSP> //No-break space

* <USP>  //Any other Unicode “space separator”

## Line Terminator

* <LS> //Line separator

* <PS> //Paragraph separator

## keywords and reserved words

### keywords

新增9个关键字，case switch default finally try catch throw do instanceof

### future reserved words

减少上述9个关键字

## identifier

以任意的Unicode letter字符和$以及_开头还有\Escape字符，后面跟上任意的unicode字符均可。

不能是保留字。

Unicode letter：any character in the Unicode categories “Uppercase letter (Lu)”, “Lowercase letter (Ll)”, “Titlecase letter (Lt)”,

“Modifier letter (Lm)”, “Other letter (Lo)”, or “Letter number (Nl)”.  （具体这几类字符，可以自行查询。）

## punctuator

新增 === 和 !==

### other

\[\]符号，在ES2.0中，\[\]仅仅用于数组访问的下标，ES3.0中新增含义：创建并初始化一个数组，并且可以嵌套。

\{\}符号，在ES2.0中，其仅仅表示块级区域,ES3.0中新增含义：创建并初始化一个对象，可嵌套。

## Literal

新增regular表达式，有两种：第一种是不带flag的Regular表达式，/正则表达式/；第二种是带flag的Regular的表达式，/正则表达式/flag。

正则表达式第一个字符不能是终止符，不能是*，不能是单个的\（可以是转义字符，例如：\b），不能是/，正则表达式不能为空。 

/正则表达式/flags会初始化并创建一个正则表达式对象实例。

## Statements

新增：

* The do-while Statement

* The switch Statement

* Labelled Statements

* The throw statement

* The try statement

## Expressions

### Primary Expressions

新增：

* Array Initialiser

* Object Initialiser

### Left-Hand-Side Expressions

新增：

*  Function Expressions

### Relational Operators

新增：

* The instanceof operator

###  Equality Operators

新增:

* The Strict Equals Operator ( === )

* The Strict Does-not-equal Operator ( !== )


## Native ECMAScript Object

新增：

* RegExp (Regular Expression) Objects

* Error Objects

### The Global Object

新增:

URI相关的编解码prerproty：

* decodeURI (encodedURI)

* decodeURIComponent (encodedURIComponent)

* encodeURI (uri)

*  encodeURIComponent (uriComponent)

这个4个与URI相关的API及其重要，使用比较频繁。

### Object objects

Prototype object新增的一些properties:

* toLocaleString()

* hasOwnProperty(V)

* isPrototypeOf(V)

* propertyIsEnumerable(V)

### Function objects

Prototype object新增：

* apply(thisArg, argArray)

* call(thisArg [ , arg1 [ , arg2, … ] ] )

现在，这个两个property也是经常被使用的。

### Array objects

Prototype obejct新增：

* toLocaleString()

* concat( [ item1 [ , item2 [ , … ] ] ] )

* pop()

* push( [ item1 [ , item2 [ , … ] ] ] )

* shift()

* slice(start, end)

* splice (start, deleteCount [ , item1 [ , item2 [ , … ] ] ] )

* unshift( [ item1 [ , item2 [ , … ] ] ] )

### String objects

Prototype object新增：

* concat( [ string1 [ , string2 [ , … ] ] ] )

* localeCompare (that)

* match (regexp)

* replace (searchValue, replaceValue)

* search (regexp)

* slice (start, end)

* toLocaleLowerCase ( )

* toLocaleUpperCase ( )

### Number objects

Prototype object新增：

* toLocaleString()

* toFixed (fractionDigits)

* toExponential (fractionDigits)

* toPrecision (precision)


### Date objects

Prototype object新增：

* toLocaleTimeString ( )

* toDateString ( )

* toTimeString ( )

* toLocaleDateString ( )


### RegExp objects

这是新增的一个对象，正好对应了ES3.0对正则表达式的支持。

其构造函数包含两个参数：

RegExp(pattern, flags)

其中pattern代表正则表达式，flags代表正则表达式的模糊。

flags:

g：global，全局模式，将匹配所有的匹配项。

i:ignoreCase，忽略大小写。

m:multiline，多行匹配模式。

Prototype object的一些properties:

* exec(string)

* test(string)

* toString()

Instance的一些properties:

* source：说明该正则对象的pattern,不包含开头和结尾的斜杠。

* global：说明该正则对象是否是全局匹配模式。

* ignoreCase：说明该正则对象是否是忽略大小写模式。

* multiline：说明该正则对象是否是多行匹配模式。

* lastIndex：记录下一次搜索开始的位置，始终从0开始。

这些状态量说明了该正则表达式实例的内部情况。


### Error objects

Error object主要就是配合throw语句使用的，即其主要用在try/catch的异常处理机制中。

构造函数：

Error(message):其中message代表需要抛出的错误信息。

Prototype object的一些properties：

* name：错误对象名，对于Error来说，其就是error。

* message：消息，抛出的错误信息。

* toString ( )

Native Error Types:

* EvalError

* RangeError

* ReferenceError

* SyntaxError

* TypeError

以上Native Error Types的prototype都具有两个重要的properties:

* name

* message


# ES5.0（2009，ES5.1于2011年发布）

## ES5.0新增

### accessor properties

存取器properties，这是后来能够实现object hook的核心。

### reflective creation and inspection of objects

这应该得益于存取器属性吧,同时可以使用相应的API重新定义某些Property的attributes。

### program control of property attributes

可以通过相应的API来定义property的attributes,例如Object.defineProperties()。

### additional array manipulation functions

额外的一些数组操作函数。

### support for the JSON object encoding format

从ES5.0开始，JSON正式登陆。

### Strict mode

严格模式下，具有更好的报错信息，已经更好的安全特性。

严格模式应该是ES5.0所做的最大的改动了。


## source text

起步支持unicode3.0（这里规定了源字符的范围，U0000到U10FFFF的所有字符）

## White Space

新增:

* <BOM> //Byte Order Mark

## keywords and reserved words

### keywords

新增：debugger

### reserved words

由于添加了strict mode，所以保留字改动较大。

#### non-strict mode：

class  

enum      

extends     

super     

const     

export    

import
 
#### strict mode：

implements     

let      

private      

public     

yield    

interface     

package    

protected    

static

## Literal

### Regular

新增限制：

第一个字符不能是行终结符，*，\，/，[;

最后有一个字符不能是行终结符，],\。

## Executable Code and Execution Contexts

这部分有所改变，新定义了一系列的操作与一些新概念。

详见：章节 10

以下是新增的部分概念：

* Lexical Environments

* Environment Records

  1. Declarative Environment Records

  2. Object Environment Records

  3. The Global Environment

* Declaration Binding Instantiation

## Statements

### The debugger statement

该语句是新增的，对应于debugger关键字，用于调试，当JS引擎知道该语句的时候，就会断下来，相当于断点了。

## Native ECMAScript Object

新增:

* The JSON object

### The Object objects

#### Properties of Object Constructor

新增：

* getPrototypeOf ( O )

* getOwnPropertyDescriptor ( O, P )

* getOwnPropertyNames ( O )

* create ( O [, Properties] )

* defineProperty ( O, P, Attributes )

* defineProperties ( O, Properties )

* seal ( O )

* freeze ( O )

* preventExtensions ( O )

* isSealed ( O )

* isFrozen ( O )

* isExtensible ( O )

* keys ( O )

这些新增的API增强了Object的功能。

### The Function objects

Properties of prototype object:

新增:

* bind (thisArg [, arg1 [, arg2, …]])

### The Array objects

#### Properties of the Array Constructor

新增:

* isArray ( arg )

#### Properties of prototype object

新增:

* indexOf ( searchElement [ , fromIndex ] )

* lastIndexOf ( searchElement [ , fromIndex ] )

* every ( callbackfn [ , thisArg ] )

* some ( callbackfn [ , thisArg ] )

* forEach ( callbackfn [ , thisArg ] )

* map ( callbackfn [ , thisArg ] )

* filter ( callbackfn [ , thisArg ] )

* reduce ( callbackfn [ , initialValue ] )

* reduceRight ( callbackfn [ , initialValue ] )

### The String objects

Properties of prototype object

新增：

* trim ( )

### The Date objects

#### Properties of the Date Constructor

新增:

now ( )

#### Properties of the Date Prototype Object

新增:

* toISOString ( )

* toJSON ( key )

### The JSON objects

这是ES5.0新增的一个对象，用于支持JSON数据格式。

注意点：JSON对象是一个单例对象。

随着JS对JSON数据格式的原生支持开始，JSON逐渐成为web的标准数据格式，xml也逐步退出历史舞台。

JSON对象具有两个API:

JSON.parse ( text [ , reviver ] ):该API用于将字符串反序列化为一个JSON对象格式。

JSON.stringify ( value [ , replacer [ , space ] ] )：该API用于将JSON对象格式序列化为字符串。

关于stringify这个API有一个非常重要的点需要注意，所有函数和原型成员都会有意地在结果中省略。此外，值为undefined的任何属性也会被跳过。

## Strict mode

严格模式应该是ES5.0中最重要的东西了,也是最大的改动之一了，但是使用严格模式的特性，往往会造成一些兼容性问题，所以不应该使用全局的严格模式，而是应该将其限制在一定范围之内。

[详解](https://github.com/comefromezero/ReadECMA-262/blob/main/notes/strictmode.md)


# ES6.0(ES2015)

ES6.0应该是到现在为止变化最大的一版ES了，其添加的诸多特性极大的提高了JS的工程化能力与性能。

## ES6.0新增

ES6.0除了新增了这些个特性之外，对于原有的一些特性也做了重大升级，但是在这里不一一列出。

### modules

对应import/export，这正是ES6.0中加入的模块化系统。

在这之前，JS一直没有模块化系统，无法将大型程序拆分为很多小模块，这也就导致JS的工程能力较弱。

为了解决JS的模块化的问题，先驱们也提出一些模块化解决方案：

* IIFE（Immediately Invoked Function Expression）

* AMD (Asynchronous Module Definition）

典型代表实现：RequireJS

* CMD(Common Module Definition)

实现：SeaJS。

* CommonJS

这是JS服务器端的一种模块化，Node.js正是使用这种模块化。

* UMD(Universal Module Definition)

UMD是一种跨平台（浏览器端，服务端，web APP端等）的模块化方案，使用该种模块化方案，可以很好地兼容AMD， CommonJS等模块化语法。

### class declarations

class/extends以及super()

这个特性也算是终于正经的引入了对象与继承机制了。

### lexical block scoping

let/const

这个特性的引入算是最终解决了JS没有局部作用域的问题，终结了使用闭包来构建局部作用域的时代。

### iterators and generators

yield与generator函数

这个特性使得函数执行可以暂缓以及分段执行，从而增强了JS的异步能力。

### promises for asynchronous programming

promise对象

这个特性直接提供了一种链式的异步任务的执行方法。

### destructuring patterns

解构赋值

这是一种多值的赋值方式，极大的方便了对数组取值，同时方便了对多返回值函数的处理。

### proper tail calls

尾递归调用

这个特性可以优化一般的尾递归函数，使得递归到底的时候，递归函数直接计算完成，这是一种对某些形式的递归函数的优化办法。

这个一种递归的编程办法，在编译器中尾递归编程方法通常能够得到很好的优化，从而提高该种形式递归的执行效率，同时也防止了栈溢出。

ES6.0引入了这个特性，那么一旦JS解释器支持了这个特性，那么这种形式的递归调用就会得到JS解释器的优化，从而提高执行效率与防止调用栈溢出。

### 其他一系列的数据类型结构

set/weakset 

map/weakmap

proxy/reflect

## source text

起步支持unicode5.1（这里规定了源字符的范围，U0000到U10FFFF的所有字符）

## White Space

新增:

* <ZWNBSP> //ZERO WIDTH NO-BREAK SPACE

## keywords and reserved words

### keywords

新增：

class

extends

super

import

export

const

yield

注意:let真的不是关键字，哈哈哈，在ES5.0中它被加入到严格模式下的保留字中，在ES6.0中为什么不加入到关键字中呢？我猜测应该是为了兼容性，毕竟谁也不知道以前的某些JS代码是不是使用let作为了标识符。

### future reserved words

enum

await

## identifier

在原来的基础上，添加了另外一些特殊的规则。

比较有意思的两个点：

var let=123456; //非严格模式下，这是合法的，因为在非严格模式下let不是一个保留字。

let let=123456; //非严格模式下，这不是合法的，ES6.0文档的13.3.1.1指出，在let语句中，boundname不能是let。这显然是合理，毕竟如果在let语句中使用let作为标识符，就无法区分let究竟是标识符还是声明语句了。

let yield=123456; //在非generator函数中，这是合法的，虽然yield是关键字，这就很神奇。按照ES6.0文档中的identifier的binding来说，这确实可以。

## Punctuators

新增：

...（扩展运算符）

=> (箭头函数)

## Literals

### Number

新增：

1）、二进制

二进制使用0b或者0B开头。

2）、八进制

八进制使用0o或者0O开头。

### Template Literal Lexical Components（ES6.0新增的内容，中文叫多行字符串或者模板字符串）

这是新增的内容，主要用途是书写模板。

形式：

\`这中间是多行字符串\`（这两个点是反引号，ESC下面那个键。）


## Types

新增:

symbol（primitive type）

## Types Conversion

ES6.0文档的7.1章节，新增了symbol类型转换的内容。

## Executable Code and Execution Contexts

这个部分改动比较大，将一些代码执行的操作都抽象为了一些数据结构与相应的抽象操作，从而使用这些数据结构与抽象操作说明执行过程。

详见: 章节 8

新增的一些概念:

* Code Realms

* Jobs and Job Queues

* ECMAScript Initialization

### Lexical Environments

新增：

#### Function Environment Records

#### Global Environment Records

#### Module Environment Records

### Types of Source Code

新增:

* Module Code

详见：章节 8

## Statements

新增：

* Declarations and the Variable Statement

由于新增了let和const这两个关键字，于是variable与这两个关键字的语句合二为一，统称为Declarations and the Variable Statement。

1. Let and Const Declarations

2. Variable Statement
  
* Iteration Statements

1. The for-in and for-of Statements

其中，for-of语句是新增的。

## Expressions

### Primary Expression

新增：

* Function Defining Expressions

  1. FunctionExpression

  2. GeneratorExpression

  3. ClassExpression

* Regular Expression Literals

* Template Literals

### Left-Hand-Side Expressions

新增：

* The super Keyword

* Tagged Templates

* Meta Properties

### Assignment Operators

新增:

* ArrowFunction

* Destructuring Assignment(解构赋值)

还有另外一些expressions不知道属于哪一类，但是应该都算是新增:

* Function Definitions

* Arrow Function Definitions

* Method Definitions

* Generator Function Definitions

* Class Definitions

* Tail Position Calls

* ...（扩展运算）

## Functions and Classes

这一部分就是原来的Function Definitions的内容，但是由于ES6.0增加了Class的内容，所以这里就变为FUnctions and Classes。

* Function Definitions //普通函数的定义

以下是这部分在ES6.0文档中新增:

* Arrow Function Definitions

* Method Definitions

* Generator Function Definitions

* Class Definitions

* Tail Position Calls

详见: 章节 14

### Function Definitions

这一部分没什么变化。

### Arrow Function Definitions

这里定义了新增的箭头函数形式。

### Method Definitions

这里规定的是对象中的方法的形式。

### Generator Function Definitions

这里规定了生成器函数的定义形式。


### Class Definitions

这里规定了class的定义形式，包含了基本对象定义与继承。

### Tail Position Calls

尾递归的优化计算。

## Scripts and Modules

原来的Program变为这部分。

由于ES6.0增加了module的内容，所以不再是简单的一个Program了，而是分为Script与Module了。

* Scripts

* Moudles

详见: 章节 15

## Native ECMAScript Object

### The Object objects

#### Properties of the Object Constructor

新增：

* assign ( target, ...sources )

* getOwnPropertySymbols ( O )

* is ( value1, value2 )

* setPrototypeOf ( O, proto )

### The Function objects

#### Properties of the Function Constructor

* Function.prototype[@@hasInstance] ( V )

#### Properties of Function instances

新增:

* name

### The Symbol objects

新增的一个对象，对应于symbol类型。

symbol对象会生成一个唯一值，可以用作对象的property的名字，主要应用场景也是防止对象的属性名重复。

在一些框架中使用的多，防止属性被覆盖以及创建私有方法等。

详见：ES6.0章节19.4

### The Number objects

#### properties of the Number Constructor

新增:

* Number.EPSILON

* Number.MAX_SAFE_INTEGER

* Number.MIN_SAFE_INTEGER

* isFinite ( number )

* isInteger ( number )

* isNaN ( number )

* isSafeInteger ( number )

* parseFloat ( string )

* parseInt ( string, radix )

### The Math object

该对象也新增了一些Function properties，但是基本都是无关紧要的，这里就不一一列举了。

### The String objects

#### Properties of the String Constructor

新增:

* fromCharCode ( ...codeUnits ) //新增的参数扩展形式的property，老的形式依然可用。

* fromCodePoint ( ...codePoints )

* raw ( template , ...substitutions )

#### Properties of the String Prototype Object

新增:

* codePointAt ( pos )

* concat ( ...args ) //新增参数扩展形式，老的形式依然可以用。

* endsWith ( searchString [ , endPosition] )

* includes ( searchString [ , position ] )

* normalize ( [ form ] )

* repeat ( count )

* startsWith ( searchString [, position ] )

#### String.prototype \[ @@iterator ]( )

从ES6.0开始，String具备迭代器，于是String成为一个可迭代对象。

语法：

``` Javascript
str[Symbol.iterator]() //返回一个迭代器对象
```

#### String Iterator Objects

访问上面的迭代器property会返回一个迭代器对象，迭代器对象具有某些可访问property，其中next()是一定具备的。

##### The %StringIteratorPrototype% Object

* %StringIteratorPrototype%.next ( )

* %StringIteratorPrototype% [ @@toStringTag ]

语法:

``` Javascript
let iterators=str[Symbol.iterator]();
iterators[Symbol.toStringTag];//访问迭代器对象的@@toStringTagproperty。
iterators.next(); //访问迭代器对象的next()方法。
```

### The RegExp objects

#### Properties of the RegExp Constructor

新增：

* get RegExp [ @@species ]

RegExp[@@species] 访问器属性返回RegExp 的构造器。

访问方法：

``` Javascript
RegExp[Symbol.species]
```

#### Properties of the RegExp Prototype Object

* get RegExp.prototype.flags

* get RegExp.prototype.global

* get RegExp.prototype.ignoreCase

* get RegExp.prototype.multiline

* get RegExp.prototype.source

* get RegExp.prototype.sticky

* get RegExp.prototype.unicode

* RegExp.prototype [ @@replace ] ( string, replaceValue )

语法：

``` Javascript
regexp[Symbol.replace](str)
``` 

* RegExp.prototype [ @@search ] ( string )

语法：

``` Javascript
regexp[Symbol.search](str)
``` 

* RegExp.prototype [ @@split ] ( string, limit )

语法：

``` Javascript
regexp[Symbol.split](str)
``` 

* RegExp.prototype [ @@match ] ( string )

语法：

``` Javascript
regexp[Symbol.match](str)
``` 

改动：

RegExp的实例properties

在ES6.0（ES2015）之前，所有的RegExp实例都具有source, global,ignoreCase,  multiline等数据属性，但是ES6.0（ES2015）这些properties都改为prototype object的accessor（存取器）属性了。

但是RegExp实例仍然具备如下Property:

* lastIndex

### The Array objects

新增一个构造函数形式：

Array (...items )

#### Properties of the Array Constructor

新增：

* from ( items [ , mapfn [ , thisArg ] ] )

* of ( ...items )

* get Array [ @@species ]

语法:
``` Javascript
Array[Symbol.species];//返回Array的构造函数。
```

#### Properties of the Array Prototype Object

新增：

* copyWithin (target, start [ , end ] )

* entries ( )

* fill (value [ , start [ , end ] ] )

* find ( predicate [ , thisArg ] )

* findIndex ( predicate [ , thisArg ] )

* keys ( )

* push ( ...items ) //这里是参数形式改变，实际上以前版本的形式也是可以使用的。实际上这只是文档中的表达形式的改变，表示支持扩展运算符的形式。

* concat ( ...arguments ) //这里是参数的形式改变，实际上以前的版本的形式也是可以使用的。实际上这只是文档中的表达形式的改变，表示支持扩展运算符的形式。


* splice (start, deleteCount , ...items ) //增加的新形式，老的形式依然可以用。

* toLocaleString ( [ reserved1 [ , reserved2 ] ] ) //增加新形式，老的形式依然可以用。

* unshift ( ...items ) //增加新形式，老的形式依然可以用。

* values ( ) //返回array的iterator。

* Array.prototype [ @@iterator ] ( )

Array具备迭代器，所以Array是一个可迭代对象。

语法：
``` Javascript
arr[Symbol.iterator]();//默认情况下，返回值与values()相同,返回迭代器对象。

arr[Symbol.iterator];//返回values()函数。
```

* Array.prototype [ @@unscopables ]

Symbol 属性 @@unscopable 包含了所有 ES2015 (ES6) 中新定义的、且并未被更早的 ECMAScript 标准收纳的属性名。这些属性被排除在由 with 语句绑定的环境中。

语法:
``` Javascript
arr[Symbol.unscopables];
```

#### Array Iterator Objects

##### The %ArrayIteratorPrototype% Object

* %ArrayIteratorPrototype%.next( )

* %ArrayIteratorPrototype% [ @@toStringTag ]

访问语法：
``` Javascript
let arr = ['a', 'b', 'c', 'd', 'e'];

let eArr = arr[Symbol.iterator]();

eArr.next();

eArr[Symbol.toStringTag];
```

### The TypedArray objects

定型数组是ES6.0新增的结构，目的是提升向原生库传输数据的效率。

#### The TypedArray Constructors

* %TypedArray% ( )

* %TypedArray% ( length )

* %TypedArray% ( typedArray )

* %TypedArray% ( object )

* %TypedArray% ( buffer [ , byteOffset [ , length ] ] )

以上是四种形式的构造函数。

TypedArray可以是如下类型:

* Int8Array

* Uint8Array

* Uint8ClampedArray

* Int16Array

* Uint16Array

* Int32Array

* Uint32Array

* Float32Array

* Float64Array

其他的Properties，详见：章节22.2

强相关章节：24.1 ArrayBuffer 24.2 DateView

### The JSON objects

新增：

* JSON [ @@toStringTag ]

语法:
``` Javascript
JSON[Symbol.toStringTag];
```

### The Map objects

新增对象，这是一种键值对的数据结构。键和值可以是任意的类型值。

#### The Map Constructor

* Map() //无参数形式

* Map([ iterable ]) //可迭代对象作为参数，例如Array。

#### Properties of the Map Constructor

* get Map [ @@species ]

返回Map的构造函数。

#### Properties of the Map Prototype Object

* clear ( )

* delete ( key )

* entries ( )

* forEach ( callbackfn [ , thisArg ] )

* get ( key )

* has ( key )

* keys ( )

* set ( key , value )

* values ( )

* get Map.prototype.size

* Map.prototype [ @@iterator ] ( ) //具备迭代器，是一个可迭代对象。

* Map.prototype [ @@toStringTag ]

#### Map Iterator Objects

##### The %MapIteratorPrototype% Object

* %MapIteratorPrototype%.next ( )

* %MapIteratorPrototype% [ @@toStringTag ]

### The WeakMap objects

这也是一个新增的对象，一种新增的键值对数据结构。键必须是对象，值可以是任意类型值,除此之外，它的功能也稍弱于Map。

#### The WeakMap Constructor

* WeakMap();

* WeakMap([iterable]); //参数是可迭代对象，例如Array。

#### Properties of the WeakMap Prototype Object

* delete ( key )

* get ( key )

* has ( key )

* set ( key , value )

* WeakMap.prototype [ @@toStringTag ]

可以看到，功能相对于Map的确少了很多。


### The Set objects

Set是新增的对象，这是一种新增的数据结构，它是一种集合结构，集合中的值具有唯一性，不能出现两个相同的类型值。

#### The Set Constructor

* Set (  )

* Set ( [ iterable ] )

#### Properties of the Set Constructor

* get Set [ @@species ] //返回Map的构造函数。


#### Properties of the Set Prototype Object

* add ( value )

* clear ( )

* delete ( value )

* entries ( )

* forEach ( callbackfn [ , thisArg ] )

* has ( value )

* keys ( )

* get Set.prototype.size

* values ( )

* Set.prototype [ @@iterator ] ( ) //Set也具有迭代器。

* Set.prototype [ @@toStringTag ]

#### Set Iterator Objects

##### The %SetIteratorPrototype% Object

* %SetIteratorPrototype%.next ( )

* %SetIteratorPrototype% [ @@toStringTag ]

### The WeakSet objects

新增的一个对象，它是对象的集合。与Set相比，它保存的元素只能是对象。

#### The WeakSet Constructor

* WeakSet (  )

* WeakSet ( [ iterable ] )

#### Properties of the WeakSet Prototype Object

* add ( value )

* delete ( value )

* has ( value )

* WeakSet.prototype [ @@toStringTag ]

WeakSet的功能比Set弱上不少。

### The ArrayBuffer objects

新增的一个对象，用于在内存中分配特定字节数的内存区域。

#### The ArrayBuffer Constructor

* ArrayBuffer( length ) //单位是字节

#### Properties of the ArrayBuffer Constructor

* isView ( arg )

* get ArrayBuffer [ @@species ]

#### Properties of the ArrayBuffer Prototype Object

* get ArrayBuffer.prototype.byteLength

* slice ( start, end )

* ArrayBuffer.prototype [ @@toStringTag ]

### The DataView objects

#### The DataView Constructor

* DataView (buffer [ , byteOffset [ , byteLength ] ] )

#### Properties of the DataView Prototype Object

* get DataView.prototype.buffer

* get DataView.prototype.byteLength

* get DataView.prototype.byteOffset

* getFloat32 ( byteOffset [ , littleEndian ] )

* getFloat64 ( byteOffset [ , littleEndian ]

* getInt8 ( byteOffset )

* getInt16 ( byteOffset [ , littleEndian ] )

* getInt32 ( byteOffset [ , littleEndian ] )

* getUint8 ( byteOffset )

* getUint16 ( byteOffset [ , littleEndian ] )

* getUint32 ( byteOffset [ , littleEndian ] )

* setFloat32 ( byteOffset, value [ , littleEndian ] )

* setFloat64 ( byteOffset, value [ , littleEndian ] )

* setInt8 ( byteOffset, value )

* setInt16 ( byteOffset, value [ , littleEndian ] )

* setInt32 ( byteOffset, value [ , littleEndian ] )

* setUint8 ( byteOffset, value )

* setUint16 ( byteOffset, value [ , littleEndian ] )

* setUint32 ( byteOffset, value [ , littleEndian ] )

* DataView.prototype[ @@toStringTag ]

### Iteration

迭代器是ES6.0新增的内容。

一个对象是否可迭代，取决于其是否具有迭代器。

#### @@iterator

对象内部的迭代器property的名字，[Symbol.iterator]。

这是一个函数，返回迭代器对象。

#### next()

迭代器对象必须具有的property，这是一个函数，返回一个Resultobject。


#### ResultObject

必须具有如下properties:

* done //true:迭代到末尾了。false:迭代尚在中间。

* value //当前正迭代的element的值。

### The GeneratorFunction Objects

与The Function objects类似，这是一种特殊的函数对象，成为生成器函数对象。

#### The GeneratorFunction Constructor

* GeneratorFunction (p1, p2, … , pn, body)

#### Properties of the GeneratorFunction Constructor

* length

* GeneratorFunction.prototype [ @@toStringTag ]

#### GeneratorFunction Instances

* length

* name

* prototype

### The Generator Objects

这是满足iterator要求的Generator函数的实例对象。

#### Properties of Generator Prototype

* next ( value )

* return ( value )

* throw ( exception )

* Generator.prototype [ @@toStringTag ]

### Promise objects

Promise是一个新增的对象，其目的就是为了解决回调地狱，Promise对象是一种链式调用，在ES6.0之前，其他的一些库都已经实现了Promise。

这个可以说是ES6.0的重要特性了。

一个Promise对象具有3种状态：

* pending // 待定状态，通过执行其他函数可以转变为fulfilled或者rejected状态，一般来说，刚创建的Promise对象，其是pending状态。

* fulfilled // fulfilled状态就会执行p.then(f,r)中的f函数。

* rejected // rejected状态就会执行p.then(f.r)中r函数。

#### The Promise Constructor

* Promise(executor) //excutor这个参数必须写，而且excutor这个参数是一个两个参数的函数，其会立即得到执行。

#### Properties of the Promise Constructor

* Promise.all ( iterable )

* Promise.race ( iterable )

* Promise.reject ( r )

* Promise.resolve ( x )

* get Promise [ @@species ]

#### Properties of the Promise Prototype Object

* catch ( onRejected )

* then ( onFulfilled , onRejected )

* Promise.prototype [ @@toStringTag ]

### The Reflect Object

ES6.0新增的对象，它不是一个函数对象，所以它不具备构造函数，于是它不能够被构造，即实例化。

Reflect Ojbect提供了一系列的API，这些API可用于代理访问某个对象。

详见：章节26.1

强相关：章节 26.2 Proxy Object

### The Proxy Objects

ES6.0新增的对象，通过它可以创建一个对象的代理对象，然后进行各种拦截操作。

#### The Proxy Constructor

* Proxy ( target, handler )

#### Properties of the Proxy Constructor

* revocable ( target, handler )

Proxy的核心在于handler的编写，所有的拦截操作都在handler中定义。


# ES2016

## ES2016新增

* 指数运算符(**)

* Array.prototype.includes()

## source text

起步支持unicode8.0（这里规定了源字符的范围，U0000到U10FFFF的所有字符）

## Punctuator

新增:

**（幂运算符）

**=（幂运算赋值运算符）

## Expressions

### Exponentiation Operator

新增:

* \**(幂运算)

### Assignment Operators

新增:

* \**=（幂运算赋值）

## Native ECMAScript Object

### The Array Objects

#### Properties of the Array Prototype Object

新增:

* includes ( searchElement [ , fromIndex ] )

### The TypedArray Objects

#### Properties of the TypedArray Prototype Object

新增:

* includes ( searchElement [ , fromIndex ] )

# ES2017

## ES2017新增

* Async Functions

async/await

* Shared Memery

The SharedArrayBuffer Object

* Atomics along with smaller language

The Atomics Object

* library enhancements

新增了一些原生对象的方法。

## source text

要求支持最新的unicode标准。


## keywords and reserved words

### keywords

新增:

await

注意点:await虽然是关键字，但是在某些情况下(非module和非async/await函数中，其可以作为标识符。)，其可以作为标识符，类似于yield，这里不展开论述，需要记住得是，await不要用作标识符，永远都不要。另外需要注意的一点：async不是关键字，其可以作为标识符，但是最好不用使用async当做标识符，所以永远也不要使用async作为标识符。

具体可以看 12.1.1

## Expressions

### Primary Expression

#### Function Defining Expressions

新增:

* AsyncFunctionExpression

### Unary Operators

新增:

* AwaitExpression  //用于异步函数之中，启动执行异步代码的中断标记。

### Assignment Operators

新增:

* AsyncArrowFunction

## Executable Code and Execution Contexts

新增的一些概念:

### RunJobs ( )

### Agents
  
  1. AgentSignifier( )

  2. AgentCanSuspend( )

### Agent Clusters

### Forward Progress

## Functions and Classes

新增:

* Async Function Definitions

* Async Arrow Function Definitions

## Native ECMAScript Object

### The Object objects

#### Properties of the Object Constructor

新增:

* entries(O)

* getOwnPropertyDescriptors(O)

* values(O)

### The String objects

#### Properties of the String Prototype Object

新增:

* endsWith ( searchString [ , endPosition ] )

* padStart( maxLength [ , fillString ] )

### The SharedArrayBuffer Objects

这是新增的一个对象，增加了共享内存的特性。该对象类似于ArrayBuffer。

利用web work可以创建在浏览器后台运行的线程，工作主线程从而可以继续执行并响应UI。在这种情况下，后台运行的线程与主线程之间就会有交换数据的需求，在以前，数据交换往往是复制原始数据的一部分，然后交互传递，现在有了共享内存，这些线程之间就可以直接通过共享内存来交换数据了。

由于一些安全问题，该对象在现在的主流浏览器中被禁止使用，因此不做过多描述。

详见:章节24.2

强相关:章节 24.4 Atomics

### The Atomics objects

这也是新增的一个对象，主要提供对共享内存的原子性操作。

详见:章节 24.4


# ES2018

## ES2018新增

* asynchronous iteration via the AsyncIterator protocol and async generators

支持异步迭代特性，即for...of...可以进行异步迭代了，这有利于写出循环式的异步任务。

* four new regular expression features

the dotAll flag, named capture groups, Unicode property escapes, and look-behind assertions.

*  rest parameter and spread operator support for object properties

{...obj}

## Expressions

###  Primary Expression

新增:

* AsyncGeneratorExpression //对应于异步迭代特性


## Statements

### Iteration Statements

新增:

* forfor-awaitawait-ofof Statements //异步迭代特性


## Functions and Classes

新增:

* Async Generator Function Definitions

## Native ECMAScript Object

### The Symbol Objects

#### Properties of the Symbol Constructor

新增:

* Symbol.asyncIterator


### The RegExp objects

####  Properties of the RegExp Prototype Object

新增:

* get RegExp.prototype.dotAll //对应正则的doeAll模式。

### Iteration

新增：

增加了异步迭代器以及其所必须的properties。

### AsyncGeneratorFunction Objects

这是新增的一个对象，对应于异步的Generator函数。

详见: 章节 25.3

### AsyncGenerator Objects

这是新增的一个对象，它是AysncGeneratorFunction Object的实例。

详见: 章节 25.5

### Promise Objects

#### Properties of the Promise Prototype Object

新增:

* finally ( onFinally )

# ES2019

## ES2019新增

* introduces a few new built-in functions

 1. flat and flatMap on Array.prototype for flattening arrays

 2. Object.fromEntries for directly turning the return value of Object.entries into a new Object

 3.  trimStart and trimEnd on String.prototype as better-named alternatives to the widely implemented but non-standard String.prototype.trimLeft and trimRight builtins

* a few minor updates to syntax and semantics

1. Updated syntax includes optional catch binding parameters and allowing U+2028 (LINE SEPARATOR) and U+2029 (PARAGRAPH SEPARATOR) in string literals to align with JSON

* requiring that Array.prototype.sort be a stable sort

* requiring that JSON.stringify return well-formed UTF-8 regardless of input

* clarifying Function.prototype.toString by requiring that it either return the corresponding original source text or a standard placeholder

## Statements

### The try Statement

新增：可选catch的try语句

* 不带catch的try语句， try Block Finally。

## Native ECMAScript Objects

### The Object Objects

#### Properties of the Object Constructor

* Object.fromEntries ( iterable )

### The Symbol objects

#### Properties of the Symbol Prototype Object

新增:

* get Symbol.prototype.description

### The String Objects

#### Properties of the String Prototype Object

新增:

* trimStart ( )

* trimEnd ( )

### The Array Objects

#### Properties of the Aarry Prototype Object

新增:

* flat( [ depth ] )

* flatMap ( mapperFunction [ , thisArg ] )

# ES2020

## ES2020新增

* introduces the matchAll matchAll method for Strings

* produce an iterator for all match objects generated by a global regular expression

* import() import(), a syntax to asynchronously import Modules with a dynamic specifier

* Promise.allSettled, a new Promise combinator that does not short-circuit

* globalThis, a universal way to access the global thisthis value

* BigIntBigInt, a new number primitive for working with arbitrary precision integers

* export * as ns from 'module' export * as ns from 'module' syntax for use within modules

* increased standardization of for-infor-in enumeration order

* import.meta import.meta

* Nullish coalescing Operator(空值处理)

* Optional chaining（可选链）