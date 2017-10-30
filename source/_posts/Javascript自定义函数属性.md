---
title: Javascript自定义函数属性
date: 2017-10-07 00:45:14
categories: "前端"
tags:
     - javascript
     - js函数
description:
---

> Javascript中函数不是一个原始值，而是一种特殊的对象，也就是说，函数可以拥有属性。
<!--more-->

*这是个新大陆，利用好的话可以简化很多代码。当然这不是什么高端函数，这个大陆只是一种思维。*

比如，假设你想写一个返回一个唯一整数的函数，不管在哪里调用函数都会返回这个函数。而函数不能两次返回同一个值，为了做到这一点，函数必须能够跟踪它每次返回的值，而且这些值的信息需要在不同的函数调过程中持久化。可以将这些信息存放在一个全局变量中，但这并不是必须的，因为这个信息仅仅是函数本身用到的。最好将这个信息保存到函数对象的一个属性中，下面这个例子就实现了这样一个函数，每次调用函数都会返回一个唯一的整数：
```
// 初始化函数对象的计数属性
// 由于函数声明提前了，因此这里是可以函数声明
// 之前给它的成员赋值的
uniqueInteger.counter = 0;

// 每次调用这个函数都会返回一个不同的整数
// 它使用一个属性来记住下一次将要返回的值
function uniqueInteger() {
    return uniqueInteger.counter+; // 先返回计数器的值，然后计数器自增1
}
```
来看另一个例子，下面这个函数factorial()使用了自身的属性（将自身当作数组来对待）来缓存上一次的计算结果：
```
// 计算阶乘，并将结果缓存至函数的属性中
function factorial(n) {
    if (isFinite(n) && n>0 && n==Math.round(n)) {
        if (!(n in factorial))
            factorial[n] = n*factorial(n-1);
        return factorial[n];                
    }
    else return NaN;  // 如果输入有误
}
```
