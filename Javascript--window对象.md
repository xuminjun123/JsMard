# Window 对象

## 1. 自身方法



- `open`: 打开一个新窗口

  参数 ：window.open("页面路径（必填）" ， "打开目标（``_self` 、`_blank`）" ， "配置")

  ~~~javascript
  window.open("https://baidu.com","_blank");
  
  // 第三个参数使用
  window.open("https://baidu.com",null,"width=200;height=200");
  ~~~

  

- `alert`: 网页弹窗

- `confirm`: 确定弹窗

- `prompt` ：

.....

## 2. 对象属性

- `location`: 地址栏对象
  - href ：返回 URL 锚部分
  - hash : 返回 hash部分
  - host ：返回主机名和端口
  - hostname：返回主机名
  - port：返回端口
  - replace ：
  - reload : 刷新当前页面
  - search： 返回一个 URL 查询部分
  
- `navigator`:  浏览器相关 （名称、版本....）【返回的假的信息】，没什么用的api
- `history`: 历史记录 【只能获取当前网页的历史记录】
  - go：前进、后退
  - back ：后退
  - forword ：前进
- `console`:
  - log :打印内容
  - valueOf: 打印dom
  - dir ：打印对象结果
  - time : 