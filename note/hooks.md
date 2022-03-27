# Hooks

- [Hooks 的作用](#1-Hooks-的作用)
- [Hooks 方法](#2-Hooks-方法)
  - [useState()](#21-useState)
  - [useEffect()](#22-useEffect)

# 1. Hooks 的作用
`hooks` 为函数式组件提供了状态合生命周期。以下两个组件分别是在类组件的模式下，以及函数式组件的模式下实现的。

函数式组件通过 `useState` 让这个函数拥有了属于自己的状态合改变状态的方法。相比于使用传统的方法，函数式组件更加简洁。
```js
// 传统方法
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
// 使用 useState 
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

# 2. Hooks 方法
- useState
- useEffect
- useContext
- useReducer
- useRef
- useMemo
- useCallback

## 2.1. useState

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

## 2.2. useEffect

告诉 `React` 组件需要在渲染后执行某些操作。

之前很多具有副作用的操作，例如「网络请求」，「修改 UI」 等，一般都在 `class` 组件的 `componentDidMount` 或者是 `componentDidUpdate` 等生命周期中进行操作。在函数组件中是没有这些生命周期概念的，只能返回想要渲染的元素。在函数组件中也有执行副作用操作的地方了，就是使用 useEffect 函数。

有如下例子，在 `useEffect` 中执行更新 `DOM` 的操作。为计数器增加一个功能，将 document 的 title 设置为包含了点击次数的消息。

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

## 2.3. useContext

在组件之间共享状态，可以做状态的分发，避免了 react 逐层通过 props 传递数据。

受上下文对象（从中 React.createContext 返回的值）并返回该上下文的当前上下文值。当前上下文值由树中调用组件上方 value 最近的 prop 确定 <MyContext.Provider>。

```js
import React, { createContext } from 'react';
import Foo from './Foo';

import './App.css';

export const ThemeContext = createContext(null);

export default () => {

    return (
        <ThemeContext.Provider value="light">
            <Foo />
        </ThemeContext.Provider>
    )
}
```

```js
import React, { useContext } from 'react';

import { ThemeContext } from './App';

export default () => {
    
    const context = useContext(ThemeContext);

    return (
        <div>Foo 组件：当前 theme 是：{ context }</div>   
    )
}
```

## 2.4. useReducer

useState 的替代方案。 接受类型为 `(state, action) => newState 的reducer`，并返回与 dispatch 方法配对的当前状态。

- 当 state 状态值结构比较复杂时，使用 useReducer 更有优势。
- 使用 useState 获取的 setState 方法更新数据时是异步的；而使用 useReducer 获取的 dispatch 方法更新数据是同步的。

```js
import React, { useReducer } from 'react';

const initialState = {count: 0};

function reducer(state, action) {
    switch (action.type) {
        case 'increment':
            return {count: state.count + 1};
        case 'decrement':
            return {count: state.count - 1};
        default:
            throw new Error();
    }
}

export default () => {
    
    // 使用 useReducer 函数创建状态 state 以及更新状态的 dispatch 函数
    const [state, dispatch] = useReducer(reducer, initialState);
    return (
        <>
            Count: {state.count}
            <br />
            <button onClick={() => dispatch({type: 'increment'})}>+</button>
            <button onClick={() => dispatch({type: 'decrement'})}>-</button>
        </>
    );
}
```

## 2.5. useRef

useRef 返回一个可变的 ref 对象，其 .current 属性被初始化为传递的参数（initialValue）。返回的对象将存留在整个组件的生命周期中。

```js
import React, { useRef, useState, useEffect } from 'react'; 

export default () => {
    
    // 使用 useRef 创建 inputEl 
    const inputEl = useRef(null);

    const [text, updateText] = useState('');

    // 使用 useRef 创建 textRef 
    const textRef = useRef();

    useEffect(() => {
        // 将 text 值存入 textRef.current 中
        textRef.current = text;
        console.log('textRef.current：', textRef.current);
    });

    const onButtonClick = () => {
        // `current` points to the mounted text input element
        inputEl.current.value = "Hello, useRef";
    };

    return (
        <>
            {/* 保存 input 的 ref 到 inputEl */}
            <input ref={ inputEl } type="text" />
            <button onClick={ onButtonClick }>在 input 上展示文字</button>
            <br />
            <br />
            <input value={text} onChange={e => updateText(e.target.value)} />
        </>
    );

}
```

