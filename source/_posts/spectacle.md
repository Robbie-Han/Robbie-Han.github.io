spectacle 踩坑总结
===
  spectacle 是一款免费的窗口调节工具，对比可以在Mac 中下载收费的`Magent`
### 一、Download:
   点击找到仓库：[spectacle](https://github.com/eczarny/spectacle)

下载到本地: ` git@github.com:eczarny/spectacle.git`

### 二、Build:
* 安装 **carthage** ：`brew install carthage`

* 运行：`carthage bootstrap --platform Mac`

  * 此时可能会报错：

    >`xcrun: error: unable to find utility "xcodebuild", not a developer tool or in PATH`

  * 解决方法：[点击跳转](https://www.jianshu.com/p/4baf84ef2e76)
* 运行：` open Spectacle.xcodeproj`
  * 此时可能会报错：

    >`Command PhaseScriptExecution failed with a nonzero exit code
`

  * 解决方法：[点击跳转](https://juejin.im/post/5ba35cc05188255c7c655a8c)

### 三、Run:
  在xcode中: `command+R`

### 四、build后的大坑：
[点击跳转可以直接下载](https://spectacleapp.com/)
:sob::sob::sob::sob::sob:






