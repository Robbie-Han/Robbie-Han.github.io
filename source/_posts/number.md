---
title: 关于number的判断
toc: true
tags: 
- JS
- number
---
## 判断是不是Number
```
typeof num === 'number';
Object.prototype.toString.call(num);//[object Number]
```
## 判断是不是整数：
使用原生方法：Number.isInteger(num)//true
## 判断是不是浮点数：
方法一：
```
function isFloat(num){
  if(typeof num === 'number'){
    return false;
  }
  return ~~num !== num
}
```
详解：
```
如果num是整数，则~~num === num
~5 = -5-1,~~-6 = 6-1 =5
如果是浮点数，则~5.5 = -6,~~-6 = 5, 5.5 !== 5

```
方法二：
```
function isFloat(num){
  if(typeof num === 'number'){
    return false;
  }
  return num % 1 !== 0
}
```