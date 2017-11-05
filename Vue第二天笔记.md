# 内容回顾

## MVVM
	M：model
	V：View
	VM：View-Model 相当于控制器，起到调度的作用
	
	好处:
		耦合性低
		视图复用性强
		
## 指令
	通过指令可以让程序员较少对dom的操作，把关注点放在数据上
	
	v-text 插值表达式{{}} 纯文本
	v-html 可以解析html
	v-bind 绑定，html标签的属性值，不是写死的
	 v-bind: / :
	v-on 绑定事件 v-on: / @ click dbclick mousexxx
	v-if/v-show v-if/v-else 一定要挨着写
	v-for  (item,index) in 数组  key="唯一的值"

## 组件
	概念:功能代码的集合，组件就相当于可以看到的页面
	好处:把一些零散的代码封装起来，使用的时候，通过组件的名称使用
	
	五种
	前四种(看得懂就行，实际开发中一般推荐使用第五种)
		第一种:先定义，再注册，再使用
			var 组件 = Vue.extend({})  var 组件 = {}
			Vue.component('组件的名称',组件)
			id=app的div中，通过自定义标签的形式使用
				<组件的名称></组件的名称>
				
		第二种:定义注册一步到位，再使用
		
		第三种:对定义组件的时候，template属性优化
			<template id="templateId"></template>
			template:"#templateId"
			
		第四种:对定义组件的时候，template属性优化
			<script id="templateId" type="text/html">
			</script>
			template:"#templateId"
			
	第五种，单文件组件，不能直接运行在浏览器中，webpack通过loaders的形式，来转成浏览器能过执行的代码

## 过滤器
	对服务器返回的数据，进行过滤，把数据过滤成符合展示需求的数据
	
	私有
		定义在组件
		filters:{
			过滤器：函数，接收要过滤的原始数据，返回过滤之后的数据，要参数和返回值
		}
		
		特点:只能在该组件中使用
	
	全局
		Vue.filter('过滤器的名称',处理函数)
		处理函数中必须要有参数与返回值
		
	注意点:
		过滤器处理函数中的参数说明，第一个参数，就是要过滤的原始数据，第二个参数，就是调用过滤器的时候，传递的第一个参数

## 路由
	作用:
		根据触发的不同的路径，展示不同内容在浏览器中给用户看
		
	Angular
		html
			ng-vew
			<a></a>
			
		js
			模块.config
				路径
				templateUrl:''
				
	Vue
		html
			router-view
			<router-link to="/路径"> ===> a标签
		
		js
			1、定义组件
			
			2、创建路由对象，设置路由规则
				const router = new VueRouter({
					routes:[
						{path:'路径',component:'组件'}
					]
				})
				
			3、把router注入到根实例 
				new Vue({
					el:'#app',
					router
				})

## 发送网路请求
	vue-resource
		导入vue
		导入vue-resource
		
	GET：
		this.$http.get(url).then(function(response){
			
		},function(err){
			
		})
		
	POST：
		this.$http.post(url,{key:value,key1:value1},{emulateJSON:true}).then(function(response){
			
		},function(err){
			
		})
		
	JSONP：
		this.$http.jsonp(url).then(function(response){
			
		},function(err){
			
		})
	

-----------------------

# 今日内容目标

## Webpack

### 概念
	Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许
	多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还
	可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加
	载。通过 loader 的转换，任何形式的资源都可以视作模块，比如 
	CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、
	Coffeescript、 LESS 等。
	
	和Gulp比较
		Gulp 同步打包的方式 require("")
		
	优势:
		http://zhaoda.net/webpack-handbook/what-is-webpack.html
		
		保护源代码
	
	达到的理解程度
		1、webpack能打包我们的源代码，把我们所有的源代码最终打包成一个bundle.js
		2、很强大，使用任何模块组织的代码(CommonJS、AMD、ES6xxx)都能打包
		3、打包优化之后，就可以直接上线
	

### 核心概念
	
	入口:
		webpack打包的入口文件
	
	输出:
		这个就是对源代码打包之后，得到的文件，文件我们一般命名为bundle.js
	
	Loader:
		默认情况下，webpack只能打包.js结尾的文件，但是webpack提供了很多Loader，能打包项目中任何文件
	
	配置文件:
		简化我们的配置，让我们少写代码
	
	插件:
		比如压缩js,比如开发阶段实现的热重载,xxx
		为了让webpack更加强大
		
### 如何学习&查找Webpack资料
	入门:http://zhaoda.net/webpack-handbook/start.html
	
	官网:
		1.x https://webpack.github.io/
		2.x https://webpack.js.org/
	
	优化:百度搜索webpack优化

	出了问题:百度 www.stackoverflow.com
	

### 实际演练
	前提:
		安装好`webpack`全局包 npm i webpack -g

#### 打包单个.js文件
		步骤：
			1、切换到项目根目录
			2、使用webpack全局包打包即可
				webpack 入口文件(entry.js) 输出文件(bundle.js)
			3、打包得到bundle.js，建立index.html，在index.html
			中导入打包之后的bundle.js
			4、运行
			
		注意点:
			在index.html中导入的一定是打包之后的输出文件
	
#### 打包多个具有依赖关系的.js文件
		前提:
			写好entry.js中的代码，也写好module.js中的代码
			根据我们CommonJS来组织我们的代码的

		步骤：
			1、切换到项目根目录
			2、使用webpack全局包打包即可
				webpack 入口文件(entry.js) 输出文件(bundle.js)
			3、打包得到bundle.js，建立index.html，在index.html
			中导入打包之后的bundle.js
			4、运行
			
		注意点:
			在index.html中导入的一定是打包之后的输出文件
			Webpack 会分析入口文件，解析包含依赖关系的各个文件。
			这些文件（模块）都打包到 bundle.js 。

	
#### 打包非.js文件
	打包的步骤和上面一样，但是有注意事项
	
	Loaders:https://doc.webpack-china.org/loaders/
	
	以打包.css文件为例（需要额外做的步骤）	
		1、安装style-loader&css-loader
			cnpm i style-loader css-loader --save-dev
		2、在入口文件中导入css的时候，按照下面这样写
			require('!style-loader!css-loader!./site.css')
			
		3、针对第二步，如果导入的css过多，还可以做一个简化，在入口文件，导入的时候，可以不用写前面的
			require('./site.css')
			但是，在使用webpack打包的时候，得这样写
			webpack entry.js bundle.js --module-bind "css=style-loader!css-loader"
			
		注意点:
			"css=style-loader!css-loader" 使用双引号即可，不然会报错
	
#### 配置文件
	作用:简化打包的操作

	步骤:
		1、在项目根目录下创建一个文件名称叫 webpack.config.js的文件（默认文件名称）
		
		2、把我们原先在cmd中写的命令，全部写到webpack.config.js中(强烈建议大家拷贝)
		
		3、最后在根目录下，执行webpack即可打包了
	
#### 插件
	作用:让我们Webpack的功能更加强大
	
	全局包&本地包
		安装方式不一样 
			全局包 npm i webpack -g
			本地包 npm i webpack --save-dev
			
		使用的场合不一样
			全局包 用在终端里面，执行命令
			本地包 用在项目里面的
			
		安装的地方不一样:
			全局包:是安装在个人目录下	C:\Users\你自己的用户名\AppData\Roaming\npm
			
			本地包:项目的根目录的node_modules中
			
		注意点:
			有些包既要全局安装，又要在项目中安装，不要觉得奇怪，应用的地方不一样
			plugins在我们的webpack.config.js中写的时候，必须和entry,output,module同级
	
#### webpack打包的指令说明
	webpack --progress
	webpack --config 指定文件名称
	webpack --watch 监控源文件，只要发生了更改就可以自动打包【了解】
	wepack -p 压缩，局限性，自带的压缩里面对部分es6还是压缩不了，用webpack这个第三方中uglifyjs 【了解】
	
	如果以后发现在终端里面有很长的命令需要执行，可以把它写在package.json中的scripts里面，这个里面也是通过属性名称和值的方式来记录的，以后我们就可以在终端中 npm run 属性名称，他就会把属性名称对应的值，拿到终端中去执行
	
-----------------------

## 手动搭建项目结构

### 基本步骤
	1、把项目中的最基本的文件和文件夹建立起来
		src : 项目的源代码目录
		 |-- main.js 项目打包的入口文件
		 |-- App.vue 项目启动之后看到的第一个组件(根组件)
		 
		package.json: 项目的配置文件
		webpack.develop.config.js
	
	2、在我们浏览器中，看到一个Hello Vue
	
	3、实现我们项目的所见及所得(更改项目的源代码，能在浏览器看到效果)

### 在我们浏览器中，看到一个Hello Vue
	1、在App.vue template中写了 Hello Vue
	
	2、在webpack.develop.config.js中写了
		entry
		output
		
	3、main.js中写代码
		3.1 导入App.vue
		
		3.2 在我们的浏览器中要想看到App.vue中Hello Vue
			第一个.vue文件要被webpack打包，需要借助一个vue-loader的东西
				
			第二个，我们要想App.vue写的内容被浏览器识别，必须导入Vue
		
		3.3 导入vue
			import Vue from 'vue'
			创建一个根实例，里面要写两个属性
				el:Vue解析的范围
				render:决定把哪个组件挂在到id=app的div中去
				参考:https://cn.vuejs.org/v2/guide/render-function.html
				
	4、打包
		在webpack.develop.config.js中配置vue-loader
	
		webpack --config webpack.develop.config.js --progress
			bundle.js
			
	5、运行
		5.1 在项目根目录新建一个index.html
			id=app的div
		5.2 在index.html导入bundle.js
		

### 当我们更改了App.vue(项目启动之后，看到的第一个组件)之中的内容，在浏览器中实时看到其效果，并且是不刷新浏览器的情况下
	本地包 html-webpack-plugin
		代码写在 webpack.develop.config.js中的plugins里面
		作用:
			它是以一个参照html为模版，在浏览器的内存中，生成一个index.html，并且自动给我们导入在内存中生成bundle.js
			
			
		使用步骤:
			1、安装html-webpack-plugin webpack webpack-dev-server
			
			2、在项目的根目录下创建一个参照的html（template.html）
				 注意：参照文件只要写id=app的div即可，其它不要写
				 
			3、在webpack.develop.config.js中的plugins中写代码
				见webpack.develop.config.js

	全局包 webpack-dev-server 
		代码写在 终端
		它能把我们的项目的源代码打包成bundle.js（放在浏览器内存中的）
		
		运行项目，在内存中生成bundle.js并且把bundle.js插入到index.html中,并且最后运行index.html
		
		在终端里面生成的指令：https://webpack.github.io/docs/webpack-dev-server.html
		
		webpack-dev-server --progress --config webpack.develop.config.js --port 3008 --open --hot 
	
			
### webpack-dev-server & webpack
	相同点:
		都能对源代码打包，webpack-dev-server 很厉害，webpack能做的事，它都能做，并且还能做webpack不能做的事情，比如热更新
		webpack-dev-server & webpack 打包的指令和后面接的参数都是一样的 --progerss --config ...
		它们两个在打包的时候，都是全局包
		
	不同点:
		wepack-dev-server 开发阶段使用，打包出来的东西放在浏览器内存中，运行速度特别快
		
		webpack 生产阶段使用，会在文件夹中生成一个bundle.js，这个文件最终是要和index.html最终一起发布到服务器上面去

-----------------------

## 今日项目中用的包
	1、搭建项目时，在浏览器中想看到Hello Vue
		vue vue-loader vue-template-compiler style-loader css-loader
		
		vue:解析Vue指令和template标签
		vue-loader：加载和转译 Vue 组件
		vue-template-compiler style-loader css-loader 这几个都是vue-loader依赖的，所以必须安装，不然报错
		
		安装
			cnpm i vue --save
			cnpm i vue-loader vue-template-compiler style-loader css-loader --save-dev
			
	2、实现热更新的时候
		html-webpack-plugin webpack webpack-dev-server
		
		安装:
			cnpm i html-webpack-plugin webpack webpack-dev-server --save-dev
			
## vue-cli的使用
	https://github.com/vuejs/vue-cli
	
	安装:
		 npm install -g vue-cli
		 
	生成项目
		vue init webpack-simple my_vue
	
	运行
		cd my_vue
		npm install
		npm run dev
	
	