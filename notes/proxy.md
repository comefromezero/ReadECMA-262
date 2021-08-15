# 代理与反射（es6）

代理（proxy）与反射(reflect)是es6新增的非常强力的特性，它提供给我们hook对象的某些操作的API，使得我们可以监控对象的某些操作。（Vue3就是使用proxy和reflect实现data的监控，从而解决了vue2无法监控数组和对象的问题。）

但是它也有严重的兼容性问题，我们没有办法使用es5的特性来完全模拟一个proxy与reflect，所以在一些低版本的浏览器上该特性无法使用的时候，我们没有一个完全模拟的方案来降级，这是需要特别注意的。

## 代理的使用

1. 被代理对象（目标对象）

被代理对象是一个对象，它是我们真正要访问的对象。

2. handler对象

该对象中我们可以定义各种hook钩子，通过这些钩子，我们可以对被代理对象实现各种访问限制。当然，该对象也可以是一个空对象，那样的话，就相当于没有定义任何hook钩子，与直接访问被代理对象一样。

3. Reflect API

我们可以通过Reflect API对一个对象进行操作,所以我们实际上可以通过Reflect API来代替各种操作，例如，赋值、删除、访问等。

4. Proxy API

我们通过Proxy API来实现被代理对象和handler对象之间的关联，同时获得一个代理对象，我们通过代理对象来访问目标对象中的property。

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

