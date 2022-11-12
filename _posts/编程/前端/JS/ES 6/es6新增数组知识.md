**json的数组格式**

```javascript
// json 数组格式
let json = {
	'0': '1111',
	'1': '2222',
	'2': '3333',
	length:3
}
let arr = Array.from(json);
console.log(arr); // 打印 [ '1111', '2222', '3333' ]
```

**Array.of 方法**

```javascript
// Array.of 方法
let arr = Array.of(3,4,5,6);
console.log(arr); // 打印 [ 3, 4, 5, 6 ]
```

**find()**

```javascript
// find() 实例方法(必须先有实例)  value 要查找的值  index 下表  arr 查找的范围
let arr = [1,2,3,4,5];
console.log(arr.find(function(value,index,arr){
	return value > 1;
}));  // 打印 2   如果没有查找到 则打印 undefined
```

**fill()**

```javascript
// fill() 实例方法 替换数组内容
let arr = ['1111','2222','3333']
arr.fill('web',1,3);  // 第一个参数 替换成的值 第二个参数 开始替换的位置(数组从0开始) 第三个参数 替换到的位置(从1开始)
console.log(arr);  // 打印 [ '1111', 'web', 'web' ]
```

**数组遍历**

```javascript
let arr = ['111','222','333'];
for(let item of arr){
	console.log(item); //输出内容 打印 111 222 333
}
```

```javascript
let arr = ['111','222','333'];
for(let item of arr.keys()){
	console.log(item); //输出下标 打印 0 1 2
}
```

**打印下标和内容 entries()**

```javascript
let arr = ['111','222','333'];
for(let item of arr.entries()){
	console.log(item); // 打印 [ 0, '111' ] [ 1, '222' ] [ 2, '333' ]
}
```

```javascript
let arr = ['111','222','333'];
for(let [index,value] of arr.entries()){
	console.log(index+':'+value); // 打印 0:111 1:222 2:333
}
```

```javascript
let arr = ['111','222','333'];
let list = arr.entries();
console.log(list.next().value); // 打印 [ 0, '111' ]
```

**补漏**

```javascript
// 对象的函数解构 json
let json={
	a: 'jspang',
	b: '技术胖'
}
function fun({a,b='web'}){
	console.log(a,b)
}
fun(json);  // 打印 jspang 技术胖
```

```javascript
// 数组解构
let arr=['111','222','333'];
function fun(a,b,c){
	console.log(a,b,c);
}
fun(...arr);  // 打印  111 222 333 
```

```javascript
// in 的用法
let obj = {
    a: '技术胖',
    b:'jspang'
}
console.log('c' in obj)  // 打印 false

// in 数组空位判断
let arr = ['jspang',,,]
console.log(0 in arr);  // 打印 true  除了0其他下标都是false
```

```javascript
// 数组遍历 
// 1.for of
let arr = ['111','222','333'];
for(let item of arr){
	console.log(item);    // 打印 111 222 333
}

// 2.forEach
arr.forEach((item,index) => {return console.log(index,item)}); 
arr.forEach((item,index) => console.log(index,item)); 
// 打印 0 111  1 222  2 333

// 3.filter
arr.filter(x => console.log(x)); // 打印  111 222 333 

// 4.some
arr.some(x => console.log(x)); // 打印  111 222 333 
```

```javascript
// 数组转化为字符串 
// 1.toString() 方法
let arr = ['111','222','333'];
console.log(arr.toString());  // 打印 111,222,333
// 2.join()
console.log(arr.join('|'));  // 打印 111|222|333

```



