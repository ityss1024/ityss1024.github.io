<h1 align='center'>Proxy 预处理</h1>

<div style='color: #ff9933'>注意一定要写return</div>

**set 和 get**

```javascript
// proxy 代理 ES6 增强 预处理
let pro = new Proxy({
	add:function(val){
		return val+100;
	},
	name:'I am JSPang'
},{
	// get 在得到网络值之前  我们做一些事情
	get:function(target,key,property){ //第一个参数 是上面的对象体  
		console.log('预处理中....');
		console.log(target,key,property) // 打印 { add: [Function: add], name: 'I am JSPang' } name { add: [Function: add], name: 'I am JSPang' }
		return target[key];   // 打印 I am JSPang
	},
	// set 设置一些值
	set:function(target,key,value,receiver){
		console.log(target,receiver);
		console.log(`setting ${key} = ${value}`);
		console.log(target);  //  这时对象体没有改变  注意一定要返回
		return target[key]=value;
	}
});  // 第一个大括号放 对象体   第二个对象是预处理方法
// get
console.log(pro.name);
//set 
pro.name='技术胖'  // 打印 setting name = 技术胖
console.log(pro.name);  // 打印 技术胖
```

**apply**

```javascript
let target = function() {
	return 'I am JSPang';
}
let handler = {
	apply(target,ctx,args){
		console.log('do apply');
		return Reflect.apply(...arguments);
	}
}
let pro = new Proxy(target,handler);
console.log(pro());  // 打印 I am JSPang
```

