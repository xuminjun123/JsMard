# Javascript -- DOM篇

## 1.==DOM 节点==

**DOM** 【旧】

- `document.body` : 获取body节点
- `document.head `：获取head元素节点
- `document.links`：获取页面上所以的超链接元素节点， 【类数组】
- `documnet.anchors`获取页面上所以的锚链接元素节点（具有name属性）



**DOM 【新】 ** -- 加了 **s** 都是类数组 

- `document.getElementById`: 通过id 获取对应的id的元素
- `document.getElementsByTagName`: 通过元素名称获取元素 【类数组】
- `document.getElementsByClassName` ：通过元素类样式 获取 【类数组】
- `document.getElementByName`：通过元素的name 属性值获取
- `document.querySelector`: 通过css选择器获取元素 ， **只会获取第一个** 【ie8以下无效】
- `document.querySelectorAll`： 通过css选择器获取元素 ， **得到所有匹配結果**【ie8以下无效】【类数组】



**细节**

- 在所有得到的类数组中，除了`querySelectorAll` 其他方法都是实时更新的





## 2.==根据节点关系获取节点==

- `parentNode` : 获取父节点 -- 就是 获取元素
- `previousSibling`: 获取上一个兄弟节点
- `nextSibling` : 获取下一个兄弟节点
- `childNodes`:获取所以的子节点
- `firstChild`:获取第一个子节点
- `lastChild`: 获取最后一个子节点
- `attributes`：获取某个元素的属性节点



## 3. 获取元素节点 

**这些一般不会使用**：

- `parentElement`: 获取父节点  -- 就是 获取元素
- `previousElementSibling`: 获取上一个 兄弟元素
- `nextElementSibling `：获取下一个兄弟元素
- `children` ：获取子元素
- `firstElementChild`: 获取第一个子元素 【ie9无法识别】
- `lastElementChild`: 获取最后一个子元素 【ie9无法识别】



关系如图 ：

![节点关系图](D:\typora\JSmark\JSImage\节点关系图.png)





## 4. 获取节点信息

**这些一般不会使用**：

- `nodeName`:获取节点名称

- `nodeVlaue`: 获取节点 的值

- `nodeType`: 获取节点的类型 ，返回 一个数字 【如下图】 

  

节点信息图 ：

<img src="D:\typora\JSmark\JSImage\节点名称.png" alt="节点名称" style="zoom: 80%;" />





# DOM 元素操作

## 1. 获取和设置元素属性

**ＨＴＭＬ原生属性设置和获取**  

 通用方式 ：（ 一般不用 这种）

- `setAtttribute`: 设置属性

-  `getAttribute` :  获取属性



常用方式 ：`dom对象.属性名` ：【推荐】



细节 ：【了解】

- 正常的属性即使没有复制， 也有默认值
- 布尔属性在dom对象中，得到的是 boolean 
- 某些表单元素可以获取到某些不存在的属性
- 某些属性与标识符冲突，此时，需要更换属性名





**自定义属性**

HTML5 自定义属性使用 `data-` 作为前缀； 

遵从`data-` 自定义属性规范，可以使用 `dom对象.dataset.属性名`控制属性



**删除自定义属性**

- `removeAttribute("自定义属性")` ：删除自定义的属性，原生属性无法删除

- `delete dom对象.dataset.属性名` ：  删除自定义的属性。 【推荐】







## 2. ==获取和设置元素内容==

- `innerHTML` ：获取和设置元素的内部HTML文本。
- `innerText`: 获取和设置元素内部的**纯**文本 ，仅仅到元素内部 的文本 。

- `textContent` :  获取和设置元素内部的文本 ， 得到内部所有的文本（包含空格，注释）





## 3.  元素结构重构

- `父元素.appendChild(元素)` ： 在某个元素末尾加入一个子元素
- `appendChild()`: 可以添加多个元素

- `父元素.insertBefore(待插入的元素，哪一个元素之前)`

- `父元素.replaceChild(替换的元素，被替换的元素)`





## 4. ==创建元素==

- `document.createElement("元素名")` : 创建一个元素    
- `document.createTextNode("文本")` ：创建一个文本节点
- `DocumentFragment()`:创建文本片段





## 5. 克隆元素



- `dom对象.cloneNode() ` : 复制一个新的dom对象并返回 ，（true） 表示深度克隆





## 6. ==删除元素==

- `removeChild()`: 父元素调用 ，传入子元素

- `remove()`: 删除自身元素







# ＤＯＭ元素样式

## 1. 控制 dom 元素的 类样式

- `className` : 获取或设置元素的类名
- `classList`：dom4 的新属性。是一个用于控制元素类名的对象
  - `add` : 用于添加一个类名
  - `remove`： 用于移除一个类名
  - `contain`：用于判断一个类名是否存在
  - `toggle`： 用于添加/移除一个类名



## 2. 获取样式

**css短横线命名，需要转换为小驼峰**

- `dom.style` ：得到的是**行内元素**对象

- `window.getComputedStyle(dom元素)`： 得到某个元素的最终计算样式
  - 第二个参数，用于得到某个元素的伪元素样式



## 3. 设置样式

- `dom.style.样式名 = 值` ；设置的是行内样式 





