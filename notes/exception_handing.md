# 错误异常处理

 ES提供了异常处理机制，即try、catch、trrow、finally三种语句。

 语法如下：

``` Javascript
 try { 
 // 可能出错的代码
} catch (error) { 
 // 出错时要做什么
}

```

``` Javascript
 try { 
 // 可能出错的代码
} catch (error) { 
 // 出错时要做什么
}
finally{
    //不管是执行完try还是catch，最终都会执行这里的代码。
}
```

``` Javascript
 try { 
 // 可能出错的代码
 trhow "出错了";//如果我们知道这里要出错，就应该直接在这里处理，因为这样更明确，可维护性更好。
} catch (error) { 
 // 出错时要做什么
}
finally{
    //不管是执行完try还是catch，最终都会执行这里的代码。
}
```

同时ECMA-262也规定了以下8中错误类型：

* error（用户自定义异常的时候使用。）
* InternalError
* EvalError（计算Eval出错的时候。）
* RangeError（数值越界的时候。）
* ReferenceError（在变量不是预期类型，或者访问不存在的方法时。）
* SyntaxError（r 经常在给 eval()传入的字符串包含 JavaScript 语法错误时发生，在 eval()外部，很少会用到 SyntaxError。这是因为 JavaScript 代码中的语法错误会导致代码无
法执行。）
* TypeError（在变量不是预期类型，或者访问不存在的方法时。）
* URIError（在使用 encodeURI()或 decodeURI()但传入了格式错误的URI 时。）

error是基类，其他的错误类型都是从error继承而来，因此都具备error基类的全部property。

到目前为止（2021年8月10日），出了firefox和IE,其他主流浏览器都没有实现InternalError。

注意：上述类型的错误都是对象，所以当我们需要判断捕获的异常是哪种类型的异常的时候，需要使用instanceof运算符。

一些抛出异常示例:
``` Javascript
throw new SyntaxError("I don't like your syntax."); 
throw new InternalError("I can't do that, Dave."); 
throw new TypeError("What type of variable do you take me for?"); 
throw new RangeError("Sorry, you just don't have the range."); 
throw new EvalError("That doesn't evaluate."); 
throw new URIError("Uri, is that you?"); 
throw new ReferenceError("You didn't cite your references properly."); 
//自定义错误常用的错误类型是 Error、RangeError、ReferenceError 和 TypeError。
```

## 浏览器端的异常处理

在浏览器端，对于error类的实现有三个property比较重要，分别是Error.prototype.message（异常附带的消息）、Error.prototype.name（异常的类名）、Error.prototype.stack（异常发生时的调用栈,发生异常的位置。）。而其他类都是继承自error，所以，它们也具备这三个peoperty。所有的主流浏览器都实现了这三个property，所以兼容性没有任何问题，利用这三个property，我们可以对未处理异常进行默认捕获，从而在后续过程中分析异常发生时的位置，从而修复这个未处理异常。

如果我们知道这里有一个异常要发生，我们应该处理好该异常，但是我们不能预知所有异常，所以给web页面添加默认的异常处理就非常重要，我们往往在默认异常处理中将本次异常记录日志到服务器中。

默认异常处理往往有两种添加方式：第一种将所要执行的所有Js代码通过try...catch...包围起来（当今的web页面显然不可能）；第二种给浏览器窗口添加error事件处理（未处理的异常最终都会触发window的error事件。图片加载也有error事件。）。

### 将异常日志记录到服务器

想要将异常日志记录到服务器，自然而然是要经过http协议将异常日志发送到服务器，这里我们可以使用Ajax或者使用Jsonp的方式，相比之下Jsonp的方式通用性更好。