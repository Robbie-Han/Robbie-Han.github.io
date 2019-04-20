---
title: redux 基础
tags: 
- React
---
# redux笔记
[点击查看图解](https://images2017.cnblogs.com/blog/1097840/201708/1097840-20170802140748615-1446659032.png)
<p>action: 一个操作的定义，大概是这个样子, 本身是一个对象</p>

```
{
    type:'add',
    todo 
}
```
actionCreater: 一个函数，返回结果是一个action


```
function add (todo) {
        return {
            type: 'add',
            todo
        }
    }
```

reducer： 真正更新数据操作的函数，大概是这么个样子
==此处return状态不可以直接改，可以用解构，对象还可以Object.assign()==

```
// reducer
let todoReducer = function (state = todoList, action) {
    switch (action.type) {
        case 'add':
            return [...state, action.todo]
        case 'delete':
            return state.filter(todo => todo.id !== action.id)
        default:
            return state
    }
}
```

store： 只有一个,把action,state,reducer连接起来的对象。有如下方法

> dispatch：触发一个action
> 
> subscribe ： 订阅store
> 
> getState ：获得当前的state
> 
> replaceReducer ：更换reducer
 
/* 简单示例 */

```
let { createStore } = self.Redux
 
//默认state
let todoList = []
// reducer
let todoReducer = function (state = todoList, action) {
    switch (action.type) {
        case 'add':
            return [...state, action.todo]
        case 'delete':
            return state.filter(todo => todo.id !== action.id)
        default:
            return state
    }
}
 
//创建store
let store = createStore(todoReducer)
 
//订阅
function subscribe1Fn() {
    console.log(store.getState())
}
let sub = store.subscribe(subscribe1Fn)
 
store.dispatch({
    type: 'add',
    todo: {
        id: 1,
        content: '学习redux'
    }
})
 
store.dispatch({
    type: 'add',
    todo: {
        id: 2,
        content: '吃饭睡觉'
    }
})
 
store.dispatch({
    type: 'delete',
    id: 2
})
 
// 取消订阅
sub()
 
console.log('取消订阅后：')
store.dispatch({
    type: 'add',
    todo: {
        id: 3,
        content: '打游戏'
    }
})
```
[输出结果点击查看](https://images2017.cnblogs.com/blog/1097840/201708/1097840-20170802142828193-478843503.png)


