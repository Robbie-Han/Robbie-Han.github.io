---
title: Array.prototype.flat()
toc: true
tags: 
- JS
- Array
- flat
---
## flat函数
flat这个函数的方法很少的使用，它的意思就是将数组的元素‘打平’。说的感觉挺悬乎的，其实这是一个很简单的函数。那么下面我想通过这几方面来研究它：1、如何使用flat? 2、它是不是有副作用？会影响原数组？3、原生的flat方法是怎么实现的？
## flat函数的用法
flat的语法：`var newArray = arr.flat(depth)`，其中的depth的值是个number类型。
> deepth指的提取嵌套数组的结构深度，默认值为 1

## 实测flat

![20190729203145.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190729203145.png)

测试的结果如上图所示。
- 第一个方框说明当depth的值大于数组元素的嵌套深度的时候会将所有的数组元素打平输出。
- 第二个红框则说明了，使用flat方法不会影响原数组

那数组的那些方法会影响原数组呢？列举几个常见的：
```
sort()、reverse()、splice()、push()、pop()、shift()、unshift()
```
那数组的那些方法不会影响原数组呢？列举几个常见的：
```
map()、forEach()、reduce()、filter()、join()、concat()、slice()
```
<!--more-->
## 原生方法实现：
```js
Array.prototype._flat = function(depth = 1){
	var result = [];
	var length = this.length;
	if(depth === 0) return this;
	for(var i = 0; i < length; i++){
		if(this[i] instanceof Array){
			result = [...result, ...this[i]._flat(depth - 1)];
		}else {
			result.push(this[i]);
		}
	}
	return result
}
```
实现思路：递归嵌套数组

对数组的元素进行判断，如果是数组就递归，不是数组就推进result中。递归当depth为0的时候截止。最后返回result
## MDN的‘打平’思路：
### 使用递归：
```js
var arr1 = [1,2,3,[1,2,3,4, [2,3,4]]];

function flattenDeep(arr1) {
   return arr1.reduce((acc, val) => Array.isArray(val) ? acc.concat(flattenDeep(val)) : acc.concat(val), []);
}
flattenDeep(arr1);
```
利用reduce的递归方法，来将所有的元素遍历，如果是数组就递归，不是数组放进迭代acc里

- 思考

`把acc换成push如何？`push返回的是数组的length。那样的话 acc = length。会怎么样？

### 不用递归：
```js
function flatten(input) {
    var stack = [...input];
    var result = [];
    while(stack.length){
        var value = stack.pop();
        if(!Array.isArray(value)){
            result.unshift(value);
        }else{
            stack = [...stack,...value];
        }
    }
    return result
}
```
数组从后向前解析，遇到不是数组的就直接头插result中，如果是数组，将数组结构和剩余的源数组链接，重复操作。

### 更简单的做法：

前提：处理的数组，不管有多少层，只有数字类型
```js
var arr1 = [1,2,3,[1,2,3,4,[2,3,4]]];
arr1.join().split(',').map(value => +value);

// arr1.join() 的结果"1,2,3,1,2,3,4,2,3,4"
```




