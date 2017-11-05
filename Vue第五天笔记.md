# 内容回顾

## 根据路由显示隐藏返回和Tabbar

	关键点:
		监控到路由的变化，watch--->$route
		
	显示/隐藏 返回按钮 v-show
	显示/隐藏 tabBar :class="xx?'':''"
	
## 评论子组件
	为什么要抽取

	抽取的步骤
		1、创建子组件(独立的组件，具有template,style,script)
		2、父组件集成子组件
		3、父组件传值给子组件
		
## 图片分享
	1、获取数据
	
	2、渲染页面
	
	3、优化样式

------------------

# 今日目标

## 图片预览

### 获取数据，展示出来
	1、使用vue-resource获取数据
	
	2、使用mui的九宫格布局

### 实现图片预览
	基于Vue:
		https://github.com/xLogic92/vue-picture-preview
		https://xiecg.github.io/other/vue-fancybox/#/baseUsage
		
### PhotoSwipe
	原生js写的，很多地方都可以用
		http://photoswipe.com/
		
### Vue-Preview
	集成
		安装 npm i vue-preview -S
		import VuePreview from 'vue-preview'
		Vue.use(VuePreview)
	
	使用
		 参考文档:https://github.com/LS1231/vue-preview

------------------

## 商品功能

### 商品列表
	1、获取数据
	
	2、渲染
	
### 商品详情
	1、跳转到商品详情
		1.1、创建一个商品详情组件
		1.2、在商品列表组件触发router-link
		1.3、在main.js中设置路由规则
	
	2、抽取轮播图
	
	3、渲染商品详情
	
	4、编程式导航
	
### 抽取轮播
	1、创建一个轮播子组件
	
	2、在home.vue、goodsinfo.vue中集成
	
	3、home.vue和goodsinfo.vue传递数据给轮播子组件，让轮播子组件做事情
		3.1、把首页需要轮播数据的url和商品详情中需要轮播数据的url当作参数传递过去即可
		
### 图文介绍
	1、监听图文按钮的点击
	
	2、通过编程式导航跳转到图文介绍组件，并且跳转过去的同时，把商品id带过去
		通过路由规则的设置才知道要跳转到哪个组件中去
	
	3、来到了图文介绍组件，拿着id发送网络请求
	
	4、渲染
	
	触发路由靠的是 命名路由的方式，传参是通过params

### 商品评论
	1、监听商品评论的点击
	
	2、通过编程式导航的方式，跳转到商品评论组件中去，并且要把商品的id带过去
	
	3、来到了商品评论组件，将我们的商品id传递给评论子组件
	
	触发路由靠的是 path的方式，传参是通过query
	
	关于究竟用哪种方式触发路由及哪种方式传参，根据实际业务来

------------------

## 加入购物车功能

### 数量子组件内部数据发生变化之后，告知父组件
	1、在商品详情父组件中集成数量选择子组件
		1.1、创建一个subnumber.vue
		1.2、集成到父组件中(goodsinfo.vue)
		1.3、实现subnumber内部的逻辑（界面和逻辑）
	
	2、当子组件中的值发生更改之后传递给父组件
		通过自定义事件 click dbclick
		
		
### 子组件传值给父组件
	1、子组件(发送发)，通过$emit触发自定义事件传值
		this.$emit('numberChange',this.count)
		
	2、父组件(接收方)，通过v-on:监听自定义事件，实现处理函数，接收到值
		注意：在监听事件的时候，我们处理函数，你写上函数名称即可
	
		<subnumber v-on:numberChange="getGoodsCount"></subnumber>
		
		getGoodsCount(count){
           console.log("---子组件传递过来的值---",count)
        }

------------------