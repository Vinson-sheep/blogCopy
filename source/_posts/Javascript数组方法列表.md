---
title: Javascript数组方法列表
date: 2017-10-06 01:26:25
categories: "前端"
tags:
     - javascript
     - js数组
description:
---

> ECMAScript 3在Array.prototype中定义了一些很有用的操作数组的函数，ECMAScript 5新新增了一些新的数组遍历方法。
<!--more-->

## ECMAScript 3
1. `a.join()`合并数组元素转换为字符串
2. `a.reverse()`反转数组
3. `a.sort()`排列数组元素
4. `a.concat()`合并多个数组
5. `a.slice()`截取数组元素并返回新数组
6. `a.splice()`数组操作万能方法
7. `push()`和`pop()`插入/删除最后一个元素
8. `unshift`和`shift()`插入/删除最后一个元素
9. `toString()`和`toLocaleString()`
### Array.sort()
`Array.sort()`方法将数组中的元素排序并返回排序后的数组。当不带参数调用`sort()`时，数组元素以字母表顺序排序：

如果数组包含`undefined`元素，它们会被排列到数组的尾部。

为了按照其他方式而非字母表顺序进行组排序，必须给sort()方法传递一个比较函数。

假设第一个参数应该在前，比较函数应该返回一个小于0的数值。反之，假设第一个参数应该在后，函数应该返回一个大于0的数组。并且，假设两个值相等，函数应该返回0.
```
var a = [33, 4 ,1111, 222];
a.sort();               // 字母表顺序：1111,222,33,4
a.sort(function(a,b) {  // 数值顺序： 4，33，222，1111
    return a-b;
});
a.sort(function(a,b) { return b-a});  //数值大小相反的顺序
```
### Array.concat()
`Array.concat()`方法创建并返回一个新数组，它的元素包括调用`concat()`的原始数组的元素和concat()的每个参数。
```
var a = [1,2,3];
a.concat(4,5);          // [1,2,3,4,5]
a.concat([4,5]);        // [1,2,3,4,5]
a.concat([4,5],[6,7]);  // [1,2,3,4,5,6,7]
a.concat(4,[5,[6,7]]);  // [1,2,3,4,5,[6,7]]
a                       // [1,2,3]:a没有改变
```
### Array.slice()
```
var a = [1,2,3,4,5];
a.slice(0,3);   // [1,2,3]
a.slice(3);     // [4,5]
a.sliec(1.-1);  // [2,3,4]
a.slice(-3,-2); // [3]
```
### Array.splice()
不同于`slice()`和`concat()`，`splice()`会修改调用的数组。

如果省略第二个参数，从起始点开始到数组结尾的所有元素都将被删除。
```
var a =[1,2,3,4,5,6,7,8];
a.splice(4);      //  返回[5,6,7,8];a是[1,2,3,4]
a.splice(1,2);    //  返回[2,3];a是[1,4]
a.splice(1,1);    //  返回[4];a是[1]

var a = [1,2,3,4,5];
a.splice(2,0,'a','b');  // 返回[];a是[1,2,'a','b',3,4,5]
a.splice(2,2,[1,2],3);  // 返回['a','b'];a是[1,2,[1,2],3,3,4,5]
```

## ECMAScript 5
ECMAScript 5中的数组方法都不会修改它们调用的原始数组。当然，传递给这些方法的函数是可以修改这些数组的。

1. `forEach()`从头到尾遍历数组。
2. `map()`将每个元素传递给函数，并返回一个数组
3. `filter()`过滤函数，返回一个被过滤的数组
4. `every()`和`some()`用来判断数组属性的方法
5. `reduce()`和`reduceRight()`迭代函数
6. `indexOf()`和`lastIndexOf()`搜索函数

### Array.forEach()
这个函数可以修改原始数组。
```
var data = [1,2,3,4,5]; // 要求和的数组
// 计算数组元素的和值
var sum = 0;            // 初始化为0
data.forEach(function(value) { sum += value; });
                        // 将每个值累加在sum上
sum;                    // => 15
//每个数组元素自加1
data.forEach(function(v,i,a) {a[i]=v+1});
data                    // => [2,3,4,5,6]
```
这个方法的遍历如需终止，需要将方法放在try块中。（犀牛书p156）
### Array.map()
```
a = [1,2,3];
b = a.map(function(x) {return x*x; }); // b是[1,4,9]
```

### Array.filter()
函数的返回值如果是true或者是能转换为true值，那么传递给判定函数的元素就是这个子集的成员，它将被添加到一个作为返回值的数组中。例如：
```
a = [5,4,3,2,1];
smallvalues = a.filter(function(x) {return x<3}); // [2,1]
everyother = a.filter(function(x,i) {return i&2==0}); // [5,3,1]
```

### Array.every()和Array.some()
`every()`和`some()`方法是数组的逻辑判定：它们对数组元素应用指定的函数进行判定，返回`true`或`false`。
```
a = [1,2,3,4,5];
a.every(function(x) { return x < 10; });      // true:所有的值<10
a.every(function(x) { return x * 2 === 0;});  // fasle:不是所有的值都是偶数
```

```
a = [1,2,3,4,5];
a.some(function(x) {return x%2===0;});  // true
a.some(isNaN);                          // false
```

### reduce()和reduceRight()
`reduce()`和`reduceRight()`方法使用指定的函数将数组元素进行组合，生成单个值。
```
var a=[1,2,3,4,5];
var sum = a.reduce(function(x,y) {return x+y }, 0);
```
这里的x可以看作是迭代的值，y是元素，第二个参数0是x的初始值。

`reduceRight()`工作原理和`reduce()`一样，不同的是它按照数组索引从高到低处理数组，而不是从低到高。

### indexOf()和lastIndexOf()
`indexOf()`和`lastIndexOf()`搜索整个数组中具有给定值的元素，**返回找到的第一个元素的索引或者如果没有找到就返回-1**。`indexOf()`从头到尾搜索，而'lastIndexOf()'则反向搜索。
```
a = [0,1,2,1,0];
a.indexOf(1);     // => 1: a[1]是1
a.lastIndexOf(1); // => 3: a[3]是1
a.indexOf(3);     // => -1: 没有值为3的元素
```
`indexOf()`和`lastIndexOf()`可以提供第二个参数，指定从那个索引开始搜索。利用第二个参数可以搜索全部的值的索引。
```
pos = a.indexOf(x, pos);
```
