# 课堂笔记

1. react介绍

  1. web
    ​	react
    ​	react-dom
    ​	react-router
    ​	redux
    ​	axios (jquery ajax)
    ​	antd
  2. app
    ​	react-native
  3. desktop
    ​	electron
  4. server
    ​	next.js
  5. vr
    ​	webvr

2. 脚手架

  全局安装（只需要装一次）

  $ npm install create-react-app -g

  创建项目并且启动

  $ create-react-app app01
  $ cd app01
  $ npm run start

3. 通过vscode/ webstorm

4. react项目结构
  node_modules
  public
  ​	favicon.icon
  ​	index.html
  src
  ​	index.js 		入口文件
  ​	App.js 		根组件
  .gitignore
  package.json

5. 语法
  index.js

  ```
  	// 将组件App渲染到id为root的元素内
  	ReactDOM.render(
  		<App/>,
  		document.getElementById('root')
  	)
  ```

  App.js
  ​	组件介绍

  ```
  import React, { Component } from 'react';
  class App extends Component{
  	constructor(props){
  		super(props);
  		this.state = {
  			msg:'hello world',
  			students:[{},{}]
  		}
  	}
  	handleClick=()=>{
  		this.setState({
  			msg:'你好'
  		})
  	}
  	render(){
  		return (
  			<div>
  				<h2 onClick={this.handleClick}>{this.state.msg}</h2>
  
  			</div>
  		)
  	}
  
  }
  ```

6. 项目体验

http://jxy.me/react-antd-admin/#/