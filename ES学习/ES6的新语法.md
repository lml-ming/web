## 一、ES6的新语法

### (1) let和const

- **let 声明一个变量**
- **const 声明一个常量**

### (2) 字符串扩展

- **includes(param)：返回布尔值，表示是否找到了param参数字符串**
- **startsWith(param)：返回布尔值，表示param参数字符串是否在原字符串头部**
- **endsWith(param)：返回布尔值，表示param参数字符串是否在原字符串尾部**

### (3) 数组解构

```js
let arr = [1, 2, 3]
const [a, b, c] = arr
console.log(a) // a= 1
console.log(b) // b= 2
console.log(c) // c= 3
12345
```

### (4) 对象解构

```js
const person = {
	name:'xu',
	age:20,
}
const { name:newName, age:newAge } = person
console.log(newName) // newName= xu
console.log(newAge ) // newAge = 20
1234567
```

### (5) 函数参数默认值

```js
function add(a, b=1){
	return a+b;
}
123
```

### (6) 箭头函数

- **函数只有一个参数**

```js
function show(a){
	console.log(a);
}
==>
const show2 = a => console.log(a);
12345
```

- **函数有多个参数**

```js
function add(a,b){
	console.log(a+b);
}
==>
const add2 = (a,b) => console.log(a+b);
12345
```

- **函数有多个参数，且多行代码**

```js
function add(a,b){
	let c = a + b
	return c;
}
==>
const add2 = (a,b) =>{
	let c = a+b;
	return c;
}
123456789
```

### (7) 箭头函数结合解构表达式

```js
const person = {
	name:'xu',
	age:20,
}
const hello2 = ( {name} ) => console.log(name);
12345
```

### (8) map函数

- **map函数接收一个函数，然后返回处理后的数组**

```js
let arr = [1, 2, 3]
let newArr = arr.map(item => return item+1);
// 返回 [2, 3, 4]
123
```

### (9) reduce函数

- **reduce函数接收一个函数和一个初始值（可选），然后返回处理后的一个数值**

```js
let arr = [1, 2, 3]
let newArr = arr.reduce((a,b)=>return a+b);
// 返回6
123
```

### (10) 扩展运算符

- **扩展运算符是…，将数组或者对象转为用逗号分隔开的参数序列**

```js
console.log(...[1, 2, 3]) // 1,2,3

//数组合并
let arr = [...[1, 2, 3],...[4,5,6]]
console.log(arr) // 1,2,3,4,5,6

//与解构表达式结合
const [first, ...rest] = [1,2,3]
console.log(rest) // 2,3
123456789
```

### (11) 异步函数Promise

- **扩展运算符是…，将数组或者对象转为用逗号分隔开的参数序列**

```js
const p = new Promise((resolve, reject)=>{
	setTimeout(()=>{
		let num = Math.random();
		if(num<0.5){
			resolve('success' + num);
		} else{
			reject('error' + num);
		}
	});
});

p.then(value=>{
	console.log(value);
}).catch(error=>{
	console.log(error);
})
12345678910111213141516
```

## 一、新集合Set

- **Set类似于数组，但是成员的值都是唯一的，没有重复的值，可以类比于C++中的集合Set**

### (1) 初始化Set

```js
const s = new Set([1,2,3,4,4,2]);
console.log(s); // Set(4) {1, 2, 3, 4}

123
```

### (2) Set转化成Array

```js
const items = new Set([1,9,4,6]);
const array = Array.from(items);
console.log(array); // [1,9,4,6]
123
```

#### (3) 打印Set的大小

```js
const s = new Set([1,2,3,4,4,2]);
console.log(s.size); // 4
12
```

#### (4) Set是否含有某个元素

```js
const s = new Set();
s.add(6).add(8).add(8);
console.log(s.size); // 2
console.log(s.has(6)); // true
console.log(s.has(7)); // false
console.log(s.has(8)); // true
123456
```

#### (5) Set删除某一个元素

```js
const s = new Set();
s.add(6).add(8).add(8);
console.log(s); // Set(2) {6, 8}
s.delete(6);
console.log(s); // Set(2) {8}
12345
```

#### (6) Set获取某一个元素

```js
const set = new Set([1, 2, 3, 4, 4]);
const result = [...set][1];
console.log(result);
123
```

#### (7) Set添加某一个元素

```js
const result= new Set();
result.add(1)
console.log(result);
123
```

#### (8) Set清除所有元素

```js
const result= new Set([2,1,5]);
result.clear()
console.log(result);
123
```

#### (7) Set应用—数组去重

```js
function dedupe(array) {
  return Array.from(new Set(array));
}

dedupe([1,1,2,3]); // [1,2,3]
12345
```

#### (8) 遍历Set

```js
// Set中的键=值
let set = new Set(['aaa', 'bbb', 'ccc']);

// 遍历Set中所有的键
for(let item of set.keys()) {
  console.log(item);  // aaa bbb ccc
}

// 遍历Set中所有的值
for(let item of set.values()) {
  console.log(item);  // aaa bbb ccc
}

// 遍历Set中所有的键值对
for(let item of set.entries()){
  console.log(item);  // ["aaa", "aaa"],["bbb", "bbb"],["ccc", "ccc"]
}

// 使用 for of 遍历Set中所有的值
for (let item of set) {
    console.log(item); // aaa bbb ccc
}

// 调用forEach()方法
set.forEach((value, key) => {
    console.log(key + ' : ' + value)
});
// aaa:aaa bbb:bbb ccc:ccc
12345678910111213141516171819202122232425262728
let s = new Set([6,7,8]);
// map 将原数组映射成新数组
s = new Set([...s].map(x => x * 2));
console.log(s); // [12,14,16]

// filter返回过滤后的新数组
s = new Set([...s].filter(x => (x % 3) ==0));
console.log(s); //[6]

// 实现并集、交集、差集
let s1 = new Set([6,7,8]);
let s2 = new Set([4,7,6]);

let union = new Set([...s1, ...s2]);
console.log(union);

let intersect = new Set([...s1].filter(x => s2.has(x)));
console.log(intersect);

let difference = new Set([...s1].filter(x => !s2.has(x)));
console.log(difference);

// 利用原Set结构映射出一个新的结构，然后赋值给原来的Set结构
let s1 = new Set([1,2,3]);
s1 = new Set([...s1].map(val => val *2));
console.log(s1);

// 利用Array.from
let s2 = new Set([1,2,3]);
s2 = new Set(Array.from(s2, val => val * 2));
console.log(s2);
```