---
title: React路由
tags: 
- React
- rooter
- 路由
---
# 待更新
## 前言
最近回顾了react路由的相关知识，然后看了history相关的源码来从本质上区分react中常用的两种路由hashRooter和browserRooter之间的区别，发现两者最大的区别有两点，一点是在事件监听上，另一点是在页面刷新上。源码的大致的功能看明白了，但是还有许多细节需要之后的时间去完善。下面做一下技术总结。

## React路由常用组件：
在 [React Rooter](https://reacttraining.com/react-router/web/api/Route)的官方文档里对React常用的路由组件例如：
`<Router>、<Roote>、<Switch>、<Redict>、<Link>`有详细的讲解，包括路由的匹配规则等都有详细的描述,此处不想过多的赘述它们的使用，只做简要的概括。

- Router：
   - 在公司项目里使用的包是'react-router-dom'而不是'react-rooter'，这是因为前者是基于后者的，在'react-rooter'的基础上加入了一些新的组件，例如`<Link> 、<HashRooter>、<browserRooter>`。[参考链接](https://github.com/mrdulin/blog/issues/42)
  - 在引入的时候可以直接`import { BrowserRouter as Rooter, Route, Link } from "react-router-dom";`也可以直接引入Rooter，然后再Rooter的history属性上绑定 hashRooter或browserRooter，不过这样比较麻烦，因为我们需要实例化history依赖中的createHashHistory或者createBrowserRooter方法。
- Route
  - 负责渲染具体的业务组件，负责匹配url和对应的组件
  - 有三种渲染的组件的方式：component(对应的组件)、render(值是匿名函数，函数里渲染组件)、children(不关心path的匹配，无论哪种路由都会渲染)
  - component属性值最好是组件，如果是匿名函数的话，由于route通过属性component的值使用React.createElement来构造组件，而函数是引用类型，每次都不是同一个函数，会导致每次渲染都要生成新的组件。
- Switch
  - 匹配到一个Route子组件就返回不再继续匹配其他组件。
- Link
  - Link是对a标签的封装，通过createHref函数将to里的字段和基础字段的拼接生成新的href。
  当点击Link组件的时候会阻止a的默认事件，并将href的值传入history.pushState()。
<!--more-->
## HarshRooter和BrowserRooter的区别：
HarshRooter和BrowserRooter分别是对Rooter组件的history属性为hashHistory和browserHistory的封装。HarshRooter和BrowserRooter的区别说到底是hashHistory和browserHistory的区别。而hashHistory使用的是createHashHistory方法，browserHistory使用的是createBrowserRooter。

公司项目使用的HashRooter,举个项目中的例子:

项目的URL：
`https://dev.cn-northwest-1.test.bwtsi.cn/#/Tradeshift.Proforma/2ede5898-a031-49bc-9334-71c454759efa?from=ProformaManagerAP%2FsourceDocuments`

```js
const history = createHashHistory();
const baseAppHash = _.chain(window.top.location.hash)
	.split(__app.id)
	.take(1)
	.concat(__app.id)
  .join('').value();
  
  // baseAppHash :'#/Tradeshift.Proforma'
  // pathName: '/2ede5898-a031-49bc-9334-71c454759efa'
  // search: "?from=ProformaManagerAP%2FsourceDocuments"
  // hash: ''

history.listen(location => {
	window.top.location.hash = [
		baseAppHash,
		location.pathname,
		location.search,
		location.hash
	].join('');
});

export const HashRouter = history;
```
从上面的例子可以看出，系统在使用`<Rooter history = {}>`这种形式来使用Rooter组件的时候，我们需要对属性值通过实例化createHashHistory()并通过实例中的listen来监听文档hash的变化。

### 源码上看区别
源码中的createHashHistory.js和createHashHistory.js中的history已经不是浏览器的history对象了，它在内部对history的一些方法做了封装，最后将history返回。

history的结构：
```js
 const history = {
    length: globalHistory.length,
    action: 'POP',
    location: initialLocation,
    createHref,
    push,
    replace,
    go,
    goBack,
    goForward,
    block,
    listen
  };
```
其中globalHistory就是浏览器history的对象。history中的go, goBack, goForward对应封装了原生的history.go、history.back()、history.forward()方法。

location的结构：
```js
history.location = {
  pathname: "/2ede5898-a031-49bc-9334-71c454759efa",
  search: "?from=ProformaManagerAP%2FsourceDocuments", 
  hash: "", 
  state: undefined
  }
```
从这个结构可以看出，history.location是浏览器location的封装，这个在HarshRooter和BrowserRooter中两者的定义没有区别。


