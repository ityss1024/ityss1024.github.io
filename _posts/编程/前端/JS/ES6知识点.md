### 变量和常量

```
var是全局声明  let是局部声明   const是常量声明
```

### 数据解构

常用于 json 数据解构  和  map 数据解构

#### 数组解构

```javascript
let [a,b,c]=[0,1,2];
console.log(a);console.log(b);console.log(c); // 输出 0 1 2
```

#### 对象解构

```javascript
let {foo,bar} = {foo:'JSP',bar:'技术胖'};
console.log(foo+bar); // 输出 JSP技术胖
```

没有key值的 按照顺序结构  对象的解构是要求有key值得

```javascript
let foo;
({foo} = {foo:'技术胖'});  // 注意要加 ()  不然报错
console.log(foo);  // 打印技术胖
```

先声明了  在解构  需要在解构代码最外面加 ()  才可以 解构成功

#### 字符串解构赋值

```javascript
const [a,b,c] = 'JSP';
console.log(a);console.log(b);console.log(c); // 输入 J S P
```

#### 总结   =  两边 相同的结构  右边给左边的变量一一对应赋值



### 箭头函数

```javascript
var add=(a,b=1) =>{return a + b;}
console.log(add(1));  // 打印 2
注意:在箭头函数中不允许使用new的，不能当构造函数使用
```

### es异步编程

```javascript
要了解异步编程，就要了解promise的概念
new Promise()  创建一个promise对象 最先执行里面的代码
.then函数  先执行下面的同步代码，在执行.then()函数里面的代码

async 相当于new Promise() 即声明为 promise函数
await await以下的代码 就放在.then函数里面(在同一个大括号里面)
例子:
function sleep(ms) {
    return new Promise(function(resolve, reject) {
        setTimeout(resolve,ms);
    })
}

async function handle(){
    console.log("AAA")
    await sleep(5000)
    console.log("BBB")
}

handle();

// AAA
// BBB (5000ms后)
```

### 扩展运算符和rest运算符

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

### 数组相关知识

#### json的数组格式

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

#### Array.of 方法

```javascript
// Array.of 方法
let arr = Array.of(3,4,5,6);
console.log(arr); // 打印 [ 3, 4, 5, 6 ]
```

#### find()

```javascript
// find() 实例方法(必须先有实例)  value 要查找的值  index 下表  arr 查找的范围
let arr = [1,2,3,4,5];
console.log(arr.find(function(value,index,arr){
	return value > 1;
}));  // 打印 2   如果没有查找到 则打印 undefined
```

#### fill()

```javascript
// fill() 实例方法 替换数组内容
let arr = ['1111','2222','3333']
arr.fill('web',1,3);  // 第一个参数 替换成的值 第二个参数 开始替换的位置(数组从0开始) 第三个参数 替换到的位置(从1开始)
console.log(arr);  // 打印 [ '1111', 'web', 'web' ]
```

#### 数组遍历

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

#### 打印下标和内容 entries()

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

#### 补漏

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

