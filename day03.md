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

- componentWillReceiveProps 【UNSAFE_componentWillReceiveProps】

- shouldComponentUpdate

- componentWillUpdate【UNSAFE_componentWillUpdate】

  组件将要被更新

- componentDidUpdate

  组件被更新

- componentWillUnmount

  在组件将要被卸载的时候调用