---
title: 关于align-items:center和align-content:center的思考
tags: 
- CSS
- flex
- align-items
- align-content
toc: true
---

## 前言
flex布局中可以通过flex-direction来设置主轴和交叉轴，其中align-items则是用来操作在交叉轴方向的布局方式的。关于flex的基础讲解推荐这篇[文章](https://www.cnblogs.com/qcloud1001/p/9848619.html)。

## align-items
align-items定义了元素在交叉轴上的对齐方式。

单行的center情况不用细说，多行的时候使用align-items的表现会是怎么样呢？

![20190825165139.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190825165139.png)

当align-items设置多行元素center的时候，有点类似于space-around的感觉。每两个块中间的高度是外侧高度的两倍。每行元素的中线在自己所分空间的交叉轴方向居中。

## align-content
对于align-content，它会吧所有元素看成一个整体，在交叉轴居中。
![20190825165710.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190825165710.png)

---
代码演示链接：https://codepen.io/ustc-han/pen/bGbBYOa?editors=1100
