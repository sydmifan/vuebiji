# 内容回顾

## 生命周期
	beforeCreate
	beforeDestory 
	
	注意:
		生命周期钩子是Vue提供的，我们程序员只需要实现相应的生命周期钩子即可，在生命周期钩子，写上自己的业务逻辑即可，这样的话，Vue就会在恰当的时机调用并且执行我们缩写的代码

## 非父子组件传值
	1、搞一个公共的vue对象 bus
	
	2、在传值方，通过bus.$emit('xxx',{name:'xxx',count:10})触发事件
	
	3、在接收方，通过bus.$on('xxx',function(count){
				   })
		注意:事件只需要注册一次


## Vuex
	概念
	
### 五大核心概念
	State 状态(数据)
	Getters 从State中获取数据
	Mutations 同步的方式对State中的数据进行更改
	Actions 异步的方式对State中的数据进行更改
		注意：这个得借助Mutations中的方法进行更改
		
	Modules 创建多个仓库
	
### 代码
	1、集成Vuex
		安装
		导入
		使用
	
	2、在项目中使用
		2.1 创建了空仓库
		2.2 别忘记注入进来
		2.3 写store中的代码
			state :{goodsList:[]},
			mutations : {
				函数
			}
			actions:{
			}
			getters:{
			}

-------------------------

# 今日目标

## 各大电商购物车数据如何存储
	Vuex 内存存储机制
	
	京东:
		没有登录的时候，默认在本地 cookies
			优势:减少服务器资源消耗，充分利用用户浏览器的资源
			
			缺点:可能会流失客户
		
		登录之后 存在服务器
		
	淘宝:
		都是存在服务器
		
		优点:客户的流失率可能会小一些
		缺点:消耗服务器资源
			
		
## 购物车
	[
		{goodsId:"87",count:2},{goodsId:"88",count:3},
		{goodsId:"87",count:3}
	]

### 购物车代码思路分析
	1、获得数据
	
		[
			{goodsId:"87",count:2},{goodsId:"88",count:3},
			{goodsId:"87",count:3}
		]
		
		===> 目标
		[
			{goodsId:"87",count:5,title:'xxx'},
			{goodsId:"88",count:3,title:'xxx'}
		]
		
			1.1、把存在Vuex中的数组，转化成对象
				[
					{goodsId:"87",count:2},{goodsId:"88",count:3},
					{goodsId:"87",count:3}
				]
			
				===> var tempObj = {"87":5,"88":3}
				
			1.2、遍历对象，把key放入到一个数组中
			
				===> ["87","88"]
			
			1.3 把数组中的商品id,给他整成符合后台要求的字符串参数
			
				===> 87,88
				
			1.4 发送请求，请求回来之后，给我们每个商品动态加上count
			
				[
				{goodsId:"87",count:tempObj["87"],title:'xxx'},
				{goodsId:"88",count:tempObj["88"],title:'xxx'}
				]
	
	2、展示商品列表
		2.1、展示购物车列表
		2.2、展示提示信息
	
	3、购物车里面操作的业务逻辑
		1、开关发生变化的时候
			统计信息(抽取公共的方法)
			删除按钮样式的变化
			
		2、删除按钮的删除操作
			Vuex中的对应的数据要干掉
			购物车中对应的数据要删除掉
			统计信息(抽取公共的方法)
			App.vue中徽标的值要发生变化

-------------------------

## 以后工作中遇到问题如何去做

	特别是你初步的时候，看起来很难的功能
	1、先把整体功能做一个区分
	
	2、再对各个功能各个击破
	
## 支付流程的体验(以美团买汉堡包用支付宝支付为例)
	1、登录
	
	2、提交订单
		在后台数据库中生成一条该用户买的商品的记录
			 id        name          price pay_status
	 		zni763   汉堡王猪肘子     39.9   0
	 		
	 		
	 		
	 https://mclient.alipay.com/home/exterfaceAssign.htm?alipay_exterface_invoke_assign_client_ip=47.74.9.76&body=%E7%BE%8E%E5%9B%A2%E8%AE%A2%E5%8D%95-124231929078451505985191&subject=%E7%BE%8E%E5%9B%A2%E8%AE%A2%E5%8D%95-124231929078451505985191&sign_type=RSA&notify_url=http%3A%2F%2F10.53.86.13%3A8966%2Fpaygate%2Fnotify%2Falipay%2Fpaynotify%2Fwap&out_trade_no=124231929078451505985191&return_url=http%3A%2F%2Fmeishi.meituan.com%2Fi%2Forder%2Fresult%2F3948233345&sign=PcXeDQ7r4AVP1Fbz8pvKcS%2Bvkoppr8uvr6sw5wO6aXJjAnRCNhKtym%2FGmrCW%2Fo8quf3I8758hlg6fH2cAkbu0tGNPxMtUba2WrAtJ5dvap7apRodhT2XqFm7Xc4aA%2BS9P3%2Fa90nZiu0WbMZn4B%2FMREABb7CaRasrLbQJq%2BODQag%3D&_input_charset=utf-8&enable_paymethod=balance%2CcreditCardExpress%2CdebitCardExpress%2CmoneyFund&it_b_pay=1440m&alipay_exterface_invoke_assign_target=mapi_direct_trade.htm&alipay_exterface_invoke_assign_model=cashier&total_fee=15&service=alipay.wap.create.direct.pay.by.user&seller_id=2088311465207164&partner=2088311465207164&alipay_exterface_invoke_assign_sign=_z_r2k6a8_u_lt_ko_fp_q_ywdcji_s_if_y_e_q_tbehn6_g_v_rk_mxwj4k9_k5jb_ns_ftxg%3D%3D&payment_type=1
	 
### 有哪些人参与
	公司老板&财务
		前提准备  营业执照、纳税证明和支付宝签约，成为他的合作商户
		支付宝审核通过之后，会给你颁发一个唯一的标识符
		
		美团:
			2088311465207164
	
	前台(前端、iOS、Android)
		让用户选择商品，购买
		
		1、提交订单
			让后台记住这个订单 
			
		4、当用户选择了支付方式之后，发送请求给后台
			让后台返回给我对应平台的一些支付的加密信息
			
		6、浏览器接收到了支付宝那一大堆加密的信息之后，window.location.href = ""
	
	后台
		
		2、在后台数据库中记录该订单信息
			id        name          price  pay_status
	 		zni763   汉堡王猪肘子     39.9      1
	 		
	 	3、把选择支付方式的页面返回给浏览器，让用户能看到
	 	
	 	
	 	5、在后台生成有关支付宝的加密信息
	 		https://mclient.alipay.com/home/exterfaceAssign.htm?alipay_exterface_invoke_assign_client，把这一大堆信息返回给浏览器
	 		
	 	7、当用户支付成功之后，支付宝服务器，会发送请求给美团后台，这样，后台接收到请求之后，就会把，最刚开始生成的订单的状态，更改为已支付