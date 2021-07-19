# 优化

## 首页 打包优化

1. nginx 开启 gzip 

2. 使用Vue CLI 自带的webpack 包体积优化工具，他可以查看各个模块的size大小，

   只需要在build 后面加上 -- report 参数 即可，我们把命令配置到pageage.json 里面，方便 `npm run report` 打包生成report ,

   -  网上说的 先安装 webpack-bundle-analyzer 包 ，其实不需要安装

   示例 ：

   ~~~js
     "scripts": {
       "serve": "vue-cli-service serve",
       "build": "vue-cli-service build",
      	// 加入这一行
       "report":"vue-cli-service build --report"
     },
   ~~~

3. 配置完成之后 ，运行 npm run report ，会在build同时，

   在dist目录生成一个 report.html ，打开可以看见 是哪一个 文件占用较大。

4. 假设 Echarts 文件较大，可以改为 外部引用，

   ~~~javascript
   // vue.config.js
   module.exports = {
       configureWebpack:{
           externals:{
               echarts:"echarts"
           }
       }
   }
   ~~~

   ~~~javascript
   <!-- public/index.html -->
   <!-- 写在head最下面 或者body 最下面 -->
   <script src="https://lib.baomitu.com/echarts/5.1.0/echarts.common.js"></script>   
   ~~~

   

   Element UI  改为按需引入（见官网） 需要先外部引入 vue

##　Ｖｕｅ　优化

# 

https://www.bilibili.com/video/BV1Y4411772w/?spm_id_from=autoNext



