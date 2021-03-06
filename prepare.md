

# 前后台分离开发介绍

## 1. 大前端开发	

​	首先应该明确，现在的前端开发是完全脱离后台的，和Java中的jsp以及和c#中的asp是没有任何关系的。以前，传统的开发是使用jsp或者asp开发，是以为Java为主导的。而现在倡导前后台完全分离，各大公司都在实施，使得前端开发更加独立。

​	所以大家不管是学习后台开发还是学习前端开发都要简单很多。因为技术更加集中。你们不需要考虑过多的东西，只需要专心考虑自身学习的方向即可。

​	那么有人又会问，前台后分离开发后如何才能完成一个项目呢。当然，也会有交叉，多数情况下而交叉仅仅会出现在数据交互的时候，比如举个例子，前端想显示所有的学生信息，而学生信息存储在数据库中，我们如何处理呢？

- 首先：会有人告诉前后台开发者需求，为什么要显示所有学生信息，显示哪些信息（字段,比如：姓名，性别，手机号），这时候前端就开始绘制table，然后设置table-header。数据可以模拟。
- 与此同时，后台开发者也没闲着，他们会设计数据库，然后编写JDBC代码进行数据库操作完成CURD操作，最后通过servlet/springmvc/struts2等mvc技术暴露接口
- 当后台接口暴露出来后，前端这时候就有了数据来源，直接调用后台接口就可以获取学生数据，然后把表格模拟的数据更换成从后台获取的数据即可

也就是说要想完成一个企业级项目，我们要维护一个团队，在这个团队中，分工明确，前端负责页面显示，后端负责数据供给。相互配合。

前端学习路线

- **第一阶段 【重构】**

  > 前端三要素

  1. Html5（不学习api调用，比如拖拽，画布，本地存储等）
  2. css3 （重点学习盒模型，布局（浮动布局，伸缩盒布局，响应式布局），动画）
  3. Javascript基础 （也就是ECMAScript5，重点学习语法，正则表达式，函数，数据，算法，JS面向对象等）
  4. DOM (文档对象模型)
  5. BOM (浏览器对象模型, 重点是Ajax)



- **第二阶段【DOM驱动框架】**

  > 这一阶段是前端非常基础性的框架学习

  1. jQuery （学习jquery是如何处理DOM的，包括如何封装ajax）
  2. Bootstrap (最简单也是流行度最广泛的前端组件库，用于快速构建响应式页面)
  3. Highcharts (数据可视化框架，用于图表显示，例如饼状图，柱状图，折线图，蜘蛛图等等)
  4. Animate.css (经典的CSS3动画库，可以很方便的实现动画而不用写大量的底层代码)
  5. FontAwesome/ IconFont （字体图标库，可以像使用字体一样使用图标） 
  6. axios(纯粹的ajax框架，虽然jquery中也有，但是我们使用更多的是axios) 



- **第三阶段【数据驱动框架】（企业级框架阶段）**

  > 到此为止都还算简单，真正复杂的东西来了、、、如果利用传统的html/css/js开发前端代码，太累，并且团队协作很困难，没有模块化的概念。这时候ECMAScript6出现了，也就是ES6。但是这个版本的JS很多语法浏览器并不支持，谁支持呢？NodeJS支持呀，所有我们就可以在NodeJS中开发，然后开发完毕后把ES6转换为ES5最终跑在浏览器上。折腾一大圈又回归到html/css/js上了。
  >
  > 为了开发高效，我们使用ES6，为了使得这样的代码能够运行在浏览器上我们需要借助一些列眼花缭乱的技术：

  1. ES6 （javascript的高级版本，包含了类，承诺，异步函数等等新JS功能）

  2. babel (用于将ES6转换为ES5)

  3. webpack (构建工具，babel可以集成到webpack中)

  4. sass (新一代css开发技术，可以在sass中快速构建css代码。当然浏览器不支持，可以使用webpack中的插件进行转化)​	


这个阶段也最为困难，一般学习 Vue系列框架或者 react系列框架或者Angular系列框架。这三套系列框架都提供了核心技术，路由解决方案，状态管理解决方案，hybird app解决方案，常用组件库。一般企业级开发要求 react/vue/angular熟悉其中之一即可。这里我重点介绍前两套学习路线

1. Vue (vue的核心)

2. VueRouter (路由管理)

3. vuex (数据状态管理)

4. Elementui（饿了么团队开源出来的VUE组件库）

5. weex （阿里巴巴团队开源出来的byhird app解决方案，用于利用vue技术开发手机APP）


实际上到此为止，基本上可以满足大部分企业的用人需求。那么还有一些大型公司使用react,作为初学者我们只需要在vue/react中选择一个体系学习即可。下面谈谈react，他的学习难度要大一些：

1. react （react核心，其余模块均依赖它，类似于vue）
2. react-dom (专业处理dom的。vue中直接在vue框架中集成，没有单独列出来)
3. react-router (路由管理,类似于vue-router)
4. redux (数据状态管理，类似于vuex，有同学可能听说过mobx 与redux类似但是相对简单一些)
5. redux-thunk/redux-saga (redux的封装，底层redux使用起来相对复杂一些，这两个框架选择其一即可)
6. react-native （与weex类似，用于开发手机APP，但是效率会更高一些）
7. react-electron (与electron配合开发跨平台桌面版应用程序)



- **第四阶段 【微信端开发】**

  > 这个阶段实际上不用怎么学，直接用就可以

  1. 微信公众号
  2. 微信小程序、支付宝小程序

- **第五阶段 【NodeJS】**

  > 如果前面都搞定了那么你基本就是前端大神了。但是如果想成为一名真正的架构师，除了懂前端之外，后台也务必通晓。但是学前端的如何学习后台呢？后台不是Java/python/c#/php搞得么，哈，告诉你把，nodejs也可以，只不过这个代码务必要运行在nodejs上，而不是运行在浏览器上的

  1. NodeJS内置模块（File,Http等模块）
  2. Express (mvc框架，类似于Java中的servlet)
  3. Mysql (这里面的Mysql指的是nodeJS中的mysql框架，当然你要提前学习Mysql这个数据库)



差不多喽，如果你对技术的追求无止境，那么这时候看看Java学习真正的服务端开发也不是一个什么不好的事情。然后看看Python,比如我就喜欢用Python来读取一些传感器数据，来驱动一个硬件来

## 2. JavaEE企业级开发

传统的JavaEE企业级开发是Java为主，动态页面一般也由Java工程师使用JSP技术来完成。但是这种开发方式有很大的弊端，后台工程师需要考虑页面布局，样式调整甚至于页面优化等这些前端技术从而导致后台工程师无法真正的集中精力完成后台开发（比如数据库操作，文件操作，excel操作等），此外，这种开发效率也十分低下，后期维护成本也比较高。所以越来越多的公司采用前后台完全分离的方式进行开发，在这种模式下，后台工程师只需要集中精力处理后台业务即可，通过swagger暴露接口给前端。那么前端集中精力处理页面以及用户体验，通过swagger来查看后台暴露给出来的接口，然后通过ajax来访问这些接口获取数据，然后将这些数据动态显示到页面中。

那么如何学好Java技术呢？

- **第一阶段【Java基础】**


1. Linux （腾讯云注册学生账号，购买腾讯云服务器，安装ubuntu镜像）

2. CoreJava （在linux操作系统下完成CoreJava学习，语法, 数组，面向对象，集合，线程，IO，异常，网络编程，Java8新特性）

3. XML （掌握Java操作XML以及解析XML的技术 SAX、DOM4J）

4. 数据库ORACLE/MYSQL （掌握DDL 和 DML即数据库定义语言和数据库修改语言；可以通过终端来操作数据库）

5. JDBC （数据库连接技术）


- **第二阶段【JavaWeb基础】**


1. Html /css （简单的学习html标签和CSS选择器及样式，明确其语法即可）

2. Servlet/jsp (这个是Javaweb基础，务必掌握 http协议，request ,response原理及api，session cookie原理及应用)

3. 企业级开发工具应用（重点掌握maven/git/github）


- **第三阶段【企业级框架应用】**


1. spring 基础（掌握依赖注入，面向切面编程基础技术）

2. springboot (掌握springboot创建架构项目的方式)

3. springmvc （基于servlet的mvc框架）

4. mybatis (JDBC框架)

5. mybatis generator (根据数据库快速生成代码的框架)

6. spring security (spring的认证框架)

7. swagger (API框架，可以迅速产生swagger文档，方便前后台数据对接)


- **第四阶段【微服务架构】**


1. fastdfs (分布式图片存储)
2. OAuth2 （身份认证框架）
3. rabbitmq （消息队列）
4. redis (数据缓存技术)
5. springcloud 微服务总体解决方案













