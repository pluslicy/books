# Redux-thunk 简介

### 1. 介绍

Redux Thunk是属于Redux的一个中间件，它可以使action生成函数（action generator）返回一个函数而不是一个函数对象。返回的函数接受dispatch, getState可以用来分发action或者获取仓库数据。

```javascript
const INCREMENT_COUNTER = 'INCREMENT_COUNTER';

function increment() {
  return {
    type: INCREMENT_COUNTER
  };
}

function incrementAsync() {
  return function(dispatch) {
    setTimeout(() => {
      // Yay! Can invoke sync or async actions with `dispatch`
      dispatch(increment());
    }, 1000);
  };
}
```

### 2. 应用

安装

````shell
$ npm install redux-thunk
````

在createStore函数中的第二个参数上设置中间件，这时候当我们分发异步action的时候是可以被中间件thunk处理的

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers/index';

// Note: this API requires redux@>=3.1.0
const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);
```

### 3. es6中异步函数解决方案

Generator 函数是 ES6 提供的一种异步编程解决方案，语法行为与传统函数完全不同。Generator 函数有多种理解角度。语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。执行 Generator 函数会返回一个遍历器对象。

形式上，Generator 函数是一个普通函数，但是有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态（`yield`在英语里的意思就是“产出”）,`yield`表达式就是暂停标志。

```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
hw.next()	// { value: 'hello', done: false }
hw.next()	// { value: 'world', done: false }
hw.next()	// { value: 'ending', done: true }
hw.next()	// { value: undefined, done: true }
```

上面代码定义了一个 Generator 函数`helloWorldGenerator`，它内部有两个`yield`表达式（`hello`和`world`），即该函数有三个状态：hello，world 和 return 语句（结束执行）。

遍历器对象的`next`方法的运行逻辑如下。

（1）遇到`yield`表达式，就暂停执行后面的操作，并将紧跟在`yield`后面的那个表达式的值，作为返回的对象的`value`属性值。

（2）下一次调用`next`方法时，再继续往下执行，直到遇到下一个`yield`表达式。

（3）如果没有再遇到新的`yield`表达式，就一直运行到函数结束，直到`return`语句为止，并将`return`语句后面的表达式的值，作为返回的对象的`value`属性值。

（4）如果该函数没有`return`语句，则返回的对象的`value`属性值为`undefined`。

```javascript
var axios = require('axios');
var co = require('co');

// ajax
function loadStudent(){
    return axios.get('http://134.175.154.93:8099/index/findAllCategory');
}
//异步函数定义
function* load(){
    let result1 = yield loadStudent();
    let result2 = yield loadStudent();
    console.log(result1.data);    
    console.log(result2.data);
}

// 自动执行异步函数
co(load())
```



[demo](https://github.com/pluslicy/redux.git)

[视频资料](https://pan.baidu.com/s/1w_BiQqSC0z3F2_ARlOwd9A)提取码: 81fb