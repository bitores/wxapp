#小程序知识点

[API文档](https://mp.weixin.qq.com/debug/wxadoc/dev/api/?t=20161107)

[组件属性](https://mp.weixin.qq.com/debug/wxadoc/dev/component/swiper.html?t=20161107)

[在线演示](https://weui.io)

[下载地址](https://github.com/weui/weui)

###小结
  
  	0、文件导入
  		<import src="../a.wxml"/>
  		<include src="../a.wxml"/>
  		import "../common.wxss";
	1、规定屏幕宽度rpx(df750rpx), rem(20rem)
	2、内联样式影响渲染速度
	3、可使用模板template片段
		定义模板
		<template name="msgItem">
		  <view>
		    <text> {{index}}: {{msg}} </text>
		  </view>
		</template>
		使用 is 导入模板, data 传入数据
		<template is="msgItem" data="{{...item}}"/>


	4、App生命周期：onLaunch|onShow|onHide|...自定义
		other.js
		var appInstance = getApp()
		console.log(appInstance.globalData)
	4.1、不要在App()中使用 getApp()
	4.2、不要在 onLaunch 的时候调用 getCurrentPage()
	4.3、不要在其它地方调用 app的生命周期函数

	5、Page生命周期：onLoad|onReady|onShow|onHide|onUnload|...自定义
	6、扩展事件：onPullDownRefresh(下拉-触发)、onReachBottom(上拉-触底)
	7、事件绑定：1.组件事件绑定函数如bindtap="tabName" 2.在Page中定义如tabName
	8、view不仅作为组件、也可作为变量
	9、几乎所有组件都有各自定义的属性
	10、data-参数： 小写 e.target.dataset.*
	11、wx:for 循环数据，下标index,值item
	12、wx:if 切换高消耗 ，hidden初始化高消耗



###组件

	1、小写：所有组件及属性
	2、- ：连字符
	3、组件共同属性： id | class | style | hidden | data-* | bind*/catch*
	3.1、样式共同属性：#id | .class | element | element,element | ::after | ::before
	4、组件分类
	4.1、视图窗器 view/scroll-view/swiper
	4.2、基础 icon/text/progress
	4.3、表单组件 button/checkbox/form/input/label/picker/radio-group/radio/slider/switch/textarea


###代码


**route** 

	> 页面打开、重定向、返回
	wx.redirectTo|wx.navigateTo({
		url:"test?id=1"
		[,success:func,fail:func,complete:func]
	})

	wx.navigateBack({
		delta:1 // getCurrentPages()
	})

	storage-10M
	wx.setStorageSync(key,data)
	wx.setStorage({
		key:"key",
		data:"value"
		[,success:func,fail:func,complete:func]
		
	})


	var res = wx.getStorageInfoSync();
	wx.getStorageInfo({
		success:function({keys:[],currentSize:1024,limitSize:2048})
		[,fail:func,complete:func]
	})

	var res = wx.getStorageSync(key)
	wx.getStorage({
		key:"key",
		success:function({data:"value"})
		[,fail:func,complete:func]
	})


	wx.removeStorageSync(key)
	wx.removeStorage({
		key:"key",
		success:function({data:"value"})
		[,fail:func,complete:func]
	})

	wx.clearStorageSync()
	wx.clearStorage();

	try{//Sync...}catch(e){}


**toast**

	wx.hideToast()
	wx.showToast({
		title:""
		[,icon:"success|loading",duration:1000,success:func,fail:func,complete:func]
	})

	wx.showModal({
		title:"",
		content:""
		[,showCancel:true|false,cancelText:"",confirmText:"",cancelColor:"#000000",confirmColor:"#000000",success:func,fail:func,complete:func]
	})

	wx.showActionSheet({
		itemList:["",""]
		[,itemColor:"#000000",success:function({cancel:true|false,tapIndex:\d}),fail:func,complete:func]
	})


**Image**

	wx.chooseImage({
		success:function({tempFilePaths:[]}),
		[,fail:func,complete:func,count:9,sizeType:["original|compressed"],sourceType:["album|camera"]]
	})
	wx.previewImage({
		urls:[""]
		[,success:func,fail:func,complete:func,current:"urls[0]"]
	})

	wx.getImageInfo({
		src:""
		[,success:function({width:0,height:0}),fail:func,complete:func]
	})

	telephone
	wx.makePhoneCall({
		phoneNumber:""
		[,success:func,fail:func,complete:func]
	})

	File



**login**

	wx.login({
		[success:function({errMsg:"",code:"有效期五分钟"}),fail:func,complete:func]
	})

	请求
	wx.request({
		url:""
		[,success:func,fail:Func,complete:Func,method:"GET|POST...",data:""|{},header:{}]
	})

	webSocket
	wx.connectSocket({
		url:""
		[,success:func,fail:Func,complete:Func,method:"GET|POST...",data:{},header:{}]
	})

	wx.onSocketOpen(callback)
	wx.onSocketError(callback)
	wx.onSocketMessage(callback)
	wx.sendSocketMessage({
		data:""|[]
		[,success:Func, fail:func, complete:Func]
	})
	wx.closeSocket()
	wx.onSocketClose(callback)





