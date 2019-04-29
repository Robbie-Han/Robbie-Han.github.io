---
title: ES5和ES6面向对象的写法
tags:  
- JS
- 继承
toc: true
---
# ES5和ES6面向对象的写法：

## ES5代码：


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
        Vipuser.prototype = new User();
        Vipuser.prototype.constructor = Vipuser;

        Vipuser.prototype.showLevel=function(){
                console.log(this.level);
        }

        var v1 = new Vipuser('hum',12,3);
        v1.showName();
        v1.showAge();
        v1.showLevel();
```
 <!--more-->
## ES6代码：      
==注意User后面没有括号==


```
class User{
        constructor(name,age){
            this.name = name;
            this.age = age;
        }
        showName(){
            console.log(this.name);
        }
        showAge(){
            console.log(this.age);
        }
     }

     class Vipuser extends User{
        constructor(name,age,level){
            super(name,age);
            this.level = level;
        }
        showLevel(){
            console.log(this.level);
        }
     }
var v1 = new Vipuser('han',10,2);
v1.showName();
v1.showAge();
v1.showLevel();
```
