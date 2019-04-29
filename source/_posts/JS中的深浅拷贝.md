---
title: js中的深拷贝和浅拷贝
tags: 
- JS
- 深拷贝
toc: true
---
### 如何区分JS的拷贝是深拷贝还是浅拷贝
如果B复制了A，然后B的改变也会对A产生影响，则是浅拷贝。如果B的改变与A无关，则是深拷贝。
 
### 基本数据类型和引用数据类型
对于基本数据类型，变量的数据存放在栈中，数据复制后会开辟新的内存，两者互不影响。但是这不是深拷贝，深拷贝是针对引用类型来讲的。

对于引用类型，数据保存在堆中，栈内存中定义的变量对应的是对堆内存的引用地址。引用类型的赋值操作，只是对引用地址的拷贝。其中一个的改变必然会影响到另一个。

### 实现深拷贝的方法：

- 递归操作：

```
function deepClone(obj){
    let objClone = Array.isArray(obj) ? [] : {};
    if(obj && typeof obj === "object"){
        for(key in obj){
            if(obj.hasOwnProperty(key)){
                //判断ojb子元素是否为对象，如果是，递归复制
                if(obj[key]&&typeof obj[key] ==="object"){
                    objClone[key] = deepClone(obj[key]);
                }else{
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}    
```
<!--more-->

- 使用Json的stringyfy和pase方法：

```
function deepClone(obj){
    let _obj = JSON.stringify(obj),
        objClone = JSON.parse(_obj);
    return objClone
}    
let a=[0,1,[2,3],4],
    b=deepClone(a);
a[0]=1;
a[2][0]=1;
console.log(a,b);
//a
(4) [1, 1, Array(2), 4]
0: 1
1: 1
2: (2) [1, 3]
3: 4
length: 4
__proto__: Array(0)
//b
(4) [0, 1, Array(2), 4]
0: 0
1: 1
2: (2) [2, 3]
3: 4
length: 4
__proto__: Array(0)
```
- 使用Lodash的_.cloneDeep(value)

  [lodash官方文档](https://lodash.com/docs/4.17.11#cloneDeep)

### 关于slice()和contact()方法是不是深拷贝：
对于数组，如果数组不存在嵌套，那么这两个方法确实能不影响原数组，实现'深拷贝'，但如果存在嵌套就会失效，所以不是真正的深拷贝，真正的深拷贝无论元素有多少层都会深度拷贝。

eg:
~~~
let a=[0,1,[2,3],4];
const b=a.slice();
a[0]=1;
a[2][0]=1;

//a
(4) [1, 1, Array(2), 4]
0: 1
1: 1
2: (2) [1, 3]
3: 4
length: 4
__proto__: Array(0)

//b
(4) [0, 1, Array(2), 4]
0: 0
1: 1
2: (2) [1, 3]
3: 4
length: 4
__proto__: Array(0)

~~~




