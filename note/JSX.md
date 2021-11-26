# JSX
## 01.作用
JSX 是 ECMAScript 一个类似 XML 的语法拓展，可以快速生成 react 元素的一种语法，是React.createElement() 的语法糖。可以在 Js 中，使用 HTML 模板语法描述页面内容。

React 认为渲染逻辑本质上是和其他 UI 逻辑内在耦合，比如在 UI 中需要绑定处理事件，在某些时刻状态发生时需要通知到 UI，以及需要在 UI 中展示准备好的数据。

React 没有采用将标记与逻辑进行分离到不同文件这种人为的分离方式，而是通过把两者共同存放在称之为组件的松散耦合单元之中，来实现关注点的分离。

- JSX 执行更快，在编译为 Js 代码后进行了优化
- JSX 是静态类型的，大多是类型安全的。使用 JSX 进行开发时应用程序的质量会变高。

```js
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
	element,
    document.getElementById('root')
)
```
```js
const element1 = <div tabIndex="0"></div>;
const element2 = <img src={user.avatarUrl} />
```

## 02.规则
- JSX 只能有一个根元素，标签必须是闭合的
- 通过 `{}` 嵌入 Js 表达式
- 被 babel 转换成 React.createElement 的函数调用，创建一个描述 HTML 消息的 JS 对象
- `JSX`中的子元素可以为字符串字面量。
- `JSX`中的子元素可以为`JSX`元素。
- `JSX`中的子元素可以为存储在数组中的一组元素。
- `JSX`中的子元素可以为`Js`表达式，可与其他类型子元素混用；可用于展示任意长度的列表。
- `JSX`中的子元素可以为函数及函数调用。
- `JSX`中的子元素如果为`boolean/null/undefined`将会被忽略，如果使用`&&`运算符，需要确保前面的是布尔值，如果是`0/1`则会被渲染出来。
- 在对象属性中定义`React`组件，可以使用`object`的点语法使用该组件。
- `React`元素会被转换为调用`React.createElement`函数，参数是组件，因此`React`和该组件必须在作用域内。
- `React`元素需要大写字母开头，或者将元素赋值给大小字母开头的变量，小写字母将被认为是`HTML`标签。
- 不能使用表达式作为`React`元素类型，需要先将其赋值给大写字母开头的变量，再把该变量作为组件。