# 代理与反射（es6）

代理（proxy）与反射(reflect)是es6新增的非常强力的特性，它提供给我们hook对象的某些操作的API，使得我们可以监控对象的某些操作。（Vue3就是使用proxy和reflect实现data的监控，从而解决了vue2无法监控数组和对象的问题。）

但是它也有严重的兼容性问题，我们没有办法使用es5的特性来完全模拟一个proxy与reflect，所以在一些低版本的浏览器上该特性无法使用的时候，我们没有一个完全模拟的方案来降级，这是需要特别注意的。

## 代理的使用

1. 被代理对象（目标对象）

被代理对象是一个对象，它是我们真正要访问的对象。

2. handler对象

该对象中我们可以定义各种hook钩子（或者称为捕获器），通过这些钩子，我们可以对被代理对象实现各种访问限制。当然，该对象也可以是一个空对象，那样的话，就相当于没有定义任何hook钩子，通过代理访问与直接访问被代理对象一样，这种情况下，我们称之为空代理。

3. Reflect API

我们可以通过Reflect API对一个对象进行操作,所以我们实际上可以通过Reflect API来代替各种操作，例如，赋值、删除、访问等。

4. Proxy API

我们通过Proxy API来实现被代理对象和handler对象之间的关联，同时获得一个代理对象，我们通过代理对象来访问目标对象中的property。

注意：代理对象也是一个对象，因此我们可以通过Proxy API建立一个代理对象的代理。

例子：

``` Javascript
    const target = { 
     foo: 'bar' 
    }; 
    const handler = {
     get(trapTarget, property, receiver) { 
     console.log(trapTarget === target); 
     console.log(property); 
     console.log(receiver === proxy); 
     } 
    }; 
    const proxy = new Proxy(target, handler); 
    proxy.foo; 
    // true 
    // foo 
    // true 
    
    // 或者，我们可以通过参数直接访问被代理对象的
    const target = { 
     foo: 'bar' 
    }; 
    const handler = { 
     get(trapTarget, property, receiver) { 
     return trapTarget[property]; 
     } 
    }; 
    const proxy = new Proxy(target, handler); 
    console.log(proxy.foo); // bar 
    console.log(target.foo); // bar
```
在上面的两个例子中，我们在hook钩子中使用参数来操作目标对象的property，实际上，这种方式并不需要通过参数来操作，相反通过Reflect API来操作将更加方便。

``` Javascript
    const target = { 
     foo: 'bar' 
    }; 
    const handler = { 
     get() { 
     return Reflect.get(...arguments); 
     } 
    }; 
    const proxy = new Proxy(target, handler); 
    console.log(proxy.foo); // bar 
    console.log(target.foo); // bar
```

## 可以撤销的代理

有时候可能需要中断代理对象与目标对象之间的联系。对于使用 new Proxy()创建的普通代理来说，这种联系会在代理对象的生命周期内一直持续存在。

Proxy 也暴露了 revocable()方法，这个方法支持撤销代理对象与目标对象的关联。撤销代理的操作是不可逆的。而且，撤销函数（revoke()）是幂等的，调用多少次的结果都一样。撤销代理之后再调用代理会抛出TypeError。

``` Javascript
 foo: 'bar' 
}; 
const handler = { 
 get() { 
 return 'intercepted'; 
 } 
}; 
const { proxy, revoke } = Proxy.revocable(target, handler); 
console.log(proxy.foo); // intercepted 
console.log(target.foo); // bar 
revoke(); 
console.log(proxy.foo); // TypeError
```

## hook钩子中如何操作被代理对象？

1. 直接通过hook钩子提供的参数来

在每一个hook钩子中，我们可以访问三个重要的参数target(第一个参数，被代理的对象，目标对象),property（访问的property）,value(值),reciever（代理对象）。当这些hook钩子被触发的时候，Js引擎会自动设置这三个参数值，我们就能够使用这三个参数了。

2. 通过Reflect API

Reflect API可以用于在hook中操作目标对象，也可以在其他地方直接用于操作一个对象。它本身就是ES6新增的一种对象操作API，通过Reflect，我们可以访问对象内部的操作办法，并且可以通过返回结果得知这些方法的执行状态（在ES6以前往往是抛出错误），使我们能够更好的处理这些错误，另外可以使用Reflect API代替一些操作，使这些操作变成函数，从而变得更加语义化。

注意：钩子通过代理对象触发，不同的钩子有不同的触发条件，例如,x的set钩子，只能通过proxy_x.y=10000触发，不能通过proxy_x.y.z=10000触发，因为proxy_x.y.z=10000触发的是y（y作为x的一个property，其可以是一个对象，当然其也可以是一个代理对象。）的set钩子。如果y不是一个代理对象，那么proxy.y.z=10000就不会触发任何钩子，因为钩子不存在。因此如果想要实现某个对象的property的钩子，就需要将这个property对象的对象转换称为一个对应的代理对象。所以在Vue3中，递归处理了对象，当一个property是一个对象的时候，就会使用Proxy()这个API创建一个代理对象从而实现对原对象的代理，也可以实现object的观察。对于x的get钩子而言，不管是proxy_x.y还是proxy_x.y.z都可以触发get钩子。

## 几个应用场景

1、监控某个对象的数据访问。

2、对某个对象进行动态打补丁。
