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

