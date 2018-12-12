# day02 JSX

## 1. 介绍

jsx语法比较有意思，既有点像Javascript又有点像Html。jsx是Javascript语法的扩展，在react中主要用于描述页面。

```jsx
const element = <h1>Hello, world!</h1>;
```

jsx实际上是如下代码的语法糖

```jsx
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```

编译为：

```javascript
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)
```

## 2. 语法

### 2.1 在JSX中嵌入语法

在JSX的大括号中可以嵌入任意表达式

```jsx
class Part1 extends Component{
  // 构造函数
  constructor(props){
    super(props);
    this.state = {
      msg:'hello world',
      user:{
        name:"terry"
      }
    }
  }
  // 渲染
  render(){
    return (
      <div>{this.state.msg} ，{1+1} ，{this.state.user?this.state.user.name:'no person!'}</div>
    )
  }
}
```

## 2.2 JSX也是表达式

可以在一个方法中将jsx当做一个表达式返回，常用语**条件渲染**和**列表渲染**

```jsx
class Part1 extends Component{
  // 构造函数
  constructor(props){
    super(props);
    this.state = {
      //登录用户
      user:{
        name:"terry"
      },
      //用户列表
      persons:[{
        name:"terry",
        age:12
      },{
        name:"larry",
        age:13
      }]
    }
  }
  // 渲染
  render(){
    //条件渲染
    let header ;
    if(this.state.user){
      header = <h2>{this.state.user.name}</h2>
    } else {
      header = <h2>未登录</h2>
    }
      
    return (
      <div>
        //获取变量进行条件渲染
        <div>{header}</div>
        //列表渲染
        <ul>
          {
            this.state.persons.map((item)=>{
              // 返回jsx
              return <li>{item.name}</li>
            })
          }
        </ul>
      </div>
    )
  }
}
```



### 2.3 JSX属性

```jsx
const element = <img src={user.avatarUrl}></img>;
```

### 2.4 子元素

如果标签内元素为空，可以使用'/>'结束

```jsx
const element = <img src={user.avatarUrl} />;
```

JSX标签也可以嵌入子标签

```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### 2.5 jsx中的props

调用组件的时候可以传递任何参数作为prop，如下代码，在MyComponent中通过props.foo可以获取值10。注意，无论是使用函数或类来声明一个组件，它决不能修改它自己的props。

```jsx
<MyComponent foo={1 + 2 + 3 + 4} />
```

- 传递字符串

  ```jsx
  <MyComponent foo='this is foo' />
  //或
  <MyComponent foo={'this is foo'} />
  ```

- 传递布尔类型

  ```jsx
  <MyComponent foo />
  //或
  <MyComponent foo={true} />
  ```

- 传递数字

  ```jsx
  <MyComponent foo={12} />
  ```

- 传递数组

  ```jsx
  <MyComponent foo={[1,2,3,4,5]} />
  ```

- 传递对象

  ```jsx
  let obj = {name:'terry',age:12}
  <MyComponent foo={obj} />
  //或
  <MyComponent foo={...obj} />
  ```

- 设置默认值

  ```jsx
  class MyDiv extends React.Component{ 
    constructor(props){
      super(props);
    }
    render(){
      return (
        <div>hello div,{this.props.name}</div>
      )
    }
  }
  //设置默认值
  MyDiv.defaultProps = {
    name:'terry'
  }
  
  ReactDOM.render(
    <MyDiv name='jacky'/>,
    document.getElementById('app')
  );
  ```


### 2.6 JSX子元素

在MyComponent组件中可以通过 props.children 访问子元素

```jsx
<MyComponent>Hello world!</MyComponent>
```



## 3. 初始组件

### 3.1 组件定义

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



### 3.2组件渲

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



---

[课堂视频](https://pan.baidu.com/s/19nuTMxGScdmSxxdXBhIbhA) 提取码: zqfb 

