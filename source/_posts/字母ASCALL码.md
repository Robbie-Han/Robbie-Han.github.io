---
title: 字母的ASCALL
toc: true
tags: 
- JS
- ASCALL
---
## codeware题
```
Write a method that takes an array of consecutive (increasing) letters as input and that returns the missing letter in the array.
['a','b','c','d','f'] -> 'e'
['O','Q','R','S'] -> 'P'
```
解决方案：
```
function findMissingLetter(array){
  const toNumArray = array.map((item)=>item.charCodeAt());
  for(i=0;i<toNumArray.length-1;i++){
    if(toNumArray[i+1]-toNumArray[i] > 1){
       return String.fromCharCode(toNumArray[i]+1);
    }
  }
}
```
网友更好的答案：
```
function findMissingLetter(array)
{
   var i=array[0].charCodeAt();
   array.map(x=>  x.charCodeAt()==i?i++:i);
   return String.fromCharCode(i);
}
```
### 字母转ASCALL使用charCodeAt()
```
'a'.charCodeAt();//97
```
### ASCALL转字母使用fromCharCode()
```
String.fromCharCode(65)//A
```