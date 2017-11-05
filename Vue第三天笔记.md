# 内容回顾

## Webpack基本使用

### 能做什么?
	构建项目，可以把所有的模块(CommonJS AMD ES6)都当作模块来处理
	
### 核心概念
	入口
		入口文件导入其它文件
		
	输出
		最终打包之后的一个结果(html,css,js,静态资源)
		
	Loaders
		能打包除js的静态资源
		
	配置文件
		默认是 webpack.config.js
		
	Plugins
		插件，让Webpack的功能更加的强大
		
### 基本用户
	1、打包当个js文件 webpack 入口.js 输出.js
	2、打包多个有依赖关系的文件  webpack 入口.js 输出.js
	3、打包.css文件 webpack 入口.js 输出.js --bind xxx
	4、配置文件  webpack
	5、插件的使用 

-------------------

## 搭建项目

### Hello Vue
	1、创建必要的文件和文件夹
	
	2、App.vue写代码
	
	3、main.js中写代码
	
	4、在webpack.develop.config.js的Loader中配置对vue的支持
		
	5、使用webpack打包
		webpack --config webpack.develop.config.js
		
	6、自己在根目录下创建index.html手动导入bundle.js
		注意：一定要加一个id=app的div


### 实现热更新
	一个全局包 webpack-dev-server
		作用:打包源代码，在浏览器内存中生成一个bundle.js
		
	一个本地包 html-webpack-plugin
		作用:以一个参照文件为模版，在内存中生成一个index.html
			模版文件中写id=app的div，不要写导入script
			
-------------------

# 课程目标

## vue-cli【了解】
	作用，快速构建项目
	
	使用步骤:
		安装全局包 npm install -g vue-cli
		
		生成项目 
		
		运行项目

## App.vue
	这个启动项目之后看到的第一个组件
	
	结构
		Header
			mint-ui
		
		中间动态变化
			vue-router
			
		TabBar
			mint-ui
			
### mint-ui
	概念:
		mint-ui是一个基于Vue的`移动端`的UI类库
		`PC端`:http://element.eleme.io/#/zh-CN/component/installation
	
	官网:https://mint-ui.github.io/#!/zh-cn
	
	
	文档说明:
		js components 用在.vue组件的script标签里面的，这个第三大部分的组件使用的时候需要导入
		
		css components&form component 用在.vue文件的template里面的，注意，如果你在入口文件中集成了，在每个.vue组件的template中直接用就行了
	
	步骤:
		1、集成	
			1.1、安装第三方包
				npm install mint-ui -S/--save
				
			1.2、在main.js中写代码集成到项目中
				import Mint from 'mint-ui'
				Vue.use(Mint)
		
		2、在需要的地方使用
			App.vue
				<mt-header fixed title="买买买"></mt-header>
				
			发现样式没有，我们导入样式import 'mint-ui/lib/style.css'，注意，需要添加对css的支持
			
### vue-router
	1、集成
		1.1 安装
			npm i vue-router -S
		
		1.2 在main.js中集成
			import VueRouter from 'vue-router'
			Vue.use(VueRouter)
	
	2、使用
		html
			router-view 占位
			router-link 触发超链接
		
		js
			1、创建组件，在main中导入
			2、创建路由对象设置路由规则
			3、把路由对象注入到根实例中
	
---------------------

## 首页组件

### 轮播图
	步骤:
		1、发送网络请求，获取数据
			vue-resource
			$.ajax
			xxx XMLRequest
			
			集成vue-resource
				装包
				在main.js中集成
				
			使用vue-resource
				在home.vue的script标签里面使用
		
		
		2、找个轮播的组件，给他数据，让其轮起来
			https://mint-ui.github.io/docs/#/zh-cn2/swipe

### 九宫格导航
	1、集成mui
		1.1、把我们的mui的源文件拷贝到statics目录下面去
		1.2、在main.js中导入mui.css即可
		
		注意：因为mui.css又导入了fonts.ttf，所以需要安装file-loader&url-loader来处理
	
	
	2、使用
		
	
---------------------

## 新闻列表&新闻详情

### 新闻列表
	1、跳转到新闻列表组件
		1.1、创建newslist.vue
		1.2、在main.js中写代码
			导入
			设置路由规则
		1.3、在home的九宫格中触发它
			router-link
	
	2、发送网络请求
	
	3、渲染组件
	
### momentjs
	网址:http://momentjs.cn/
	
	集成
		安装	 npm i moment -S
		导入 import moment from 'moment'
		
### 新闻列表中对时间的处理
	moment + 全局过滤器

### 新闻详情
	1、跳转到新闻详情
	
	2、发送网路请求
	
	3、渲染组件

--------------------

## 其它

 	main.js中有根实例 (Vue对象)
 	
 	home.vue 通过export default {}(Vue对象)
 	
 	
 	区别:
 		作用不同:
	 		main.js的Vue对象，决定把组件内容显示到页面的哪个地方(el决定)，最先把哪个组件展示出来(render)
	 		
	 		home.vue(每个组件中的)，为自己组件内部的template服务的
	 		
	 	生命周期不同:
	 		main.js中的Vue对象，生命周期和应用程序是一样
	 		
	 		home.vue只要不再浏览器上面展示了，它就挂了

--------------------

## 我们今日安装的第三方包

	1、在搭建App.vue的头部和TabBar的时候要用到
		mint-ui
		安装方式:
			npm install mint-ui -S
			
	2、在进行中间内容切换的时候，需要用到vue-router
		安装方式:
			npm install vue-router -S
			
	3、在发送网络请求要用到的第三方包，vue-resource
		安装方式:
			npm installl vue-resource -S
			
	4、在集成mui的时候，导入字体文件，这个时候需要用到file-loader&url-loader
		安装方式:
			npm install file-loader url-loader --save-dev
			
	5、在新闻列表&新闻详情中格式化日期，使用moment
		安装方式：
			npm install moment -S

--------------------