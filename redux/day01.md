# day01基本概念

### 1. 为什么使用redux

使用Javascript开发单页面程序的时候，我们需要管理很多很多状态（state），例如: 服务器的响应，本地生成的尚未持久化到服务器的数据（表单数据），激活的路由，选中的标签，是否显示加载动效或分页器等等。管理不断变化的状态非常困难，状态的改变可能会引起页面的变化，而页面的改变也会引起状态的改变，这种改变异常复杂，以至于我们很难捋清业务实现功能。为了规范的管理各种状态，我们可以使用状态管理机制。

### 2. 核心概念

- model

  模型，用于保存状态；注意：不能直接修改state中的值

  ```js
  {
    todos: [{
      text: 'Eat food',
      completed: true
    }, {
      text: 'Exercise',
      completed: false
    }],
    visibilityFilter: 'SHOW_COMPLETED'
  }
  ```

- action

  如果想要修改model中的值，必须发起一个action，这里需要注意的是Action实际上是一个普通的Javascript对象。使用action来修改state的好处在于可以很清楚的描述发生了什么事情，例如type取值为'ADD_TODO' ，那我们就明白要添加TODO，text值为TODO的内容。

  ```js
  { type: 'ADD_TODO', text: 'Go to swimming pool' }
  { type: 'TOGGLE_TODO', index: 1 }
  { type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }
  ```

  action是数据从应用传递到store中的有效载荷。它是store数据的唯一来源！一般来说你会通过[`store.dispatch()`](https://www.redux.org.cn/docs/api/Store.html#dispatch) 将 action 传到 store。Action本质上是一个对象，但是我们约定，action 内必须使用一个字符串类型的 `type` 字段来表示将要执行的动作。除了 `type` 字段外，action 对象的结构完全由你自己决定。参照 [Flux 标准 Action](https://github.com/acdlite/flux-standard-action) 获取关于如何构造 action 的建议。



  action创建函数，注意，action创建函数是用来创建action的函数，而action是一个普通JavaScript对象。在 Redux 中的 action 创建函数只是简单的返回一个 action

  ```javascript
  const ADD_TODO = 'ADD_TODO';
  function addTodo(text) {
    return {
      type: ADD_TODO,
      text
    }
  }
  ```

  如果我们想要发起一个action就可以

  ```javascript
  store.dispatch({type: 'ADD_TODO', text: 'Go to swimming pool'})
  //或者
  store.dispatch(addTodo('Go to swimming pool'))
  ```

​	注意：默认情况下action不能是异步的！必须是同步的。action生成函数也必须是纯函数，只能返回一个对象，并且是同步返回。

- reducer

  那么，如何把action与model关联起来呢？我们可以开发一些函数，这些函数用来接收state与action，并且返回state

  ```javascript
  function todos(state = [], action) {
    switch (action.type) {
    case 'ADD_TODO':
      return state.concat([{ text: action.text, completed: false }]);
    case 'TOGGLE_TODO':
      return state.map((todo, index) =>
        action.index === index ?
          { text: todo.text, completed: !todo.completed } :
          todo
     )
    default:
      return state;
    }
  }
  ```

  在使用reducer的时候需要注意，每个reducer中处理的state如果是独立的那么尽可能拆分开，这样可以简化reducer的开发。在使用的时候我们可以使用combineReducers函数再次合并。

  ```javascript
  import { combineReducers } from 'redux'
  import {
    ADD_TODO,
    TOGGLE_TODO,
    SET_VISIBILITY_FILTER,
    VisibilityFilters
  } from './actions'
  const { SHOW_ALL } = VisibilityFilters
  
  // 1. 处理filter的reducer
  function visibilityFilter(state = SHOW_ALL, action) {
    switch (action.type) {
      case SET_VISIBILITY_FILTER:
        return action.filter
      default:
        return state
    }
  }
  // 2. 处理todos的reducer
  function todos(state = [], action) {
    switch (action.type) {
      case ADD_TODO:
        return [
          ...state,
          {
            text: action.text,
            completed: false
          }
        ]
      case TOGGLE_TODO:
        return state.map((todo, index) => {
          if (index === action.index) {
            return Object.assign({}, todo, {
              completed: !todo.completed
            })
          }
          return todo
        })
      default:
        return state
    }
  }
  // 3. 合并reducer
  const todoApp = combineReducers({
    visibilityFilter,
    todos
  })
  
  export default todoApp
  ```


### 3. 使用原则

- 整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中

- state为只读

- 使用纯函数进行修改




### 4.redux在react中的应用

创建项目，然后安装依赖(redux、react-redux)，如果要想在react组件中使用store，需要在根组件的外部包裹Provider标签（react-redux提供），此外，每个组件在暴露的时候需要调用connect函数（react-redux提供），这时候可以在组件内部使用this.props获取store的值。

```shell
$ create-react-app redux-test01
$ yarn add redux react-redux
```

1. 目录架构

   可以根据公司规定或者个人习惯来定义目录结构

   ```
   src
   	store					状态机
   		student				学生模块
   			index.js		用于定义学生模块action常量以及action生成函数
   			reducers.js 	用于定义学生模块reducers
   		teacher 			教师模块
   			index.js		用于定义教师模块action常量以及action生成函数
   			reducers.js 	用于定义教师模块reducers
   		index.js 		统一出口
   	pages				页面
   		student
   			Layout.js 	学生模块总体布局页面
   		teacher
   			Layout.js	教师模块总体布局页面
   	App.js 				根模块文件
   	index.js			入口文件
   ```

2. 细节



   - src/store/student/index.js

     ```javascript
     export const ADD_STUDENT = 'STUDENT_ADD'
     
     export function addStudent(student){
       return {
         type:ADD_STUDENT,
         payload:student
       }
     }
     ```


   - src/store/student/reducers.js

     ```javascript
     import { combineReducers } from 'redux'
     import {
       ADD_STUDENT
     } from './index'
     
     // 处理学生数据
     function list(state = [],action){
       switch(action.type){
         case ADD_STUDENT:
           return [...state,action.payload]
         default :
           return state
       }
     
     }
     
     // 处理过滤器条件
     function filter(state={filter:'All'},action){
       return state;
     }
     
     // 合并reducer，对外暴露统一的接口
     export default combineReducers({
       list,
       filter
     })
     ```

   - src/store/index

     ```javascript
     import {createStore,combineReducers} from 'redux'
     import student from './student/reducers'
     
     // 合并不同模块的reducer，对外提供统一接口
     const rootReducer = combineReducers({
       student
     })
     
     export default createStore(rootReducer)
     
     ```


   - src/index.js

     在跟组件外部使用Provider标签包裹，并且绑定store属性，意味着App组件以及其子组件都可以访问store中的值

     ```javascript
     import React from 'react';
     import ReactDOM from 'react-dom';
     import './index.css';
     import App from './App';
     import * as serviceWorker from './serviceWorker';
     import {Provider} from 'react-redux'
     import store from './store'
     
     ReactDOM.render(
       <Provider store={store}>
         <App />
       </Provider>, document.getElementById('root'));
     
     serviceWorker.unregister();
     
     ```

   - src/student/Layout.js

     ```javascript
     import React , {Component} from 'react'
     import {connect} from 'react-redux'
     import {
       addStudent
     } from '../store/student'
     
     class Student extends Component {
       constructor(props){
         super(props);
         setInterval(() => {
           // 分发action，用于改变state
           this.props.dispatch(addStudent('terry'))
         }, 1000);
       }
     
       render (){
         const {student} = this.props;
         return (
           <div>
             hello student
             <div>
               {JSON.stringify(student)}
             </div>
           </div>
         )
       }
     }
     // 连接redux
     export default connect(state=>state)(Student)
     ```



[demo](https://github.com/pluslicy/redux.git)
















