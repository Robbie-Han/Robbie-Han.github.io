---
title: Math对象常用方法
toc: true
tags: 
- JS
- Math
---
## 1.Math.abs(x);
传入一个非数字形式的字符串或者 undefined/empty 变量，将返回 NaN。传入 null 将返回 0。
```
Math.abs('-1');     // 1
Math.abs(-2);       // 2
Math.abs(null);     // 0
Math.abs("string"); // NaN
Math.abs();         // NaN
```
## 2.Math.ceil(x):
函数返回大于或等于一个给定数字的最小整数。
<!--more-->
## 3.Math.max(value1[,value2, ...])
```
一组数的最大值
Math.max(10, 20); 

//数组中的最大值
var arr = [1, 2, 3];
var max = Math.max(...arr);
```
研究了一下求数组最大值的原理
```
var arr = [1, 2, 3];
Math.max.apply(Math, arr);

// => Math.max(1,2,3)
```

## 4.Math.pow(base, exponent) 
base：基数

exponent：指数
## 5.Math.random() 
[0,1)内的随机数，没有参数
```
//求两个整数之间的随机整数
function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min)) + min; //不含最大值，含最小值
}
//含最大值，含最小值 
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
}
```
## 6.Math.round(num) 
四舍五入，当num为负数时，小数大于0.5则舍入到绝对值更大的数，等于0.5则舍入相邻临近正无穷的数
```
Math.round(-1.5) //-1
Math.round(-1.4) //-1
Math.round(-1.6) //-2
```
## 7.Math.sqrt(num)
返回数的平方根