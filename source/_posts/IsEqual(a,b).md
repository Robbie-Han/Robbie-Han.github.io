title: Promise.all()手工代码实现
toc: true
tags: 
- JS
- 深比较
- _.isEqual()
---
# Js深比较探究
## 深比较的思路：
1、对于非引用类型：数字、字符串、null、undefined、布尔类型，使用===操作既可以判断出来。

`对于特殊的NaN === NaN 为false和 0===-0 为true这两种情况要特殊处理。但是写深比较函数不讨论这两种情况，因为我觉的这两种值没有意义，业务中也不会出现这两种值，但是他们在_.isEqual()下是相等的。`

2、对于日期类型(Date)、正则类型(RegExp)不能使用 === 处理，需要单独做处理。

3、对于Object和Array类型则需要递归处理，Object和Array的元素可能包括任何数据类型。
<!--More-->
## 深比较函数
```
const equals = (a, b) => {
  if (a === b) return true;
  if (!a || !b || (typeof a !== 'object' && typeof b !== 'object')) return a=== b;
  if (a instanceof RegExp && b instanceof RegExp) return ''+a === ''+b;
  if (a instanceof Date && b instanceof Date) return a.getTime() ===  b.getTime();
  if (a.__proto__ !== b.__proto__) return false;
  let keys = Object.keys(a);
  if (keys.length !== Object.keys(b).length) return false;
  return keys.every(k => equals(a[k], b[k]));
};
```