# Strict Mode 

严格模式在ES5中引入，其当初引入的目的是为了使JS的行为变得更加明确。 

开启严格模式之后，JS的行为会发生改变，这一点需要注意。 

## For What 

* 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为,提高对新手的友好程度。
* 消除代码运行的一些不安全之处，保证代码运行的安全，严格模式下一些错误会抛出异常。
* 提高编译器效率，增加运行速度。
* 为未来新版本的Javascript做好铺垫。 

## How to use it? 
### Strict mode for scripts 
`
// Whole-script strict mode syntax 

'use strict'; 

var v = "Hi! I'm a strict mode script!"; 

`


## Changes In Strict Mode 

* 持续更新中