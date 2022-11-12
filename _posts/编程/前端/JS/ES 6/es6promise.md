<h1 align='center'>promise </h1>

```javascript
// promise  解决 es5 回调地狱(回调函数的多层嵌套)
let state = 1;
function step1(resolve,reject){
	console.log('1.第一步');
	if(state == 1) {
		resolve('第一步完成 开始第二步');
	}else{
		reject('第一步没有完成')
	}
}
function step2(resolve,reject){
	console.log('1.第二步');
	if(state == 1) {
		resolve('第二步完成 开始第三步');
	}else{
		reject('第二步没有完成')
	}
}
function step3(resolve,reject){
	console.log('1.第三步');
	if(state == 1) {
		resolve('第三步');
	}else{
		reject('第三步没有完成')
	}
}
new Promise(step1).then(function(val){
	console.log(val);
	return new Promise(step2);
}).then(function(val){
	console.log(val);
	return new Promise(step3);
}).then(function(val){
	console.log(val);
}); // 打印 1.第一步 第一步完成 开始第二步 1.第二步 第二步完成 开始第三步 1.第三步 第三步
```



```vue
// 第一步执行
let myPromise = new Promise(resolve => {
        getUserInfo(username).then(res => {
        // console.log(res);
        resolve(res.data.org.id)

        })
    })
// 下一步执行
myPromise.then(res => {
    this.params = {}
    this.params['id'] = res
    getJsonChidById(this.params).then(response => {
    this.cityList = JSON.parse(response.data) //得到所选城市下面的所有数据
})
```

