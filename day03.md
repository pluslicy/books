# day03 组件

## 1. 组件定义

- 函数定义

  该函数接收一个单一的props对象并返回一个React元素

  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```

- 类定义（ES6）

  使用ES6中的语法定义一个组件类

  ```jsx
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
  ```



## 2. 组件渲染

通过函数ReactDOM.render() 将Weblcome组件渲染到id为root的元素上

```jsx
ReactDOM.render(
  <Welcome name="Sara" />,
  document.getElementById('root')
);
```

如上代码发生了如下一些事情

1. 我们对`<Welcome name="Sara" />`元素调用了`ReactDOM.render()`方法。
2. React将`{name: 'Sara'}`作为props传入并调用`Welcome`组件。
3. `Welcome`组件将`<h1>Hello, Sara</h1>`元素作为结果返回。
4. React DOM将DOM更新为`<h1>Hello, Sara</h1>`。
5. 当name发生变化的时候Welcome组件又会重新渲染

