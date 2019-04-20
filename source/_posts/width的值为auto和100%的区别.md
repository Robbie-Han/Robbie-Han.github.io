---
title: 关于width
tags: 
- CSS
---
### **width:auto**

---
- [ ] 父元素的content = 子元素（content + padding + border + margin )
- [ ] 子元素（包括content+padding+border+margin）撑满整个父元素的content区域。

- [ ] 子元素有margin、border、padding时，会减去自身content区域相对应的width值
- 此时的自元素有点像IE盒模型，宽高的值就是父元素的宽高。
---
### **width:100%**

---

- [ ] 父元素的content = 子元素的content
- [ ] 强制将子元素的content区域 撑满 父元素的content区域
- [ ] 子元素有margin、border、padding时，不改变子元素content区域的width，而是溢出父盒子，保持原有值

- 此时的自元素有点像盒模型。
---
贴段代码做参考：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style type="text/css">
        * {
            margin: 0;padding: 0;
        }
        body {
            background: #dcdcdc;
        }
        .box {
            width: 400px;
            border: 3px solid red;
            padding: 0 50px;
        }
        .box1 {
            width: auto;
            height: 100px;
            background: pink;
            padding: 0 50px;
            margin: 0 50px;
            border-width: 0 50px;
            border-style: solid;
            border-color: green;
        }
        .box2 {
            width: 100%;
            height: 100px;
            background: gold;
            padding: 0 50px;
            margin: 0 50px;
            border-width: 0 50px;
            border-style: solid;
            border-color: green;
        }
    </style>
</head>
<body>
<div class="box">
    <div class="box1"></div>
    <div class="box2"></div>
</div>
</body>
</html>

```



