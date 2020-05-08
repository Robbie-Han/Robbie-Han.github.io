---
title: query-string中parse的源码实现
tags: 
- JS
toc: true
---
## 前言
query-string模块在做地址解析查询参数时，会经常用到，在项目中自己曾经通过对`location.search`做过查询参数和值的解析，但是代码写出来还是很长的，而且当别的同事看你的代码时，很可能不知道你写的是什么，所以在此处我们完全可以使用query-string来辅助我们开发。

我曾经在这篇[博客](https://robbie-han.github.io/2018/12/20/queryString%E6%A8%A1%E5%9D%97/)里写到过具体用法，此处不再赘述，网上教程也很多，简单易懂。我们的重心是queryString.parse(str)功能的实现，下面的代码是仿照源码所写，实现了queryString.parse(str)的功能。

## 源码实现
```js
function splitFirst(item, flag) {
 // 定位首次出现的 '=',避免value中有等号
  const index = item.indexOf(flag);
  let key, value;
// 如果没有等号，则是'name = null' 的简写'name'
  if(index === -1) {
    key = item;
    value = null;
  } else {
    key = item.slice(0, index);
    value = item.slice(index + 1);
  }
  return [key, value];
}

function parse(str) {
  // 创建一个没有原型的空对象
  let result = Object.create(null);
  // 判断str为空或不是字符串时，返回{}
  if(!str || typeof str !== 'string') return result;
  // 如果传入的字符串第一个字符是#||&||?，替换为‘’
  const newStr = str.trim().replace(/^[#&?]/, '');
  // 对字符串拆分为数组
  const input = newStr.split('&');
  //遍历数组
  for(let item of input) {
    //取出每一项'name=100'中的key和value
    let [key, value] = splitFirst(item, '=');
    // 判断对象中有没有该key,没有的化直接加入，
    if(!result[key]) {
      result[key] = value;
    }else {
      // 对象中已存在该key,有value是string和数组两种情况
      // name = 'han',name = [han,li]
      if(typeof result[key] === 'string') {
        const t = result[key];
        result[key] = [t, value];
      }else {
        result[key].push(value)
      }
    }
  }
  return result
}
parse('name=han&name=li&age=10')

```