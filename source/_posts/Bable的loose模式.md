---
title: Babel的loose模式的坑
tags: 
- JS
- babel
---
## 项目中Babel的loose的坑
对Set的解构：
```
const set = new Set([1,2,3,4]);
[...set]
```
我想得到[1,2,3,4]
但是如果项目的Babel配置中使用Loose模式(勾选左侧的ES-2015-loose)，在Babel中的解析：
```
"use strict";

var set = new Set([1, 2, 3, 4]);
[].concat(set);
```
这种解析方式就很难受了，它不是通过Array.from()来解析的。这样的情况还存在Map中，这种方式对数组类型显然没有影响。

**在Babel的normal模式下的解析：**
<!--more-->
```
"use strict";

function _toConsumableArray(arr) { return _arrayWithoutHoles(arr) || _iterableToArray(arr) || _nonIterableSpread(); }

function _nonIterableSpread() { throw new TypeError("Invalid attempt to spread non-iterable instance"); }

function _iterableToArray(iter) { if (Symbol.iterator in Object(iter) || Object.prototype.toString.call(iter) === "[object Arguments]") return Array.from(iter); }

function _arrayWithoutHoles(arr) { if (Array.isArray(arr)) { for (var i = 0, arr2 = new Array(arr.length); i < arr.length; i++) { arr2[i] = arr[i]; } return arr2; } }

var set = new Set([1, 2, 3, 4]);

_toConsumableArray(set);
```
- 先判断是不是数组，是的话返回数组
- 再判断是不是可迭代的对象Symbol.iterator in Object(iter)，如果没成功，判断是不是类数组对象
- 使用Array.from(),将set转成数组

**参考链接:**

https://w3ctech.com/topic/1708
https://github.com/babel/babel/issues/8298