---
title: js中的深拷贝和浅拷贝
tags: 
- JS
- 深拷贝
toc: true
---
### 如何区分JS的拷贝是深拷贝还是浅拷贝
>浅拷贝:只对其第一层基础类型的属性进行复制开辟新空间，引用类型只存地址，指向同一块空间
深拷贝:则递归复制了所有层级，全部开辟新的空间，不会影响先前的对象
 
### 基本数据类型和引用数据类型
对于基本数据类型，变量的数据存放在栈中，数据复制后会开辟新的内存，两者互不影响。但是这不是深拷贝，深拷贝是针对引用类型来讲的。

对于引用类型，数据保存在堆中，栈内存中定义的变量对应的是对堆内存的引用地址。引用类型的赋值操作，只是对引用地址的拷贝。其中一个的改变必然会影响到另一个。

### 实现浅拷贝的方法：
首先要明确，对引用类型采用直接赋值，不是浅拷贝
举个例子：
```
let x = {
    a: 1,
    b: { z: 0 }
};
let y = x
y === x   // true，代表它们指向同一块空间
y.a === x.a   // true
y.a = 2
x.a  // 2 x的值也发生的改变
y.b === x.b   // true，代表它们指向同一块空间
x.b.z = 100
y.b.z     // 100
```
上述例子中，x对y的赋值操作不属于浅拷贝，浅拷贝对于a属性中的非引用类型应该开辟新的存储空间，即对`y.a = 2`的操作不应该影响到原对象x.a的值。

![20190630101009.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190630101009.png)

#### 如何算浅拷贝？
```
function shallowCopy(src) {
  let dst = {};
  for (var prop in src) {
    if (src.hasOwnProperty(prop)) {
      dst[prop] = src[prop];
    }
  }
  return dst;
}
let obj = { a:1, arr: [2,3] };
let shallowObj = shallowCopy(obj);
```
此时对于属性值是基本数据类型的会开辟新的内存空间，互不影响。对于引用类型的则是地址的拷贝。改变其中一个另一个也会改变。
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
[参考链接](https://github.com/muwenzi/Program-Blog/issues/62)



