---
title: Object.create()和new Object()的区别
tags:  
- JS
- Object.create()
- new Object()
toc: true
---
# 1.Object.create()
Object.create()方法创建一个`新对象`，使用现有的对象来提供新创建的对象的__proto__。
## 1.1 语法
 ```
 Object.create(proto, [propertiesObject])
 ```
`proto`: 新创建的对象的原型对象

` [propertiesObject]`: 默认是undefined,当为对象的时候，将对象添加到原型上。
<!--more-->
## 1.2 Object.create() 和 new Object()
Object.create()是将它里面的参数添加到对象的原型上，而不是添加到对象本身。
```
const person = {
  isHuman: false,
  printIntroduction: function () {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = Object.create(person);

me.name = "Matthew"; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // inherited properties can be overwritten

me.printIntroduction();·
// expected output: "My name is Matthew. Am I human? true"

```
![20190708102318.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190708102318.png)

由上图可以看出 Object.create()是将它里面的参数添加到对象的原型上，而不是添加到对象本身。

使用Object.create()创建的对象会把person的内容添加到me的原型上，而不是添加到me的构造函数上。
```
const person = {
  isHuman: false,
  printIntroduction: function () {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = new Object(person);
```
![20190708103210.png](https://raw.githubusercontent.com/USTC-Han/picMap/master/img/20190708103210.png)
此时person中的内容将加到me的构造函数中。
## 1.3 {} 和 new Object() 和 Object.create(Object.prototype)
```
var newObj = {}
newObj.__proto__ === new Object().__proto__ ===  Object.create(Object.prototype).__proto__
```
## 1.4 Object.create()在继承中的使用
```
function User(name,age){
    this.name = name;
    this.age = age;        
}

User.prototype.showName=function(){
    console.log(this.name);
}
User.prototype.showAge=function(){
    console.log(this.age);
}

function Vipuser(name,age,level){
    User.call(this,name,age);
    this.level = level;
}
Vipuser.prototype = Object.create(User.prototype);
Vipuser.prototype.constructor = Vipuser;

Vipuser.prototype.showLevel=function(){
    console.log(this.level);
}

var v1 = new Vipuser('hum',12,3);
v1.showName();
v1.showAge();
v1.showLevel();
```
```Vipuser.prototype = Object.create(User.prototype);和 Vipuser.prototype = new User();```这两个的区别在于，前者的子集只会继承父集中原型中的属性和方法，而后者子集的原型中包含父集原型中的属性、方法以及`构造函数中的属性和方法`，可以复制到控制台查看。
