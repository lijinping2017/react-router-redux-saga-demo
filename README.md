# 基于create-react-app引入router、redux、saga技术栈的搭建 


## 一、背景说明

一个复杂的网站很多时候需要实现页面的跳转，多数据的更新和传递，此时需要一个容器管理数据和快速拿到每个组件中想要的数据，以及达到可以实现异步操作等，这时就需要在 `react` 中引入 `router`、`redux`、`saga` 插件，使用这整套 `react` 技术栈来实现网站的设计了，以下是基于 `create-react-app`  引入 `router、redux、saga` 技术栈的具体操作：


## 二、操作步骤

### 1、创建项目
(1)、进入到你想创建项目存放的磁盘文件，比如 `D:\test` 文件，双击进入 `test` 文件后，在空白的地方按住 `shift` 键再用鼠标点击右键，选择在**此处打开命令窗口（w)**,此时会弹出一个命令行窗口。

(2)、我们需要使用create-react-app脚手架创建一个项目，此时在命令行窗口中输入

`create-react-app react-router-redux-saga-demo`

回车后等待项目安装完成，此时项目名称为 `react-router-redux-saga-demo`。

(3)、安装完成后，我们会在 `D:\test` 中看到新增的 `react-router-redux-saga-demo` 文件，文件结构如下：

	├── node_modules                  // 模块安装依赖包
	├── public                        //公共文件，可以不用管
	│   ├── favicon.ico               //图标
	│   ├── index.html                //入口html
	│   ├── manifest.json             //manifest配置文件，指定应用名称、图标等信息
	├── src 						  //编写自己代码的存放文件
	│   ├── App.css                   //app的引用css文件
	│   ├── App.js					  //组件js文件
	│   ├── App.test.js               //测试文件
	│   ├── index.css                 //idnex引用的css文件
	│   └── index.js				  //页面入口文件
	│   ├── logo.svg                  //页面图片
	│   ├── serviceWorker.js          //加速程序运行文件
	├──.gitignore                     //提交到远程代码库时要忽略的文件
	├──package.json                   //用来声明项目的各种模块安装信息，脚本信息等
	├──package-lock.json              //用来锁定模块安装版本的，确保安装的模块版本一致
	├──README.md					  //盛放关于这个项目的说明文件 


### 2、启动项目

此时我们要验证一下项目能否运行成功，则在命令行窗口中输入

`cd react-router-redux-saga-demo`

进入到项目里面，再输入命令

`npm star`

后，在弹出的浏览器 `localhost://3000` 页面下能看到页面展示出来，如下图：

![react](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/react.jpg)

就说明项目能正常运行成功了。

### 3、安装Router、Redux和Saga插件

(1)、由于 `create-react-app` 没有集成 `router、redux、saga` 有关的插件，因此想要使用这些插件，首先我们要安装这三个有关的插件，分别为：

（1）router插件：`react-touter-dom`

（2）有关 `redux` 的插件：`redux`、`react-redux`

（3）saga插件： `redux-saga`

由于刚刚启动了项目，服务器在运行中，因此在安装插件之前先结束进程，具体操作是：在命令行窗口中按住 `ctrl+c` 键结束运行，然后在命令行中输入

`npm install react-touter-dom redux react-redux redux-saga --save-dev`

回车等待安装完成。

(2)安装完成后，打开 `package.json` 文件，我们会看到 `devDependencies` 多了刚安装的四个插件的名称及版本号信息，如图所示：

![package-json](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/package-json.jpg)

此时项目就可以使用 `router`、`redux`、`react-redux`、 `redux-saga` 这四个插件了。

### 4、使用Router的步骤

#### (1)、创建router组件

在 `src` 文件夹下创建一个名为 `components` 的文件夹，用来存放项目的自定义组件，在`components` 文件夹下创建三个 `js` 文件，分别为 `Home.js`、 `News.js`、 `MyRoter.js` 代码如下：

Home.js

	import React,{Component} from 'react';
	
	class Home extends Component{
		constructor(props) {
			super(props);
		}
	
		render() {
			return(
				<div>
					<h4>这是首页</h4>
				</div>
			)
		}
	}
	
	export default Home;




News.js
	
	import React,{Component} from 'react';
	
	class News extends Component{
		constructor(props) {
			super(props);
		}
	
		render() {
			return(
				<div>
					<h4>这是新闻页面</h4>
				</div>
			)
		}
	}
	
	export default News;




MyRouter.js

	import React,{Component} from 'react';
	
	import {BrowserRouter as Router,Link,Route} from 'react-router-dom';
	import Home from './Home';
	import News from './News';
	
	class MyRouter extends Component{
		constructor(props) {
			super(props);
		}
	
		render() {
			return(
				<Router>
					<div>
						<Link to='/'>首页</Link>
						<Link to='/news'>新闻</Link>
					</div>
					<Route exact path='/' component={Home} />
					<Route path='/news' component={News} />
				</Router>
			)
		}
	}
	
	export default MyRouter;

#### (2)、修改App.js

此时使用有 `router` 的组件已经创建成功了，这时我们需要在 `App` 主组件中挂载渲染我们的 `MyRoter` 组件，`App.js` 的代码如下：

	
App.js
	
	import React from 'react';
	import './App.css';
	import MyRouter from "./components/MyRouter";
	
	function App() {
	  return (
	    <div className="App">
	      <MyRouter />
	    </div>
	  );
	}
	
	export default App;

#### (3)、测试router页面跳转效果

这时我们需要在浏览器中查看我们编写的代码是否在页面上生效，重新启动项目，在命令行中输入

`npm start`

启动成功后在浏览器中 `localhost://3000` 中会看到新的页面，此时页面是这样的：

![home](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/router-home.jpg)

出现这样的页面就说明项目没有错误，达到了我们想要的效果，这时要验证一下点击链接时是否能进行页面跳转，当点击新闻链接的时候，页面展示的是新闻组件的内容，如下图:

![news](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/router-news.jpg)

点击首页链接，展示的是首页的内容，因此实现了页面的跳转了。



### 5、使用redux的步骤

下面我们以一个计数器为例，我们为了页面具有逻辑性，基于上面路由的跳转，我们想要页面加载完成的时候在首页 `Home.js` 组件中显示使用 `redux` 完成的计数器效果，具体操作如下：

#### (1)、修改Home.js

修改 `Home.js`，使得在 `Home.js` 中使用 `redux` 实现计数器效果，代码如下：

Home.js

	import React, { Component } from 'react';
	
	import { connect } from 'react-redux';
	import { increaseAction, decreaseAction } from '../actions.js';
	
	class Home extends Component {
		constructor(props) {
			super(props);
		}
	
		componentDidMount() {
		    console.log(this.props)
		} 
	
		render() {
			return(
				<div>
					<h2>这是计数器效果：</h2>
					<h2>{this.props.counter}</h2>
					<button onClick={this.props.increase}>增加</button>
					<button onClick={this.props.decrease}>减少</button>
				</div>
			) 
	    
	  	}
	}
	
	const mapStateToProps = (state) => {
		return {
			counter: state.counterReducer
		}
	}
	
	const mapDispatchToProps = (dispatch) => {
		return {
			increase: ()=>dispatch(increaseAction),
			decrease: ()=>dispatch(decreaseAction)
		}
	}
	
	export default connect(mapStateToProps,mapDispatchToProps)(Home);



因为要使用 `redux`，因此在 `Home.js` 文件头部引入 `connect` 方法。此时在 `Home.js` 文件的最后通过使用 `connect(mapStateToProps,mapDispatchToProps)(Home)` 方法，将 `store`和 `Home.js` 组件连接起来，并传入两个参数 `mapDispatchToProps` 和 `mapDispatchToProps`，使 `Home.js` 组件可以拿到 `store` 树上的 `state` 值以及 `dispath` 方法。

`Home.js` 的头部通过 `import { increaseAction, decreaseAction } from '../actions.js`语句引入 `increaseAction` 和 `decreaseAction`，`actions.js` 文件代码具体见下一步操作。


#### (2)、编写actions.js、reducer.js

在 `src` 文件夹下创建两个 `js` 文件，分别为 `actions.js` 和 `reducer.js`,具体代码如下：

actions.js
	
	export const increaseAction  = {
		type: "Add",
		data: 1
	}
	
	export const decreaseAction  = {
		type: "Sub",
		data: 1
	}




reducer.js

	import { increaseAction, decreaseAction } from './actions.js';

	const  counterReducer = (state = 0,action) => {
		switch(action.type) {
			case 'Add':
				return state + action.data;
			case 'Sub':
				return state - action.data;
			default:
				return state;
		}
	}

	export const rootReducer = combineReducers({
		counterReducer
	})
	
	export default rootReducer;

使用combineReducers()方法将多个reducer以对象的形式包含起来，实现了store树中只有一个根节点。

#### (3)、修改index.js

此时要将 `reducer` 处理返回的 `state` 值放入 `store` 树上，因此要修改 `index.js` 代码，具体代码如下：

index.js

	import React from 'react';
	import ReactDOM from 'react-dom';
	import './index.css';
	import App from './App';
	import * as serviceWorker from './serviceWorker';
	
	import rootReducer from './reducer';
	import { createStore } from 'redux';
	import { Provider } from 'react-redux';
	
	const store = createStore(rootReducer);
	
	ReactDOM.render(
		<Provider store={store}>
			<App />
		</Provider>, 
		document.getElementById('root')
	);
	
	serviceWorker.unregister();	

#### (4)、测试redux项目是否成功

到这里使用 `redux` 的步骤基本完成了，这时我们需要在浏览器中查看我们编写的代码是否在页面上生效，在浏览器 `localhost://3000` 页面中刷新一下，此时页面是这样的：

![redux](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/redux-home.jpg)

出现这样的页面就说明项目没有错误，达到了我们想要的效果，这时要验证一下点击**增加**按钮数值是否**加1**，点击**减少**按钮时数值是否**减1**，测试结果如下：

点击**增加**按钮：

![increase](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/redux-add.jpg)

点击**减少**按钮：

![decrease](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/redux-sub.jpg)

此时的页面效果可以说明了我们已经完成了 `react` 中结合了 `router` 和 `redux` 实现页面跳转和计数器的效果了。



### 6、使用saga的步骤

下面我们通过使用 `saga` 实现异步请求数据，想要在点击**新闻链接**的时候跳转要 `New.js` 组件并**点击获取数据按钮**来实现将异步请求回来的数据展现在页面上。

#### (1)、修改News.js

News.js

	import React, { Component } from 'react';
	
	import { connect } from 'react-redux';
	import { asyncAction } from '../actions.js';
	
	class News extends Component {
		constructor(props) {
			super(props);
		}
	
		componentDidMount() {
		    console.log(this.props)
		} 
	
		render() {
			return(
				<div>
					<h2>异步请求回来的数据：</h2>
					<button onClick={this.props.getdata}>点击获取数据</button>
					<ul>
						{
							this.props.dataArray.map((value,key) => {
								return (
									<li key={key}>
										{value.title}
									</li>
								)
							})
						}
					</ul>
				</div>
			) 
	    
	  	}
	}
	
	const mapStateToProps = (state) => {
		return {
			dataArray: state.asyncReducer
		}
	}
	
	const mapDispatchToProps = (dispatch) => {
		return {
			getdata: ()=>dispatch(asyncAction)
		}
	}
	
	export default connect(mapStateToProps,mapDispatchToProps)(News);



#### (2)、创建saga.js文件

首先在 `src` 文件夹下创建一个 `saga.js` 文件，用于编写 `saga` 异步操作的函数，具体代码如下：

saga.js

	import { takeEvery, call, put, all } from "redux-saga/effects";
	import { AsyncAction, getDataAction } from "./actions";
	import axios from 'axios';
	
	function* watchSaga() {
		yield takeEvery("AsyncData",workSaga);
	}
	
	function axiosData() {
		return  axios.get('https://jsonplaceholder.typicode.com/todos')
	}
	
	function* workSaga() {
		const data = yield call(axiosData);
		yield put(getDataAction(data.data));
	}
	
	export default function* rootSagaMiddle() {
		yield all([
			watchSaga()
		])
	}

`saga` 文件中使用到了 `axios` 发起异步请求，它是一个插件，因此在这之前要先安装 `axios` 这个插件，在命令行窗口中输入

`npm install axios --save-dev`

安装完后就可以在 `saga.js` 文件头部引用 `saga` 了， `takeEvery()` 用来监听所有 `dispath` 出来的 `action`，当 `action.type`  匹配时就触发 `workSaga` ,`call()` 用来发送指令，由 `saga` 中间件去执行获取异步数据请求操作，`put()` 用来派发一个 `action`，用于 `reducer` 接受 `action`，处理 `state`。


#### (3)、修改actions.js、reducer.js

在 `actions.js` 中新增两个 `action` 对象，并在 `reducer.js` 文件中新增对匹配`action.type` 的场景操作 `state`。代码如下：

actions.js
	
	export const increaseAction  = {
		type: "Add",
		data: 1
	}
	
	export const decreaseAction  = {
		type: "Sub",
		data: 1
	}
	
	export const asyncAction  = {
		type: "AsyncData"
	}
	
	export function getDataAction(data) {
		return {
			type: "GetData",
			data: data
		}
	}


reducer.js

	import { increaseAction, decreaseAction, getDataAction } from './actions.js';
	import { combineReducers } from "redux";
	
	const  counterReducer = (state = 0,action) => {
		switch(action.type) {
			case 'Add':
				return state + action.data;
			case 'Sub':
				return state - action.data;
			default:
				return state;
		}
	}
	
	const  asyncReducer = (state = [],action) => {
		switch(action.type) {
			case 'GetData':
				return action.data;
			default:
				return state;
		}
	}
	
	const rootReducer = combineReducers({
		counterReducer,
		asyncReducer
	})
	
	export default rootReducer;


#### (4)、修改index.js

此时使用到了 `saga` 中间件，并使 `saga` 运行起来，因此要修改 `index.js` 文件代码，具体代码如下：

index.js
	
	import React from 'react';
	import ReactDOM from 'react-dom';
	import App from './App';
	import * as serviceWorker from './serviceWorker';
	import { createStore,applyMiddleware} from "redux";
	import createSagaMiddleware from "redux-saga";
	import rootReducer from "./reducer.js";
	import { Provider } from "react-redux";
	import rootSagaMiddle from "./saga";
	
	const sagaMiddle = createSagaMiddleware();
	const store = createStore(
		rootReducer,
		applyMiddleware(sagaMiddle)
	);
	
	sagaMiddle.run(rootSagaMiddle);
	
	
	ReactDOM.render(
		<Provider store={store}>
			<App />
		</Provider>,
		document.getElementById('root')
	);
	
	serviceWorker.unregister();


#### (5)、测试saga项目是否成功

到这里使用 `saga` 的步骤基本完成了，这时我们需要在浏览器中查看我们编写的代码是否在页面上生效，因为需要刷新浏览器 `localhost://3000` 页面，此时页面是这样的：

![saga](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/redux-home.jpg)

当我们点击**新闻按钮**时会跳到**新闻页面**，此时的页面是这样的：

![saga](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/saga-news.jpg)

出现这样的页面就说明项目没有错误，达到了我们想要的效果，这时要验证一下点击**点击获取数据**按钮时，是否在页面中将异步数据展示出来，测试结果如下：

点击**点击获取数据**按钮：

![getdata](https://github.com/lijinping2017/react-router-redux-saga-demo/raw/master/reactStack-images/saga-getData.jpg)


好了，此时的页面效果可以说明了我们成功的实现了 `saga` 来获取异步数据的效果了。

### 7、总结
本节我们已经完成了基于 `create-react-app` 引入 `router`、`redux`、`saga` 技术栈的脚手架搭建，整个流程中使用到了 `router` 实现页面的跳转，并在组件中方便的实现了使用 `redux` 的`store` 树来获取数据并实现页面的更新，以及通过 `saga` 来实现以同步的方法处理异步获取数据的操作，整个`react` 技术栈在一个复杂的网站中就显得尤为的重要了。


