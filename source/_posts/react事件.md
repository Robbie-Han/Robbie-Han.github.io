---
title: react 事件处理
tags: 
- React
---
## react 事件处理的几个方法：
#### class定义组件，在constructor函数绑定回调函数：
```
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isToggleOn: true,
      value: 10
    };

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this,12); // 要点一(作用域绑定和传参)
  }

  handleClick(v) {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn,
      value: v
    })); 
  }

  render() {
    return (
      <div>
        <button onClick={this.handleClick}>   // 要点二 （回调函数）
           {this.state.isToggleOn ? 'ON' : 'OFF'}
        </button>
        <p>{this.state.value}</p>
      </div>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```
当组件的方法使用ES5来写的话，需要将函数绑定到组件中。class 的方法默认不会绑定 this。如果你忘记绑定 this.handleClick 并把它传入了 onClick，当你调用这个函数的时候 this 的值为 undefined。
```
"use strict";

function name() {
  console.log(this);\\ undefined
}

name();
```
这种写法还有一个弊端，当组件被多次使用的时候，多分同样的功能的函数将保存在内存中，比较冗余。

#### 使用ES6语法定义函数。
```
class LoggingButton extends React.Component {
  // 此语法确保 `handleClick` 内的 `this` 已被绑定。
  // 注意: 这是 *实验性* 语法。
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}

```
ES6定义的箭头函数，函数內的this是在函数定义的时候绑定的，而ES5定义的函数则是在函数被调用的时候绑定的。所以使用箭头函数的时候，函数的this会绑定组件
LoggingButton

#### 回调函数使用箭头函数

```
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this); //使用ES5
  }

  render() {
    // 此语法确保 `handleClick` 内的 `this` 已被绑定。
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```
回调函数使用ES6的语法，在LoggingButton组件每次被渲染的时候都会重新生成回调函数，如果子组件通过props使用该函数，则会引起重复渲染。