# proxy

## 作用

- 扩展（增强）对象一些功能

  比如 ： Vue.config.keyCodes.enter = 65

- proxy 作用：比如 Vue 中拦截 
  
  ​							预警、上报、拓展功能 、统计、增强对象
  
  
  
- proxy 是设计模式一种 ，代理模式  
  
  

## 语法

==new Proxy(target,handler);==

let obj = new Proxy(被代理的对象， 对代理对象做的操作) ；

~~~javascript
handler() {

	set(){ }    // 设置的时候干的事情

	get(){ }    // 获取的时候干的事情  可以起到拦截作用

   deleteProperty(){ } // 删除 的时候干的事情
 
	has() { } // 问你有没有这个东西  'xxx' in obj

	apply()  // 调用函数处理

 ....

}
~~~





## 案例

-- 语法案例 property === 代理对象. 属性中的 属性

~~~javascript
let obj = {
    name:"xxx"
};

let newObj = new  Proxy(obj,{
    get(target,property) {
        // console.log(target,property)  // { name: 'xxx' } aaa

        console.log(`访问了${property}属性`);
        return target[property];
    }
})
// newObj.aaa;
console.log(newObj.name);
~~~



-- 实战案例

实现一个，访问一个对象身上属性 ，默认不存在的是时候给 undefind ,希望如果不存在错误（警告）信息。

~~~javascript
let obj = {
    name:"xxx"
};

let newObj = new  Proxy(obj,{
    get(target,property) {
        
       // 使用in关键字 检测对象中属性的存在与否可以通过几种方法来判断。 
       if(property in target) {   
           return target[property];
       }else {
        //    throw new  ReferenceError(`${property}属性不在此对象`)

        console.log(`${property}属性不在此对象`);
        return '^_^';
           
       }
    }
})
// newObj.aaa;
console.log(newObj.name);
console.log(newObj.age); // obj 上没有 age ,抛出错误
~~~











