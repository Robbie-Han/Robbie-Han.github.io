---
title: 模块调试技巧 - npm link
tags: 
- Node
- npm link
- create-react-app
---
## 前言
在本地开发npm包后，如何实现在本地调试修改后的npm包？频发的发布上线调试显然是不可靠的，npm link可以很好的解决问题。
## npm link
首先，在我们正在开发的模块的命令窗口使用`npm link`，我们会得到如下图的结果,此时就代表link成功
![20190902134410.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190902134410.png)

## create-react-app
[create-react-app](https://github.com/facebook/create-react-app)是一款React应用开发工具,我们可以在控制台通过`npx create-react-app my-app`来安装，然后`cd my-app`进入app，此时我们创建了一个很简单的react项目。

此时，我们在本项目中输入`npm link <packageName>`
![20190902135218.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190902135218.png)

> 注意： 如果本地安装了nvm，要保证npm link 和 npm link packageName 在同一个node版本中，不然会报错

此时就可以在项目中引入该包，然后测试包的功能是否正常。
![20190902135404.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190902135404.png)

测试完毕后，可以使用`npm unlink <npmPackage>`断开链接

相关知识链接：[npx](http://www.ruanyifeng.com/blog/2019/02/npx.html)、[create-react-app](https://github.com/facebook/create-react-app)

参考链接一：https://ui.muwenzi.com/apps/start/usage

参考链接二：https://github.com/atian25/blog/issues/17

参考链接三：https://juejin.im/post/5be0fe39518825171726d671