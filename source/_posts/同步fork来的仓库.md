---
title: 如何同步自己fork来的仓库
tags: 
- Git
---
如何同步自己fork来的仓库
===
### 一、fork来的仓库的痛点：

我们在进行Github协同开发的时候，往往会去fork一个仓库到自己的Github中，过一段时间以后，原仓库可能会有各种提交以及修改，很可惜，Github本身并没有自动进行同步的机制，这个需要我们手动去执行，现在我来演示一下如何进行自己的仓库和原仓库进行Gith同步的操作。
<!--more-->

### 二、源仓库同步步骤：
1. 进入项目目录，执行如下命令：查看你的远程仓库的路径。
```
git remote -v
```
result:
```
origin	git@github.com:USTC-Han/v4-debug-helper.git (fetch)
origin	git@github.com:USTC-Han/v4-debug-helper.git (push)
```
2.配置原仓库的路径：
```
git remote add upstream 原仓库SSH
```
3.再次查看远程目录的位置：
```
git remote -v
```
result:
```
origin	git@github.com:USTC-Han/v4-debug-helper.git (fetch)
origin	git@github.com:USTC-Han/v4-debug-helper.git (push)
upstream  git@github.com:TradeshiftCN/v4-debug-helper.git (fetch)
upstream  git@github.com:TradeshiftCN/v4-debug-helper.git (push)
```
4.抓取原仓库的修改文件：
```
git fetch upstream
```
5.在本地master 合并远程的master分支：
```
git merge upstream/master
```
6.推到远端仓库
```
git push origin
```
<font color = red>注意事项：</font>
     
    当自己的分支merge远端的分支可能会生成一条merge信息，
    而这条信息可能会影响下次向源仓库提PR，
    可以用 git rebase upstream/master 代替merge
### 三、fork和clone的区别：
`fork是生成一份同样的代码到自己的gitHub仓库，然后再将自己的仓库的代码clone到本地，修改后推到自己的仓库，然后提PR到源仓库。这么做的主要原因是自己不是原仓库的授权的贡献者，如果直接push到原仓库会报错。`

`git clone 拷贝远端仓库代码到本地，修改后可以直接推到远端`

### 四、fetch和pull的区别：
`fetch + merge 的功能与pull的功能等同，当确定拉下来的代码不会有什么问题，直接git pull`

git fetch的样例：
```
git fetch origin master:tmp
git diff tmp 
git merge tmp
```
