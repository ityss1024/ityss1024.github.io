<h1 align="center">1.Set</h1>

<div style='color: #ff9933'>Set 只当了解</div>

```javascript
// Set 数据结构  特点是去重 只能放数组 不能放对象 
let setArr = new Set(['jspang','技术胖','web']);
console.log(setArr);  // 打印 Set { 'jspang', '技术胖', 'web' }

// 追加元素 add()
setArr.add('前端职场')
console.log(setArr);   // 打印 Set { 'jspang', '技术胖', 'web', '前端职场' }

// 去重特点
let setArr1 = new Set(['jspang','技术胖','web','jspang']);
console.log(setArr1);  // 打印 Set { 'jspang', '技术胖', 'web' }

// 查找 has
console.log(setArr.has('jspang'));  // true
console.log(setArr.has('胖子'));  // false

// 删除 delete
setArr.delete('jspang');
console.log(setArr);  // 打印 Set { '技术胖', 'web', '前端职场' }

// 清空Set
setArr1.clear();
console.log(setArr1);  // 打印 Set {}

// 输出 循环
for(let item of setArr){
	console.log(item);  // 打印 技术胖 web 前端职场
}
setArr.forEach((value) => console.log(value)); // 打印 技术胖 web 前端职场

// size属性 
console.log(setArr.size) // 打印 3
```

<h1 align='center'>2.WeakSet</h1>

```javascript
// WeakSet  特点 能放对象 类似与懒加载
let weakObj = new WeakSet(); // 不能直接赋值 否则报错
let obj = { a: 'jspang',b: '技术胖' };
weakObj.add(obj);
console.log(weakObj);  // 打印 WeakSet { <items unknown> }
```

<div style='color: #ff9933'>推荐使用map</div>

<h1 align='center'>3.Map</h1>

```javascript
// map  key => value 存储数据
let json = {
	name: 'jspang',
	skill: 'web'
}
console.log(json.name); // 打印 jspang
// =>
var map = new Map();
// 增加 set()
map.set(json,'iam');
console.log(map);  // 打印 Map { { name: 'jspang', skill: 'web' } => 'iam' }
map.set('jspang',json); 
console.log(map);  
// 打印 Map {
//   { name: 'jspang', skill: 'web' } => 'iam',
//   'jspang' => { name: 'jspang', skill: 'web' }
// }

// 查找 get('key值') 返回 value
console.log(map.get(json));  // 打印 iam
console.log(map.get('jspang')); //  打印 { name: 'jspang', skill: 'web' }

// 删除 delete()
map.delete(json);
console.log(map);  // 打印 Map { 'jspang' => { name: 'jspang', skill: 'web' } }

// size 属性 
console.log(map.size) // 1

// 查找 has('key值') 返回 true 或者 false
console.log(map.has('jspang')); // true
console.log(map.has('胖子')); // false

// 清空map
map.clear()
console.log(map); // 打印 Map {}

// 总结
// set:添加 get,has:通过key查找 delete:通过key删除 clear():清空map size: 返回map大小(多少对k-v)
```

