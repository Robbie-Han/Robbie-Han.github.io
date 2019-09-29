---
title: Reducer的整合者combineReducers
tags: 
- React
- Redux
- toc: true
---

### 前言
在公司的项目中我们可以发现我们代码中的reducer并不是都写在一个reducer.js中，而是被划分了代表特殊功能的小的reducer。然后在同级目录会创建一个index.js,里面引入了所有的reducer,并通过combineReducers整合在一起。例如：`combineReducers({lines: lines,document: document})`;我们的state对象里面也会做同样的划分`state = {lines: {}, document: {}};`。

### combineReducers
前言中我们提到，系统会将state和更新state的reducer进行划分，每个可以表示特定功能的数据。然后通过combineReducers将它们组合在一起。此处我们就举例说明一下combineReducers怎么使用

#### 举例说明
```js
// reducers.js
export default (theDefaultReducer = (state = {a: 1}, action) => state)

export const firstNamedReducer = (state = {b: 2}, action) => state

export const secondNamedReducer = (state = {c:3}, action) => state
```
<!--more-->
```js
// rootReducer.js
import { combineReducers, createStore } from 'redux' //从redux中引入combineReducers方法

import theDefaultReducer, {
  firstNamedReducer,
  secondNamedReducer
} from './reducers'  // 引入各个reducers.js

// 整合所有reducer
const rootReducer = combineReducers({
  default: theDefaultReducer,
  first: firstNamedReducer,
  second: secondNamedReducer
})
// combineReducers 返回的结果传给createStore
const store = createStore(rootReducer)
console.log(store.getState())

//state：{default: {a: 1}, first: {b: 2}, second: {c:3}}

```
由例子可知，此时的reducer实际上combineReducers的返回值。combineReducers通过整合所有reducer。然后返回的结果rootReducer传给createStore生成store。

此处的createStore函数我们没有initialState和enhancer参数。enhancer代表的是applyMiddleWares(middlewares),此处不讨论中间件，所以省略。那么initialState的参数呢？initialState的参数其实在项目中可以省去的。只要在reducer函数的参数上 `function reducer(state = initialState, action){return state}`将同文件的initialState传给state当默认值就行。此时当creatStore函数执行时，内部会有一次的dispatch初始action，此时会将
initialState传给currentState；此时在外层执行store.getState()会返回系统的状态树。

简写版creatStore.js
```js
export default function createStore(reducer, preloadedState, enhancer) {
  var currentState = preloadedState;//得到初始init，没有传递则为undefined;
  var currentReducer = reducer;
  function getState() {
    return currentState
  }
  function dispatch(action) {
    //执行传入的reducer函数，该函数返回一个新的state对象，并赋值给currentState变量
    currentState = currentReducer(currentState, action)
  }
  dispatch({ type: ActionTypes.INIT }) //执行dispatch函数，初始化state
}
```
## combineReducers源码
在讨论combineReducers源码的时候我们首先要明确这个函数的输入和期望的输出。首先输入是一个对象，对象的属性key对应的是一个function类型的子reducer。输出是一个整合过的rootReducer,既然是reducer那它的函数参数就是(state, action),返回的是state。这个state是整个app整合过的store;

```js
export default function combineReducers(reducers) {
  // 取得对象的key，组成数组
  const reducerKeys = Object.keys(reducers)
  const finalReducers = {}
// 遍历对象，将reducers中value为函数的值存在finalReducers对象中
  for (let i = 0; i < reducerKeys.length; i++) {
    const key = reducerKeys[i]
    if (typeof reducers[key] === 'function') {
      finalReducers[key] = reducers[key]
    }
  }

  const finalReducerKeys = Object.keys(finalReducers)
  // 返回的是一个reducer。函数是一个闭包，保存对finalReducers的引用，所以将返回值传给createStore后依旧可以调到被切分的reducer和state。
  return function combination(state = {}, action) {
    // 设置标记state是否更新
    let hasChanged = false
    // 保存返回的新的state;
    const nextState = {}
    // 遍历每个被切分的reducer，如果找到对应的actionType就返回新state并把haschange改为true。没有与之对应的返回传入的state,state不变。
    for (let i = 0; i < finalReducerKeys.length; i++) {
      const key = finalReducerKeys[i]
      const reducer = finalReducers[key]
      const previousStateForKey = state[key]
      const nextStateForKey = reducer(previousStateForKey, action)
      nextState[key] = nextStateForKey
      hasChanged = hasChanged || nextStateForKey !== previousStateForKey
    }
    // 通过hasChange判断状态是否修改
    return hasChanged ? nextState : state
  }
}
```
此处的state初始默认为空，当createStore函数执行的时候会出发初始化action，通过遍历每个reducer生成初始的State。

参考链接一：https://github.com/Aaaaash/blog/issues/2
参考链接二：https://segmentfault.com/a/1190000009479302
源码： https://github.com/reduxjs/redux/blob/ab5cafdd50ee740261032cef94935c1f99354173/src/combineReducers.js

