---
title: mouseenter和mouseove的区别
tags:  
- Web
- mouseenter
- mouseover
toc: true
---

## 前言：
在做`input`组件的时候，需要有一个鼠标悬浮后，出现一个小图标，点击小图标清楚文字的事件。如下图：

![20191012200452.png](https://robbie-blog.oss-cn-shanghai.aliyuncs.com/img/20191012200452.png)

此时如果使用`mouseover`和`mouseout`事件控制图标显示，发现如果鼠标移到icon边界，就会出现icon闪烁。这代表着`mouseleave`事件被触发，显示图标的变量变为`false`.
<!--more-->
## mouseenter和mouseove的区别

类似` mouseover`，它们两者之间的差别是 `mouseenter `不会冒泡，也就是说当指针从它的子层物理空间移到它的物理空间上时不会触发。对应的`mouseout`和`mouseleave`相同。这就导致了在icon的边界，`mouseover`和`mouseout`的频繁切换，表现出现icon闪烁。

此[链接](https://qianlongo.github.io/zepto-analysis/example/event/mouseEnter-mouseOver.html)直观的展示了两者的区别，可以点击查看。







