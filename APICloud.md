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

- api对象和前端框架



