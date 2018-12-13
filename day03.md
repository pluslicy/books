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



### 3.4 传递参数

如果想要传递参数给事件处理函数，需要在事件绑定的时候调用bind方法，然后将this作为第一个实参，其他的参数可以自定义。但是要注意，在事件处理函数中，第一个参数为你绑定的第二个形参，... ，最后一个参数为event对象

```javascript
class MyComponent extends React.Component{
  handleClick = (param,event)=>{
    console.log(event);
    console.log(this);
    console.log(param);
  }
  render(){
    return (
      <div onClick={this.handleClick.bind(this,1)}>hello MyComponent</div>
    )
  }
}
```

当然，还有一种方式也可以传递参数

```
class MyComponent extends React.Component{
  
  handleClick = (event,p1,p2)=>{
    console.log('event',event);
    console.log('p1',p1);
    console.log('p2',p2);
    console.log('this',this);
  }
  render(){
    return (
      <div>
        <div onClick={(e)=>this.handleClick(e,1,2)}>hello MyComponent</div>
      </div>
    )
  }
}

```

```
<MyDiv onClick={this.handleClick}>

class MyDiv extends Component{
    handleClick = (event)=>{
        //this 箭头函数机制保证this指向当前组件实例对象 this.props;this.state;this.handleClick
        // event 为事件对象 preventDefault cancelBubble 
    }
}

<MyDiv onClick={this.handleClick.bind(this,1,2,3)}>

class MyDiv extends Component{
    handleClick = (a,b,c,event)=>{
        //this 箭头函数机制保证this指向当前组件实例对象 this.props;this.state;this.handleClick
        // event 为事件对象 preventDefault cancelBubble 
    }
}


<MyDiv onClick={(e)=>{this.handleClick(1,2,3,e)}}>

class MyDiv extends Component{
    handleClick = (a,b,c,event)=>{
        //this 箭头函数机制保证this指向当前组件实例对象 this.props;this.state;this.handleClick
        // event 为事件对象 preventDefault cancelBubble 
    }
}

```

[课堂视频](https://pan.baidu.com/s/1oLUJ-CPSgNYx0NTfgzvKdA) 提取码: 7pk5



















