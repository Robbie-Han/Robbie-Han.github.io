---
title: webSocket 和 webWorker
tags: 
- Web
- H5
- webSocket
- web Worker
toc: true
---
## WebSocket
  WebSocket是html5中提出的一个新的应用层通信协议，位于OSI模型的应用层，建立在TCP链接上。

  HTTP存在缺陷，请求只能客户端发起。如果要实时的更新的服务器的状态变化需要使用Ajax轮询，轮询的效率比较低，浪费资源。

  WebSocket最大的特点是服务器可以主动向客户端推送消息，客户端也可以向服务端推送消息，实现了全双工通信。可以将WebSocket看成HTTP协议的补充，
  在之前HTTP协议中使用Keep-alice connection是在一次TCP链接中可以传输多次HTTP请求，但是依旧采用轮询的方式。WebSocket 解决的第一个问题是，
  通过第一个 HTTP request 建立了 TCP 连接之后，之后的交换数据都不需要再发 HTTP request了。

## Web Worker

js采用的是单线程模式，也就是说所有任务只能在同一个线程上运行，随着多核CPU的普及，单线程无法充分发挥计算机的计算能力。

Web Worker的作用，就是为 JavaScript 创造多线程环境，允许主线程创建 Worker 线程，将一些任务分配给后者运行。在主线程运行的同时，Worker 线程在后台运行，两者互不干扰。等到 Worker 线程完成计算任务，再把结果返回给主线程。这样的好处是，一些计算密集型或高延迟的任务，被 Worker 线程负担了，主线程（通常负责 UI 交互）就会很流畅，不会被阻塞或拖慢。

Worker 线程一旦新建成功，就会始终运行，不会被主线程上的活动（比如用户点击按钮、提交表单）打断。这样有利于随时响应主线程的通信。但是，这也造成了 Worker 比较耗费资源，不应该过度使用，而且一旦使用完毕，就应该关闭。

Web worker的几个重要的特点：
1、传给worker中的脚本需要与主线程的脚本文件同源。
2、Worker 线程与主线程不在同一个上下文中，不能执行Dom操作，如果需要可以通过消息传递将数据传递给主线程。
3、worker线程无法运行本地文件，只能执行线上文件。

常用API：
主线程：
- 创建worker:
    var worker = new Worker('js脚本')；
- 消息传递：
    worker.postMessage()：向 Worker 线程发送消息。
    worker.onmessage：message 事件的监听函数，发送过来的数据在event.data属性中
- worker错误监听：
    worker.onerror：worker内部运行出错的时候，调用主线程onerror
- 终止worker：
    worker.terminate()：立即终止 Worker 线程。

worker：
- 消息传递：
    postMessage()：向 Worker 线程发送消息。
    onmessage：message 事件的监听函数，发送过来的数据在event.data属性中
- 加载脚本：
    importScripts()
- 关闭worker: 
    close()：关闭 Worker 线程



[参考链接1](http://www.ruanyifeng.com/blog/2017/05/websocket.html)

[参考链接2](https://blog.csdn.net/lldouble/article/details/80742082)

[参考链接3](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)

[参考链接4](https://www.zhihu.com/question/20215561/answer/40250050)
