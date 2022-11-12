

主要用于 不确定参数个数 ...

#### 扩展运算符 ...

示例 

```javascript
function jspang(...arg) {
	console.log(arg[0]);
	console.log(arg[1]);
	console.log(arg[2]);
}
jspang(1,2); // 输出 1 2 undefined
```

所以 ...扩展运算符到底有什么用呢  看接下来的例子

```javascript
let arr1 = ['www','baidu','com']
let arr2 = arr1;
console.log(arr2); // 打印 [ 'www', 'baidu', 'com' ]
arr2.push('YSS');
console.log(arr1); // 打印  [ 'www', 'baidu', 'com', 'YSS' ]  
```

let arr2 = arr1   并没有开辟新的内存空间 把 arr1 的内存空间 映射到了 arr2  当改变arr2 的时候 自然 arr1 的值也改变了    这就可以用扩展运算符来解决问题

```javascript
let arr1 = ['www','baidu','com']
let arr2 = [...arr1];  // 修改代码  使用扩展运算符
console.log(arr2); // 打印 [ 'www', 'baidu', 'com' ]
arr2.push('YSS');
console.log(arr1); // 打印 [ 'www', 'baidu', 'com' ]
console.log(arr2); // 打印 [ 'www', 'baidu', 'com', 'YSS' ]
```

#### rest 运算符  ...

rest  剩余的意思  当我们能确定有些参数的时候  用  rest 

```javascript
function jspang(first, ...arg) {
	for(let i = 0;i<arg.length;i++){
		console.log(arg[i]);
	}
}
jspang(0,1,2,3,4,5,6,7) // 输出 1 2 3 4 5 6 7
```

代码优化  ES6 新支持语法

```javascript
function jspang(first, ...arg) {
	for(let val of arg){
		console.log(val);
	}
}
jspang(0,1,2,3,4,5,6,7) // 输出 1 2 3 4 5 6 7
```

