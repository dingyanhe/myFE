# 微信小程序商城开发--注意要点
来自[这里][yy_store]

### 收货地址
  微信提供了这个api:`wx.chooseAdress`,[在这里][api_choose_dress]
### 最多控制在10栈左右
  微信提供的这个api:`wx.navigateTo(OBJECT)`,[在这里][api_navigate-to]
### 页面传值
  方法有多种:
  
1.链接传值:微信提供了这个api:`wx.navigateTo(OBJECT)`,[在这里][api_navigate-to]
示例代码:
```javascript
wx.navigateTo({
  url: 'test?id=1'
})
```
```javascript
//test.js
Page({
  onLoad: function(option){
    console.log(option.query)
  }
})
```

2.本地存储:微信有提供这个api: 数据缓存,[在这里][api_storage]
示例代码:
```javascript
wx.setStorage({
  key:"key",
  data:"value"
})
```
```javascript
wx.getStorage({
  key: 'key',
  success: function(res) {
      console.log(res.data)
  } 
})
```


------------------------------
[yy_store]:http://www.wxapp-union.com/article-3101-1.html '微信小程序商城开发--注意要点'
[api_choose_dress]:https://developers.weixin.qq.com/miniprogram/dev/api/address.html#wxchooseaddressobject '微信官方api收货地址'
[api_navigate-to]:https://developers.weixin.qq.com/miniprogram/dev/api/ui-navigate.html '微信官方最多跳10栈页面'
[api_storage]:https://developers.weixin.qq.com/miniprogram/dev/api/data.html '微信数据缓存'
