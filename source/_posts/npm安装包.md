---
title: 如何使用npm下载特定版本的包
tags: 
- Node
---
##如何使用npm下载特定版本的包：

npm install parseString@<version>

批量安装包：当需要安装多个包时，可以在package.json的dependencies中添加相应的包名和版本号，使用npm install安装所有的包。

```
{
    "name": "node-echo",
    "main": "./lib/echo.js",
    "dependencies": {
        "argv": "0.0.2"
    }
}
```
npm update 包名 ；可以把对应的包更新到最新的版本。


