## 内容回顾

------------------

## 今日目标

### Vue项目打包上线

#### 步骤
	1、在项目的根目录，创建一个针对生产环境的配置文件webpack.publish.config.js
	
	2、在我们package.json的scripts标签中，添加一个pub的指令，指令的内容就是webpack --progress --config webpack.publish.config.js
	
	3、在我们的webpack.publish.config.js把开发阶段中的内容拷贝过来，并且进行修改，改成符合生产条件的代码
	
### html-webpack-plugin 说明
	开发阶段，在内存中生成一个index.html，并且配合webpack-dev-server一起用，并且会自动导入bundle.js
	
	生成阶段，他会在dist目录生成一个实实在在的index.html并且也会自动加上导入bundle.js的代码
	
### 优化的第一步
	压缩
		压缩bundle.js
			使用UglifyJS，但是要是用UglifyJS必须先把我们的代码从es6转成es5
		
		压缩index.html
		
### 压缩bundle.js的步骤(1.61M)
	1、必须先把我们项目的代码从es6转成es5
		使用babel来转换我们的es6代码
		参考:https://babeljs.io/docs/setup
		
		1.1、先安装包
			cnpm install --save-dev babel-loader babel-core babel-preset-env
			
		1.2、在webpack.publish.config.js中的loaders中添加一个配置
			{ test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
			
		1.3 在项目根目录下面创建一个.babelrc的配置文件，在里面设置好预设(preset)，能够使用什么样的预设转化百分之多少的es6代码
	
	2、在借助我们webpack内置的UglifyJS来压缩js
		参考:https://cn.vuejs.org/v2/guide/deployment.html
		
	注意：因为项目中使用了vue-prview，别忘记在loaders中给它配置一下，否则有问题
		{
            test: /vue-preview.src.*?js$/,
            loader: 'babel-loader'
        }
        
### 压缩index.html
	参考:https://github.com/jantimon/html-webpack-plugin
		https://github.com/kangax/html-minifier#options-quick-reference
		
### 优化的第二步
	拆分bundle.js，把一些内容从bundle.js剥离出来
	
	思考:
		1、图片，从bundle.js中剥离出去，放在一个专门的文件夹中
		2、把项目中用到的第三方的包从bundle.js中剥离出来，形成单独的js文件
		3、把css从bundle.js中剥离出来，提取到一个单独的css文件中
		
	建议:
		上面的三个内容的配置的代码比较多，能理解多少就理解多少，不明白的再看看文档，或是看看我的代码，工作中需要可以直接拷贝过去即可。
		
### 优化第二步之抽离图片
	参考:https://doc.webpack-china.org/loaders/url-loader
	
	可以给url-loader设置一个阀值
	loader: 'url-loader?limit=4000&name=images/[name]-[hash:5].[ext]'
	
### 优化第二步之抽离第三方包
	参考:https://doc.webpack-china.org/plugins/commons-chunk-plugin/
	
	步骤:
		1、更改入口文件
			以对象的形式配置，属性名称（打包出来的js文件名称）:值(第三方包的名称/自己项目源代码打包的入口main.js)
			
		2、更改输出文件
			output: { //项目打包之后的输出文件
		        path: path.join(__dirname,'dist'),
		        filename: 'js/[name].js'
		    }
		    
		3、在plugins中增加一个插件的配置
			new webpack.optimize.CommonsChunkPlugin({name:["vuePreview","moment","vueResource","quanjiatong","mintUi"],minChunks: Infinity})
			
### 优化第二步之抽离css
	参考:https://doc.webpack-china.org/plugins/extract-text-webpack-plugin/
	
	步骤:
		1、安装包
			cnpm i extract-text-webpack-plugin --save-dev
			
		2、导入
			const ExtractTextPlugin = require("extract-text-webpack-plugin")
			
		3、更改css-loader的配置
			{
                test: /\.css$/,
                use: ExtractTextPlugin.extract({
                    fallback: "style-loader",
                    use: "css-loader"
                })
            }
            
        4、在plugins中新增一个配置即可
        	new ExtractTextPlugin("css/styles.css")
	
### 额外补充，打包之前干掉dist目录
	clean-webpack-plugin
	使用:https://github.com/johnagan/clean-webpack-plugin
	
### 浏览器出现缓存的原因
	请求方式为GET
	url没有变化

------------------

### 微信小程序
	运行在`微信`里面的一种小程序
	
	原生的App
	
	基于微信平台
	
	步骤:
		1、注册&填写信息
		
		2、开发
		
		3、发布
		
### 开发者工具
	https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html
	

	App.json 
		https://mp.weixin.qq.com/debug/wxadoc/dev/framework/config.html

------------------

React-Native