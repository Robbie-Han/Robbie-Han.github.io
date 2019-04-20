### max-height，min-height，height一起使用时，优先级问题

---
**常规操作：**

max-height 这个属性会阻止 height 属性的设置值变得比 max-height 更大。

max-height 属性用来设置给定元素的最大高度.如果height 属性设置的高度比该属性设置的高度还大,则height 属性会失效,max-height 重载（覆盖掉） height.

同理min-height同时也是限定height的值小于min-height的值，当他小于min-height的时候，则取min-height.

max-height(顶) > height  >min-height(保底)

**非常规操作：**

如果min-height的值大于max-hight， 那么无论heightd的值大于min-height还是小于min-height的值都会取min-height的值.

但是我觉得正常人应该不会把min-height的值设的比max-height的值吧，哈哈。

---
> 参考链接：
http://www.cnblogs.com/websmile/p/9506878.html
