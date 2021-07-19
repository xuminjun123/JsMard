# JS


## scrollIntoView

该`scrollIntoView()`方法将调用它的元素滚动到浏览器窗口的可见区域。




| **alignToTop** | **[可选]，目前之前这个参数得到了良好的支持**                 |
| -------------- | ------------------------------------------------------------ |
| true           | 元素的顶部将对齐到可滚动祖先的可见区域的顶部。对应于`scrollIntoViewOptions: {block: "start", inline: "nearest"}`。这是默认值 |
| false          | 元素的底部将与可滚动祖先的可见区域的底部对齐。对应于`scrollIntoViewOptions: {block: "end", inline: "nearest"}`。 |

| scrollIntoViewOptions | [可选]，目前这个参数浏览器对它的支持并不好，可以查看下文兼容性详情 |
| --------------------- | ------------------------------------------------------------ |
| behavior              | [可选]定义过渡动画。`"auto"`,`"instant"`或`"smooth"`。默认为`"auto"`。 |
| block                 | [可选] `"start"`，`"center"`，`"end"`或`"nearest"`。默认为`"center"`。 |
| inline                | [可选] `"start"`，`"center"`，`"end"`或`"nearest"`。默认为`"nearest"`。 |



实例 ： 



~~~javascript
document.querySelector(`#${name}`).scrollIntoView({
    behavior: "smooth",
    block: "center",
    inline: "nearest"
});
~~~







类似于a 标签的 锚点

~~~html
<a href="#mubiao">点击此处到目标位置</a>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>						<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

<div id="mubiao">
    目标位置
</div>

~~~



Vue 案例

~~~html
<template>
    <div class="wrap">
        <ul>
            <li><a href="javascript:void(0)" @click="goAuchor('#one')">第一</a></li>
            <li><a href="javascript:void(0)" @click="goAuchor('#two')">第二</a></li>
            <li><a href="javascript:void(0)" @click="goAuchor('#three')">第三</a></li>
            <li><a href="javascript:void(0)" @click="goAuchor('#four')">第四</a></li>
        </ul>
        <div id="one" class="one"></div>
        <div id="two" class="two"></div>
        <div id="three" class="three"></div>
        <div id="four" class="four"></div>
    </div>
</template>

<script>
    export default {
        methods:{
            goAuchor(id){
                console.log(id)
                document.querySelector(id).scrollIntoView(true)
                var auchor=this.$el.querySelector(id)
                console.log(auchor)
                console.log(auchor.getBoundingClientRect().top)
                document.body.scrollTop=auchor.offsetTop
            }
        }
    };
</script>

<style scoped>
    .wrap {
        width: 100%;
        height: 100%;
    }
    .one{
        width: 100%;
        height: 500px;
        background-color: red;
    }
    .two{
        width: 100%;
        height: 500px;
        background-color: blue;
    }
    .three{
        width: 100%;
        height: 500px;
        background-color: green;
    }
    .four{
        width: 100%;
        height: 500px;
        background-color: yellow;
    }
    ul{
        width: 100%;
        height: 30px;
        margin: 0;
        padding: 0;
    }
    li{
        list-style: none;
        float: left;
        background-color: rebeccapurple;
        height: 100%;
        margin-left: 50px;
        cursor: pointer;
    }
</style>

~~~

 



##  css3的animation属性

~~~html
<div></div>
<style>
    div
    {
        width:100px;
        height:100px;
        background:red;
        position:relative;
        animation:mymove 5s infinite;
        -webkit-animation:mymove 5s infinite; /*Safari and Chrome*/
    }

    @keyframes mymove
    {
        1% {left:0px;}
        20%{left:200px;}
        50% {left:300px;}
        100%{left:200px;}
    }

    @-webkit-keyframes mymove /*Safari and Chrome*/
    {
        1% {left:0px;}
        20%{left:200px;}
        50% {left:300px;}
        100%{left:200px;}
    }
</style>
~~~





## 自适应网站

~~~css
使用 clamp() CSS函数，我们可以创建仅具有一个属性的响应式网站。
~~~



clamp() 函数的作用是把一个值限制在一个上限和下限之间，当这个值超过最小值和最大值的范围时，在最小值和最大值之间选择一个值使用。

clamp() 函数接收三个用逗号分隔的表达式作为参数，按最小值、首选值、最大值的顺序排列。

- 当首选值比最小值要小时，则使用最小值。
- 当首选值介于最小值和最大值之间时，用首选值。
- 当首选值比最大值要大时，则使用最大值。

