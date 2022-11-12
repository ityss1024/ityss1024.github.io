**ES5对象的赋值**

```javascript
let name = 'jspang'
let skill = 'web'
let obj = {name:name,skill:skill}
console.log(obj)  //打印 { name: 'jspang', skill: 'web' }
```



**ES6对象的赋值**

```javascript
let name = 'jspang'
let skill = 'web'
let obj = {name,skill}
console.log(obj)  //打印 { name: 'jspang', skill: 'web' }
```



```javascript
// key值的构建
let key="shill";
var obj={
	[key] : 'web'
}
console.log(obj)   // 打印  { shill: 'web' }
```



```javascript
// 自定义对象方法
let obj ={
	add:function(a,b){
		return a + b;
	}
}
console.log(obj.add(1,2)) // 打印 3
```



```javascript
// is() 对象间的比较
let obj1={
	name: '123'
}
let obj2={
	name: '123'
}
console.log(obj1.name === obj2.name)  // 打印 true ES5语法 
 // === 判断等值等类型  == 判断等值 
console.log(Object.is(obj1.name,obj2.name)) // 打印 true ES6语法 
```



```javascript
// === 同值相等   is() 严格相等
console.log(+0===-0);  // true
console.log(NaN===NaN); // false  无法知道NaN的值  所以为false

console.log(Object.is(+0,-0)); // false  一个是 + 一个是 - 严格 不相等
console.log(Object.is(NaN,NaN)); // true NaN 完全一样  严格相等
```



```javascript
let a = {a:'jspang'};
let b = {b:'技术胖'};
let c = {c:'web'};
let d = Object.assign(a,b,c);
console.log(d);  // 打印 { a: 'jspang', b: '技术胖', c: 'web' }
```

