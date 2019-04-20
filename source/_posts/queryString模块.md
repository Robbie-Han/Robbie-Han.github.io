---
title: queryString模块
tags: 
- Node
---
## queryString模块
### 1. 安装：
    npm install query-string;
### 2. 引入：
    import queryString from 'query-string';
### 3. 应用：
#### - parse方法：
queryString.parse()方法用于将一个查询字符串解析为 JavaScript对象。

```
var str = 'foo=bar&abc=xyz&abc=123';

queryString.parse(str)
// { foo: 'bar', abc: [ 'xyz', '123' ] }
```
queryString.parse()一共有四个参数，第一个是待解析字符串，**第二个参数默认**‘&’，**第三个参数默认使用**‘=’。

应用举例：*地址栏解析*
使用该方法会自动的去掉前面的？或者hash符号

*[JS](https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=js&oq=markdown&rsv_pq=ebf79fd80000d7e3&rsv_t=3dc6iuXLdZkFX9hdim9%2FvbE1mEIMj9TwDql89cx66DYUM1SuJSoSCRyBwes&rqlang=cn&rsv_enter=1&inputT=2192&rsv_sug3=22&rsv_sug1=18&rsv_sug7=101&rsv_sug2=0&rsv_sug4=3745)* 点击链接,在控制台输入*window.location.search*得到下面的内容

```
window.location.search
"?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=js&oq=markdown&rsv_pq=ebf79fd80000d7e3&rsv_t=3dc6iuXLdZkFX9hdim9%2FvbE1mEIMj9TwDql89cx66DYUM1SuJSoSCRyBwes&rqlang=cn&rsv_enter=1&inputT=2192&rsv_sug3=22&rsv_sug1=18&rsv_sug7=101&rsv_sug2=0&rsv_sug4=3745"
```
eg:
```
console.log(location.search);
//=> '?foo=bar&abc=xyz'
 
const parsed = queryString.parse(location.search);
console.log(parsed);
//=> {foo: 'bar',abc: 'xyz'}
 
console.log(location.hash);
//=> '#token=bada55cafe'
 
const parsedHash = queryString.parse(location.hash);
console.log(parsedHash);
//=> {token: 'bada55cafe'}
```

```
var str = 'name:Sophie;shape:fox;condition:new';
queryString.parse(str, ';', ':')

// {
//   name: 'Sophie',
//   shape: 'fox',
//   condition: 'new',
// }
```
这样做地址解析很方便

#### -Stringify方法
queryString.stringify()是parse方法的逆操作：
eg:

```
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' }) 
// returns 
'foo=bar&baz=qux&baz=quux&corge=' 
 
querystring.stringify({foo: 'bar', baz: 'qux'}, ';', ':') 
// returns 
'foo:bar;baz:qux'
```



