# APICloud 学习笔记

## Chapter 1  - APICloud App开发流程

- 查看APICloud的API文档
	
		地址：https://docs.apicloud.com/
		
- 扩展API调用方式

```
	//核心API在window.api对象下，可以直接调用
	api.methodName(param, callback)
	//扩展模块需要require导入，遵守CommonJS规范
	var module = api.require('moduleName')
	module.methodName(param, callback)
	
	param:{} 									//参数，是一个JSON对象
	callback：function(ret, err){}		//回调函数，是一个Function对象，异步调用的结果通过此函数返回
```

- 开发者工具 - APICloud Studio2

- 移动端真机测试软件：AppLoader （官方下载地址：https://docs.apicloud.com/Download/download）

## Chapter 2 - App整体框架，完成App静态页面开发

- APICloud App启动过程，了解config.xml配置文件

	APICloud引擎初始化时会创建两个UI组件实例，分别是Widget和Window。Widget是APICloud App运行时的最小单位，就是说APICloud App想要运行必须
至少有一个Widget。一般来说一个App有一个Widget就足够了，此时可以把Widget当做App本身。之后Widget会创建一个根Window对象（Root Window），这个
Window会装载一个HTML页面也就是应用打开的第一个页面，这个HTML页面可以通过config.xml配置打开&lt;content src = "index.html"/&gt;这一行。

	config.xml配置文件：配置App相关重要的配置信息。

	APICloud引擎初始化完成后会发出两个重要的事件：
	
	1. content事件：读取config.xml配置，打开App默认页面
	
	2. apiready事件：这个事件是api对象准备完成后产生的
	
```javascript
	<script type = "text/javascript">
		apiready = function(){
			//TO DO
		}
	</script>
```

- APICloud五大组件

	1. Widget
	
	2. Layout
	
	3. Window

	4. Frame
	
	5. UIModule
	
	首先是Widget，Widget当中可以包含Layout、Window和UIModule；在Window中，可以包含Layout、Frame和UIModule；Layout中可以包含Window和Frame；
	Frame中只能包含UIModule
	
- api对象和前端框架

	开启状态栏沉浸模式
	
	1. config.xml配置
	
```xml
	<preference name="statusBarAppearance" value="true"/>
```
	2. 页面元素使用$api.fixStatusBar().
	
```javascript
	//设置页面顶部元素沉浸
	$api.fixStatusBar( $api.byId('header') );
	//设置状态栏样式
    api.setStatusBarStyle({
		style: 'dark',
		color: '#fff'
	});
```

	优化点击事件和tapmode
	
	在点击发生的元素上添加tapmode属性

```html
	<div tapmode onclick = "goBack()">Back</div>
```
	如果动态创建了包含tapmode的元素，之后需要调用以下代码使之生效
	
```
	api.parseTapmode()
```

	tapmode支持赋值CSS样式及动态改变元素样式，实现Native的点击效果
	
```html
	<div tapmode = "btn-press" class = "btn" onclick = "goBack()">Back</div>
```

## Chapter 3 - APICloud和服务器通讯

```javascript
	api.ajax({
		url: 'http://10.40.120.136:3000/doc/biz/catalog/tree',
		method: 'get',
		data: {
			values: {

			},
			files: {

			}
		}
	},function(ret, err){
	  if(ret){
		console.log("Status is : "+ret.status)
		console.log("Message is : "+ret.message)
		console.log($api.jsonToStr(ret))
	  }

	});
```

## Chapter 4 - 加载更新服务端数据，实现本地的数据存储

- doT模板引擎

```html
	<!DOCTYPE html>
	  <html>
	  <head>
		  <meta charset="utf-8">
		  <meta name="viewport" content="maximum-scale=1.0,minimum-scale=1.0,user-scalable=0,width=device-width,initial-scale=1.0"/>
		  <title>title</title>
		  <link rel="stylesheet" type="text/css" href="../css/api.css"/>
		  <style>

		  </style>
	  </head>
	  <body>
		<script type="text/template" id = "dotTemplate">
		  {{~ it:user:index}}
			{{? user.deleted !== true}}
			  <div>{{= index + 1}}</div>
			  <div>{{= user.name}}</div>
			  <hr>
			{{?}}
		  {{~}}
		</script>
	  </body>
	  <script type="text/javascript" src="../script/api.js"></script>
	  <script type="text/javascript" src="../script/doT.min.js"></script>
	  <script type="text/javascript">
		var users = [
		  {name:"Sam"},
		  {name:"Jack",deleted:true},
		  {name:"Harry"},
		  {name:"Tom"}
		]
		var ts = document.getElementById("dotTemplate").innerHTML;
		var ft = doT.template(ts);
		ts = ft(users)
		document.body.innerHTML = ts
		  apiready = function(){

		  };
	  </script>
	  </html>
```

- 本地存储和图片缓存

- 下拉刷新、上拉加载

- 理解APICloud应用沙箱机制

- APICloud资源访问协议使用

- 常用对话窗口

- APICloud平台的事件机制
