# JavaScript进阶-高级特性及ES6

任务

- 对象的扩展

- let和const
- Object.keys()
- for...of
- 扩展运算符
- Set 和 Map
- 模版字符串
- 默认参数
- rest参数
- 箭头函数
- 解构赋值





### 对象的扩展

###### 方法的简写

```
// ES6
const person = {
	sayName() {
		console.log('我是pyy')
	},
	sayAge() {
		console.log('我17岁')
	},
}

// ES5
var person = {
	sayName: function() {
		console.log('我是pyy')
	},
	sayAge: function() {
		console.log('我17岁')
	},
}
```



###### 属性简写

当对象的属性名和属性值相同时，可以简写。

```
// ES6属性简写
const name = 'pyy'
const age = 17
const person = {name,age}
// 等同于
const person = {name:name,age:age}
```



### let和const

###### let

ES6 新增了`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效。

例如：

```
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

var命令声明的变量会发生“变量提升”现象，即变量可以在声明之前使用，值为undefined。`let`命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

```
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

`let`不允许在相同作用域内，重复声明同一个变量。

```
// 报错
function fn() {
  let a = 10;
  var a = 1;
}

// 报错
function fn() {
  let a = 10;
  let a = 1;
}
```

注意： 只有使用var声明的变量才是全局变量。

总结：

- `let`不允许在相同作用域内，重复声明同一个变量。
- `let`不存在变量提升，它所声明的变量一定要在声明后使用。
- `let`声明的变量只在它**所在的代码块**有效。



###### 块级作用域

ES5 只有全局作用域和函数作用域，没有块级作用域。

所以导致内层变量可能会覆盖外层变量。

```
var tmp = new Date();

function f() {
  console.log(tmp);
  if (false) {
    var tmp = 'hello world';
  }
}
f(); // undefined
```

变量提升，内层的`tmp`变量覆盖了外层的`tmp`变量。

还会导致用来计数的循环变量泄露为全局变量。

```javascript
var s = 'hello';
for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}
console.log(i); // 5
```

上面代码中，变量`i`只用来控制循环，但是循环结束后，它并没有消失，泄露成了全局变量。



`let`实际上为 JavaScript 新增了块级作用域。

先来看看使用var声明的：

```
function fn() {
  var n = 5;
  if (true) {
    var n = 10;
  }
  console.log(n); // 10
}
fn()
```

然后我们来看看使用let声明的：

```
function fn() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
fn()
```

函数有两个代码块，都声明了变量`n`，运行后输出 5。这表示外层代码块不受内层代码块的影响。

注意：ES6 的**块级作用域必须有大括号**，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。

**进阶：**

ES6 允许块级作用域的任意嵌套。

例如：

```
// 5层嵌套
{{{{{
	let a = 100;
	console.log(a); // 100
}}}}}
```

变法1:

```
// 6层嵌套
{{{{{
	let a = 100;
	{console.log(a)} // 100
}}}}}
```

变法2:

```
// 6层嵌套
{{{{{
	{let a = 100;}
	{console.log(a)} // 报错
}}}}}
```

变法3:

```
// 5层嵌套
{{{{{
	{let a = 100;}
	console.log(a) // 报错
}}}}}
```

变法4:

```
// 5层嵌套
{{{{
	let a = 100;
	{
		{console.log(a)} // 100
  }
}}}}
```

变法5:

```
// 5层嵌套
{{{{
	{let a = 100;}
	{
		{console.log(a)} // 报错
  }
}}}}
```

扩展：

只要块级作用域内存在`let`命令，它所声明的变量就“绑定”这个区域，不再受外部的影响。

```
if(true) {
	// if条件语句块不会创建一个新的作用域
   var a = 100; // a 依然在全局作用域中
}
console.log(a);// 100
```

```
if(true) {
  let a = 100;
}
console.log(a); //报错  a is not defined
```

```
var a = 1;

if (true) {
  a = '100'; 
}
console.log(a)
```

```
var a = 1;

if (true) {
  a = '100'; 
  let a;
}
console.log(a)
```

```
var a = 1;

if (true) {
  let a = '100'; 
}
console.log(a)
```

所以如果区块中存在`let`和`const`命令，这个区块对这些命令声明的变量，从一开始就形成了**封闭作用域**。

并且在代码块内，使用`let`命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”。

扩展中的扩展：

```
let a = 10
if(true) {
    console.log(a);
    let a = 20; // 报错
}
```



```
var y = y;
let x = x;
// 因为暂时性死区,使用let声明变量时，只要变量在还没有声明完成前使用，就会报错。在变量x的声明语句还没有执行完成前，就去取x的值，导致报错x 未定义。
```



###### const

1. `const`声明一个只读的常量。一旦声明，常量的值就不能改变。

   ```
   const MAX = 5;
   MAX = 10;// TypeError: Assignment to constant variable.
   ```

2. `const`声明的变量不得改变值，这意味着，`const`一旦声明变量，就必须立即初始化，不能留到以后赋值。

   ```
   const MAX; // SyntaxError: Missing initializer in const declaration
   ```

3. `const`声明的变量只在声明所在的块级作用域内有效。

   ```
   if (true) {
     const MAX = 5;
   }
   
   console.log(MAX) // Uncaught ReferenceError: MAX is not defined
   ```

4. `const`命令声明的常量也是不会变量提升

   ```
   if (true) {
     console.log(MAX); // ReferenceError
     const MAX = 5;
   }
   ```

5. 不可重复声明

   ```
   var min = "1";
   let max = 25;
   
   // 以下两行都会报错
   const min = "2";
   const max = 30;
   ```

Const小结：

- `const`一旦声明变量，就必须立即初始化
- 不能重复声明
- 不能再赋值
- 只在声明所在的块级作用域内有效。
- `const`命令声明的常量也是不提升
- 为了表示变量是常量(不可修改)，所以一般**约定变量名全大写**



###### 总结

- var可以重复声明，let、const不可以
- var声明的变量是全局变量，let、const不是，只在声明所在的块级作用域内有效。
- var声明的变量存在变量提升，let、const不是
- var、let声明的变量可以再赋值，const不行
- var、let可以先声明后赋值，const不行，一旦声明变量就必须立即初始化。



### Object.keys()

`Object.keys()` 方法会返回一个指定`object`对象的属性组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致 。

语法：

```
Object.keys(obj)
```

例子：

```
let obj = {
	name: 'pyy',
	age: 17,
	sex: 'man'
}
console.log(Object.keys(obj)); // ['name','age','sex']
```

用于数组时，获取的是数组的索引。（了解）

```
let arr = ['pyy',17,'man'];
console.log(Object.keys(arr)); // ['0', '1', '2']
```





### for...of

官方描述：一个数据结构只要部署了`Symbol.iterator`属性，就被视为具有 iterator 接口，就可以用`for...of`循环遍历它的成员。也就是说，`for...of`循环内部调用的是数据结构的`Symbol.iterator`方法。（了解）

###### 数组

前言：数组原生具备`iterator`接口（即默认部署了`Symbol.iterator`属性），`for...of`循环本质上就是调用这个接口产生的遍历器

语法：

```
for(let 变量 of 数组名) {
  console.log(v); 
}
```

与for...in的对比：

- 原有的`for...in`循环，只能获得对象的键名(数组中就是索引)，不能直接获取键值
- `for...of`循环，允许遍历获得键值(数组中就是数组元素)。

```
let arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a); // 0 1 2 3
}

for (let a of arr) {
  console.log(a); // a b c d
}
```



###### 字符串

字符串也可以使用。

```
// 字符串
let str = "hello";
for (let s of str) {
  console.log(s); // h e l l o
}
```



###### 对象

对于普通的对象，`for...of`结构不能直接使用，会报错。（可以使用for...in）

```
let obj = {
	name: 'pyy',
	age: 17,
	sex: 'man'
}

for (let v in obj) {
	console.log(v); // name  age  sex
}

for (let v of obj) { // 报错
	
}
```

替代：

```
let obj = {
	name: 'pyy',
	age: 17,
	sex: 'man'
}
for (let key of Object.keys(obj)) {
  console.log(key); // 键名
  console.log(obj[key]); // 键值
  console.log(key + ': ' + obj[key]); // 键值对
}
```







### 模版字符串

模板字符串是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

```
// 普通字符串
`qwwqdfqeq`

// 多行字符串
`131213
eweqweqeq`

// 字符串中嵌入变量
let name = "pyy", age = 17;
`我是${name},我今年${age}岁`
```

注意：模板字符串中嵌入变量，需要将变量名写在`${}`之中，内部可以放入任意的表达式，还可以进行运算，以及引用对象属性，甚至还可以调用函数。

```
// 表达式
let x=1,y=2;
`${x} + ${y} = ${x + y}`

// 进行运算
`${x} + ${y * 2} = ${x + y * 2}`

// 引用对象属性
let obj = {x: 1, y: 2};
`${obj.x + obj.y}`

// 调用函数
function fn() {
  return "pyy";
}
`我是${fn()}，嘿嘿嘿`
```





### 扩展运算符

概念：扩展运算符`...`是es2015的新特性，也被称为rest或者spread运算符,能够去简化一些数据的操作。

###### 数组中

可以理解为扩展运算符在数组中的作用是将数组给展开。

1. 复制数组

   ```
   const a1 = [1, 2];
   const a2 = [...a1];
   ```

2. 合并数组

   ```
   const a1 = [1, 2];
   const a2 = [3, 4];
   const a3 = [5, 6];
   const a4 = [...a1, ...a2, ...a3];
   console.log(a4); // [1,2,3,4,5,6]
   ```

3. 与解构赋值结合

   ```
   const [first, ...rest] = [1, 2, 3, 4, 5];
   first // 1
   rest  // [2, 3, 4, 5]
   ```

   注意：如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错。

注意： **扩展运算符是浅拷贝**（拷贝的是**引用数据类型的地址**）

```
const a1 = [{ foo: 1 }];
const a2 = [{ bar: 2 }];
const a3 = [...a1, ...a2];
a3[0] === a1[0] // true
```

```
let arr = [1, 2, 3, 4, 5, { name: 1 }];
let arr1 = [...arr];
arr[5].a = 2
console.log(arr1);
console.log(arr);
```



###### 对象

同样，扩展运算符是浅拷贝对象

```
let obj = {
    name: 'pyy',
    age: 19,
    o: {
        sex: 'man'
    }
}

let obj1 = {...obj};
obj.o.sex = 20;
console.log(obj1);
console.log(obj);
```





合并对象

```
let obj1 ={
  name:'张三',
  age:12,
  address:{
  	city:'成都'
  }
};
let obj2 ={
  name:'pyy',
  sex: 'man',
  sayName:{
  	city:'成都'
  }
};
let newObj ={...obj1, ...obj2};
console.log(newObj);
/*{
  name: 'pyy',
  age: 12,
  address: { city: '成都' },
  sex: 'man',
  sayName: { city: '成都' }
}*/
```

合并对象时，前面对象先展开，后面对象的属性，会**覆盖前面对象的属性**。

```
let obj1 ={
  name:'张三',
  age:12,
  address:{
  	city:'成都'
  }
};
let obj2 ={
  name:'pyy',
  sex:'man',
  address:{
  	city:'北京'
  }
};
let newObj ={...obj1, ...obj2};
obj1.address.city = 'cd' // newObj不会改变
obj2.address.city = 'bj' // 引用
obj2.sex = 'woman' // 非引用
console.log(newObj);
```



###### 函数

一般用于函数的参数中

1. 形参中(rest参数)

   会将所有的实际参数放入到数组中，并在函数体里使用

   ```
   function demo(...d){
     	console.log(d); // [1,2,3,4]
    }
   demo(1,2,3,4);
   ```

   注意：如果有多个形式参数，`…`必**须是最后一个**，表示把剩余的参数放入到数组中

   ```
   function demo(first,...d){ 
     	console.log(d); // [2,3,4]
    }
   demo(1,2,3,4);
   ```

2. 实参中

   表示把数据进行展开，即相当于传入了多个实际参数。

   ```
   let arr = [1,2,3];
   let str = "abc";
   function demo(a,b,c){
   	console.log(a,b,c);
   }
   demo(...arr); // 实际效果：demo(1,2,3)
   demo(...str); // 实际效果：demo('a','b','c');
   ```

   如果实际参数大于了形式参数的数量，那么多余的实际参数会被忽略掉

   ```
   let arr = [1,2,3];
   let str = "abcdefg";
   function demo(a,b,c){
   	console.log(a,b,c);
   }
   demo(...arr); // 实际效果：demo(1,2,3)
   demo(...str); // 实际效果：demo('a','b','c','d','e','f','g');
   // 输出： 'a','b','c'
   ```

3. 结合使用

   ```
   let arr = [1,2,3];
   let str = "abcdefg";
   function demo(a,b,c, ...d){
   	console.log(a,b,c);
   	console.log(d)
   }
   demo(...arr); // 实际效果：demo(1,2,3)
   demo(...str); // 实际效果：demo('a','b','c','d','e','f','g');
   ```

   



###### 字符串

扩展运算符还可以将字符串转为真正的数组。

```
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```





### rest 参数

ES6 引入 rest 参数（形式为`...变量名`），用于获取函数的多余参数，这样就不需要使用`arguments`对象了。rest 参数搭配的变量是一个**数组**，该变量将**多余的参数放入数组中**。

```
function demo(...d){ 
    console.log(d); // [1,2,3,4]
 }
demo(1,2,3,4);
function demo(first,...d){ 
    console.log(d); // [2,3,4]
 }
demo(1,2,3,4);
```

注意：rest 参数之后不能再有其他参数（即**只能是最后一个参数**），否则会报错

```
function f(a, ...b, c){} // // 报错
```

注意：函数的`length`属性，不包括 rest 参数和参数的默认值。

```
function f(x,y=1,...d) {
  console.log(x);   // undefined
  console.log(y);   // 1
  console.log(d); // []
}
f()
console.log(f.length); // 1
```



### Set 和 Map

###### Set

ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

`Set`本身是一个构造函数，用来生成 Set 数据结构。

语法：

```
let s = new Set();
// 添加数据方法：（了解）
s.add(1)
s.add(2)
s.add(1)
s.add(3)
// 获取长度（了解）
console.log(s.size); // 3   因为成员的值都是唯一的
```



`Set`函数可以接受一个数组作为参数，用来初始化。

```
const set = new Set([1, 2, 3, 4, 4]); // 类似于数组，不是真数组
const arr = [...set];// 变为真数组
```

所以所以所以就有了**去除数组重复成员的方法**：

```
// 去除数组的重复成员
[...new Set(array)]
```

也可以用于去除字符串里面的重复字符。

```
[...new Set('ababbc')].join('')
// "abc"
```



注意：

- 向 Set 加入值的时候，不会发生类型转换，所以`5`和`"5"`是两个不同的值。
- Set 内部判断两个值是否不同，类似于精确相等运算符（`===`）。
- 精确相等运算符认为`NaN`不等于自身。
- 两个对象总是不相等的。

```
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
console.log(set.size); // 1
// 向 Set 实例添加了两次NaN，但是只会加入一个。这表明，在 Set 内部，两个NaN是相等的。
```

```
let set = new Set();

set.add({});
set.size // 1

set.add({});
set.size // 2
```



###### Map

背景： js中的对象，本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，**各种类型的值（包括对象）都可以当作键**。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应。

`Map`本身是一个构造函数

语法：

```
const m = new Map();
```

例子：

```
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content'); // 将对象o当作m的一个键  
console.log(m); //   Map { { p: 'Hello World' } => 'content' }
console.log(m.size); // size属性返回 Map 结构的成员总数。
m.get(o) // "content"  // 读取这个键

m.has(o) // true    // 是否拥有这个键
m.delete(o) // true // 删除这个键
m.has(o) // false
```



###### 总结(重点)

- Set成员的值都是唯一的，没有重复的值，可以用来数组去重
- Map类似于对象，也是键值对的集合，但是键名可以是各种类型的值（包括对象）。







### 默认参数

###### 语法

ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。

```
function log(x, y = 'china') {
  console.log(x, y);
}

log('Hello') // Hello china
log('Hello', 'chengdu') // Hello chengdu
log('Hello', '') // Hello
```

注意：

1. 参数变量是默认声明的，所以不能用`let`或`const`再次声明。

   ```
   function fn(x = 5) { // 参数变量x是默认声明的
     let x = 1; // 报错
     const x = 2; // 报错
   }
   ```

2. 使用参数默认值时，函数不能有同名参数。

   ```
   function fn(x,x,y) {} // 不报错
   function fn(x,x,y=1) {} // 报错
   ```

   

###### 默认参数的位置

通常情况下，定义了默认值的参数，应该是函数的尾参数。如果非尾部的参数设置默认值，实际上这个参数是没法省略的（需要写上undefined）。

```
function f(x = 1, y) {
  return [x, y];
}
f(, 1) // 报错
f(undefined, 1) // [1, 1]
```

注意： 如果传入`undefined`，将触发该参数等于默认值，`null`则没有这个效果。

```
function f(x = 1, y = 2) {
  console.log(x, y);
}

f(undefined, null)
// 1 null
// x参数对应undefined，结果触发了默认值，y参数等于null，就没有触发默认值。
```





### 箭头函数

ES6 允许使用“箭头”（`=>`）定义函数

语法：

```
let 函数名 = () => {}
```

例如：

```
let f = (a,b) => {
	return a + b
}
// 等同于
let f = function (a,b) {
 return a + b
};
```

1. 如果箭头函数**只有一个参数**，那么可以省略圆括号（如果没有参数或者参数有多个，那么圆括号都不能省略）

   ```
   let f = v => {
   	return v + 1
   }
   ```

2. 如果箭头函数的代码块部分**只有一条语句**，那么可以省略大括号和return字(两个要一起省略，写了大括号有返回值就要写return)

   ```
   let f = v => v + 1;
   let f = (x,y) => x + y;
   ```

   

3. 由于大括号被解释为代码块，所以如果箭头函数直接**返回一个对象**，必须在对象外面加上括号，否则会报错。

   ```
   // 报错  因为对象的{}被解析成为了函数的{}
   let getObj = name => { name: name, age: 14 };
   // 不报错
   let getObj = name => ({ name: name, age: 14 });
   ```

4. 注意箭头函数this问题

   ```
   // 箭头函数没有自己的this值，箭头函数中所使用的this都是来自函数作用域链（可以理解为拿取它父级的this）
   // 箭头函数体内的this对象，就是定义该函数时所在的作用域指向的对象，而不是使用时所在的作用域指向的对象。
   ```
```
    var name = 'window';
   const o = {
       name: 'o',
       f(){
       	console.log(this.name);
       }
   }
   o.f()
```

   ```
 var name = 'window';
const o = {
       name: 'o',
       f: () => {
       	console.log(this.name);
       }
   }
   o.f()
   // 作用域是指函数内部，这里的箭头函数，也就是f，所在的作用域其实是最外层的js环境，因为没有其他函数包裹；然后最外层的js环境指向的对象是winodw对象，所以这里的this指向的是window对象。
   ```

   ```
    var name = 'window';
   const o = {
       name: 'o',
       f(){
           let foo = () => {
               console.log(this.name);
           }
           return foo;
       }
   }
   o.f()();
   ```

   ```
   const o = {
         f() {
           // let fn = function() {
           //   console.log(this);
           // }
           let fn = () => {
             console.log(this);
           }
           fn()
         },
       }
       o.f();
   ```
   额外需要注意：（背，面试爱问   1-3点）

   1. 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。
   2. 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
      3. this指向问题： 箭头函数体内的this对象，就是定义该函数时所在的作用域指向的对象，而不是使用时所在的作用域指向的对象。
      4. 不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。



### 解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

###### 数组的解构赋值

以前，为变量赋值，只能直接指定值。

```
let a = 1;
let b = 2;
let c = 3;
```

ES6 允许写成下面这样。

```
let [a, b, c] = [1, 2, 3];
```

上面代码表示，可以从数组中提取值，按照**对应位置**，对**变量赋值**。

本质上，这种写法属于“模式匹配”，只要等号两边的**模式相同**，左边的变量就会被赋予对应的值。

解构分为完全解构和不完全解构。

- 完全解构：
  - 变量的数量跟数组里的数据量是一致的。
- 不完全解构
  - 如果是数组的数据量不够，即变量过多，剩余的变量就是undefined
  - 如果是数组的数据量过多，剩余的数据没有被接收

例如：

```
let [x, , y] = [1, 2, 3];
x // 1
y // 3
```

```
let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // [2, 3, 4]
```

```
let [x, y, ...z] = ['a'];
x // "a"
y // undefined
z // []
```

```
let [foo] = []; // foo  === undefined
let [bar, foo] = [1]; // foo  === undefined
```

```
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```

```
// 都会报错
let [foo] = 1;
let [foo] = false;
let [foo] = NaN;
let [foo] = undefined;
let [foo] = null;
let [foo] = {};
```

解构赋值允许指定默认值。

```
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```

注意，ES6 内部使用严格相等运算符（`===`），判断一个位置是否有值。所以，只有当一个数组成员严格等于`undefined`，默认值才会生效。

```
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null
```



###### 对象的解构赋值

注意：

当对象的key和value都一样的时候，可以简写。

例如： 

```
let obj = {
	name: name,
	age: age
}
可以简写为
let obj = {
	name,
	age
}
```



解构不仅可以用于数组，还可以用于对象。

```javascript
let { foo: foo, bar: bar } = { foo: 'aaa', bar: 'bbb' }; // 一一对应
```

变法1:

```
let { foo, bar } = { foo: 'aaa', bar: 'bbb' }; // 就是上面的简写
```

变法2:  

```
let { foo: f1, bar: f2 } = { foo: 'aaa', bar: 'bbb' }; // 还是一一对应
// 观察： 解构就是等号左右两侧一一对应。 左边{}里的foo和bar是匹配的模式，用来匹配右边对象的key。  而f1、f2才是变量，用来接收(赋值) 为右边对象相应key对应的value
```

注意：

- 如果解构失败，变量的值等于`undefined`。
- 对象结构是没有次序的，变量与属性同名，就能取到值。

```
let { bar: f1, foo1: f2 } = { foo: 'aaa', bar: 'bbb' };
```



**默认值:**

对象的解构也可以指定默认值。

```
let {x = 3} = {};
x // 3

let {x, y = 5} = {x: 1};
x // 1
y // 5

let {x: y = 3} = {};
y // 3

let {x: y = 3} = {x: 5};
y // 5
```

注意：**默认值生效的条件是，对象的属性值严格等于`undefined`。**

```
let {x = 3} = {x: undefined};
x // 3

let {x = 3} = {x: null};
x // null
```

上面代码中，属性`x`等于`null`，因为`null`与`undefined`不严格相等，所以是个有效的赋值，导致默认值`3`不会生效。



###### 字符串的解构赋值

字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象

```
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```





扩展总结：

- 解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。
- 由于`undefined`和`null`无法转为对象，所以对它们进行解构赋值，都会报错。





###### 函数参数的解构赋值

函数的参数也可以使用解构赋值。

```
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

上面代码中，函数`add`的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量`x`和`y`。对于函数内部的代码来说，它们能感受到的参数就是`x`和`y`。

函数参数的解构也可以使用默认值。

```
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```

注意和下面代码的对比

```
function move({x = 0, y = 0}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // 报错
```



解构的用途：

1. 交换变量的值

   ```
   let x = 1;
   let y = 2;
   [x, y] = [y, x];
   ```

   ```
   let x = 1;
   let y = 2;
   let [x,y] = [y,x]; // 会报错 因为又声明了变量x、y
   console.log(x,y);
   ```
   
   



### 练习

1. 定义一个函数，传入多个数据，完成字符串拼接并返回（要求：  使用rest参数，函数形参）。

2. 将以下二维学生数组转为一维学生对象数组（要求：定义一个函数，函数不能接收数组）（需要使用的技术：1. 对象属性的简写   2.调用函数实参使用扩展运算符  3. 不能定义其他数组）

   ```
   let students = [
              ['pyy',12,'男'],//姓名 年龄  性别 
              ['wyz',23,'男'],
              ['wemz',33,'女']
     ];
     
     得到下面的格式：
     let students = [
     	{ name: 'pyy', age: 12, 'sex': '男'},
     	{ name: 'pyy', age: 12, 'sex': '男'},
     	{ name: 'pyy', age: 12, 'sex': '男'},
     ];
    
   ```

3. ```
   // 先自己分析这两种方式的输出，然后打印查看结果再分析
   let obj = {
   	name: 'pyy'
   }
   let obj1 = obj;
   obj.name='wyz'
   console.log(obj1)
   
   
   let obj = {
   	name: 'pyy'
   }
   let obj1 = { ...obj }
   obj.name='wyz'
   console.log(obj1);
   
   
   
   
   
   
   let obj = {
   	name: 'pyy',
   	o: {
   		a: 1
   	}
   }
   let obj1 = { ...obj }
   obj.o.a = 2;
   console.log(obj1);
   ```

   




### 补充

###### 内存空间

基本数据类型： 存放在栈中。引用数据类型，数据存储在堆中，变量中存储的是堆地址。

基本数据类型赋值时，拷贝的是数据；引用类型赋值时，拷贝的是地址。



扩展： 栈使用的是一级缓存， 他们通常都是被调用时处于存储空间中，调用完毕立即释放。Js一般用于存储基本数据类型    堆则是存放在二级缓存中，生命周期由虚拟机的垃圾回收算法来决定（并不是一旦成为孤儿对象就能被回收）。所以调用这些对象的速度要相对来得低一些。一般用于存储引用类型。





###### 深浅拷贝

浅拷贝是指**复制**指向某个对象的**指针（地址）**而不复制对象本身，新旧对象还是共享同一块内存，修改一个另一个也会改变。

深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象。

**常见的浅拷贝的实现方式**

1. Object.assign()

2. concat()

3. 扩展运算符...

4. 赋值=
5. slice（了解）







**深拷贝的实现方式**

1. JSON.parse(JSON.stringify())序列化数组或对象

   原理： 用JSON.stringify将对象转成JSON字符串，再用JSON.parse()把字符串解析成对象，新的对象产生了，而且对象会开辟新的栈，实现深拷贝。

   用法：

   ```
   let arr=[1,2,3,{ x: 1 }];
   let str = JSON.stringify(arr);
   let newArr = JSON.parse(str);
   arr[3].x=2;
   console.log(arr);
   console.log(newArr);
   ```

   缺陷：

   - 序列化时会把函数和undefined丢失
   - 会把NaN序列化为null

   好处：

   - 判断数组是否包含某对象，或者判断对象是否相等。

     ```
     let arr = [
         {name:'pyy'},
         {name:'wyz'},
         {name:'gtl'},
     ];
     let obj = {name:'wyz'}
     console.log(JSON.stringify(arr).includes(JSON.stringify(obj)));
     ```

   - 判断两数组/对象是否相等

     ```
     let a = [1,2,3],b = [1,2,3];
     console.log(JSON.stringify(a) === JSON.stringify(b));
     ```

   - 让本地存储可以存储对象。

   

   

   2. 递归实现深拷贝

      ```
      // 深拷贝对象
      function deepClone(o) {
          let obj = {};
          for (let key in o) { // 遍历目标
              if (typeof o[key] === 'object') { // 如果值是对象，就递归一下
                  obj[key] = {};
                  obj[key] = deepClone(o[key]);
              } else { // 如果不是，就直接赋值
                  obj[key] = o[key];
              }
          }
          return obj;
      }
      ```

      ```
      // 深拷贝对象、数组
      function deepClone(o) {
          let obj = o.constructor === Array ? [] : {}; // 判断复制的目标是数组还是对象
          for (let key in o) { // 遍历目标
              if (typeof o[key] === 'object') { // 如果值是对象，就递归一下
                  obj[key] = o[key].constructor === Array ? [] :{}; // 判断复制的目标是数组还是对象
                  obj[key] = deepClone(o[key]);
              } else { // 如果不是，就直接赋值
                  obj[key] = o[key];
              }
          }
          return obj;
      }
      ```

      



###### 对象的方法

Object.assign()

Object.assign方法用于将所有可枚举属性的值从一个或多个源对象分配到目标对象。它将返回目标对象

语法： 

```
let obj = Object.assign(target,...sources)；
// target: 目标对象
// sources: 源对象。
// obj: 目标对象。
// 注意：如果目标对象中的属性具有相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。
```

例子：

```
// 复制一个对象
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```

```
const o1 = { a: 1 };
const o2 = { b: 2 };
const o3 = { c: 3 };

const obj = Object.assign(o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
console.log(o1);  // { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。
```

```
const o1 = { a: 1 };
const o2 = { b: 2 };
const o3 = { c: 3 };

const obj = Object.assign({},o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
console.log(o1);  // { a: 1 }, 注意对比，o1自身不会改变。
```

```
const o1 = { a: 1, b: 1, c: 1 };
const o2 = { b: 2, c: 2 };
const o3 = { c: 3 };

const obj = Object.assign({}, o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 } 后面的源对象的属性将覆盖前面的源对象的属性。
```



Object.defineProperty()





Object.is()

`Object.is()` 方法判断两个值是否为同一个值。

语法：

```
let result = Object.is(value1, value2);
```



```
Object.is('foo', 'foo');     // true
Object.is('foo', 'bar');     // false
Object.is([], []);           // false
let foo = { a: 1 };
let bar = { a: 1 };
Object.is(foo, foo);         // true
Object.is(foo, bar);         // false

// 特例
Object.is(0, -0);            // false
0 === -0 										 // true
Object.is(0, +0);            // true
Object.is(-0, -0);           // true
```



###### 异常

try{

​	校验代码是否有错（是否有异常）

}catch(error){

​	如果有异常，该异常的相关信息会保存在参数error中，error是一个异常对象。

​	 console.log(error);

​      console.log(error.name);

​      console.log(error.message);

}finally{

​	无论有无异常，都会执行finally中的代码

}

例如：

```
 		var a =1;
        try{
            a=2;
            console.log(a);
            console.log(b);
            console.log('123');
        }catch(error){
           	console.log(error);
            console.log(error.name);
            console.log(error.message);
        }finally{
            console.log('无论有无异常，都会执行finally中的代码');
        }
        console.log('处理异常后程序会继续执行，而不会报错停止');
```





###### 内置对象

**Math**

方法：

```
1. abs:获取绝对值
2. round：四舍五入
3. floor：向下取整
4. ceil：向上取整
5. random：0-1之间的随机数，不包含1
6. sqrt：某个数的平方根是这个值
7. pow：x的y次方
8. min:求几个数中的最小数
9. max:求几个数中的最大数
```

```
console.log(Math.abs(-9));//9
console.log(Math.round(-4.2));//-4
console.log(Math.floor(4.3));//4
console.log(Math.ceil(4.3));//5
console.log(Math.sqrt(4));//2 
console.log(Math.pow(4,3));//64 
console.log(Math.max(4,3,2,9));//9
console.log(Math.min(4,3,2,9));//2
```



**Date**

JavaScript唯一可以处理时间 的内置类。

方法

```
1. 获取当前时间
let now = new Date();

2。 获取年月日 时分秒
时间对象名.getFullYear() ;获取年份
时间对象名.getMonth();获取月份，从0开始 0~11 表示1到12月
时间对象名.getDate();获取当月的天数
时间对象名.getHours();获取小时数，24小时制
时间对象名.getMinutes();获取分钟数
时间对象名.getSeconds();获取当前的秒数
时间对象名.getDay();获取星期几 0~6  0表示星期天  6表示星期六
时间对象名.getTime();获取当前时间和1970年1月1日0时0份0秒之间的毫秒数
```





###### toFixed

`toFixed()` 方法用来格式化一个数值(四舍五入得指定位数小数，去掉剩余小数)。

语法：

```
number.toFixed(参数)
```

参数：小数点后数字的个数，0 到 20 之间，省略默认为0.

```
let num = 12345.6789;

num.toFixed();         // 12346：进行四舍六入五
num.toFixed(1);        // 12345.7：进行四舍六入五
num.toFixed(6);        // 12345.678900：用0填充

// 了解：
2.55.toFixed(1)       // ？   
```

```
2.55-2.5  // 0.04999999999999982
// 由于2.55不是精确表示的，而2.5是可以精确表示的，所以2.55 - 2.5就可以得到0.05存储的值。可以看到确实是比0.05小。
// 根本原因在于2.55的存储要比实际存储小一点，导致0.05的第1位尾数不是1，所以就被舍掉了。
// js计算精度存在问题  0.1 + 0.2 === 0.3   =>  false
```



### 扩展

###### 解构

1. 如果要将一个已经声明的变量用于解构赋值，必须非常小心。

   ```
   let x;
   {x} = {x: 1};
   // SyntaxError: syntax error
   ```

   上面代码的写法会报错，因为 JavaScript 引擎会将`{x}`理解成一个代码块，从而发生语法错误。只有不将大括号写在行首，避免 JavaScript 将其解释为代码块，才能解决这个问题。

   ```
   // 正确的写法
   let x;
   ({x} = {x: 1});
   ```

2. 由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

   ```
   let arr = [1, 2, 3];
   let {0 : first, [arr.length - 1] : last} = arr;
   first // 1
   last // 3
   ```

   上面代码对数组进行对象解构。数组`arr`的`0`键对应的值是`1`，`[arr.length - 1]`就是`2`键，对应的值是`3`。方括号这种写法，属于“属性名表达式”。

3. 类似数组的对象都有一个`length`属性，因此还可以对这个属性解构赋值。

   ```
   let {length : len} = 'hello';
   len // 5
   ```

4. 解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

   ```
   let {toString: s} = 123;
   s === Number.prototype.toString // true
   
   let {toString: s} = true;
   s === Boolean.prototype.toString // true
   ```

   上面代码中，数值和布尔值的包装对象都有`toString`属性，因此变量`s`都能取到值。

5. 函数参数的解构赋值

   ```
   function move({x, y} = { x: 0, y: 0 }) {
     return [x, y];
   }
   
   move({x: 3, y: 8}); // [3, 8]
   move({x: 3}); // [3, undefined]
   move({}); // [undefined, undefined]
   move(); // [0, 0]
   ```

   上面代码是为函数`move`的参数指定默认值，而不是为变量`x`和`y`指定默认值，所以会得到与前一种写法不同的结果。

6. 交换变量

   ```
   let a = 10, b = 20;
   [b, a] = [a, b]; // a=20 b=10
   ```

   注意下面的写法是错误的：

   ```
   let a = 10, b = 20;
   let [b, a] = [a, b];// 报错 Identifier 'b' has already been declared
   ```

   只是交换两个变量的数据，而不是重新声明变量。



###### 扩展运算符

1. 复制数组

   ```
   const a1 = [1, 2];
   // 方式1
   const a2 = [...a1];
   // 方式2  但是不建议 
   const [...a2] = a1; 
   ```

2. ```
   let obj = { x: 1, y: 2, z: 3 }
   console.log([...obj]) // TypeError
   ```

   如何让上述扩展成功呢？

   需要知识点：

    Symbol.iterator
   为每一个对象定义了默认的迭代器。该迭代器可以被 for…of 循环使用。

   Reflect.ownKeys
   静态方法 Reflect.ownKeys() 返回一个由目标对象自身的属性键组成的数组。

   - next 方法是迭代器iterator的一个方法
   - 它的返回至少有一个对象，且对象中有两个属性：value＆done
   - value 用于定义迭代出来的值
   - done 布尔类型：
     设置true，则直接返回；不设置或者设置false，则继续走方法，类似for循环。

   所以：

   ```
   let obj = { x: 1, y: 2, z: 3 }
   obj[Symbol.iterator] = function() {
   		return {
   			next:function(){
   				let objArr = Reflect.ownKeys(obj)
   				if (this.index < objArr.length-1) {
   					let key = objArr[this.index];
   					this.index++;
   					return { value: obj[key] };
   				} else {
   					return { done: true };
   				}
   			},
   			index:0
   		}
   }
   console.log([...obj]) // [1, 2, 3]
   ```

   





