# forbid-wechat-share
禁止微信里的页面分享功能
```
|--src
|----|-assets
|------|-js
|--------|-hideShare.js
|----main.js
|--index.html
```

### index.html
```
<head>
  <script src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
</head>
```

### main.js
```
import './src/assets/js/hideShare'
```

### hideShare.js
```
import axios from 'axios'
axios({
  url: 'http://github.com/wanlixin?id=' + params,
  method: 'get'
}).then( res => {
  wx.config({
    appId: resp.data.appId, // 必填，公众号的唯一标识
    timestamp: resp.data.timestamp, // 必填，生成签名的时间戳
    nonceStr: resp.data.nonceStr, // 必填，生成签名的随机串
    signature: resp.data.signature,// 必填，签名
    jsApiList: [
        "onMenuShareTimeline",
        "onMenuShareAppMessage",
        "hideAllNonBaseMenuItem"
    ] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2
  });
  wx.ready(function () {
      wx.hideAllNonBaseMenuItem();
  });
  wx.error(function (err) {
      console.log('config失败' + err);
  });
}).catch( err => {
  //
})
```
 
