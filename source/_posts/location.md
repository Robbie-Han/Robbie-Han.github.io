---
title: window.location
tags:  
- location
toc: true
---
## location
### location.href
  - location.href对应的是整个URL。
```js
https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/origin
```
### location.origin
  - 从协议名到pathname之间的部分,如果有协议包含协议名。
```js
var result = window.location.origin; // Returns:'https://developer.mozilla.org'
```
### location.host
返回主机名和端口号
```js
location.href = "https://developer.mozilla.org:443/en-US/HTMLHyperlinkElementUtils.host"
location.host == "developer.mozilla.org:443"
```
### location.hostname（主机名）
返回主机名
```js
location.href = "https://developer.mozilla.org:443/en-US/HTMLHyperlinkElementUtils.host"
location.host == "developer.mozilla.org"
```
### location.pathname
返回路径名
```js
location.href = "https://developer.mozilla.org:443/en-US/HTMLHyperlinkElementUtils.host"
location.pathname == "en-US/HTMLHyperlinkElementUtils.host"
```
当遇到？#字符时会截止
```js
https://www.google.com/search?q=window.location&oq=window.lo&aqs=chrome.2.69i57j0l5.9017j0j0&sourceid=chrome&ie=UTF-8
location.pathname === 'search'
```
### location.search
返回？及后面的url字段
```js
https://www.google.com/search?q=window.location&oq=window.lo&aqs=chrome.2.69i57j0l5.9017j0j0&sourceid=chrome&ie=UTF-8
location.search === "?q=window.location&oq=window.lo&aqs=chrome.2.69i57j0l5.9017j0j0&sourceid=chrome&ie=UTF-8"
```
### location.hash
返回#后字段
```js
https://dev.cn-northwest-1.test.bwtsi.cn/#/Tradeshift.Proforma/1ede5898-a031-49bc-9334-71c454759efa?from=ProformaManagerAP%2FsourceDocuments
location.hash == `#/Tradeshift.Proforma/1ede5898-a031-49bc-9334-71c454759efa?from=ProformaManagerAP%2FsourceDocuments`
```
## location.search和location.hash的坑
理想状态下我们可以直接拿到类似于`?/a=b&b=c`和`#comment`这样的字段，但是这里是有坑的

eg:
```js
// http://career.cloud.cmbchina.com/index.html#jobList?id=96574F8D-C7ED-4772-AE7C-BAC896D190C1
location.search = ''
location.hash = '#jobList?id=96574F8D-C7ED-4772-AE7C-BAC896D190C1'
```
其实这个现象会存在于使用hashRooter的react项目中。所以如果路由用的hashRooter，来取search参数是需要手动用代码取的。
如果你以为取search的时候，只要使用location.search，那就掉坑里了。具体怎么操作可能还需要观察一下接口定义，目前并没有想到一劳永逸的算法。当然如果项目不用hash路由的话，那就使用location.search。



