# websocket

 ## 前端 

1. login
   - 用户名输入 / 进入聊天室的按钮
   - input username(6) -> localhost -> 进入聊天室
   - 
2. home
   - 列表 / 消息输入框 / 发送按钮
   - localhost  -> username / message / id / 消息时间 - -- >后端socket



前端 事件 (都有事件对象)

- open
- close
- error
- message   接受广播来的数据



## 后端

接收 ---> 消息数据 ---> 广播所有连接到 socket 的服务客户端



后端 

- open 
- close
- error
- connection  链接成功之后才会没有message
  -  message 接受客户端发送来的数据 - --> 广播



## Vue-websocket

在发送消息页面:

~~~vue
<ul v-for="(item,index) in msgLists" :key="index">
    <li>{{item}}</li>
</ul>
<input v-model="msg" />
<button @click="handSend">
    发送
</button>
~~~

~~~vue 
const ws = new WebSocket('后端地址')
~~~

~~~vue
data(){
	msg:"",
	msgLists
}，

mounted() {
	// 绑定 open
	ws.addEventListener('open',this,handleWsOpen.bind(this),false);

	// 绑定 close
	ws.addEventListener('close',this,handleWsClose.bind(this),false);

	// 绑定 Error
	ws.addEventListener('error',this,handleWsError.bind(this),false);
	
	// 绑定 Message
	ws.addEventListener('message',this,handleWsMessage.bind(this),false);
},
methods:{
	handleSend(){
		// 发送 send() 给后端 传 JSON字符串
		ws.send(JSON.Stringify({
			id:new Date().getTime(),
			user:this.username,
			dateTime:new Date().getTime()
			msg: this.msg
		}));
		this.msg = '';
	},

	handleWsOpen(e) {

	},
	handleWsClose(e) {
		
	},
	handleWsError(e) {
		
	},
	handleWsMessage(e) { // 接受后端 handleMesage() 的信息
		consloe.log(e)
		const msg = JOSN.parse(e.data);
		// .... 这里 赋值 消息列表
		// 如
		this.msgList.push(msg)
	},
}
~~~







## node-websocket



~~~javascript
const Ws = require('ws');

;((Ws)=>{
	const server = new Ws.Server({port:8000});
	
    const init = ()=>{
        bindEvent();
    }
    
    function bindEvent(){
        server.on('open',handOpen);
        server.on('close',handClose);
        server.on('error',handError);
        server.on('connection',handConnection);
    }
    function handOpen() {
        
    }
    function handClose(){
        
    }
    function handError(){
        
    }
     function handConnection(){
        
         ws.on('message',handleMessage);
    }
    
    function handleMesage(msg){  // 接受前端 send() 信息 ，接受处理
        console.log(msg);
        server.clients.forEach((c)=>{ // 给所有客户端发送消息
            c.send(msg)
        })
    }
    init();
})(Ws);

~~~



























