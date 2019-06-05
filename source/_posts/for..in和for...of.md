---
title: for...in 和 for...of对比
toc: true
tags: 
- JS
- for...in 
- for...of
---
# for...in 和 for...of 对比
## 1. 关于for...in

### 1.1 MDN的定义
> for...in语句以**任意顺序**遍历一个对象`自有的、继承的、可枚举的、非Symbol的属性`。对于每个不同的属性，语句都会被执行。

思考：通过这个定义，我得到三点结论：
  * for...in 遍历的结果不一定和被遍历对象的顺序相同。
  * for...in 不但可以遍历被遍历对象的自有属性，还可以遍历原型上的和继承来的可枚举属性。
  *  String 的 indexOf()  方法或 Object的toString()方法，这些显然是原型上不可枚举的属性
### 1.2 for...in 语法
```
for (variable in object) {...}
```
其中 variable为属性名，object是被遍历对象。
### 1.3 for...in 能不能遍历数组？
> 数组索引只是具有整数名称的枚举属性，并且与通用对象属性相同。不能保证for ... in将以任何特定的顺序返回索引。

考虑到遍历数组不能直接得到数组元素和索引顺序的不确定性，所以最好不要使用for...in。另外for...in的便利还有可能把数组原型上的属性遍历出来。
<!--More-->
#### 1.3.1 数组使用for...in举例
```
//向数组的原型上添加属性
Array.prototype.sayHello = function(){
    console.log("Hello")
}
Array.prototype.str = 'world';

var myArray = [1,2,10,30,100];
myArray.name='数组';

for(let index in myArray){
    console.log(index);
}
/*
0
1
2
3
4
name
sayHello
str
*/
```
### 1.4 for...in 遍历对象
使用for...in遍历对象可以直接知道对象的key,间接知道对象每项对应的值，这么使用显然是合理的。

#### 1.4.1 对象使用for...in举例
```

// 向原型上添加属性
Object.prototype.sayHello = function(){
  console.log('Hello');
}
Object.prototype.str = 'World';
var myObject = {name: 'zhangsan', age: 100};

for(let index in myObject){
    console.log(index);
}
/*
name
age
sayHello
str
*/
```
#### 1.4.2 如何只遍历自有属性
  使用`hasOwnProperty()`,可以保证只迭代自身属性
```
for(let index in myObject){
    if(myObject.hasOwnProperty(index)){
        console.log(index)
    }
}
```
## 2. 关于for...of
### 2.1 MDN的定义
> for...of 语句在可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句。

思考：通过这个定义，我得到三点结论：
* for...of 只能用于可迭代对象，且可以通过迭代的过程中直接拿到属性值。
* 对象是不可以迭代的，显然不适用于for...of。
* for...of 和forEach()在遍历数组的时候会有什么不同呢？
### 2.2 for...of 语法

```
for (variable of iterable) {
    //statements
}
```
variable对应每次迭代中属性的值，iterable对应的是被迭代的对象。
### 2.3 for...of 遍历可迭代的对象
#### 2.3.1 for...of迭代数组
```
let iterable = [10, 20, 30];

for (let value of iterable) {
    value += 1;
    console.log(value);
}
// 11
// 21
// 31

```
#### 2.3.2 for...of迭代字符串
```
let iterable = "boo";

for (let value of iterable) {
  console.log(value);
}
// "b"
// "o"
// "o"
```
    对字符串和数组的迭代是比较常用的，其它可迭代的数据类型在项目中见的比较少
#### 2.3.3 for...of迭代set
```
let iterable = new Set([1, 1, 2, 2, 3, 3]);

for (let value of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```
    这个例子也佐证了利用set可以对数组去重。[...iterable]解构给数组即可

### 2.3.4 for...of迭代Map
```
let iterable = new Map([["a", 1], ["b", 2], ["c", 3]]);

for (let entry of iterable) {
  console.log(entry);
}
// ["a", 1]
// ["b", 2]
// ["c", 3]

for (let [key, value] of iterable) {
  console.log(value);
}

// 1
// 2
// 3
```
    Map这个迭代引发思考：[key, value]是 entry的解构写法？那iterable是不是某种迭代器的简写？
#### 2.3.4.1 集合对象迭代器：
ES6中有三种类型的集合对象：Array Set和 Map，
这是三者都包含三种迭代器：
* entries() 返回一个迭代器，其值为多个键值对的集合 [key,value]
* values()  返回一个迭代器，其值为集合的值 value
* keys() 返回一个迭代器，其值为集合中所有的键名 key

      思考：
      * 对于Array和Set类型的对象，这三个迭代器意义不大。数组的index用遍历器迭代没啥意义，对于Set,键值相同。
      * 对于Map是有意义的，可以得到Map中每个元素的键和值

eg: 对于Set
```
let iterable = new Set([3322, 2233]);

for (let entry of iterable.entries()) {
  console.log(entry);
}
/*
[3322, 3322]
[2233, 2233]
*/
```
eg: 对于Map
```
let iterable = new Map([["a", 1], ["b", 2], ["c", 3]]);
// 键：
for (let key of iterable.keys()) {
  console.log(key);
}
// 值
for (let value of iterable.values()) {
  console.log(value);
}
```
### 2.3.5 for...in迭代arguments
```
function iterator(){
 for (let argument of arguments) {
    console.log(argument);
  }
}
iterator('han','robbie','TS')
// han
// robbie
// TS
```
# 3. for...in 和for...of总结
     对于for...in，它可以遍历自有的、原型上的、继承来的可枚举属性，适合去遍历对象,并得到属性名
     对于for...of，它可以遍历可迭代的对象，可以得到可迭代对象属性的值，适合遍历字符串、数组、Set、Map等
     <p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="ustc-han" data-slug-hash="NVBWgV" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="test.html">
  <span>See the Pen <a href="https://codepen.io/ustc-han/pen/NVBWgV/">
  test.html</a> by USTC-Han (<a href="https://codepen.io/ustc-han">@ustc-han</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>