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







# 键盘事件









# 表单事件





# 页面状态事件



# 其他事件



















