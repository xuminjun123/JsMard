# AJAX 基本操作

~~~javascript
// 获取dom 操作
const btn = document.getElementByTageName('button')[0];
// 绑定事件
btn.onclick = function(){
    // 1. 创建对象
    const xhr = new XMLHttpRequest();
    // 2. 初始化 设置请求方法 和 URl
    xhr.open('GET','http://127.0.0.1:9000/server');
    // 设置请求头信息
    xhr.setRequestHeader('','')
    // 3. 发送
    xhr.send();
    // 4. 事件绑定
    xhr.onreadystatechange = function(){
        // - on 监听
        // - readystate 是xhr 对象中的属性， 表示 0 ,1, 2,3,4
        // - change 改变
        
        // 状态4 : 服务端返回了所有结果
        if(xhr.readystate == 4){
            // 判断响应状态码
            if(xhr.status >= 200 && xhr.status < 300){
                // 处理结果
                // -  响应行
                console.log(xhr.status);
                // - 响应状态字符串
                console.log(xhr.statusText);
                // - 响应所有的响应头
                console.log(xhr.grtAllResponseHeaders());
                // - 响应体
                console.log(xhr.response);
                
            }else {
                
            }
        }
    }
}
~~~





## 1. Ajax  设置请求参数

~~~javascript
// get 请求带参数
xhr.open('GET', 'http://127.0.0.1:8000/server?a=100&b=200')
~~~



~~~javascript
// post 请求带参
btn.addEventListener("mouseover", function(){
    const xhr = new XMLHttpRequest();
    xhr.open("POST","http://127.0.0.1:8000/server");
    
    // 参数设置 在send 设置
    xhr.send('a=100&b=200&c=300');
  	xhr.onreadystatechange = function(){
        //....
    }
    
    
})
~~~





## 2. Ajax 设置请求头信息

~~~javascript
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');

// - 自定义设置请求头
xhr.setRequestHeader('token','xxxxxxxx')
~~~



==Content-Type==: 设置请求体类型



## 3. Ajax 请求超时与网络异常处理

~~~javascript
const xhr = new XMLHttpRequest();
// 设置超时 2s
xhr.timeout = 2000;
// 超时回调
xhr.ontimeout = function(){
    console.log('网络超时了...')
}
~~~



## 4. AJAX取消请求

~~~javascript
// 请求
let xhr = null;
btn[0].onlick = function(){
    xhr = new XMLHttpRequest();
    xhr.open("POST","http://127.0.0.1:8000/server");
    xhr.send();
}
btn[1].onlick = function(){
    xhr.abort();  // 取消请求
}
~~~





# axios 学习使用

## 1. 配置 axios

~~~javascript
// 下载 
npm install axios

import axios form 'axios'

// baseUrl
axios.defaults.baseUrl = 'http://127.0.0.1:8000/axios-server'
~~~



## 2. get请求 带参数

~~~javascript
axios.get('http://127.0.0.1:8000/axios-server', {
    params:{
        id:100
    },
    // 请求头
    headers:{
        name:'xxx'
    }
})
.then((res)=> {
    console.log(res)
})
~~~



## 3.post 请求带参数

~~~javascript
axios.post('http://127.0.0.1:8000/axios-server', {
        username: 'admin',
        password: 'admin'
    },{ 
        // url
    	params: {
            id:200
        },
    	// 请求体
    	header: {
            name: 'xxx'
        }
	}
})
.then((res)=> {
    console.log(res)
})
~~~



## 4. Axios 函数发送请求

~~~javascript
btn[0].onclick = function(){
    axios({
        // 请求方法 
        method: 'POST',
        // url 
        url:'/axios-server',
        // url 参数
        params: {
            id:'1'
        },
        // 头信息
        headers:{
            a:100
        },
        // 请求体参数
        data:{
            username: 'admin',
            password: 'xxx'
        }
    }).then((res)=>{
       	console.log(res.status);  // 响应状态码
      	console.log(res.statusText); // 响应状态字符串
       	console.log(res.headers); // 响应头信息
        console.log(res.data) // 响应体
    })
}
~~~





