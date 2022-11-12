

```javascript
// Symbol ES6 新增数据类型
// ES5 数据类型
let a = new String;  // 字符串类型
let b = new Number;  // 数字类型
let c = new Boolean; // 布尔类型
let d = new Array;  // 数组类型
let e = new Object; // 对象类型

let f = Symbol();
console.log(typeof(f));  // symbol   a,b,c,d,e 均为Object
```

```javascript
let jspang = Symbol('技术胖')
console.log(jspang);  // 打印 Symbol(技术胖)  为彩色
console.log(jspang.toString()) // 打印 Symbol(技术胖)  为黑色
```



```javascript
let jspang = Symbol();
let obj = {
	[jspang]:'技术胖'
}
console.log(obj[jspang])  // 打印 技术胖  不是obj.jspang
obj[jspang] = 'web'
console.log(obj[jspang])  // 打印 web
```

**保护输出**

```javascript
let obj = {name:'jspang',skill:'web'}
let age = Symbol();
obj[age] = 18;
console.log(obj); // 打印 { name: 'jspang', skill: 'web', [Symbol()]: 18 }
for(let item in obj){
	console.log(obj[item]); //打印  jspang  web  
}
console.log(obj[age]);  // 18
```

