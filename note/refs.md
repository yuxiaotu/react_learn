# Refs

# 1. 作用
`Refs` 是一个 获取 DOM 节点或 `React` 元素实例的工具。在 `React` 中 `Refs` 提供了一种方式，允许用户访问 DOM 节点或者在 `render` 方法中创建的 `React` 元素。

在 `React` 单项数据流中，`props` 是父子组件交互的唯一方式。要修改一个子组件，需要通过的新的 `props` 来重新渲染。
但是在某些情况下，需要在数据流之外强制修改子组件。被修改的子组件可能是一个`React` 组件实例，也可能是一个 DOM 元素。对于这两种情况，`React` 都通过 `Refs` 的使用提供了具体的解决方案。

# 2. 使用
```js
class MyComponent extends React.Component {
  constructor(props) {
    supor(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef}></div>
  }
}
```
```js
const node = this.myRef.current;
```

# 3. 函数式组件
函数式组件没有实例，不能像上面这样使用 refs。但是可以在函数组件中使用 ref 属性，就像引用 DOM 元素和类组件一样。
```js
function CustomTextInput(props) {
  let textInput = React.createRef();

  function handleClick() {
    textInput.current.focus();
  }

  return (
    <div>
      <input type="text" ref={textInput} onClick={handleClick}/>
    </div>
  )
}
```