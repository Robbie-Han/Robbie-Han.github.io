---
title: node 版本号命名
tags: 
- Node
toc: true
---
## node 版本号命名：
### 版本号的命名：
根据国际主流的惯例，我们使用「语义化版本（Semantic Versioning）」的命名方式，有时简称 SemVer。

语义化版本号（以下简称「版本号」）的格式是：<major>.<minor>.<patch>。即使用三位非负整数，以点号 . 连接。

### 每一位的含义：
<major> 即**主版本号**，俗称大版本升级。改动到主版本号时，标志着 API 发生了巨大变化，包括但不限于新增特性、修改机制、删除功能， 一般不兼容上一个主版本号。

<minor> 即**次版本号**，俗称小版本升级。当我们进行常规的新增或修改功能时，改动次版本号，但是 必须是向前兼容的。这也意味着我们 不能直接删除某个功能。如若必要，我们可以在 changelog 中标记某项功能为「即将删除（Deprecated）」，然后在下一个大版本中将其彻底删除。

<patch> 即**修订号**，俗称 bug 修复。顾名思义，如果仅仅为了修复或调整一些小问题，我们就只改动修订号。
<!--more-->

### 注意事项：
版本号前不要加 v。

不要在数字前补 0。错误示例：01.12.03。

每一位版本号按照 +1 的速度递增，不要在版本号之间跳跃。

主版本号停留在 0 的版本号，即 0.x.x 应当视作还在内部开发阶段的代码。如果代码有公共 API，此时不宜对外公开。

1.0.0 的版本号用于界定公共 API 的形成。

当次版本号递增时，修订号归零；当主版本号递增时，次版本号、修订号归零。

进行新的开发时，版本号从 0.1.0 开始。

如果不小心把一个不兼容的改版当成了次版本号发行，应当发行一个新的次版本号来更正这个问题并且恢复向下兼容。注意 不能去修改已发行的版本。

### 快速修复版本的方法：
递增一个修订号：
npm version path

递增一个次版本号:
npm version minor

递增一个主版本号:
npm version major

### npm 依赖包版本号~和^的区别:
~和^这种标记法标记的是「版本号范围（version range）」

前者会匹配最近的小版本依赖包，比如~1.2.3会匹配所有1.2.x版本，但是不包括1.3.0
 
后者会匹配最新的大版本依赖包，比如^1.2.3会匹配所有1.x.x的包，包括1.3.0，但是不包括2.0.0


---
[点击参考链接](http://taobaofed.org/blog/2016/08/05/instructions-of-semver/)

[node release](https://nodejs.org/zh-cn/download/releases/)
