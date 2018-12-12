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


### 2.6 JSX子元素

在MyComponent组件中可以通过 props.children 访问子元素

```jsx
<MyComponent>Hello world!</MyComponent>
```

