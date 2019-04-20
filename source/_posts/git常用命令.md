---
title: git常用命令
tags: 
- Git
---
### git常用操作

<!--more-->

```
新建文件： mkdir git-test 
初始化git:    git init
查看隐藏目录： ls -a 

版本回退：（git commit -m "xxx"）
git log  查看提交的文件日志
git reset --hard Head^ : 返回上次修改的部分，^^上上次提交的位置
git reset --hard 版本号前几位         返回到上次的某个版本
git reflog 当回到某个版本，又后悔了，想回到之前的那个版本 找到版本id 用上个语句返回
eg: git reset --hard HEAD@{1}

cat readme.txt 查看文本内容

撤销修改：
没有提交到暂存区：
git checkout -- readme.txt 撤销对文本的修改（本质是使用版本库中的内容覆盖到工作区）

提交到暂存区后撤销：（git add readme.txt）
将暂存区的修改撤销，重新放到工作区
git reset  HEAD readme.txt
git checkout -- reademe.txt 撤销修改

提交到版本库(git commit -m "hehh") 
参考版本回退

删除内容：
删除工作区文件 rm test.txt
删除后悔可以用 git checkout -- reademe.txt 从版本库恢复
删除版本库中
git  rm test.txt （彻底删除）

git commit -m "remove test.txt "

创建gitHub项目，建立连接
将本地从仓库和在gitHub上新建的库连接起来 new Repository -->获得SSH
git remote add origin git@github.com:USTC-Han/git-test.git
将本地仓库推到远程库git push -u origin master (首次)
以后向同一地方提交：git push origin master 

从远程仓库到本地：
git clone git@github.com:USTC-Han/git-test.git

分支：
查看分枝：git branch
创建分支：git branch  <name>
切换分支：git checkout <name>
创建并切换分支： git checkout -b <name>
合并某分支到当前的分支：git merge <name>
删除分支：git branch -d <name>

将其它分支上的commit 内容倒到另外分支上；
git cherry-pick 版本号
git push 

修改commit 描述：git commit --amend 

删除远端某个commit: git reset --hard <版本号>
// 注意使用 --hard 参数会抛弃当前工作区的修改
// 使用 --soft 参数的话会回退到之前的版本，但是保留当前工作区的修改，可以重新提交
git push origin <分支名>
报错后强推到远端
git push origin <分支名> --force

删除远端分支：
gb -r 查看远端分支
gb -r -d origin/分支名
git push origin :分支名
```
