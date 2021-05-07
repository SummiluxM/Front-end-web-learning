# JavaScript基础-数组

任务

- 数组的概念(掌握)
- 数组的使用
- 数组的遍历
- 数组的内置方法
- 二维数组





### 数组的概念

一组数据有序排列的集合就叫数组。也就是说将一组数据按一定顺序排列组合成为一个组合，这个组合就叫数组。

关于数组的几个概念：

**数组元素**： 数组中每一个数据。

**索引**：数组元素对应的编号，**从0开始**，依次递增。

**访问数组元素**：数组名称[索引]

**数组的长度**： 数组元素的个数。数组有个length属性，通过**数组名称.length**可以获取。

注意：因为索引是从0开始的，所以**数组长度 = 数组最后一个元素的索引+1**。





### 数组的使用

###### 数组的定义

1. 字面量实例化数组

   ```
   Let arr = [];
   ```

2. new字符实例化数组

   ```
   Let arr = new Array();
   ```



###### 数组的赋值

两种方式：

1. 声明数组的时候直接赋值添加元素。

   ```
   Let arr = [1,'2',3];
   Let arr = new Array(1,'2',3);
   ```

   注意： 数组元素之间以英文逗号隔开。

2. 数组索引添加元素

   ```
   let arr = [];
   arr[0] = 1; // 添加第一个数组元素(也就是索引为0),数据为1
   arr[1] = '2';
   arr[2] = 3;
   ```




###### 数组的访问

访问数组：   数组名称

访问数组中的元素：  数组名称[索引]

访问数组中的长度(数据的个数)：数组名称.length



###### 数组的修改

数组名称[索引] = 要修改的值



注意：

	1.  使用new字符实例化数组时，初始化赋值时如果是个数字，那么这个数字就代表数组的长度。例如：new Array(10); // 创建的数组有10个元素，只是都为空，但是数组的length为10。
 	2.  数组访问数组元素时，要是访问的索引不存在值，默认用undefined占位。
 	3.  如果赋值数组元素的时候，赋值的索引超过了最大的索引值，那么数组就会自动增加数组元素，中间的数据也会有占位。
 	4.  数组元素： 可以是任意类型的值（基本或者引用的都可以）。
 	5.  快速删除数组的最后一个数据方法： 数组名称.length--（了解）



###### 数组的遍历

什么叫数组的遍历：就是把数组中的元素依次取出来统一操作。

方法1:  for循环

语法：

```
for(let i = 0; i < 数组名称.length; i++) {
 		console.log(数组名称[i]); // i从0开始，到最大索引，所以可以拿到数组的每个元素。
}
```

例子：

```
let arr = ['html', 'css', 'javascript'];
for(let i = 0; i < arr.length; i++) {
	console.log(i); // i就是元素 索引
	console.log(arr[i]); // 数组名称[索引]获取数组元素，所以arr[i]就是对应的数组元素
}
```



方法2: forEach语法结构：

语法：

```
数组名称.forEach(function(item,index){
	console.log(item); // item就是数组的每个元素
	console.log(index); // index就是元素对应的索引
})
```

例子：

```
let arr = ['html', 'css', 'javascript'];
arr.forEach(function(item,index) {
	console.log(item); // item就是数组元素
	console.log(index); // index就是索引
})
```



###### 数组的内置方法

数组的内置方法就是系统已经为数组定义好了的方法,可以通过数组直接调用。

**需要注意两个点：  1. 是否改变原数组    2.  返回值**

1. arr.concat()

   此方法是连接两个或多个数组，不会更改现有数组，而是返回一个新数组。

   ```
   let newArray = oldArray.concat(value1、value2、...);
   ```

   例如：

   拼接添加新值：

   ```
   let oldArray = ['html', 'css', 'javascript'];
   let newArray = oldArray.concat('node');
   console.log(newArray);
   ```

   拼接数组：

   ```
   let oldArray = ['html', 'css', 'javascript'];
   let arr1 = [1,2,3];
   let arr2 = ['a', 'b', 'c'];
   let newArray1 = oldArray.concat(arr1, arr2);
   let newArray2 = oldArray.concat('node', arr2);
   ```

2. arr.join()

   此方法是按指定分隔符将数组分割成字符串。

   语法：

   ```
   let str = arr.join();
   ```

   注意：join()中可以指定一个字符串来分隔数组的每个元素，没有指定，数组元素用**逗号**分隔；如果是空字符串("")，则所有元素之间都没有任何字符。

   例如：

   ```
   let arr = ['html', 'css', 'javascript', 'node'];
   let str = arr.join(); //str = 'html,css,javascript,node';
   let str1 = arr.join(""); //str1 = 'htmlcssjavascriptnode';
   let str2 = arr.join("-"); //str = 'html-css-javascript-node';
   ```

3. arr.push()

   此方法是将一个或多个元素添加到数组的末尾，并返回该数组的新长度。

   语法：

   ```
   arr.push(value1, ..., valueN);
   ```

   例如：

   ```
   let arr = ['html', 'css', 'javascript'];
   let len = arr.push('node','java');
   console.log(arr); // [ 'html', 'css', 'javascript', 'node', 'java' ]
   console.log(len); // 5
   ```

4. arr.unshift()

   此方法是将一个或多个元素添加到数组的开头，并返回该数组的新长度。

   语法：

   ```
   arr.unshift(value1, ..., valueN);
   ```

   例如：

   ```
   let arr = ['html', 'css', 'javascript'];
   let len = arr.unshift('node','java');
   console.log(arr); // [ 'node', 'java','html', 'css', 'javascript' ]
   console.log(len); // 5
   ```

   注意, 如果传入多个参数，它们会被以块的形式插入到对象的开始位置，它们的顺序和被作为参数传入时的顺序一致。 于是，传入多个参数调用一次 `unshift` ，和传入一个参数调用多次 `unshift` (例如，循环调用)，它们将得到不同的结果。

   ```
   let arr = [4,5,6];
   arr.unshift(1,2,3);
   console.log(arr); // [1, 2, 3, 4, 5, 6]
   
   arr = [4,5,6]; // 重置数组
   arr.unshift(1);
   arr.unshift(2);
   arr.unshift(3);
   console.log(arr); // [3, 2, 1, 4, 5, 6]
   ```

5. arr.shift()

   此方法是从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度，并返回被移除的元素。

   语法：

   ```
   arr.shift();
   ```

   注意： `shift` 方法移除索引为 0 的元素(即第一个元素)，并返回被移除的元素，其他元素的索引值随之减 1。如果length属性的值为 0 (长度为 0)，则返回 undefined。

   例如：

   ```
   let arr = ['html', 'css', 'javascript'];
   let str = arr.shift();
   console.log(arr); // ['css', 'javascript'];
   console.log(str); // 'html'
   ```

   

6. arr.pop()

   此方法是从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度，并返回被移除的元素。

   语法：

   ```
   arr.pop();
   ```

   注意： 如果在一个空数组上调用 pop()，它将返回undefined。

   例如：

   ```
   let arr = ['html', 'css', 'javascript'];
   let str = arr.pop();
   console.log(arr); // ['html', 'css'];
   console.log(str); // 'javascript'
   ```

7. arr.reverse()

   此方法是将数组中元素的位置颠倒，并返回该数组。数组的第一个元素会变成最后一个，数组的最后一个元素变成第一个。该方法会改变原数组。返回值就是颠倒后的数组。

   语法：

   ```
   arr.reverse();
   ```

   例如：

   ```
   let arr = ['html', 'css', 'javascript'];
   arr.reverse();
   console.log(arr); // ['javascript', 'css', 'html'];
   ```

8. arr.slice()

   此方法是用来截取子数组，返回一个新的数组,原数组不会被改变,返回值是包含被提取元素的新数组。

   语法：

   ```
   arr.slice(begin, end);
   ```

   参数begin：

   - 参数可选

   - 起始索引，表示从该索引开始提取原数组元素。
   - 如果该参数为负数，则表示从原数组中的倒数第几个元素开始提取，例如：`slice(-2)` 表示提取原数组中的倒数第二个元素到最后一个元素（包含最后一个元素）。
   - 如果省略 `begin`，则 `slice` 从索引 `0` 开始。
   - 如果 `begin` 大于原数组的长度，则会返回空数组。

   参数end：

   - 参数可选

   -  终止索引，在该索引处结束提取原数组元素。`slice` 会提取原数组中索引从 `begin` 到 `end` 的所有元素（**包含 `begin`，但不包含 `end`**）。
   - 如果该参数为负数， 则它表示在原数组中的倒数第几个元素结束抽取。 `slice(-2,-1)` 表示抽取了原数组中的倒数第二个元素到最后一个元素（不包含最后一个元素，也就是只有倒数第二个元素）。
   - 如果 `end` 被省略，则 `slice` 会一直提取到原数组末尾。
   - 如果 `end` 大于数组的长度，`slice` 也会一直提取到原数组末尾。

   例如：

   ```
   let arr = ['html', 'css', 'javascript', 'node'];
   let newArr1 = arr.slice(1);
   let newArr2 = arr.slice(1,2);
   let newArr3 = arr.slice(-1);
   let newArr4 = arr.slice(-2,-1);
   let newArr5 = arr.slice(1,-1);
   console.log(newArr1); // [ 'css', 'javascript', 'node' ]
   console.log(newArr2); // [ 'css' ]
   console.log(newArr3); // [ 'node' ]
   console.log(newArr4); // [ 'javascript' ]
   console.log(newArr5); // [ 'css', 'javascript' ]
   ```

9. arr.splice()

   此方法是通过删除或替换现有元素或者添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组。

   语法：

   ```
   array.splice(start,deleteItem,item1,item2,...,itemN);
   ```

   参数start：

   - 修改的开始位置。
   - 如果超出了数组的长度，则从数组末尾开始添加内容。
   - 如果是负值，则表示从数组末位开始的第几位（从-1计数，这意味着-n是倒数第n个元素并且等价于`array.length-n`）
   - 如果负数的绝对值大于数组的长度，则表示开始位置为第0位。

   参数deleteItem：

   - 参数可选
   - **整数**，表示要移除的数组元素的个数。
   - 如果参数被省略，那么`start`之后数组的所有元素都会被删除。
   - 如果 `deleteItem`  大于 `start` 之后的元素的总数，则从 `start` 后面的元素都将被删除（含第 `start` 位）。
   - 如果 `deleteCount` 是 0 或者负数，则不删除元素。这种情况下，至少应添加一个新元素。

   参数item1,item2,...,itemN：

   - 要添加进数组的元素,从`start` 位置开始。如果不指定，则 `splice()` 将只删除数组元素。

10. arr.sort()

    此方法是对数组元素进行排序，默认按照字母顺序排序，也就是说就是按照字符编码进行排序。

    语法：

    ```
    arr.sort(sortFn);
    ```

    参数sortFn：

    - 参数可选
    - 用来指定按某种顺序进行排列的函数。
    - 函数有两个参数，第一个参数是 “第一个用于比较的元素”，第二个参数是 “第二个用于比较的元素”。
    - 如果 sortFn(a, b) 小于 0 ，那么 a 会被排列到 b 之前。
    - 如果 sortFn(a, b) 等于 0 ，那么 a 和 b 的相对位置不变。
    - 如果 sortFn(a, b) 大于 0 ，那么 b 会被排列到 a 之前。
    - 如果省略，元素按照转换为的字符串的各个字符的Unicode位点进行排序（B会在c之前，80会在9之前）。

    例子：

    ```
    let arr = [31, 6, 9, 80, 5, 55, 76, 755, 22];
    let newArr = arr.sort();  // Unicode位点排序
    console.log(newArr); // [22, 31, 5, 55, 6, 755, 76, 80, 9]
    
    let newArr1 = arr.sort(function(a, b) { // 升序
    	return a - b
    });
    console.log(newArr1); // [5, 6, 9, 22, 31, 55, 76, 80, 755]
    
    let newArr2 = arr.sort(function(a, b) { // 降序
    	return b - a
    });
    console.log(newArr2); // [755, 80, 76, 55, 31, 22, 9, 6, 5]
    ```

11. indexOf()

    `indexOf()`方法用于在数组中查询指定元素是否存在，如果存在返回匹配到的第一个索引，如果不存在，则返回-1。

    语法：

    ```
    let result = arr.indexOf(searchItem,fromIndex);
    ```

    参数searchItem：要查找的元素。

    参数fromIndex： 开始查找的位置，可选。

    返回值result：首个被找到的元素在数组中的索引位置; 若没有找到则返回 -1。

    例如：

    ```
    const arr = ['张三', '李四', '王二麻子', '彭于晏', '王二麻子'];
    console.log(arr.indexOf('王二麻子'));
    console.log(arr.indexOf('王二麻子 '));// 加了个空格 就不再相等
    ```

    扩展知识：

    参数fromIndex： 如果该值大于或等于数组长度，意味着不会在数组里查找，返回-1。如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1表示从最后一个元素开始查找，-2表示从倒数第二个元素开始查找 ，以此类推。 注意：如果参数中提供的索引值是一个负值，并不改变其查找顺序，查找顺序仍然是从前向后查询数组。如果抵消后的索引值仍小于0，则整个数组都将会被查询。其默认值为0.

    ```
    const arr = ['张三', '李四', '王二麻子', '彭于晏', '王二麻子'];
    console.log(arr.indexOf('张三',-4));
    ```

12. includes()

    `includes()` 方法用来判断一个数组是否包含一个指定的值，如果包含则返回 true，否则返回false。

    ```
    const arr = ['张三', '李四', '王二麻子', '彭于晏', '王二麻子'];
    console.log(arr.includes('王二麻子'));
    console.log(arr.includes('王二麻子 '));// 加了个空格 就不再相等
    ```

    注意：

    - 参数和indexOf()方法一致
    - 返回值是true(包含)和false(不包含)
    - 比较字符串和字符时是区分大小写。

    ```
    [1, 2, NaN].includes(NaN); // true
    [1, 2, NaN].indexOf(NaN); // -1
    ```



### 二维数组

什么是二维数组呢？一个数组里的每个数据都是一个**一维数**组，那么该数组就是二维数组。

作用：一般用来表示复合型的数据并处理。复合型的数据一般会认为是具有多个信息的个体。比如手机、学生、商品等。像学生，有姓名、性别、年龄等具体数据。一个学生数据可以用一维数组表示，那么多个学生就用二维数组来表示。

###### 初始化二维数组：

方式1:(推荐写法)

```
let arr = [
	[1,2,3],
	[4,5,6],
	[7,8,9]
]
```

方式二：

```
let arr1 = [1,2,3];
let arr2 = [4,5,6];
let arr3 = [7,8,9];
let arr = [arr1, arr2, arr3];
```

方式三：

```
let arr = new Array(
	new Array(1, 2, 3),
	new Array(4, 5, 6),
	new Array(7, 8, 9),
)
```



###### 访问二维数组中的元素

```
let arr = [
	[1,2,3],
	[4,5,6],
	[7,8,9]
];
console.log(arr[1]); // 访问arr索引为1的数组元素  => [4,5,6]
console.log(arr[1][2]); // 访问arr[1]中索引为2的数组元素  也就是说[4,5,6]中索引为2的元素 => 6
```

总结： 

`arr[i]`: 访问的是arr中索引为i的元素，这个元素又是一个新数组childArr

`arr[i][j]`:  访问数组childArr中索引为j的元素。



###### 二维数组的遍历

```
let arr = [
	[1,2,3],
	[4,5,6],
	[7,8,9]
];
for(let i = 0; i < arr.length; i++) {
	console.log(arr[i]); // arr[i]又是一个数组，必须再次遍历
	let childArr = arr[i]; // 定义变量childArr来接收arr[i]
	// 再次遍历arr[i]，也就是childArr
	for(let j = 0; j < childArr.length; j++) {
		console.log(childArr[j]); // 数组中的每一个元素
	}
}
```

例如：

求二维数组中最大值、最小值、总个数、总和、平均值。

```
let arr = [
  [80, 92, 97],
  [61, 65, 71],
  [59, 63, 70],
  [85, 87, 99],
  [76, 77, 85]
];
// 使用变量保存
let sum = 0,//和
    avg = 0,//平均值
    count = 0,//总个数
    max = 0,//最大值
    min = 0;//最小值
    //遍历二维数组
    for(let i=0; i<arr.length; i++){
        for(let j=0; j<arr[i].length; j++ ){
            count++;//每遍历出一个元素 -- 总个数自增1
            sum += arr[i][j];//累加和
            if( arr[i][j] > max ){//最大值
                max = arr[i][j];
            }
            if( arr[i][j] < min ){//最小值
                min = arr[i][j];
            }
        }
    }
```





### 数组的其他几个重要的方法

###### forEach()

 forEach语法结构：

语法：

```
数组名称.forEach(function(item,index){
	console.log(item); // item就是数组的每个元素
	console.log(index); // index就是元素对应的索引
})

```

例如：

```
let arr = ['html', 'css', 'javascript'];
arr.forEach(function(item,index) {
	console.log(item); // item就是数组元素
	console.log(index); // index就是索引
})
```



###### filter()

filter()方法常用于过滤。

`filter` 为数组中的每个元素调用一次 `callback` 函数，并且把 `callback` "**返回 true 或隐式得到为true的**"元素添加到一个新数组。

语法：

```
let newArray = arr.filter(callback(item,index,array));
```

参数item： 正在处理的当前元素

参数index： 正在处理的当前元素的索引，可选

参数array： 这个数组本身，可选

返回值newArray：一个新的、由过滤后的元素组成的数组，如果没有任何数组元素通过测试，则返回空数组。 

注意： `filter` 不会改变原数组，它返回过滤后的新数组。

例如：

```
let arr = [1,32,5,8,11,55,67,55,712,71];
let newArr = arr.filter(function(item,index,array){
	console.log(item);
  //console.log(index);
  //console.log(array);
  return item % 2 === 0
})
console.log(newArr);
```



###### map()

`map` 方法会给原数组中的每个元素都按顺序调用一次  `callback` 函数。`callback` 每次执行后的返回值（**包括 undefined**）添加到一个新数组中。

语法：

```
let newArray = arr.map(callback(item,index,array));
```

参数item： 正在处理的当前元素

参数index： 正在处理的当前元素的索引，可选

参数array： 这个数组本身，可选

返回值newArray：一个由原数组每个元素执行回调函数的结果组成的新数组。

注意： `map` 不会改变原数组。

例如：

```
let arr = [1,32,5,8,11,55,67,55,712,71];
let newArr = arr.map(function(item,index,array){
	// console.log(item);
  //console.log(index);
  //console.log(array);
  return item * 2
})
console.log(newArr);
```

总结： 

- filter、map都是返回新数组，不改变原数组
- filter是过滤，返回符合的元素。map是对每个元素进行操作，返回操作后的结果（如果函数没有写return，那么默认就会返回undefined,新数组就会装满了undefined）



###### some()

`some()` 为数组中的每一个元素执行一次 `callback` 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，`some()` 将会立即返回 `true`且不会再往后执行。否则，`some()` 返回 `false`。

一真为真

语法：

```
let isHave = arr.some(callback(item,index,array));
```

参数item： 正在处理的当前元素

参数index： 正在处理的当前元素的索引，可选

参数array： 这个数组本身，可选

返回值isHave：true或者false。数组中有至少一个元素执行callback返回一个真值，isHave就为`true`；所有元素执行callback都没有返回一个真值，那么isHave为`false`。

例如：

```
// 检测数组中是否有元素大于10。
let result = [2, 5, 8, 11, 4].some(function(item,index,array){
	 console.log(item); // 2, 5, 8, 11,有返回为true的立即返回true，不会往后再执行
  //console.log(index);
  //console.log(array);
  return item > 10
});
console.log(result); // true
```



###### every()

`every` 方法为数组中的每个元素执行一次 `callback` 函数，直到它找到一个使 `callback` 返回false的元素。如果发现了一个这样的元素，`every` 方法将会立即返回 `false`。否则，`callback` 为每一个元素返回 `true`，`every` 就会返回 `true`。

一假为假

语法：

```
let isHave = arr.every(callback(item,index,array));
```

参数item： 正在处理的当前元素

参数index： 正在处理的当前元素的索引，可选

参数array： 这个数组本身，可选

返回值isHave：true或者false。数组中有全部元素执行callback都返回真值，isHave就为`true`；否则isHave为`false`。

```
// 检测数组中是否有元素大于10。
let result = [2, 5, 8, 11, 4].every(function(item,index,array){
	 console.log(item); // 2, 5, 8, 11,有返回为false的立即返回false，不会往后再执行
  //console.log(index);
  //console.log(array);
  return item < 10
});
console.log(result); // false
```

总结：**some是一真为真，every是一假为假**。



###### reduce()

reduce()常用来做累加。

语法：

```
const result = arr.reduce(callback(acc,cur,index,array),initialValue)
```

参数acc： 累计器累计回调的累积值。也就是说是每次操作之后的累加值。注意，如果设置了initialValue，那么第一次的时候acc就为initialValue值（只有第一次的时候）。

参数cur： 正在处理的当前元素。

参数index： 正在处理的当前元素的索引，可选

参数array： 这个数组本身，可选

参数initialValue： 第一次调用callback时acc的初始值，可选。

返回值result： 函数累计处理的结果。

例如：

```
const sum = [10, 1, 2, 3].reduce(function (acc, cur) {
  console.log(cur); // 10, 1, 2, 3
  return acc + cur;
},0);
console.log(sum);  // 16
```

```
const sum = [10, 1, 2, 3].reduce(function (acc, cur) {
  console.log(cur); // 10, 1, 2, 3
  return acc + cur;
},10);
console.log(sum); // 26
```

```
const sum = [10, 1, 2, 3].reduce(function (acc, cur) {
  console.log(cur); // 1, 2, 3
  return acc + cur;
});
console.log(sum); // 16
```

注意： 如果设置了initialValue，那么第一次时acc就拿取initialValue值，如果不设置，那么第一次acc就取数组第一个值，cur取数组第二个值(cur跳过第一个值)。所以空数组时不设置initialValue值就会报错。



### 扩展

###### 判断变量是否是数组

1. instanceof

   语法：

   ```
   变量 instanceof Array;
   // 返回值为true（是）和false（不是）
   ```

   例如：

   ```
   console.log([] instanceof Array); // true
   console.log({} instanceof Array); // false
   ```

2. Array.isArray()

   语法：

   ```
   Array.isArray(变量)
   // 返回值为true（是）和false（不是）
   ```

   例如：

   ```
   Array.isArray([1, 2, 3]);  // true
   Array.isArray({foo: 123}); // false
   Array.isArray("foobar");   // false
   Array.isArray(undefined);  // false
   ```

3. Object.prototype.toString()

   语法：

   ```
   Object.prototype.toString.apply(变量) === '[object Array]';
   ```

   例如：

   ```
   Object.prototype.toString.apply([1, 2, 3]) === '[object Array]'; // true
   Object.prototype.toString.apply({foo: 123}) === '[object Array]';// false
   Object.prototype.toString.apply("foobar") === '[object Array]';// false
   Object.prototype.toString.apply(undefined) === '[object Array]';// false
   ```

了解知识：

- 鲜为人知的知识：其实 Array.prototype 也是一个数组。

  ```
  Array.isArray(Array.prototype);  // true
  ```

- instanceof 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性

  ```
  Array.isArray({ __proto__: Array.prototype }); // true
  //指定了某个对象的__proto__属性为Array.prototype，便导致了该对象继承了Array对象，这种毫不负责任的继承方式，使得基于继承的判断方案瞬间土崩瓦解。
  ```

- `Array.isArray` 优于 `instanceof`,因为Array.isArray能检测`iframes`.

  ```
  let iframe = document.createElement('iframe');
  document.body.appendChild(iframe);
  xArray = window.frames[window.frames.length-1].Array;
  var arr = new xArray(1,2,3); // [1,2,3]
  
  Array.isArray(arr);  // true
  arr instanceof Array; // false
  ```

  

###### Array.from()

Array.from()方法把一个类数组转换为真数组（浅拷贝）。

语法：

```
Array.from(要转换的类数组,mapFn,thisArg)
```

参数mapFn：可选，如果指定了该参数，新数组中的每个元素会执行该回调函数。

参数thisArg： 可选参数，执行回调函数 `mapFn` 时 `this` 对象。

理解：`Array.from()` 方法有一个可选参数 `mapFn`，让你可以在最后生成的数组上再执行一次`map` 方法后再返回。也就是说` Array.from(obj, mapFn, thisArg) `就相当于` Array.from(obj).map(mapFn, thisArg)`,



###### Array.of()

Array.of()方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型。

 `Array.of()` 和 `Array` 构造函数之间的区别在于处理整数参数：`Array.of(7)` 创建一个具有单个元素 **7** 的数组，而 `Array(7)`创建一个长度为7的空数组（**注意：**这是指一个有7个空位(empty)的数组，而不是由7个`undefined`组成的数组）。

```
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]

Array(7);          // [ , , , , , , ]
Array(1, 2, 3);    // [1, 2, 3]
```



###### 扁平化数组

flat()方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

语法：

```
let newArray = arr.flat(参数depth);
```

参数depth：指定要提取嵌套数组的结构深度，默认值为 1，使用 Infinity值，可展开任意深度的嵌套数组。

```
let arr1 = [1, 2, [3, 4]];
arr1.flat(); 
// [1, 2, 3, 4]

let arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

let arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

//使用 Infinity，可展开任意深度的嵌套数组
let arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

注意： `flat()` 方法会移除数组中的空项。

```
let arr = [1, 2, , 4, 5];
arr.flat();
// [1, 2, 4, 5]
```



###### **falsy** 值

falsy 值也叫虚值， 是在Boolean上下文中认定为 false 的值。

在 JavaScript 中只有 8 **个** **falsy** 值，分别是：false;  0;  -0;  0n;  ''、""、``;  null;  undefined;  NaN



###### truthy值

truthy值也叫真值，是在Boolean上下文中认定为 true 的值。

除了那8个falsy 值，其余的值都是真值truthy。



### 思维扩展

###### 去除数组中重复的数字

例如： [4，13，53，63，13，1，63]   =>    [4,13,53,63,1]



