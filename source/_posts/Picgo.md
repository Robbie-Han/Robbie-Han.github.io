---
title: VSCode-PicGo插件
tags: 
- 开发工具
- PicGo
- Markdown
---

## picGo插件
  使用VSCode编写MarkDown文档的时候，插入图片一般比较困难，现在使用VSCode的picGo的插件可以解决这个问题。
### 使用gitHub图床
 1、新建一个gitHub仓库，命名随意：
 2、进入settings -> Develop settings -> personal access tokens
 -> generate new token -> 输入仓库名勾选repo -> 生成tokens
 ![20190612122116.png](https://raw.githubusercontent.com/Robbie-Han/picMap/master/img/20190612122116.png)
3、进入VSCode的设置页面，填入如下信息：
![20190612122350.png](https://raw.githubusercontent.com/Robbie-Han/picMap/master/img/20190612122350.png)

4、重新启动VSCode，新建.md文件
截图后使用快捷键 cmd+opt+u,图片会自动上传到gitHub并生成MarkDown图片链接。

生成的链接：
![20190612123205.png](https://raw.githubusercontent.com/Robbie-Han/picMap/master/img/20190612123205.png)

gitHub仓库：
![20190612123139.png](https://raw.githubusercontent.com/Robbie-Han/picMap/master/img/20190612123139.png)


[参考链接](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github%E5%9B%BE%E5%BA%8A)
