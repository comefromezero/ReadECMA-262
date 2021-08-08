# 扩展运算符(...,Spread Syntax)

用于将数组或者字符串展开，或者将对象以键值对的形式展开。

## 语法

函数调用：

myFunction(...iterableObj);


字面量数组构造或字符串：

[...iterableObj, '4', ...'hello', 6];


构造字面量对象时,进行克隆或者属性拷贝（ECMAScript 2018规范新增特性）：

let objClone = { ...obj };