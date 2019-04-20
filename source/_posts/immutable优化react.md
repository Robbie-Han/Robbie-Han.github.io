## immutable的理解：
### 什么是immutable:
 Immutable 实现的原理是 **Persistent Data Structure**（持久化数据结构），也就是使用旧数据创建新数据时，要保证旧数据同时可用且不变。同时为了避免 deepCopy 把所有节点都复制一遍带来的性能损耗，Immutable 使用了 **Structural Sharing**（结构共享），即如果对象树中一个节点发生变化，只修改这个节点和受它影响的父节点，其它节点则进行共享。
####  如下图所示：
 ![image](https://camo.githubusercontent.com/9e129aaf95d2a645a860dc26532796817e8085c0/687474703a2f2f696d672e616c6963646e2e636f6d2f7470732f69322f5442317a7a695f4b5858585858637458465858627262384f5658582d3631332d3537352e676966)
 
 ### immutable对react的优化思路：
 JavaScript 中的对象一般是可变的（Mutable），因为使用了引用赋值，新的对象简单的引用了原始对象，改变新的对象将影响到原始对象。如 `foo={a: 1}; bar=foo; bar.a=2` 你会发现此时 `foo.a` 也被改成了 `2`。虽然这样做可以节约内存，但当应用复杂后，这就造成了非常大的隐患，Mutable 带来的优点变得得不偿失。
 
 为了解决这个问题，一般的做法是使用 shallowCopy（浅拷贝）或 deepCopy（深拷贝）来避免被修改，但这样做造成了 CPU 和内存的浪费，因为每次state数据的改变都会重新渲染rende函数，造成不必要的浪费。要想搞清楚为什么需要了解下react生命周期中的shouldComponentUpdate().
 
  
 ![image](https://github.com/USTC-Han/USTC-Han.github.io/blob/master/pic/%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.jpg)
 
 React的重复渲染优化的核心其实就是在shouldComponentUpdate里面做数据比较。在优化之前，shouldComponentUpdate是默认返回true的，这导致任何时候触发任何的数据变化都会使component重新渲染。这必然会导致资源的浪费和性能的低下——你可能会感觉比较原生的响应更慢。
 然而immutable只更新改变的节点和其相关父节点，减少了不必要节点的更新。大大的提高了效率。
###  seamless-immutable
seamless-immutable扩展了 JavaScript 的 Array 和 Object 对象，代码压缩后比较小，非常适合应用在react的开发项目中；
#### 常用API

```
const arr = Immutable([1, 2, 3])// 创建Immutable数组

const obj = Immutable({foo: 'bar'})// 创建Immutable数组

```
对象合并：merge

```
var obj = Immutable({status: "good", hypothesis: "plausible", errors: 0});
Immutable.merge(obj, {status: "funky", hypothesis: "confirmed"});
// returns Immutable({status: "funky", hypothesis: "confirmed", errors: 0})
```
对象/数组赋值：set单层

```
var obj = Immutable({type: "parrot", subtype: "Norwegian Blue", status: "alive"});
Immutable.merge(obj, {status: "dead"});
// returns Immutable({type: "parrot", subtype: "Norwegian Blue", status: "dead"})

var array = Immutable(["hello", "world"]); // 数组
var mutatedArray = Immutable.set(array, 1, "you");

mutatedArray // ["hello", "you"]
```
对象深层赋值：setIn

```
var obj = Immutable({type: {main: "parrot", sub: "Norwegian Blue"}, status: "alive"});
Immutable.setIn(obj, ["type", "sub"], "Norwegian Ridgeback");
// returns Immutable({type: {main: "parrot", sub: "Norwegian Ridgeback"}, status: "alive"})

数组：
var array = Immutable([["one fish", "two fish"], ["red fish", "blue fish"]]);
var mutatedArray = Immutable.setIn(array, [1, 1], "green fish");

mutatedArray // [["one fish", "two fish"], ["red fish", "green fish"]]
```
对象取值：getIn
```
var obj = Immutable({type: {main: "parrot", subtype: "Norwegian Blue"}, status: "alive"});
Immutable.getIn(obj, ["type", "subtype"]);
// returns "Norwegian Blue"

Immutable.getIn(obj, ["type", "class"], "Aves");//默认值
// returns "Aves"
```
对象中某值作为函数参数：update/updateIn
```
function add (x, y) { return x + y }
var obj = Immutable({foo: 1});
Immutable.update(obj, "foo", add, 10);
// returns Immutable({foo: 11})

function add (x, y) { return x + y }
var obj = Immutable({foo: {bar: 1}});
Immutable.updateIn(obj, ["foo", "bar"], add, 10);
// returns Immutable({foo: {bar: 11}})
```
去掉对象中某个键值对：without
```

var obj = Immutable({the: "forests", will: "echo", with: "laughter"});
Immutable.without(obj, "with");
// returns Immutable({the: "forests", will: "echo"})

var obj = Immutable({the: "forests", will: "echo", with: "laughter"});
Immutable.without(obj, ["will", "with"]);
// returns Immutable({the: "forests"})

var obj = Immutable({the: "forests", will: "echo", with: "laughter"});
Immutable.without(obj, "will", "with");
// returns Immutable({the: "forests"})

var obj = Immutable({the: "forests", will: "echo", with: "laughter"});
Immutable.without(obj, (value, key) => key === "the" || value === "echo");
// returns Immutable({with: "laughter"})
```







