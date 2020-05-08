---
title: 安装nvm管理多node版本
tags: 
- Node
toc: true
---
### 1、安装nvm

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

如果Mac使用的zsh，需要将命令中的| bash改为 | zsh
```
###### *note：[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)安装可以替换mac的bash,安装后可以安装一个喜欢的主题，界面将非常美观。*

然后在控制台 cd ~/.nvm，观察nvm是否安装完成。
<!--more-->
安装完成后可以查看自己的配置文件，是否会添加新的配置项


```
vim ~/.bash_profile
或
vim ~/.zshrc
```
新增配置项

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
控制台输入下面的语句刷新配置：

```
source ~/.bash_profile 或 source ~/.zshrc
```
### 2、安装npm 
例如安装node版本为8.xx.xx

```
nvm install 8
nvm install 10
```
系统会默认安装8或10的最新版本，如果需要特定版本，可以补全次版本号和修订号。

[node版本号讲解链接](https://github.com/Robbie-Han/Robbie-Han.github.io/blob/master/node/node%E7%89%88%E6%9C%AC%E5%8F%B7.md)

### 3、为不同的本地仓库配置不同的npm版本
切换到仓库的的根目录：

仓库1:
```
echo 8 > .nvmrc

```
仓库2:
```
echo 10 > .nvmrc

```
查看是否配置完成：
```
vim .nvmrc
```
这样不用每次切换仓库都使用 nvm use *nodeNumber*

参考链接1：https://github.com/creationix/nvm

参考链接2: https://cloud.tencent.com/developer/article/1057493



