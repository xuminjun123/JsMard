# SDK 鉴权

　## 1. 公众号安全域名设置

- 打开微信公众平台。设置安全域名

  - 1. 公众号设置，在  《JS接口安全域名》 设置

    <img src="D:\typora\JSmark\SDK\1.png" alt="1" style="zoom: 50%;" />

  - 添加域名，下载 --->>>>第三步骤 中的 文件

  <img src="D:\typora\JSmark\SDK\2.png" alt="2" style="zoom:50%;" />

  ​	

  - 将 下载 的文件，放到 本地的 public 中（这是放在本地服务端的，微信服务器暂时不会收到，应该放到远程服务器 的，不然微信不会收到）
  - 点击保存，成功会添加域名。





- 微信公众平台，设置IP白名单。

  - 设置 --->>>  安全中心 ---->>>> IP 白名单

    <img src="D:\typora\JSmark\SDK\IP.png" alt="IP" style="zoom:38%;" />

  ##  

##  引入ＪＳ文件

- index.html 引入 wx.config

~~~javascript
wx.config({
    debug:true,
    appId:'', // 公众号唯一标识
    timestamp: '', // 生成签名时间戳
    nonceStr:'', //生成签名随机串
    signature:''，// 签名
    jsApiList:[]  // js 接口
})
~~~

签名规则不能带 “ #  ”号， 参与签名字段包括（noncestr  ）随机字符串。有效的时间戳 ，jsapi_ticket,timestamp(时间戳)，url(不带 url 及其后面参数 )

 例如：

![script](D:\C盘移动过来的文件\Desktop\SDK\script.png)





## 自己的服务器接入微信

- 进入微信工作平台，服务器配置

  - 开发 --->>> 基本配置 -------->>> 服务器配置

  ![serve](D:\typora\JSmark\SDK\serve.png)





- 这里 需要验证消息的确来自 微信服务器

<img src="D:\typora\JSmark\SDK\check.png" alt="check" style="zoom:50%;" />

	 	1. 后端写一个接口，包含签名，时间戳，随机串，随机字符串，还要排序，加密

例如 ： nodejs 

后台部分 ： 



<img src="D:\typora\JSmark\SDK\node7.png" alt="node7" style="zoom: 50%;" />



	- token 要一致，如图 ：

<img src="D:\typora\JSmark\SDK\token.png" alt="token" style="zoom: 50%;" />



## 鉴权所需要的 jsapi_ticket

- jsapi_ticket 是公众号调用微信JS接口的临时票据

  正常情况下有效期为 7200秒，通过access_token获取

  参数 ： {

  ​	greant_type: ''"",

  ​	appid:"",

  ​	secret:"''

  }

开发-->>> 基本配置---》公众号开发信息



- 前端调用接口获取access_token

  接口使用微信提供，如图

![access_token](D:\C盘移动过来的文件\Desktop\SDK\access_token.png)



例如 ：

![gettoken](D:\typora\JSmark\SDK\gettoken.png)



获取到access_token 之后获取JS-SDK 权限签名算法 

<img src="D:\typora\JSmark\SDK\auth_token.png" alt="auth_token" style="zoom:50%;" />

​	代码如： 获取ticket 

 nodejs 后台部分: 

![code](D:\C盘移动过来的文件\Desktop\SDK\code.png)

这个会返回 ticket







## 获取signature签名



- 获取所需参数

<img src="D:\typora\JSmark\SDK\sha.png" alt="sha" style="zoom: 67%;" />



- 规则 ：

<img src="D:\typora\JSmark\SDK\signature.png" alt="signature" style="zoom:67%;" />





生成

<img src="D:\typora\JSmark\SDK\处理.png" alt="处理" style="zoom: 50%;" />



<img src="D:\typora\JSmark\SDK\生成.png" alt="生成" style="zoom:50%;" />



全部 ： 

![sign](D:\typora\JSmark\SDK\sign.png)

module.export  = sign;



 -- obj 包含 appid  ,tiemstamp ,nonceStr, signature ,      ---jspList ,





