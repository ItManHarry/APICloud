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

- APICloud五大组件

- api对象和前端框架



