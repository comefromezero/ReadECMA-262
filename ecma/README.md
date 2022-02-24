# 说明

这是ECMA-262标准的备份。

在ES6及以前，ECMA-262文档发布都采用ECMA-2.0，ECMA-3.0，ECMA-5.0这样的方式，即采用前缀+版本的方式来命名文档。

在ES6及以后，ECMA-262文档开始采用ECMA-2015，ECMA-2016，ES-2017等这种方式，即采用前缀+年份的方式来命名文档，同时发布的时间也改为一年一版。

于是，ES6又被称为ES2015，此后的ECMA标准，都采用ES2016，ES2017，ES218的方式来进行命名。


# ES文档中内容变化

## SourceText

起步支持unicode2.0  U+0000 to U+10FFFF（ES2.0）

起步支持unicode2.1  U+0000 to U+10FFFF（ES3.0）

起步支持unicode5.0  U+0000 to U+10FFFF（ES5.0）

起步支持unicode5.1  U+0000 to U+10FFFF（ES6.0）

起步支持unicode8.0  U+0000 to U+10FFFF（ES2016）

## comments

//单行注释  （ES2.0）

/* 多行注释 */  （ES2.0）


## keywords and reserved words

### keywords

break        for                new         var
continue  function       return      void
delete       if                   this          while
else          in                  typeof      with

### future reserved words

abstract         do                     import             short
boolean         double              instanceof      static
byte                enum               int super
case               export              interface          switch
catch              extends           long                 synchronized
char               final                  native               throw
class              finally               package           throws
const             float                  private              transient
debugger      goto                  protected         try
default           implements     public                volatile

以上为ES2.0

新增9个关键字，case  switch  difault  finally  try   catch   throw  do  instanceof,同时减少了上述9个保留字。(ES3.0)

新增关键字debugger(ES5.0)

non-strict mode reserved words：

class      enum      extends     super     const     export    import (ES5.0)
 
strict mode reserved words：

implements     let      private      public     yield    interface     package    protected    static (ES5.0)

## Punctuator

=                 >                   <                 ==                  <=                     >=
!=                ,                    !                   ~                   ?                        :
.                  &&                ||                 ++                   --                       +
\-                  *                    /                   &                    |                        ^
%                <<                 >>               >>>                +=                     -=
*=                /=                 &=               |=                   ^=                     %=
<<=            >>=               >>>=           (                       )                         {
}                  [                    ]                  ;

以上为ES2.0

新增两个字符：===    和！== （ES3.0）

## identifier

可以有以下字符组成：

26个大小写字母

$  _  

以及0-9等阿拉伯数字

不能以0-9这几个阿拉伯数字开头

不能是保留字

以上为ES2.0
