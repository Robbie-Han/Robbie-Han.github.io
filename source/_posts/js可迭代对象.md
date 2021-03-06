---
title: js可迭代对象
toc: true
tags: 
- JS
- Iterable
---
## js可迭代对象
`可迭代对象的原型中都包含Symbol.iterator 属性`
```
Set(0) {}
size: (...)
__proto__: Set
add: ƒ add()
clear: ƒ clear()
constructor: ƒ Set()
delete: ƒ delete()
entries: ƒ entries()
forEach: ƒ forEach()
has: ƒ has()
keys: ƒ values()
size: (...)
values: ƒ values()
Symbol(Symbol.iterator): ƒ values()
Symbol(Symbol.toStringTag): "Set"
get size: ƒ size()
__proto__: Object
[[Entries]]: Array(0)
```
常用的可迭代对象，有数组、Set、Map、字符串。
## 判断可迭代的方法

`Symbol.iterator in Object(iter)`
判断被判断对象的原型连上是不是有Symbol.iterator属性。
```
Symbol.iterator in Object([1,2])//true
Symbol.iterator in Object({})//false
Object(12) => Number(12)
Object() 相当于 new Object();是对Object()里内容类型的实例
```
`typeof obj[Symbol.iterator] === 'function'`
```
var arr = [];
typeof arr[Symbol.iterator] === 'function' //true
```