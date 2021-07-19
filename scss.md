# SCSS 基本使用

## :export

~~~css

$sideBarWidth: 210px;

// the :export directive is the magic sauce for webpack
// https://www.bluematador.com/blog/how-to-share-variables-between-js-and-sass
:export {
  sideBarWidth: $sideBarWidth;
}

-- 使用
import 。。。 from '..'

~~~



## 样式重置

~~~scss
* {
    box-sizing:border-box;
    outline:none;
}
html {
    font-size:13px; // 默认16px
}
body {
    margin : 0;
    font-family:Arial,Helvetica,sans-serif;
    line-height:1.2rem;
    background-color:#f1f1f1;
}
a{
    color:#999;
}
~~~





## `$` 使用 



~~~scss
$colors:(
    "primary":#db9e3f,
    "white":#fff,
    "dark":#222
)
~~~



## `@each`使用

/** text 对齐*/

~~~scss
@each $var in (left,center,right){
    .text-#{$var}{
        text-align:$var;
    }
}
~~~



文字颜色，背景

~~~scss
@each $colorkey,$color in $colors {
    .text-#{$colorkey}{
        color:$color
    }
    .bg-#{$colorkey}{
        backgroud-color:$color
    }
    
}
~~~



/** 字体大小**/

 可以使用 vscode的 **px to rem** 插件 换算, 按快捷键ALt+Z

~~~scss
$base-font-size:1rem;
$font-sizes:(
    xs:0.7692,// 10px   -- 10/13 * 1 
    sm:0.9231,// 12px
    md:1,     // 13px
    lg:1.0769,// 14px
    xl:1.2308 // 16px
);
@each $sizekey,$size in $font-sizes{
    .fs-#{$sizekey}{
        font-size:$size * $base-font-size;
    }    
}
~~~



## flex 布局



~~~scss
.d-flex{
    display:flex;
}
.flex-column{
    flex-direction:column;
}


/** 主轴对齐方式 */
$flex-jc:(
    start:flex-start,
    end:flex-end,
    center:center,
	between:space-between,
    around:space-around
);
@each $key,$value in $flex-jc{
    .jc-#{$key}{
        justify-content:$value;
    }
}

/** 垂直对齐方式 */
$flex-ai:{
    start:flex-start,
    end:flex-end,
    center:center,
	stretch:stretch
}
@each $key,$value in $flex-ai{
    .ai-#{$key}{
        justify-content:$value;
    }
}

.flex-1{
    flex:1;
} 
~~~



## 常用margin , padding 定义

~~~scss
// spacing 
// 0-5 : 0
// .mt-1 => margin top 
$spacing-types:(
  m:margin,
  p:padding
);
$spacing-directions:(
  t:top,
  r:right,
  b:bottom,
  l:left,
);
$spacing-base-size:1rem;
$spacing-sizes:(
  0: 0,
  1: 0.25,
  2: 0.5,
  3: 1,
  4: 1.5,
  5: 3,
);

//  .m-1
@each $typekey, $type in $spacing-types {
  @each $sizekey,  $size in $spacing-sizes {
    // .mt-1 { margin-top : 0.25rem }
    .#{$typekey}-#{$sizekey} {
      #{$type}: $size * $spacing-base-size;
    }
  }

  // .mx-1 , .my-1
  @each $sizekey,  $size in $spacing-sizes {
    .#{$typekey}x-#{$sizekey} {
      #{type}-left: $size * $spacing-base-size;
      #{type}-right: $size * $spacing-base-size;
    }

   .#{$typekey}x-#{$sizekey} {
      #{type}-top: $size * $spacing-base-size;
      #{type}-bottom: $size * $spacing-base-size;
    }


   // .mt-1
  @each $directionkey, $direction in $spacing-directions {
    @each $sizekey, $size in $spacing-sizes {
      // .mt {margin-top:0.25rem }
      .#{typekey}#{directionkey}-#{$sizekey} {
        #{type}-#{direction}: $size * $spacing-base-size;
      }
    }
  }
}
~~~





## @function



这个方法提供了在`scss`中计算属性的功能

~~~scss
@function r($size) {
  @return $size / 144 * 1rem;
}
// 使用
p {
  width: r(750);
}
~~~



~~~scss
// 编译后 （以html标签font-size: 150px 为例）
p {
  width: 5rem;
}
~~~

=============

~~~scs
$browser-default-font-size: 16px !default;
html {
    font-size: $browser-default-font-size;
}
@function px2rem($px){//$px为需要转换的字号
    @return $px / $browser-default-font-size * 1rem;
}
@import './silde.scss';
~~~





## @mixin 与 @include

@mixin 指令允许我们定义一个可以在整个样式表中重复使用的样式。

@include 指令可以将混入（mixin）引入到文档中。



~~~scss
@mixin borderRadius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    -o-border-radius: $radius;
    border-radius: $radius;
}

@mixin important-text {
    color: red;
    font-size: 25px;
    font-weight: bold;
    border: 1px solid blue;
}

//使用
@include borderRadius(0.1rem);

@include mixin-name;
~~~





## @extend 

`@extend`告诉 `Sass` 将一个选择器下的所有样式继承给另一个选择器。

~~~scss
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
~~~



## @for

~~~scss
@for $i from 1 through 3 {
  .item-#{$i} { width: 2rem * $i; }
}
~~~



~~~scss
// 编译为
.item-1 {
  width: 2rem;
}
.item-2 {
  width: 4rem;
}
.item-3 {
  width: 6rem; 
}
~~~



## `@while`、`@if`

##  文件导入`@import`

`css`有一个特别不常用的特性，即`@import`规则，它允许在一个`css`文件中导入其他`css`文件。然而，后果是只有执行到`@import`时，浏览器才会去下载其他`css`文件，这导致页面加载起来特别慢。

`sass`也有一个`@import`规则，但不同的是，`sass`的`@import`规则在生成`css`文件时就把相关文件导入进来。这意味着所有相关的样式被归纳到了同一个`css`文件中，而无需发起额外的下载请求。

~~~scss
@import './style/default.scss';
import "@/styles/common.scss"; // main.js 引入
~~~





##　自适应布局

~~~html
<meta name="viewport" content="width=device-width,user-scalable=no,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0">
~~~

1. width=device-width 约束视口的宽度
2. initial-scale=1.0        初始视口的宽度1倍
3. minmum-scale=1.0 初始设置最大缩放比例 1- 10
4. maxmun-scale=1.0  设置





- 宽度 使用vw / flex布局 ,  高度使用 rem（ font-size ; margin ...） `flex` 与 `rem` 结合使用更佳

- 750 设计稿 ：

  ​	指定 ： 1rem = 100px

  ​	dWidth ： 设计稿宽 = 750

  ​	font-size = （vWidth/750）* 100 + 'px'  ------    (  尺寸px / 设计稿px ) * 100  

  ​	body宽 ：750px/100px = 7.5rem

【 了解 】

 阿里 淘宝布局 ：  **flexible.js**

这是以iphone6  2倍图为基准尺寸

750分为100份     750 / 100 = 7.5px

1份 为一个a , a = 7.5px 

1rem = 10a

1rem = 10 * 7.5 = 75px



body宽 ： 750 /75 body { width：10 rem }





**插件**

1. "amfe-flexible": "^2.2.1",   // 这个可以放弃了，因为 viewport 得到众多浏览器的兼容

     "px2rem-loader": "^0.1.9",  -------->>> 会自动转换为rem 的插件

   -----------------------------------------

   1. npm install  px2rem-loader --save
   2. npm install amfe-flexible --save

 

2.  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">



3. main.js 引入

     	rem h5 适配   
     	
     	import 'amfe-flexible/index.js'

   



4. vue.config.js

~~~javasc
module.exports = {
    chainWebpack: config => {
        config.module
            .rule('scss')
            .test(/\.scss$/)
            .oneOf('vue')
            .use('px2rem-loader')
            .loader('px2rem-loader')
            .before('postcss-loader') // this makes it work.
            .options({ remUnit: 75, remPrecision: 8 })
            .end()
    }
}
~~~

如图所示　：

![scss-px2rem-loader](D:\typora\JSmark\JSImage\scss-px2rem-loader.png)

使用 

~~~html
#root{
	width:750px;
	height:750px;
}
// 浏览器会自动转换 为 rem
#root{
	width:10rem;
	height:10rem
}
~~~

第二种在node_module 

 node_modules/@vue/cli-service/lib/config/css.js，

 在 198行 添加规则：

~~~javascript
rule
    .use('px2rem-loader')
    .loader('px2rem-loader')
    .options({emUnit: 75})
~~~

注意：使用 px2rem-loader 后再使用px上有些不同：
  直接写 px ，编译后会直接转化成rem —— 除开下面两种情况，其他长度用这个
  在 px 后面添加 **/\*no\*/** ，不会转化 px，会原样输出。 —— 一般border需用这个
  在 px 后面添加 **/\*px\*/** ，会根据 dpr 的不同，生成三套代码。—— 一般字体需用这个

===========================================================================================================================





## 终极自适应办法



 \* - npm i normalize.css -S 消除浏览器之间的基础样式差异

 \* - npm i amfe-flexible -S 淘宝的一种解决方案

 \* npm i postcss-pxtorem@5.1.1     px---->>rem插件 ,可以自动换算为rem ,需指定为 5.1.1版本



1. rootValue是根标签的font-size大小

2. unitPrecision是转换成rem后的小数位数

3. propList是需要转换的属性列表

4. selectorBlackList则是一个对css选择器进行过滤的数组，比如你设置为['fs']，那例如fs-xl类名，里面有关px的样式将不被转换，这里也支持正则写法。

5. minPixelValue可以设置小于多少尺寸将不会进行转换。

   

vue.config.js

~~~javascript
module.exports = {
    productionSourceMap: false, // 生产环境是否生成 SourceMap
    css: {
        loaderOptions: {
            postcss: {
                plugins: [
                    require('postcss-pxtorem')({
                        rootValue: 75,
                        unitPrecision: 5,
                        propList: ['*'],
                        selectorBlackList: [],
                        replace: true,
                        mediaQuery: false,
                        minPixelValue: 12
                    })
                ]
            }
        }
    },
}
~~~

main 引入

~~~javascript
import "amfe-flexible"
import "normalize.css"
~~~

 【  注意 】



​			随着发展，用后处理器形容postcss 已经不合适了。目前可以使用 postcss-sass/postcss-less 对 less/sass 代码进行转化（将 less/sass 转化为 less/sass，而不是直接转化为 css）

~~~javascript
module.exports = {
    module: {
        rules: [
            {
                test: /\.(css|sass)$/i,
                use: ['style-loader', 'css-loader', 'postcss-loader', 'sass-loader'],
            },
        ]
    }
}
~~~





---------------------------

rem.js



(也不知道有没有用，先记着)

~~~javascript
// rem等比适配配置文件
// 基准大小
const baseSize = 32 // 注意此值要与 postcss.config.js 文件中的 rootValue保持一致
// 设置 rem 函数
function setRem () {
  // 当前页面宽度相对于 375宽的缩放比例，可根据自己需要修改,一般设计稿都是宽750(图方便可以拿到设计图后改过来)。
  const scale = document.documentElement.clientWidth / 750
  // 设置页面根节点字体大小（“Math.min(scale, 2)” 指最高放大比例为2，可根据实际业务需求调整）
  document.documentElement.style.fontSize = baseSize * Math.min(scale, 2) + 'px'
}
// 初始化
setRem()
// 改变窗口大小时重新设置 rem
window.onresize = function () {
  setRem()
}
~~~



