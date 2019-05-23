---
title: background
tags: 
- CSS
toc: true
---

## background-color
盒子的背景色
## background-image:url();
元素的背景图片

默认平铺满整个盒子，如果X或Y方向铺到最后一个放不下，也会铺一部分。配合background-repeat使用
## background-repeat
平铺方向

background-repeat: repeat-x;横向平铺

background-repeat: repeat-y;纵向平铺

background-repeat: no-repeat;只显示单个不平铺
<!--more-->
## background-position
[MDN关于这部分的链接](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position)

使用这个属性，默认左上角是原点，向下y，向右x轴。

background-position: 25%，75%;代表据顶部75%的高度，据左侧25%的宽度

top, left, bottom, right 代表的是在盒子边缘的位置，如只写一个，另外一个值默认50%；

background-position:right top;代表位置在盒子的左上。

background-position:right;盒子右边缘中部。

## background-attachment
背景默认是随文档流滑动的。
background-attachment：fixed;固定到某个位置，不随文档滚动。
