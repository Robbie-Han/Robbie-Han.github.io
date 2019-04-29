---
title: async函数
toc: true
tags: 
- JS
- Async
- 随笔
---
### 1、什么是async函数：

async函数是js处理异步函数的最终解决方案，它的语法看起来是用同步的代码结构来描述异步的代码。async函数返回值是一个成功或者失败状态的Promise，但必须等到内部所有的Promise执行完以后，才会发生状态改变。

#### 1.1、 async函数的优点
async/await是Generator函数的语法糖，相比之下会有如下优点：

##### 1、内置执行器：

async函数自带执行器，不需要调用next()方法。

##### 2、更好的语义：

async/await相对与*/yield来说有更好的语义

##### 3、更好的适用性：
对于yield，后面只能是thunk或者promise函数。而await后面可以是promise和原始类型值，如果不是Promise的话，会将其默认转化为Promise

##### 4、返回值是promise
async函数返回值是promise类型，而Generator函数必须是Iterator 对象
<!--more-->
### 2、async函数的语法
#### 2.1 async函数结构表达式：

```
async function name([param[, param[, ... param]]]) {
   statements
}
```
eg:

```
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  var result = await resolveAfter2Seconds();
  console.log(result);
  // expected output: 'resolved'
}

asyncCall();
// 'calling'
// after 2 second
//resolved 
```
#### 2.2、async函数的注意事项
async函数中await可以暂停函数的执行，等到异步函数返回执行结果的时候再继续执行函数。

await关键字只能用在async函数中，用在其它地方会抛错。

async函数不同于promise函数，函数中使用return不是必须的，如果含有return，则返回的Promise中的promiseValue的值不为undefide。否则依旧会返回一个promiseValue为空的Promise。

#### 3、async函数的错误处理机制

在async函数中，如果await后面的异步函数中抛出错，则async函数剩余的函数都将不会执行。

如下所示：
```
async function f() {
  await Promise.reject('出错了');
  await Promise.resolve('hello world'); // 不会执行
}
```
有时候我们希望一个await函数执行失败后，不要影响其它函数的执行。可以将await用try{}catch(){}包起来。

如下所示：
```
async function f() {
  try {
    await Promise.reject('出错了');
  } catch(e) {
  console.log(e)
  }
  return await Promise.resolve('hello world');
}

f()
.then(v => console.log(v))
// hello world

```
#### 4、async函数并发执行
当多个await命令后的函数之间没有依赖关系的时候，可以考虑让它们并发的执行：

```
var resolveAfter2Seconds = function() {
  console.log("starting slow promise");
  return new Promise(resolve => {
    setTimeout(function() {
      resolve("slow");
      console.log("slow promise is done");
    }, 2000);
  });
};

var resolveAfter1Second = function() {
  console.log("starting fast promise");
  return new Promise(resolve => {
    setTimeout(function() {
      resolve("fast");
      console.log("fast promise is done");
    }, 1000);
  });
};
var sequentialStart = async function() {
  console.log('==SEQUENTIAL START==');

  // 1. Execution gets here almost instantly
  const slow = await resolveAfter2Seconds();
  console.log(slow); // 2. this runs 2 seconds after 1.

  const fast = await resolveAfter1Second();
  console.log(fast); // 3. this runs 3 seconds after 1.
}
// sequentialStart函数执行完需要三秒，两个无关的函数顺序执行

var concurrentStart = async function() {
  console.log('==CONCURRENT START with await==');
  const slow = resolveAfter2Seconds(); // starts timer immediately
  const fast = resolveAfter1Second(); // starts timer immediately

  // 1. Execution gets here almost instantly
  console.log(await slow); // 2. this runs 2 seconds after 1.
  console.log(await fast); // 3. this runs 2 seconds after 1., immediately after 2., since fast is already resolved
}

var concurrentPromise = function() {
  console.log('==CONCURRENT START with Promise.all==');
  return Promise.all([resolveAfter2Seconds(), resolveAfter1Second()]).then((messages) => {
    console.log(messages[0]); // slow
    console.log(messages[1]); // fast
  });
}
```
`concurrentStart和concurrentPromise是两种异步函数无耦合的情况的下并发执行的方式
`



