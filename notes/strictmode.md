# Strict Mode 

严格模式在ES5中引入，其当初引入的目的是为了使JS的行为变得更加明确。 

开启严格模式之后，JS的行为会发生改变，这一点需要注意。 

正是因为严格模式下JS的行为会发生改变，所以ES6并不推荐使用严格模式。

## For What 

* 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为,提高对新手的友好程度。
* 消除代码运行的一些不安全之处，保证代码运行的安全，严格模式下一些错误会抛出异常。
* 提高编译器效率，增加运行速度。
* 为未来新版本的Javascript做好铺垫。 

## How to use it?

### Strict mode for scripts(global code) 

global code is strict mode code if it begins with 'use strict';.

``` Javascript
// Whole-script strict mode syntax
'use strict';
var v = "Hi! I'm a strict mode script!"; 
```
### Strict mode for functions 

function code is strict mode code if it begins with 'use strict'; or it is contained in strict mode code.

``` Javascript
function strict() {
  // Function-level strict mode syntax
  'use strict';
  function nested() { return 'And so am I!'; }
  return "Hi!  I'm a strict mode function!  " + nested();
}
```
not only the functiondeclaration(the example),but also FunctionExpression, GeneratorDeclaration, GeneratorExpression, MethodDefinition, or ArrowFunction.

The other thing ,when Getting a function object by Function() constructor,if the last argument is a String that is FunctionBody that begins with a 'use strict';,the returned function object is strict mode code.

``` Javascript
let func = new Function("'use strict'; return 'hello world!';");
// FunctionBody of func reference is strict mode code.
```

The Generator constructor(ES6 add) is the same as abouv.

### Strict mode for modules 

module code is always strict mode code.

``` Javascript
function strict() {
    // because this is a module, I'm strict by default
}
export default strict;
``` 

### Strict mode for class

classdeclaration and classexpression is always strict mode code.Briefly,the code in class is always strict mode code.

### Strict mode for eval()

Eval() code is strict mode code if it begins with a 'use strict';.


## Changes In Strict Mode(没有标明哪份ES文档中的，默认都是ES6) 

* 严格模式下，implements, interface, let, package, private, protected, public, static,yield是保留字。
* 严格模式下，禁止使用0开头八进制整数字面值。
传统的八进制方式，允许使用0开头表示这是一个八进制的整数字面值，在严格模式下，不再允许使用0开头的传统八进制字面值。但是，0o开头的八进制整数字面值（新的八进制字面值方式）在严格模式下依然可以使用。后一种形式的八进制整数字面值比前面一种更加明确，也是符合严格模式当初设计的目的的。

``` Javascript
'use strict';

let test = 056; //SyntaxError,严格模式下，该形式的八进制数被禁止使用。

let test1 = 0o56; //严格模式下，这种形式的八进制数依然可以使用。
```

* 严格模式下，禁止使用以0开头的非八进制的十进制整数字面值（ES2016）。
在es2016中，非严格模式下，可以使用let a=09878777;这种方式的十进制整数字面值。但是在严格模式下，这种方式的十进制整数值是被禁止的。

``` Javascript
'use strict';

let test = 0987; //SyntaxError,v严格模式下，禁止使用0开头的十进制整数字面值。
```

* 严格模式下，禁止在String Literal中使用八进制的转义序列。

``` Javascript
'use strict';

let test = "\056"; //SyntaxError,严格模式下，禁止使用八进制的转义序列。
```

* 严格模式下，如果赋值表达式的左边是未声明的标识符或者是无法解析的引用的标识符，那么就会报错ReferenceError。在非严格模式下，不会报错。

``` Javascript
test = 1000; //非严格模式下，直接对一个未声明的标识符赋值不会报错，
             //而且会在全局对象中定义一个这样的标识符。
             //这种不明确的行为往往会降低代码的可维护性。
```

``` Javascript
'use strict';

test = 10000; //严格模式下，ReferenceError。
```

* 严格模式下，如果赋值表达式的左边是不可写的对象的property，或者是未定义的对象的accessor property，亦或者是不存在的对象的property,那么就会报错TypeError。

``` Javascript

'use strict';

Object.prototype = 10000; //TypeError，因为Object.prototype的Writable属性是false。

```

* 严格模式下，eval和arguments不能作为声明的标识符,否则会报错SyntaxError。它们也不能用于赋值表达式的左值，不能用在前缀和后缀自增自减表达式中，否则会报错SyntaxError。

``` Javascript

'use strict';

let eval; //SyntaxError

let arguments; //SyntaxError

--eval; //SyntaxError

++arguments; //SyntaxError

eval++; //SyntaxError

arguments--; //SyntaxError

```

* 严格模式下，函数代码中的arguments对象中的parameter仅仅只是参数列表的一份拷贝，改变arguments对象中的参数值，并不会改变真实的参数值。在非严格模式下，arguments中的参数值与真实的参数值是关联的，改变arguments中的值则对应的参数值都会改变。

``` Javascript

function test(a,b,c){
    arguments[0]=0;
    return a+b+c;
}

console.log(test(1,2,3)); //结果：5

```

``` Javascript

'use strict';

function test(a,b,c){
    arguments[0]=0;
    return a+b+c;
}

console.log(test(1,2,3)); //结果：6

```

* 严格模式的函数，arguments会bind到arguments object，该binding是immutable的，因此arguments不能作为赋值表达式的左值，这与前面那一条一致。

* 严格模式下，函数名不能为eval和argument（与前面一致，不能作为标识符），参数名不能为eval和argument（与前面一致，不能作为标识符），不能存在相同的形式参数名，否则报SyntaxError。非严格模式下，不会有任何回应。

``` Javascript
function sum(a, a, c) { // !!! syntax error
  'use strict';
  return a + a + c; // wrong if this code ran
}
```

* 严格模式下，函数的arguments对象的callee不能被访问，一旦访问（arguments.callee）就会抛出TypeError异常。

> Arguments objects for strict mode functions define non-configurable accessor properties named "caller" and "callee" which throw a TypeError exception on access. The "callee" property has a more specific meaning for non-strict functions and a "caller" property has historically been provided as an implementationdefined extension by some ECMAScript implementations. The strict mode definition of these properties exists to ensure that neither of them is defined in any other manner by conforming ECMAScript implementations.                    ---9.4.4（ES6）
这里指出，严格模式下，arguments的会定义两个accessor property,caller与callee，它们的configurable是false，访问它们会抛出TypeError的异常。

ps:ES2017之前，为了兼容以前的一些老的implementation，严格模式下会在arguments中添加caller这个property。ES2017及以后，拿掉了这个caller property。
而且经过测试，在chrome中，在严格模式下，访问arguments.caller没有抛出异常，所以在上面我并没有写出访问arguments.caller会抛出TypeError异常。其他现代浏览器应该也是如此。

``` Javascript

'use strict';

function test(){

    arguments.callee;
}

test(); //TypeError，严格模式下，访问callee直接抛出TypeError。

```

* 严格模式下，如果try{}catch(parameter){}中的parameter是arguments或者eval，则抛出SyntaxError。

``` Javascript

try { } catch (arguments) { } //SyntaxError

```


* 严格模式下，eval中的代码会重新创建一个变量环境，之后，eval中的代码声明的变量和函数都会在这个新创建的变量环境中instantiate并binding。非严格模式下，eval中的代码的变量和函数都会在它的caller的变量环境中instantiate并binding。

``` Javascript

'use strict';

eval("var test=1000;")

console.log(test); //ReferenceError，因为test这个变量只存在eval新创建的变量环境中（严格模式下，eval会新创建一个变量环境），在全局环境中访问，这是非法的。

```

* 严格模式下，如果delete删除的property的attributes中包含一个configurable:false(意味着该property不能被删除)的attribute，那么就会抛出TypeError的异常。非严格模式下，没有任何回应。

``` Javascript

'use strict';

delete Object.prototype; // TypeError，因为prototype的configuratble:false。

```

* 严格模式下，如果delete一个变量，函数参数，函数名的引用，那么就会抛出SyntaxError。非严格模式下，这个操作不会有任何回应。

``` Javascript

'use strict';

var x;
delete x; // !!! syntax error

eval('var y; delete y;'); // !!! syntax error

```

* 严格模式下，禁止使用with语句，否则会抛出SyntaxError异常。

``` Javascript

'use strict';

with(Object){  //SyntaxError，严格模式下，不能使用with语句。
    
}

```

* 严格模式下，this指针不会被转换为指向一个object，其值可以为null或者undefined。非严格模式下，this指针会始终指向一个object，如果其没有指向一个object，其也会被转换为指向一个object。

``` Javascript

'use strict';
function fun() { return this; }

console.log(fun() === undefined); //true
console.log(fun.call(2) === 2);//true
console.log(fun.apply(null) === null);//true
console.log(fun.call(undefined) === undefined);//true
console.log(fun.bind(true)() === true);//true

```

* 严格模式下，一个实现不能随意扩展严格模式下的函数的properties，不能添加名为caller和arguments的properties，同时code也不能创建和修改名为caller和arguments的properties。这一条主要是针对严格模式下的函数的property的，保护了严格模式下，caller和arguments这两个properties不被修改。

``` Javascript

function restricted() {
  'use strict';
  restricted.caller;    // throws a TypeError
  restricted.arguments; // throws a TypeError
}
function privilegedInvoker() {
  return restricted();
}
privilegedInvoker();

```

ps：按照上面的说法，ES要求实现在严格模式下不能私自创建名为caller和arguments的 properties，而且严格模式下，ES code不能修改这两个properties，于是一些实现在严格模式下直接禁止了对这两个properties的访问，一旦访问，就直接抛出异常。

我在chrome和firefox下都测试了上面的代码，发现确实都会抛出TypeError。