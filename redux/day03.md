# Redux-saga 简介

###1. 介绍

`redux-saga` 是一个用于管理应用程序 Effect（副作用，主要指异步操作）。它的目标是让副作用管理更容易，执行更高效，测试更简单，在处理故障时更容易。你可能已经用了 `redux-thunk` 来处理数据的读取。不同于 redux thunk，你不会再遇到回调地狱了，你可以很容易地测试异步流程并保持你的 action 是干净的。

### 2. 使用

安装

```shell
$ yarn add redux-saga
```

编写副作用

```javascript
// store/saga.js
import axios from 'axios'
import {call ,put, takeEvery} from 'redux-saga/effects'

function* helloSaga() {
  let url = 'http://134.175.154.93:8099/index/findAllCategory'
  // 执行axios.get方法，并将resolve结果复制给result
  let result = yield call(axios.get,url);
  // 分发同步action，将查询结果设置到state中
  yield put({
    type:'SET_STUDENT',
    payload:result.data.data
  })
}
// 使用takeEvery监听逻辑层的dispath，也就是说当dispatch({type:'HELLO'})的使用执行hellosaga这个异步函数(action)
export default function* rootSaga(){
  yield takeEvery('HELLO',helloSaga)
}
```

应用saga

````javascript
// store/index.js
import {
  createStore,
  combineReducers,
  applyMiddleware
} from 'redux'

// 1. 导入redux-saga
import createSagaMiddleware from 'redux-saga';
// 2. 导入自定义saga
import saga from './saga'
// 自定义的模块
import studentReducer from './student'

let rootReducer = combineReducers({
  students:studentReducer
  // ... 更多的键值对
})
// 3. 创建redux-saga中间件
let sagaMiddleware = createSagaMiddleware(saga)
// 4. 引用中间件
let store = createStore(rootReducer,applyMiddleware(sagaMiddleware))
// 5. 运行saga
sagaMiddleware.run(saga)

export default store;
````

dispatch saga

```javascript
// Student.js
// ...
constructor(props){
    super(props);
    this.props.dispatch({
      type:'HELLO'
    })
}
// ...
```



### 3. saga辅助函数介绍

**takeEvery** 可以理解为注册action与effect之间的映射。当dispatch一个action的时候会对应执行响应的effect，takeEvery允许多个effect同时启动。

**takeLatest** 与takeEvery类似，在任何时刻takeLatest只允许一个effect在执行。并且这个任务是最后被启动的那个。
如果已经有一个任务在执行的时候启动另一个 effect，那之前的这个任务会被自动取消。

**call(fn, ...args)** 创建一个Effect description指导中间件调用fn并且传递args，类似于action generator。fn为generator函数或普通函数

**put(action)** dispatch一个action，只能是同步请求

[demo](https://github.com/pluslicy/redux.git)

[视频资料](https://pan.baidu.com/s/1Culg88M5OugL4Shk5a7wjw)提取码: byfr 