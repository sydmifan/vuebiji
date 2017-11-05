# 课程介绍
	1天基础内容
	7天 webpack

## 第一天
	指令
	组件
	过滤器
	路由
	网络请求
	
## 第二天
	webpack
	搭建项目（手动）
	
### 第三天---第八天
	项目
	webpack打包压缩 上线

--------------------------

## Vue的基本概念

### Vue是什么?
	渐进式 JavaScript 框架
	
	特定:
		易用
		灵活 
		性能
		
	一个用以创建用户接口的直观、快速、简洁的 MVVM 框架
	
### Vue能做什么?
	PC端 管理系统 网站
	移动端
		WebApp 
		原生App 
		
### 如何学习?
	https://cn.vuejs.org/v2/guide/
	
	https://stackoverflow.com/
	
	https://segmentfault.com/p/1210000008583242/read?from=timeline
	
### 作者
	尤雨溪
	
--------------------------

## MVVM
	M:model 模型
	V:view 视图
	VM:view-model 相当于控制器
	
	v ---> vm ---> model
					|
	v <--- vm <---  |
	
	好处:
		1、解耦
		2、方便的复用
	
--------------------------

## 指令
	{{}} 插值表达式
	
	指令:
		拓展html的标签，先在html占位，在利用真实的数据替换
		让我们程序员只操作数据，即可更新视图
		
	注意:
		Vue中的指令是以v-开头的	
		
	v-text & v-html
		给我们页面中的span p标签设置值
		v-text 纯文本
		v-html 解析带有html标签的字符串
		
	v-bind
		在html中，比如img标签为例，src的值不写死，而是src的值来自model，这个时候就要使用v-bind了
		
		注意:以后我们视图中（img）需要的数据，必须来自model的时候，这个时候你就要想到v-bind
		
		`v-bind:` 可以简写成 `:`
	
	v-on 
		绑定事件
		
		ng-click Angular中给某个元素绑定一个点击事件，一般都是给button绑定
		
		注意点：
			1、当要执行的函数没有参数的时候，可以写`()`也可以不写，如果有参数必须加上`()`
			2、v-on:可以缩写成 `@`
		
	v-model
		双向数据绑定
			model ---> 视图
			视图 ---> model
		
	v-if/v-show
		v-if&v-show 接收的是boolean值
	
		区别:
			true的时候没啥区别
			false的时候有区别 
				if 不会创建元素
				show 会创建元素，但是隐藏起来
		
		开发中如何抉择?
			如果需要频繁切换（显示） show
			如果不需要频繁切换(显示) if
			
			参考：https://cn.vuejs.org/v2/guide/conditional.html
			
		注意点:
			v-if 后面接的v-else-if v-else必须紧跟v-if的后面，中间不要有任何其它元素，否则有问题
	
	v-for
		作用:
			遍历
			你要遍历什么，就作用于哪个元素上面
			
		注意：
			1、如果要获取我们遍历的每一行的索引
			2、在使用v-for遍历元素的时候，最好给每一行设置一个唯一的标识符，通过给遍历的每个元素设置一个唯一的key值即可
		
--------------------------

##	组件
	作用:
		某一类功能代码的集合
	
	在Vue中，你就可以认为，我们看到的每一个页面就是一个组件
	组件就是代码的集合，然后我们会把实现某一功能(展示新闻列表)的代码，写在某一个文件中，我们把这个文件就称之为组件
	
	在Vue中，凡是看到.vue结尾的文件，就是一个组件，组件里面就写了很多代码
	
### 写法
	前四种，都是在html里面写的(会，看得懂就行)
		第一种:
			先定义，再注册，再使用
			
		第二种:
			定义注册一步到位，再使用
		
		第三种:都是对组件中template的内容优化
			template
		
		第四种:都是对组件中template的内容优化
	
	最后一种，在.vue(单文件组件)结尾的文件中写的
		
		
	注意点:
		1、在定义我们组件，必须给它一个根元素
		2、在组件内部定义Model，data必须是一个函数，并且函数内部必须要返回一个对象 
			参考:https://cn.vuejs.org/v2/guide/components.html#data-必须是函数
		
	
	好处:
		1、可以把那些分散的功能，写在一个组件里面去，这样body中的代码比较少，并且看上去简洁明了
	
--------------------------

## 过滤器
	作用:
		过滤数据，一般是把服务器返回的数据，过滤成符合页面展示的数据
		
		
		
	私有过滤器
		只在该组件起作用
	
	全局过滤器
		所有的组件中都起作用
		
		Vue.filter('过滤器的名称',处理函数)
		
		
	注意点:
		1、过滤器是一个函数，必须要传入值，并且必须要有返回值
		
		2、最好把Vue.filter放在组件注册之前

--------------------------

## 路由
	作用:
		前端路由：根据触发的不同的路径规则，呈现不同的页面(组件)在浏览器中
		
	Angular
		html 
			ng-view 占位
			
		js
			$routerProvider.when('/路径',{
				templateUrl:'',
				controller:'xxx'
			})
			
	Vue和上面的差不多，写法参考下面
	
	前提:
		导入vue.js
		导入vue-router.js
		
	正式写代码:
		html
			router-link 触发的超链接，底层会转成a标签
			
			router-view 相当于ng-view
			
		js
			1、定义组件(不要注册)
			
			2、创建路由对象，设置路由规则（注册组件到路由中）
				目的:触发了谁，把谁展示出来
				
			3、把我们上面创建好的路由对象，注入到根实例 (new Vue({}))
			
### 路由的其它知识点
	1、想一上来就让它呈现某个组件的内容
		重定向:https://router.vuejs.org/zh-cn/essentials/redirect-and-alias.html
	
	
	2、通过路由跳转到某一个组件的时候，如何传递参数
		动态路由匹配:https://router.vuejs.org/zh-cn/essentials/dynamic-matching.html
		

--------------------------

## 网络请求
	vue-resource
	
	前提:
		导入vue.js
		导入vue-resource.js
	
### GET请求

### POST请求
	注意点:
		this.$http.post(url,参数,{emulateJSON:true})
		
		emulateJSON:true 设置请求头的Content-Type:application/x-www-form-urlencoded

### JSONP请求
	豆瓣
	jsonp方法

--------------------------