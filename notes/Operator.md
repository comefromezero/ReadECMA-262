# Operator
.、[ ]、( )	

delete new typeof void

++、--、-、！、new、typeof、delete、void

*、/、%

+、-

＜、＜=、＞、＞=、in

==、!=

&&

II

?:

=、*=、/=、％=、+=、-=、&=、^=、!=

,(es2)

instanceof === !==(es3)

...(扩展运算符，es6)([扩展运算符不算一个运算符，列在这里是为了将ES6中的符号都整理出来](https://stackoverflow.com/questions/48656338/operator-precedence-for-js-spread-and-rest-operators/48656377#48656377))

?? ?.(ES2020新增，比较有用的两个运算符。)

## Prority of Operator

|运算符|结合性|	优先级|
|------|-----|-------|
|.、[ ]、( )、?.|从左到右|高|
|++、--、-(负号)、+(转换为数字)、！、new、typeof、delete、void|从右到左|↑|
|*、/、%|从左到右|↑|
|+(加法)、-、+(字符串连接)|	从左到右|↑|
|<<、>>、>>>|从左到右|↑|
|＜、＜=、＞、＞=、in、instanceof|从左到右|↑|
| \==、!=、\===、!\==| 从左到右|↑|
|&|从左到右|↑|
|^|从左到右|↑|
|\||从左到右|↑|
|&&|从左到右|↑|
|II|从左到右|↑|
|??|从左到右|↑|
|?:|从右到左|↑|
|=、*=、/=、％=、+=、-=、&=、^=、\|=、>>=、<<=、>>>=|从右到左|↑|
|,	|从左到右|低|

表达式的计算过程中，运算符的结合性并不影响子表达式的计算，其计算过程始终是按照优先级进行计算的。

## 几个容易混淆的算符

+(转换为数字)

正号作用于非数字类型时，会先将该类型转换为数字类型。

当正号作用于数字类型时，会保持该数字类型的正负号。

-(负号)

负号作用于非数字类型时，会现将该类型转换为数字类型，然后对该数字类型进行正负性取反。

负号作用于数字类型时，会对该数字的正负性取反。



[++、--](https://github.com/comefromezero/ReadECMA-262/blob/main/notes/PrefixAndPostfixIncDec.md)


[\==、=\==、\!=、!==](https://github.com/comefromezero/ReadECMA-262/blob/main/notes/eq_oporatorr.md)


## ES2020新增的两个运算符

??

空值合并操作符（??）是一个逻辑操作符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数。

与逻辑或操作符（||）不同，逻辑或操作符会在左侧操作数为假值时返回右侧操作数。也就是说，如果使用 || 来为某些变量设置默认值，可能会遇到意料之外的行为。比如为假值（例如，'' 或 0）时。

考虑以下场景:
``` Javascript
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0
const boo = 0 || 42;
console.log(boo);
// expected output: 42
```

?.

链式property访问操作符，该操作符特别适用于判断一个对象是否存在，如果存在就访问其中某个property的场景。

考虑以下场景：

``` Javascript
let age = group && group.zhangsan && group.zhangsan.age;  //如果group存在，则访问group中的张三成员是否存在，如果张三成员存在，则返回张三的年龄。

let age = group?.zhangsan?.age; //简洁多了。
```

附:

[MDN的操作符讲解](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

