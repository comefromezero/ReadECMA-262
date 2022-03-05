# ES2.0的特性

## source text

起步支持unicode2.0（这里规定了源字符的范围，U0000到U10FFFF的所有字符）

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

1、NULL

null

2、bool

true

false

3、Number

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

4、字符串

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

## Statements

* Block 

* Variable statement 

* Empty statement 

* Expression statement 

* The if statement 

* Iteration statements 

* The while statement 

* The for statement 

* The for..in statement 

* The continue statement 

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

比较常用的property，Function Object Instance中最有用的一个property，即length，该property表明了该function接收的参数个数。

详见：章节15.3

### Array Objects

Prototype Ojbect的toString(),join(),reverse(),sort()等Property都非常有用。

其instance中有用的property：length。

详见：章节15.4

### String Objects

Prototype Object的toString(),valueOf(),charAt(),indexOf(),lastIndexOf(),split(),substring(),toUpperCase(),toLowerCase()等都是非常常用的。

其instance中有用的property：length。

详见：章节15.5

### Booloean

Boolean比较简单，其Prototype Object总共就具备两个property:toString()和valueOf()。

详见：章节15.6

### Number

Number这个应该是比较有意思的一个Object，在实际使用过程中，很少会用到它以及它的各种properties。

Prototype Object比较有用的properties:toString()和valueOf();

详见：章节15.7

### Math

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

### Date

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