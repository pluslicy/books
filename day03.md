# day03 深入组件

## 1.局部状态

在类构造函数来初始化状态

```jsx
class MyHeader extends React.Component{
  // 构造函数，定义state,相当于vue中data
  constructor(props){
    super(props)
    // 定义组件实例自身变量
    this.state = {
      user:{
        username:'terry'
      }
    }
  }

  render(){
    let user = this.state.user;
    return <h2>欢迎您{user.username}</h2>
  }
}
```



## 2. 生命周期钩子

![](https://raw.githubusercontent.com/pluslicy/react_demos/master/assets/images/react_lifecycle.png)

- componentWillMount

  在组件将要被挂载前调用

- **componentDidMount**

  在组件被挂载之后立即调用，可以进行初始化网络请求，如果调用setState，然后可以再次渲染，但是这次渲染会发生在浏览器更新屏幕之前，用户不会发现中间状态。

- shouldComponentUpdate

  组件是否被更新，如果返回true则更新，否则不更新

- componentWillUpdate【UNSAFE_componentWillUpdate】

  组件将要被更新

- componentDidUpdate

  组件被更新

- componentWillUnmount

  在组件将要被卸载的时候调用

## 3. 事件处理函数

### 3.1 事件绑定

与vue绑定方式类似，需要在组件上通过'onXxx'来绑定事件，事件处理函数必须在双大括号内通过this来指定。事件处理函数应该定义类中，与render()，事件钩子函数在同一级别

```javascript
class MyComponent extends React.Component{
  handleClick(){
    alert('handleClick...');
  }
  render(){
    return (
      <div onClick={this.handleClick}>hello MyComponent</div>
    )
  }
}
```

### 3.2 事件对象

与DOM操作类似，通过事件对象获取目标元素，默认情况下，可以通过再事件处理函数上声明形式参数来获取event。你可以在调用event.preventDefault()来阻止默认行为，调用event.target获取目标元素，调用event.cancelable阻止事件冒泡...

```javascript
class MyComponent extends React.Component{
  handleClick(event){
    alert('handleClick...');
    console.log(event);
  }
  render(){
    return (
      <div onClick={this.handleClick}>hello MyComponent</div>
    )
  }
}
```

### 3.3 事件处理函数中的this

如果通过es6的函数声明方式来定义事件处理函数，那么在事件处理函数中的this为undefined。我们可以事件箭头函数来定义事件处理函数，这时候箭头函数中的this指向对象组件对象。

```javascript
class MyComponent extends React.Component{
  handleClick = (event)=>{
    alert('handleClick...');
    console.log(event);
    console.log(this);
  }
  render(){
    return (
      <div onClick={this.handleClick}>hello MyComponent</div>
    )
  }
}
```





