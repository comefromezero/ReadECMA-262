# 自增和自减运算符

## 前缀自增和前缀自减

前缀自增（自减）会在表达式计算之前发生，所以参与表达式运算的是自增（自减）之后的值。

在某些情况下，这种前缀自增（自减）完全没有影响，例如:

``` Javascript
let num=29;
let num1=++num; //30
```
在另外一些情况下，这种前缀自增（自减）就会有影响了，例如：

``` Javascript
let num = 29;
let num1 = --num + 2;  //30
```

## 后缀自增和后缀自减

后缀自增（自减）会在表达式计算之后发生，所以参与表达式运算的是自增（自减）之前的值。

在某些情况下，这种后缀自增（自减）跟前缀自增（自减）几乎一样，例如：

``` Javascript
let num=29;
let num1=num++; //30
```

在另外一些情况下，这种后缀自增（自减）就有所不同了，例如：

``` Javascript
let num=29;
let num1 = num-- + 2; //31
```

上面就是前缀自增（自减）与后缀自增（自减）的重要区别，也是在表达式计算过程中容易出错的地方。

## 自增和自减运算符作用于非数字类型

当自增和自减运算符作用于非数字类型的时候，会现将其他类型转换为数字类型，然后再运算自增和自减。

