# 目录
- [微信小程序商城开发--注意要点](#微信小程序商城开发--注意要点)

- [审核发布的经验(别人的)](#小程序审核发布经验).

- [小程序40问?](#关于小程序的疑问)


## 微信小程序商城开发--注意要点
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
onReady: function(){
 wx.getStorage({
   key: 'key',
   success: function(res) {
       console.log(res.data)
   } 
 });
}
```

### request的请求数量限制了10个
 微信提供了说明看[这里][api_network]
```
// 发起请求后要
onLoad() {
 const req = wx.request({
  url: 'test.php', //仅为示例，并非真实的接口地址
  data: {
     x: '' ,
     y: ''
  },
  header: {
      'content-type': 'application/json' // 默认值
  },
  success: function(res) {
    console.log(res.data)
  }
});
// 销毁
onUnLoad() {
 req.abort(); // 取消请求任务
}
}
```

## 小程序审核发布经验

### 审核时间
小程序的审核在1小时到N天不等。官方说法是不超过7个工作日，一般在3日内会有结果。（但也有用户反馈超过7个工作日仍未审核。）
审核过程中可以撤回，但除非有严重Bug，不建议撤回。因为重新提交，可能需要重新“排队”。
周末、节假日，微信审核团队会安排少量同事值班。（运气好的话，周末提审，也可以很快通过。）
所以只要有一个可发布的版本，尽早提交审核。

### 注册小程序的主体
个人和企业均可注册小程序。
但是很多类目未对个人开放，限制太多。如果小程序的服务类目不在个人允许的范围内，建议想办法使用企业主体（如注册个体工商户）。

### 常见被拒绝情形

#### 诱导关注、诱导分享朋友圈
小程序拒绝之万能法宝1，凡涉及到关注公众号、分享到朋友圈，均可能封掉相应接口。对于“分享到朋友圈”，官方建议不要出现“朋友圈”字样，可改为“保存图片”。（实际上目前也只能保存图片到系统相册，然后再分享到朋友圈。）

#### 虚拟支付
小程序拒绝之万能法宝2，凡非实物销售均可列入此范围。如付费购买音视频内容、付费购买教育课程、付费升级会员等。

#### 未取得腾讯授权，不可以借助其他小程序或app实现自身功能
如优惠券、导购类小程序。官方的答复是“领取优惠券需要复制券地址前往淘宝才算真正领取成功，属于借助其他APP实现自身功能体验”。此类小程序很大概率会被审核不通过。

#### 需补充社交-笔记类目
涉及可编辑、转发的小程序，涉及用户自定义内容及分享的小程序。如果小程序名称中含有“社区”字样，而小程序内容并无社区产品，多半会要求提供社区相关资质，因此起名也要注意。

#### 需补充社交-社区/论坛类目
涉及UGC内容，可进行回复互动，如可发贴交流的小程序。

#### 需补充文娱-视频类目
涉及在线视频观看的小程序。

#### 可用性和完整性不符合规则
小程序无具体运营内容，无法正常体验小程序。很可能是程序Bug所致，新用户（或者审核人员）打开时，不显示内容或者内容过少。建议多测试，模拟新用户或者用新的微信账号测试。同时确保提交审核的版本，有一定内容，不要出现大块的空白。建议不要显示“即将上线”的字样，等开发好了再显示该功能。

#### 关于电商平台与商家自营类目
如果小程序涉及商家入驻，为商家提供开店服务，那么必须选择电商平台。

#### 无法被搜索
部分包含恶意或风险信息的小程序（如涉嫌混淆官方产品名称、色情低俗、欺诈等），可能不能被搜索出。如“郑州推拿按摩理疗”无法被搜索，但“郑州推拿”则可以。

#### 小程序实际所提供的服务属于尚未开放的服务类目
未开放的服务有很多。这里主要是指偏门的服务，如寺院（线上供佛）服务。

#### 小程序服务涉及可编辑、发布内容，属个人未开放类目
以个人为主体开发的小程序，目前限制太多，基本上只能做信息查询类小程序。

#### 涉及xxx，请补充xxx相关类目
但是在小程序后台设置中的服务类目已经添加了xxx类目。其实还需要在提交审核时，配置功能页面，选择相应的服务类目。可以多配置几个功能页面，将设置中的服务类目全部涵盖。

### 注意事项

多测试，减少 Bug 数量，杜绝严重 Bug。在审核周期较长的情况下，减少提交审核的次数；在审核周期较短的情况下，提高提交审核的次数。

不要和别人比。别人的类似小程序能上架，你的不一定能上，原因没有。开发者要做好心理准备。

申请附近的小程序，证件号码必须完全正确，包括字母的大小写。如易混淆的阿拉伯数字“0”与英文字母“O”。

同一时间提交的小程序，不一定同一时间审核。具体审核的顺序尚不明确。

前面几次审核通过，不代表下一次审核能通过，哪怕只是改了一个Bug。因为后续审核可能发现新的“违规”问题。

文娱、社交类小程序一般会进入二次审核，由当地主管部门（网信办）审核，时间一周左右（也有用户反馈等待1个月仍未审核）。如长时间（1个月以上）仍未审核，只能联系当地主管部门，或者考虑重新提交审核。

小程序中不要出现色情、低俗内容，否则被用户举报后，容易被暂停服务。

不要在提交审核的小程序中使用测试数据，如页面上存在明显的“测试”字样。

名称中含有特殊行业名词，若没有选择相应类目，很可能会被拒绝。如名称中有“保险”二字，会要求你提供保险行业的资质。特殊名称还有：社区。

涉及区块链、贷款、彩票（只能做彩票开奖结果查询，但容易被误判）、色情低俗、代购、网赚、优惠券的小程序，基本通不过。

服务类目，尽量在创建小程序时一次性选择全面。因为后面再增加服务类目，可能需要审核，审核时间不等。

不要在页面提供二维码，供用户下载 App，否则可能会被视为“诱导下载”。

红包类小程序必须选择“社交红包”类目，且需要“增值业务电信许可证”。

涉及到UGC（用户产生内容），最好建立审核机制与关键词屏蔽功能。

小程序审核通过后，应该尽早发布。如果审核通过后，未发布，此时再提交审核，之前审核通过后的版本可能会消失。

通过第三方平台提交代码，有提交数量的限制（7天内100个左右）。当接口返回 85085 submit audit reach limit, please try later hint，表示第三方平台近7天提交审核的小程序数量过多，请耐心等待审核完毕后再次提交。为此，一些第三方平台采用半自动提交。需要在小程序管理后台取消第三方授权，通过第三方平台上传代码，再到小程序管理后台手动提交审核。

### 技巧

#### 关于版本升级
后端至少需要兼容2个版本，线上版本和待提交审核的版本。小程序和后端同时发布，这样提审的小程序，可以正常使用。

提交审核后，点击撤回审核，会显示是否已进入审核系统。

若提交审核几天后仍然处在审核中，除发现重大 Bug 外，尽量不要撤回。既然已等待几天，不妨再等两天。一般七天内肯定会审核。

关于企业认证中给腾讯账号小额打款，腾讯公司的小额打款账号为招商银行25位账号，若不支持，则不要选择这种方式认证。

微信小程序官方邮件地址：MiniProgram@tencent.com （将#换成@）

## 关于小程序的疑问
- 为什么小程序开发不能使用window?
> 页面的脚本逻辑是在JsCore中运行，JsCore是一个没有窗口对象的环境，所以不能在脚本中使用window，也无法在脚本中操作组件.

- 为什么不能使用JQuery/Zepto
> 因为这两个库需要使用到window对象

- wx.navigateTo无法打开页面
> 一个应用最多只能打开10个页面,已经打开5个之后就不会再打开了.

- 如何修改窗口的背景色
> 使用 page 标签选择器，可以修改顶层节点的样式
```css
page {

display: block;

min-height: 100%;

background-color: red;

}
```

- 网络请求的 referer
> 网络请求的 referer 是不可以设置的，格式固定为 https://servicewechat.com/{appid}/{version}/page-frame.html，其中 {appid} 为小程序的 appid，{version} 为小程序的版本号，版本号为 0 表示为开发版。

- 不能直接操作 Page.data
> 避免在直接对 Page.data 进行赋值修改，请使用 Page.setData 进行操作才能将数据同步到页面中进行渲染怎么获取用户输入能够获取用户输入的组件，需要使用组件的属性bindchange将用户的输入内容同步到 AppService。
```javascript
<input id="myInput" bindchange="bindChange" /><checkbox id="myCheckbox" bindchange="bindChange" />
var inputContent = {}
Page({
 data: {
  inputContent: {}
 },
 bindChange: function(e) {
  inputContent[e.currentTarget.id] = e.detail.value
 }
})
```

- touchmove滑动事件里面的currentTarget. id值不变动。
> touchmove / touchend 事件的 target / currentTarget 会永远是 touchstart 时的 target / currentTarget 。

- wx.request的POST方法的参数传输服务器接收不到的bug。
> wx.request post 的 content-type 默认为 ‘application/json’.如果服务器没有用到 json 解释的话，可以把 content-type 设置回 urlencoded。
```javascript
wx.request({
 ....
 method: "POST",
 header: {
  "content-type": "application/x-www-form-urlencoded"
 },
 ...
})
```

- 小程序SVG支持吗?
> image的src放远程svg可以，background-image里也可以。

- wx.request返回statusCode两端类型不一致。
> 确实有这个问题，稍后的版本将会修复。

- 关于组件的动态生成与销毁？
> 不支持动态生成组件，但可以用 wx:for 去渲染多个。

- 小程序支持热更吗？
> 不支持开发者自行更替。

- 一些接口的回调IOS和Android不一致，例如支付接口，用户取消支付后，ios只回调complete方法，android则回调fail方法，官方文档也没有任何回调说明，造成开发很困难；类似的还有图片选择接口，分享接口等等。
> 支付接口，用户取消支付后，ios只回调complete方法，android则回调fail方法，问题已记录，多谢反馈。

- 如果icon已经在服务器上了，想用直接访问网址的方法加载图片进来这样可以吗？
> 不能。

- ipad不能使用小程序？
> 暂时不支持ipad打开小程序。

- 小程序音频，视频播放器问题 。1、能够只隐藏进度条跟时间吗？2、现在iOS平台上的时间显示是0:00，但是android上会显示错误码，能够通过什么设置修改吗？
> 1：下个版本会修改这里的交互，不显示进度条和时间。2：6.5.3 版本已修复此问题。

- 拍照窗口可以加浮层吗？
> 暂时不支持。

- 开发者工具经常报jsEngineScriptError错误，会导致页面白屏。
> 移步下载最新 0.12.130400 版本的开发工具试试

- 开发者工具里面，SPA页面，更改title无效。
> wx.setNavigationBarTitle可以通过 API 改变导航栏标题。

- 请问小程序页内支持长按保存图片或分享图片吗？
> 目前没有这个功能。

- 关于swiper中的current问题。如果在新的版本中，直接设current,会产生的效果是：无论从哪个swiper元素点击进去，都会显示swiper第一个子元素的值。
> 目前swiper在处理swiper-item动态变化的情况时有一些bug，会很快修复的。

- 小程序能引用自己服务器上的wxss和js文件吗？
> 不能，无法执行远程代码。

- 苹果7，提示内部错误，内存占用过多。
> 页面做的预加载，列表中有图片，图片渲染的太多了，解决办法就是不当屏展示的图片，不让它渲染。

- 小程序体验者安卓卡在加载页面进不去，IOS可以进去。
> 这是android微信客户端旧版本的bug， 请下载最新版本的 6.5.3 客户端。

- 强制使用https，开发和测试环境下怎么联调和测试？
> 「微信web开发者工具」->「项目」->「开发环境不校验请求域名及TLS版本」。

- wx.showToast()方法无效。
> 用wx.request请求网络然后在
```javascript
complete: function (res) {
 // complete
 wx.hideToast();
 }
}
```

- 在成功方法里面如果要进行showToast的时候感觉无效，并没有弹出提示框。
> success 回调调用是在 complete 之前的，如果在 success showToast，下一步 complete hideToast 就会被冲掉showToast。

- picker 组件中的文字大小是否支持修改？
> 不支持修改。

------------------------------
[yy_store]:http://www.wxapp-union.com/article-3101-1.html '微信小程序商城开发--注意要点'
[api_choose_dress]:https://developers.weixin.qq.com/miniprogram/dev/api/address.html#wxchooseaddressobject '微信官方api收货地址'
[api_navigate-to]:https://developers.weixin.qq.com/miniprogram/dev/api/ui-navigate.html '微信官方最多跳10栈页面'
[api_storage]:https://developers.weixin.qq.com/miniprogram/dev/api/data.html '微信数据缓存'
[api_network]:https://developers.weixin.qq.com/miniprogram/dev/api/api-network.html '微信api网络请求'

