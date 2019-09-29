---
title: Promise.all()手工代码实现
toc: true
tags: 
- JS
- Promis.all()
---
# 写个函数代替promise.all()

### 百度版
这我百度过来感觉相对比较靠谱的代码：
<!--more-->
```js
function promiseAll(promises) {
  return new Promise(function(resolve, reject) {
    if (!Array.isArray(promises)) {
      return reject(new TypeError('arguments must be an array'));
    }
    var resolvedCounter = 0;
    var promiseNum = promises.length;
    var resolvedValues = new Array(promiseNum);
    for (var i = 0; i < promiseNum; i++) {
      (function(i) {
        Promise.resolve(promises[i]).then(function(value) {
          resolvedCounter++
          resolvedValues[i] = value
          if (resolvedCounter == promiseNum) {
            return resolve(resolvedValues)
          }
        }, function(reason) {
          return reject(reason)
        })
      })(i)
    }
  })
}
```
这款代码的缺陷：
* 代码冗余
* 代码只对数组类型进行操作，实际上Promise.all()的参数只要是可迭代的，都可以进行操作。

### 优化版
当我对这段代码不满意时，我参考了阮一峰大佬的《ES6 入门》和另外一本经典书《深入理解ES6》关于Iterator这一章的讲解，得到下面又换后的代码：

#### 代码优化：
```js

function promiseAll(promises) {
  return new Promise(function(resolve, reject) {
    if (typeof obj[Symbol.iterator] !== 'function') {
        return reject(new TypeError('arguments must be iterator'));
    }
    let promiseValue = [];
    let length = promises.length;

    for (let i = 0; i < length; i++) {
          Promise.resolve(promises[i]).then(function(value) {
            promiseValue[i] = value;
              if(promiseValue.length === length) {
                resolve(promiseValue)
              }
            }, function(reason) {return reject(reason)})
        }

  })
}

```

> 如有不足，欢迎指正 :grin: