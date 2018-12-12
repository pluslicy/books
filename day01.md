# day01 react入门

##1. 认识React
React 是一个用于构建用户界面的 Javascript 库。主要用于构建UI，很多人认为 React 是 MVC 中的 V（视图）。React 起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。拥有较高的性能，代码逻辑非常简单，越来越多的人已开始关注和使用它。

##2. react生态

react 的生态体系比较庞大，它在web端，移动端，服务器端，VR领域都有涉及。react可以说是目前为止最热门，生态最完善，应用范围最广的前端框架。react结合它的整个生态，它可以横跨web端，移动端，服务器端，乃至VR领域。

可以毫不夸张地说，react已不单纯是一个框架，而是一个行业解决方案。


###2.1 web端
- **react**

  核心库
- **react-router** 

  路由机制
- **redux/mobx**

  状态管理机制，Mobx 适合做一些简单的应用，原型实验，适合小的团队使用；redux适合复杂的应用，大团队，需求变化多，redux不仅应用于react，也可以应用于angular，vue等框架，只是redux和react配合使用最为契合。	

- **dva**

  另外国内蚂蚁金服前端团队基于redux, react-router打造了另一个前端框架——dva。dva简单来讲是对redux方案的集成与拓展，它突破框架的本身，形成一套略为完整的前端架构，处理了很多包括项目构建，异步处理、统一请求、统一错误处理等一系列诸多问题。

- **UI库**

  和vue,angular相比，react的UI库无疑是最为丰富的，且十分优秀。目前react的UI库有将近二十多个，这里主要列举最为优秀的几个。
  - material-ui 基于谷歌的material设计理念，因此界面非常精美，尤其适用于web开发。
  - ant design 国内蚂蚁金服开源
- **其他库**
  - **draft-js** 是由facebook开源的编辑器语言。
  - **Immutable** immutable-js是facebook推出的完全独立的一个js库，侧重函数式编程中不可变数据结构，使用Immutable可使你的react应用性能上会有很大的提升。有人说 Immutable 可以给 React 应用带来数十倍的提升，也有人说 Immutable 的引入是近期 JavaScript 中伟大的发明，因为同期 React 太火，它的光芒被掩盖了。

----
推荐技术栈： react+dva+ant design （后台应用）；react+dva+material-ui/react-toolbox （前台应用）
​	
###2.2 移动端
react-native是目前最优秀的非原生开发移动框架，一处开发，多端使用。同时具有出色的性能，支持热更新等超强的优势。vue和angular在移动端同样有建树，分别是weex和ionic+cordova。然其综合性价比仍不如react-native。

开发RN应用所用的技术栈与web端大致相同，同样需要结合redux,react-router, dva, mobx等周边生态来使用。

另外也有一些适合RN的移动端UI库。比如ant design的mobile版——ant-design-mobile，以及响应式的material-ui。

###2.3 桌面端
使用 JavaScript, HTML 和 CSS 构建跨平台的桌面应用，electronjs可以使其成为现实。electron 与react结合可以简化开发

###2.4 服务器端
- **next.js**

  react不仅涉足web端，移动端，同样在服务器端也有非常好的涉猎。而对于react服务器端渲染实践最为出色的莫过于next.js。

###2.5 VR领域
目前，VR(虚拟现实)是科技界的新生事物，也是一大革命，在未来，VR将很大程度地改变人类的生活方式。试想一下，VR将为你呈现一个虚拟现实世界，你将可以使用VR身临其境般地玩游戏，看新闻，购物，社交娱乐，看世界名景等等，这将是一个全新的世界。

webVR是VR技术在浏览器的实现。

目前VR的技术实现方案仍在起草阶段，但有些技术方案几乎是铁定的。比如作为如底层的OpenGL、WebGL、three.js。

而目前就有一些基于底层技术开发出来的webVR框架，比如——react-vr和aframe。

##3. 安装
###3.1 script导入
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>hello world</title>
	<!-- 导入react/bebel -->
	<script src="https://cdn.bootcss.com/react/16.6.0/umd/react.development.js"></script>
	<!-- 导入react-dom -->
	<script src="https://cdn.bootcss.com/react-dom/16.6.0/umd/react-dom.development.js"></script>
	<!-- 导入babel -->
	<script src="https://cdn.bootcss.com/babel-standalone/6.26.0/babel.min.js"></script>
</head>
<body>
	<div id="app"></div>
	<script type='text/babel'>
		ReactDOM.render(
      <h1>Hello, world!</h1>,
      document.getElementById('app')
    );
	</script>
</body>
</html>
```

###3.2 create-react-app

```shell
# 安装node，并且node版本应该满足 Node >= 6 and npm >= 5.2 
$ node -v
	v10.14.1
# 全局安装脚手架
$ cnpm install -g create-react-app
# 使用脚手架创建工程
$ create-react-app my-app
# 启动工程
$ cd my-app/
$ npm start
```
---
参考文档：

[课堂视频](https://pan.baidu.com/s/1Pas5OsHyeXCdzMi9TfGriQ)提取码: cj2c

[react英文文档](https://reactjs.org/)

[react中文文档](https://react.docschina.org/docs/hello-world.html)