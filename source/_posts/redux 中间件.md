---
title: react中间件
tags: 
- React
toc: true
---
# redux 中间件
###  1.什么是中间件
普通使用同步功能时，action的改变会立即触发reducer处理状态，而中间件redux的本质的目的是提供第三方插件的模式，自定义拦截 action -> reducer 的过程。变为 action -> middlewares -> reducer 。这种机制可以让我们改变数据流，实现如异步 action ，action 过滤，日志输出，异常报告等功能。

---
### 2.理解中间件预备知识
Redux 提供了一个叫 applyMiddleware() 的方法，== 可以应用多个中间件 ==，要想理解applyMiddleware，首要理解compose()的用法，而要想看懂compose()函数，首先要理解arr.reduce()方法

#### 2.1 arr.reduce()：
[详解](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
<!--more-->

eg:
```
let funcs = [fn1,fn2,fn3]
funcs.reduce((a, b) => (...args) => a(b(...args)))
```
对于数组中的每个元素，多对一迭代。最后返回 fn1(fn2(fn3(...args))
#### 2.2 compose源码

```
export default function compose(...funcs) {
  if (funcs.length === 0) {
    return arg => arg
  }

  if (funcs.length === 1) {
    return funcs[0]
  }      

  return funcs.reduce((a, b) => (...args) => a(b(...args)))
}
```
 compose(f, g, h)(...args) 结果 f(g(h(...args))).
 

---
### 3.applyMiddleware源码：

```
import compose from './compose'

export default function applyMiddleware(...middlewares) {
  return (createStore) => (reducer, preloadedState, enhancer) => {
    var store = createStore(reducer, preloadedState, enhancer)
    var dispatch = store.dispatch
    var chain = []

    var middlewareAPI = {
      getState: store.getState,
      dispatch: (action) => dispatch(action)
    }
    
    chain = middlewares.map(middleware => middleware(middlewareAPI))
    dispatch = compose(...chain)(store.dispatch)

    return {
      ...store,
      dispatch
    }
  }
}
```
看一眼，一脸懵逼，有没有……

![image]( https://gss0.baidu.com/-vo3dSag_xI4khGko9WTAnF6hhy/zhidao/pic/item/d52a2834349b033ba6049a7710ce36d3d439bd8b.jpg)

要想看懂这一堆箭头函数，还需要看一下createStore()的源码，当然如果不想理解这些箭头函数可以不看creatStore()源码；

> redux中的createStore函数写法：

```
createStore(
    rootReducers,    //reducer
    preloadedState,
    applyMiddleware( //enhancer
        thunkMiddleware,
        createLogger()
    )
)
```
> createStore源码：

```
export default function createStore(reducer, preloadedState, enhancer) {
  if (typeof preloadedState === 'function' && typeof enhancer === 'undefined') {
    enhancer = preloadedState
    preloadedState = undefined
  }

  if (typeof enhancer !== 'undefined') {
    if (typeof enhancer !== 'function') {
      throw new Error('Expected the enhancer to be a function.')
    }

    return enhancer(createStore)(reducer, preloadedState)
  }
 .......
}
```
> 显然 enhanser是applyMiddleware函数，执行第二个if语句，最后
> return enhancer(createStore)(reducer, preloadedState)
> 
等价于
> applyMiddleware(thunkMiddleware,createLogger())==(createStore)(reducer, preloadedState)==

带着这条结果回头再看applyMiddleware源码：
等价于
```
（(createStore) => (reducer, preloadedState, enhancer) => {
    var store = createStore(reducer, preloadedState, enhancer)
    var dispatch = store.dispatch
    var chain = []

    var middlewareAPI = {
      getState: store.getState,
      dispatch: (action) => dispatch(action)
    }
    
    chain = middlewares.map(middleware => middleware(middlewareAPI))
    dispatch = compose(...chain)(store.dispatch)

    return {
      ...store,
      dispatch
    }
  }）(createStore)(reducer, preloadedState)

```
>  执行到这里调用 var store = createStore(reducer, preloadedState, enhancer)
此时enhance为undefined，调用createStore时执行第一个if语句，最终返回store。


##### 总结：

- applyMiddleware 执行过后返回一个闭包函数，目的是将创建 store的步骤放在这个闭包内执行，这样 middleware 就可以共享 store 对象。

- middlewares 数组 map 为新的 middlewares 数组，包含了 middlewareAPI

- compose 方法将新的 middlewares 和 store.dispatch 结合起来，生成一个新的 dispatch 方法

- 返回的 store 新增了一个 dispatch 方法， 这个新的 dispatch 方法是改装过的 dispatch，也就是封装了中间件的执行。

#### 是不是还是有点蒙
![image](http://img.tukexw.com/img/c5ea0ded2055636f.jpg)

下面将再细化一下：
### 4.中间件的执行过程
通过上面的 applyMiddleware 和 中间件的结构，假设应用了如下的中间件: [A, B, C]，一个 action 的完整执行流程

#### 4.1 初始化阶段

一个中间件的结构为

```
function ({getState，dispatch}) {
    return function (next) {
        return function (action) {...}
    }
}
```
初始化阶段一：middlewares map 为新的 middlewares

> chain = middlewares.map(middleware => middleware(middlewareAPI))

执行过后，middleware 变为了

```
function (next) {
    return function (action) {...}
}
```
> 初始化阶段二：compose 新的 dispatch


```
const newDispatch = compose(newMiddlewares)(store.dispatch)
```

#### 4.2 compose 流程

rest.reduce((composed, f) => f(composed), last(...args))
> last(...args)是初始值，一开始 composed=store.dispatch

第一次执行

> initialValue: composedC = C(store.dispatch) = function C(action) {}

> next 闭包： store.dispatch

第二次执行：

> previousValue(composed): composedC
> 
> currentValue(f): B
> 
> return value: composedBC = B(composedC) = function B(action){}
> 
> next 闭包 composedC

第三次执行：
> previousValue(composed): composedBC
> 
> currentValue(f): A
> 
> return value: composedABC = A(composedBC) = function A(action){}
> 
> next 闭包 composedBC
> 
> 最后的返回结果为 composedABC

执行到此生成新的dispatch函数，封装好的dispatch(action)就等价与composeABC(action)
#### 执行阶段
> dispatch(action) 等于 composedABC(action) 等于执行 function A(action) {...}
> 
> 在函数 A 中执行 next(action), 此时 A 中 next 为 composedBC，那么等于执行 composedBC(action) 等于执行function B(action){...}
> 
> 在函数 B 中执行 next(action), 此时 B 中 next 为 composedC，那么等于执行 composedC(action) 等于执行function C(action){...}
> 
> 在函数 C 中执行 next(action), 此时 C 中 next 为 store.dispatch 即 store 原生的 dispatch, 等于执行store.dispatch(action)
> 
> store.dispatch 会执行 reducer 生成最新的 store 数据
> 
> 所有的 next 执行完过后开始回溯
> 
> 执行函数 C 中 next 后的代码
> 
> 执行函数 B 中 next 后的代码
> 
> 执行函数 A 中 next 后的代码
> 
> 
> 整个执行 action 的过程为 A -> B -> C -> dispatch -> C -> B -> A
> 




