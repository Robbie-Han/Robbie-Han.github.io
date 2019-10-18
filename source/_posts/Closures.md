---
title: 重新思考闭包和内存泄漏
tags:  
- JS
- 闭包
- 内存泄漏
toc: true
---

## 闭包

闭包之前的理解是，一个函数引用外部函数的内部变量时，就会生成闭包。但是这个理解其实不是特别准确，其实即使不引用也会生成闭包。正确的理解是`内部函数可以访问其父级的函数变量和参数`，此时便是一个闭包。通过一个经典例子看一下：

```js
function addHandler() {
    var el = document.getElementById('el');
    el.onclick = function() {
        this.style.backgroundColor = 'red';
    }
}
```
虽然在内部回调函数没有引用外部函数中的变量el，但该变量依旧是闭包范围的一部分，即使它可能没有在函数本身内部直接引用（通过查看函数代码）。
区别在于引擎如何优化未使用的变量。
<!--more-->
## 内存泄漏

上面函数引起内存泄漏只存在于IE浏览器中，因为IE浏览器使用垃圾回收策略是引用计数，每次触发`click`回调都会生成一个新的函数，并带有一个包含el的闭包。
因为匿名函数保持者对el的访问权，垃圾回收器无法将其从内存中删除。所以会导致内存泄漏。

但是这种情况在Chrome中不会存在，在Chrome中V8采用了一种代回收的策略，将内存分为两个生代：[新生代（new generation）和老生代（old generation)](https://thinkbucket.github.io/docsite/docs/javascript/2.memory/old-new-space)。当内部函数没有引用外部函数变量时，函数执行完整体都会被直接回收，不会引起内存泄漏。

## 参考链接：

[参考链接一](https://stackoverflow.com/questions/15801471/deeper-understanding-of-closure-in-javascript/15801663#15801663)

[参考链接二](https://stackoverflow.com/questions/15761094/dom-why-is-this-a-memory-leak/15761640#15761640)


