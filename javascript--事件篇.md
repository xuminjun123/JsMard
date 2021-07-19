# 事件



## 1. 事件流



事件捕获 、 事件目标阶段 、事件冒泡 ;



- 事件 捕获：从外往里 触发事件 ；
- 事件冒泡 ：从里往外

默认事件冒泡



如图：

<img src="D:\typora\JSmark\JSImage\事件流程.png" alt="事件流程" style="zoom:67%;" />









## 2. DOM0事件注册

 **DOM0事件绑定**

- 将事件名称前面加上 `on`,作为dom的属性名，给该属性赋值为一个函数 ，即为事件注册

  ~~~javascript
  var btn = document.getElementById("btn");
  btn.onclick = function (){
      console.log('...')
  }
  ~~~
  
  



**DOM0事件移除**

- 移除：重新给事件属性移除，通常赋值为null 何undefind

```javascript
btn.onclick = null
```





## 3. DOM2事件注册

`dom对象.addEventListener("事件名称",fn,boolean)`: 注册事件

~~~javascript
var btn = document.getElementById("btn");
btn.addEventListener("click",function(){
     console.log('...')
},true)
~~~



`dom对象.removeEventListener("事件名称",fn)`: 事件移除

~~~javascript
var btn = document.getElementById("btn"); 
var btn2 = document.getElementById("btn2"); // 移除按钮的 dom元素
function handler() {
    console.log('...')
};
btn.addEventListener("click",handler);
btn2.addEventListener("click",function(){
    btn.removeEventListener("click",hanler)
});
~~~





**与DOM0的区别**

1. DOM2可以为某个元素的同一个事件，添加**多个**处理程序，安装注册的先后顺序执行
2. DOM2 允许开发者控制事件处理的阶段 , 
3. DOM2第三个参数为 `true` ,事件在 **捕获阶段触发** ，
4. DOM2第三个参数为 对象 `{once : true }`,事件只触发一次 
5. DOM2移除事件 不能使用匿名函数





# 事件对象



事件对象封装时间的相关信息



## 1. 获取时间对象$event

- 新版本 浏览器获取方式

~~~javascript
var btn = docuemnt.querySelector("button")
btn.onclick = function(e){
    console.log(e)
}
~~~



- 旧版本获取方式 （ 落伍 ）

~~~javascript
var btn = docuemnt.querySelector("button")
btn.onclick = function(){
    console.log(window.event)
}
~~~





[题外] ：e.bubbles  可以查看元素是否冒泡 ，true ： 冒泡

~~~javascript
var btn = docuemnt.querySelector("button")
btn.onclick = function(e){
    console.log(e.bubbles) // 返回 boolean
}
~~~





## 2. 事件对象的通用成员



- `target  & srcElement` : 事件源对象

  ~~~javascript
  <button>按钮</button>
  
  var btn = docuemnt.querySelector("button")
  btn.onclick = function(e){
      console.log(e.target);   // <button>按钮</button>
  }
  ~~~

  

- `currentTarget` : 当前目标，获取事件的元素，等效于 `this`

  ~~~javascript
  var btn = docuemnt.querySelector("button")
  btn.onclick = function(e){
      console.log(this === e.currentTarget);   // true 都指向事件绑定的元素
  }
  ~~~



- `type`: 事件类型

- `preventDefault & returnValue`：阻止浏览器默认处理

  - dom0 的方式

  ~~~javascript
  var a = docuemnt.querySelector("a")
  a.onclick = function(e){
      return false   // 阻止 a标签的 跳转行为  
  }
  ~~~

  

  - dom2 的方式

  ~~~~javascript
  <a href="https://www.baidu.com">百度</a>
  
  var a = document.querySelect("a");
  a.addEventListener("click",function(e)=>{
      e.preventDefault()        // 阻止 a标签的 跳转行为  
  })
  ~~~~





- `stopPropagetion`: 阻止事件冒泡

~~~javascript
var btn = docuemnt.querySelector("button")
btn.onclick = function(e){
  e.stopPropagetion()   // 阻止 btn向上冒泡 
}
~~~



- `eventphase`: 得到事件所处阶段

  返回

  - 1： 事件捕获
  - 2： 事件目标
  - 3： 事件冒泡













# 鼠标事件

## 1. 事件类型

前缀 “on” 

- `click` : 点击 、回车键触发
- `dbclick`： 双击
- `mousedown`：按下鼠标任意键时候触发
- `mouseup`：鼠标抬起时候
- `mousemove`：鼠标在元素上移动触发
- `mouseover`: 鼠标进入元素时触发
- `mouseout`: 鼠标离开元素时触发
- `mouseenter`:   鼠标进入元素时触发 【该事件不会冒泡】
- `mouseleave`:  鼠标离开元素时触发 【该事件不会冒泡】



## 2. 事件对象

- `altKey`: 触发事件时候，是否按下键盘的alt 键

  ~~~javascript
  var btn = docuemnt.querySelector("button")
  btn.onclick = function(e){
    console.log(e.altKey)   // 返回 boolean 
  }
  ~~~

  

- `ctrlKey`:触发事件时候，是否按下键盘的ctrlKey 键

- `shiftKey`: 触发事件时，是否按下键盘的shift 键

- `button`:   触发事件时，按下鼠标的类型 ； 返回数字

  - 0：左键
  - 1：中键
  - 2：右键



​		==**位置**==

```tex
	`page` : pageX,pageY 当前鼠标距离页面的横纵坐标  【相对于页面】
    `client`: clientX 、clientY  【鼠标相对于视口】
    `offset` :offsetX 、 offsetY 【相对于事件源的内边距的 坐标】
    `screen` :screenX 、screenY  【相对于电脑屏幕】
    `x/y` : 等同于 clientX 、clientY
    `movement` :movementX 、 movementY 只在鼠标移动事件中有效【相对于上一次鼠标位置】
```







# 键盘事件



键盘事件 ，可以 阻止 默认事件，如果阻止 ，文本不会显示



## 1. 事件类型

前缀“on” 

- `keydown`: 按下键盘上任意键触发 ，如果按住不放，会重复触发此事件
- `keypress`: 按下键盘上一个**字符键**时触发

- `keyup`: 抬起键盘上任意键触发





## 2. 事件对象

- `code`：得到按键字符串，适配键盘布局
- `key`:得到按键字符串, 不适配键盘布局

- `keyCode 、which`： 得到键盘编码





# 表单事件

## 1. 表单事件类型



- `focus`: 元素聚焦时候触发【能与用户交互的元素，如 a标签 ，video，audio  ... 】
- `blur`: 元素失去焦点时候触发
- `submit`:提交表单时触发,仅在 from 表单中触发 【默认】

- `change`:表单内容改变时候触发
- `input`:  文本改变事件，即使触发   【无法阻止的】 





# 其他事件

## １.页面状态事件

> 页面渲染过程
>
> 1. 得到页面源代码
> 2. 创建document节点
> 3. 从上到下，讲元素依次添加到dom书中，每添加一个元素，进行于预渲染
> 4. 按照结构，依次渲染子节点
>
> 【结论】：
>
> -  css应该写到页面**顶部**，避免出现闪烁（如果放到页面底部，会导致元素没有样式，使用html5的默认样式，然后当读到css文件后，重新改变样式）
> - JS 应该写到页面**底部**, 避免后续渲染的阻塞，也避免运行ＪＳ得不到页面中的元素





前缀“on” 

**window**的 

- `load、DOMContentLoaded、readystatechange`

  - load: 页面中所有资源全部加载完毕的事件　
   ~~~javascript
    	window的事件  window.onload= function(){ 
       
       } 
   ~~~
  - DOMContentLoaded：dom 树构建完成之后触发 【 document 的事件 (ready事件)】

    ~~~javascript
    doucument.addEventListener("DOMContentLoaded",function(){
        
    })
    ~~~
    
  - readystatechange：页面正在加载中 ，他会触发DOMContentLoaded事件

     

- `unload、beforeunload`

  - beforeunload、unload : 关闭窗口时运行， 可以运行阻止关闭窗口 （目前还是 不会触发了）

- `scroll`：窗口发生滚动时候触发， 【window事件、元素事件】

  - 可以根据scrollTop 和 scrollLeft  获取和设置滚动距离

    <img src="D:\C盘移动过来的文件\Desktop\133.png" alt="133" style="zoom: 50%;" />

  ~~~javascript
  document.querySelector("div").onscroll = function (){
      conslole.log(this.scrollTop,this.scrollLeftthis.scrollTop = 0 ; this.scrollLeft = 0 )
      this.scrollTop = 0 ; this.scrollLeft = 0 // 回到顶部
  }
  ~~~

  **获取整个网页滚动高度**

  ~~~javascript
  window.onscroll = function(){
      conslole.log( document.documentElement.scrollTop + document.body.scrollTop  )
  }
  ~~~

  

- `resize` : 窗口尺寸发生改变 ，监听的是视口区域【window事件】

  **窗口尺寸** 如图

  <img src="D:\C盘移动过来的文件\Desktop\0.png" alt="0" style="zoom: 50%;" />

  ~~~javascript
  window.resize = function (){
      
  } 
  ~~~

  

- `contextmenu`



- `paste`
- `copy`

  























