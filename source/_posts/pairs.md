---
title: 求数组中元素和为s最先匹配元素
tags: 
- JS
- Array
---

  ```
  var sum_pairs=function(ints, s){
  let pairsObj = {}；
  for(item of ints){
    if(pairsObj[s-item]){
      return [s-item, item]；
    }
    pairsObj[item] = true；
  }
}
```
```
sum_pairs([11, 3, 7, 5],         10)
#              ^--^      3 + 7 = 10
== [3, 7]

sum_pairs([4, 3, 2, 3, 4],         6)
#          ^-----^         4 + 2 = 6, indices: 0, 2 *
#             ^-----^      3 + 3 = 6, indices: 1, 3
#                ^-----^   2 + 4 = 6, indices: 2, 4
#  * entire pair is earlier, and therefore is the correct answer
== [4, 2]
```