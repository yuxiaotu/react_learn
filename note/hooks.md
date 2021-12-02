# Hooks

## 01.作用
hooks 为函数式组件提供了状态合生命周期。以下两个组件分别是在类组件的模式下，以及函数式组件的模式下实现的。

函数式组件通过 useState 让这个函数拥有了属于自己的状态合改变状态的方法。相比于使用传统的方法，函数式组件更加简洁。
```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

```js
import { useState } from 'react';

function Example() {
    const [count, setCount] = useState(0);
    return {
        <div>
        	<p>You clicked {count} times</p>
    		<button onClick={() => setCount(count+1)}>
            	click me    
            </button>
        </div>
    }
}
```

## 02.Hooks方法
- useState
- useEffect
- useContext
- useReducer
- useRef
- useMemo
- useCallback

## 03.useState
声明一个状态变量，同时提供一个可以更新状态的函数。以状态初始值为参数，使用解构的方法将初始状态合更新状态函数赋值给对应的变量。
```js
import React, { useState } from 'react';

function Example() {
    const [count, setCount] = useState(0);
    
    return (
    	<div>
        	<p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}></button>
        </div>
    )
}
```

## 04.useEffect
告诉 React 组件需要在渲染后执行某些操作。

有如下例子，在 useEffect 中执行更新 DOM 的操作。为计数器增加一个功能，将 document 的 title 设置为包含了点击次数的消息。

```js
import React, { useState, useEffect } from 'react';
function Example() {
    const [count, setCount] = useState(0);
    
    useEffect(() => {
        document.title = `You clickend ${count} times`
    });
    
    return {
        <div>
        	<p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
               Click me
            </button>
        </div>
    }
}

```