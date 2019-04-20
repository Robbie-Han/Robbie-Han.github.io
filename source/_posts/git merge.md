---
title: async函数
tags: 
- Git
---
# git merge 的几种形式
> 转载[连接](https://liuliqiang.info/post/difference-between-merge-squash-and-rebase)
<div class="post-content">
<p>这几天我就遇到了一个问题，其实也不是遇到问题，而是遇到了疑惑，那就是我在 github 系统中 merge 同时的 PR 的时候发现有好几个选项，但是，却说不清楚这几个选项分别代表什么含义，所以就稍微花了点时间了解了下，顺带做个总结。</p>
<h3 id="toc-0">merge 的几种形式</h3>
<p>在 merge pr 的时候，默认是有三种选项的，分别是</p>
<ul>
<li>普通的 merge</li>
<li>rebase merge</li>
<li>squash merge</li>
</ul>
<p>这其实对应于我们在合并分支的时候的几种方式，所以我就以本地分支的形式来说说有啥区别。</p>
<h3 id="toc-1">一个简单的模型</h3>
<p>假设我们一开始的 master 分支上已经有了几个提交，就像这样：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101468869266.jpg" alt=""></p>
<p>然后，我们切出一条开发的分支，进行了一些 Feature 的开发，然后我们的分支可能就是这种情况：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101478786848.jpg" alt=""></p>
<p>这种情况还好，也比较常遇到，但是，现在问题来了，如果在这个时候 master 有了一些新提交（可能是其他分支合并进来的），那么这个时候情形就成了这样：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101478014577.jpg" alt=""></p>
<p>这个情况很有趣，但是我们不讨论，因为这和我们今天的主题无关，以后可以另外开一个话题来说，今天要说的是第二个情况。</p>
<h3 id="toc-2">普通 Merge</h3>
<p>说到合并分支，可能我们最熟悉的操作是这样的：</p>
<ul>
<li>先切换到目标分支（master）</li>
<li>执行命令：<code>git merge devel</code></li>
<li>删除旧分支（可以在上面一同做）：<code>git branch -D devel</code></li>
<!--more-->
<li>提交到远程分支：<code>git push origin master</code></li>
</ul>
<p>好像这样没啥问题的样子，但是这样操作之后，你知道结果是怎么样吗？假设合并之前的这样的：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101478786848.jpg" alt="15101478786848"></p>
<p>我们这么一番操作之后，那么最后我们的分支的历史将会是这样的：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101481294797.jpg" alt=""></p>
<p>是的，看上去很不错，也是一条直直的 commit line，我们在 devel 分支中的 commit 也是一个不差得保留在了 master 中。但是，很多时候，我们并不需要那么多的 commit，假设你给一个开源项目提交一个 Bug Fixes，然后一个简单的修改因为你的粗心大意 pr 了十几个 commit 过去，如果作者给你 merge 了，这就在这个项目的历史长河中增加了十几个 commit 啊，以后的人看 commit history 估计都崩溃了吧；同时，对于你自己管理的项目来说，当你 merge 之后发现有问题，想回滚都蛋疼！</p>
<h3 id="toc-3">squash merge</h3>
<p>在使用 git 的过程中，可能你遇到过想要合并多个 commit 为一个，然后很多人会告诉你用 <code>git commit --amend</code>，然后你发现里面有你的多个 commit 历史，你可以通过 pick 选择，squash 合并等等。同样得，merge 的时候也可以这么干，你只需要这么简单的两步：</p>
<ul>
<li>切换到目标分支：<code>git checkout master</code></li>
<li>以 squash 的形式 merge：<code>git merge --squash devel</code></li>
</ul>
<p>你会发现，在 master 分支上居然有未提交的修改，然后你就需要在 master 上主动提交了修改，注意，这里是你 commit 的，也就是改变了 commit 的 author。结果是这样的：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101488495274.jpg" alt=""></p>
<p>这里好了，比前面普通的 merge 来说，我们只有一个 commit 了，不管在分支中 commit 了多少，这里都只有一个！</p>
<h3 id="toc-4">rebase merge</h3>
<p>但是，作为处女座的程序员肯定是不能忍受目前的情况的，因为我们既想合并 commits，又想保留作者的信息，那么有没有什么好办法呢？肯定是有的啦，这个时候我们可以尝试一下 rebase，操作步骤是这样的：</p>
<ul>
<li><strong>先切换到 devel 分支</strong>（不一样咯）：<code>git checkout devel</code></li>
<li>变基：<code>git rebase -i master</code></li>
<li>切换回目标分支：<code>git checkout master</code></li>
<li>合并: <code>git merge devel</code></li>
</ul>
<p>这里完成了第二步之后我想你应该大概知道发生了什么事了，我们在 devel 里面对照 master 进行了变基，所谓的变基其实就是找到两个分支共同的祖先，然后在当前分支上合并从共同祖先到现在的所有 commit，所以我们在第二步的时候会选择怎么处理这些 commit，然后我们就得到了一个从公共commit 到现在的单个 commit，这个时候别人讲我们这个 commit 合并到 master 也只会在 master 上留下一个 commit 记录，就像这样：</p>
<p><img src="http://images.liuliqiang.info/2017-11-08-15101517152753.jpg" alt=""></p>
<p>虽然这个 commit history 线看上去很不错，而且也比较符合实际情况，但是我们需要注意到的有点就是分支上的开发者需要自己执行变基操作，从而导致他的原始 commit history 变化了（可以理解成被合并了）。</p>
<h3 id="toc-5">对比</h3>
<p>相比一下前面三种方式，我们可以总结出一些东西：</p>
<ol>
<li>rebase 可以尽可能保持 master 分支干净整洁，并且易于识别 author</li>
<li>squash 也可以保持 master 分支干净，但是 master 中 author 都是 maintainer，而不是原 owner</li>
<li>merge 不能保持 master 分支干净，但是保持了所有的 commit history，大多数情况下都是不好的，个别情况挺好</li>
</ol>
<p>所以，相比这么多，我是推荐使用 rebase 的，但是，当你在使用过程中，你会发现它的要求有点高，[/手动哭脸]</p>
<h3 id="toc-6">Reference</h3>
<ol>
<li><a href="https://book.douban.com/subject/3420144/">Pro Git</a></li>
<li><a href="https://stackoverflow.com/questions/2427238/in-git-what-is-the-difference-between-merge-squash-and-rebase">In git, what is the difference between merge --squash and rebase?</a> </li>
</ol>