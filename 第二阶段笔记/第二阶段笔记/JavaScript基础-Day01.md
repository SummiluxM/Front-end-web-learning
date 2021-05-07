# JavaScript基础-Day01

任务：

- JavaScript的简介（了解）
- JavaScript的使用（精通）
- JavaScript的注释（熟练）
- JavaScript的输入与输出（熟练）
- JavaScript的变量（精通）
- JavaScript的数据类型（精通）
- JavaScript的运算符(熟练)



### JavaScript的简介

1）首先我们来了解一下**程序**：

生活中的程序： 完成某件事件的流程或步骤，比如赶地铁。先买票，过安检、进闸机，坐地铁，出闸机，顺序不能打乱。

计算机中的程序：为了能够解决某件事情而编写的一系列有序指令的集合，指令即代码。实质上程序就是一堆代码。

2）然后我们来了解一下**编程语言**：

编程语言：编写计算机程序的计算机语言。

常见语言：

- JavaScript
- java
  - c
  - c#
  - python
  - php
  - go

3）最后我们来了解一下JavaScript 的基础概念：

- 为什么使用JavaScript

  - 作为网页的"灵魂",是完成一个动态页面必不可少的一部分。
  - 也能够完成主流编程语言的所有工作，而且有专门的国际组织进行维护
  - 入门简单，使用环境简单。
  - JavaScript应用场景广泛。比如动态页面、app开发、后台开发等。

- JavaScript发展 组成

  - JavaScript出生：网景为了对抗ie，在95年找了程序员用10天开发出了JavaScript。JavaScript能够带来用户跟网页交互。ie为了对抗，也开发出了类似的JScript。为了网页编程语言的更好发展，网景吧javascript1.0 提交给了ecma组织(欧洲计算机标准组织)来规范及统一标准。ecma吧JavaScript命名为ECMAScript。

  - 版本

    ECMAScript 3 ：98年，规定了JavaScript的主要内容和板块，算是第一个比较完善的版本，也是第一个流行的版本。

    ECMAScript 5： 2009年出来的。新增了很多实用的模块。也是目前所有主流浏览器都支持的版本，除了ie8.

    ECMAScript 6：指从2015年发布及之后的新版本的统称，ECMAScript2015新增了很多新模块。ecma也决定了每年发布一个新版本。官方版本号是以发布年份来决定的。比如2015年发布叫ECMAScript2015，依次类推。但是从2015年之后的版本是在ECMAScript2015基础上进行修改，所有有的机构直接将ECMAScript2015及以后的版本统称为es6。

  - **组成(实际使用的JavaScript的组成部分)**

    - 浏览器端(动态页面、app)
      - ECMAScript ：ecma组织定义的JavaScript核心语法，简称ES。跟使用环境无关。
      - BOM:  浏览器对象模型，操作浏览器窗口本身。比如新建、关闭窗口或前进、后退或刷新页面等功能
      - DOM：文档对象模型，用于操作网页，对HTML标签的增删查改以及修改css样式等等。
      
    - nodejs(后台开发)
    
      - ECMAScript ：ecma组织定义的JavaScript核心语法，简称ES。跟使用环境无关。
    
  - 兼容性
  
    - ECMAScript
      - 基本所有浏览器都支持ECMAScript 5 。ie8除外
      - ie全系不支持es6



### JavaScript的使用

###### **在node中使用JavaScript**

**安装：**

- 直接去官网下载安装文件。win7下载低版本，比如10及以下
- 一路next，安装即可
- 测试nodejs：打开命令行窗口 win+R打开，(输入cmd),输入查看版本命令

```javascript
node -v
```

 - 如果有版本号信息，那么安装成功

**使用：**

- 随便一个文件夹下创建一个以.js为后缀的文件，在里面加入以下js代码:
- 注意： 文件名不要写成node.js（在doc当中打开会出错）

```javascript
console.log("hello world");
```

```
- 在js所在文件夹打开命令行窗口-cmd.输入以下指令，来执行js文件
// 方式1：
//  快捷键： crtl+shift+~

// 方式2
// 从文件夹中路径上面，输入cmd打开命令行窗口。
```

```javascript
node  js文件名
```

```
- 正常情况下，命令行会打印一句helloworld ，表示js运行成功
```

### 

###### **在浏览器端使用JavaScript**

二种使用方式

方式1: **外链式**

通过`<script src="js文件地址">`引入js文件

```html
<script  src="js文件地址"></script>
```

方式2：**内嵌式**

	- 通过`<script type="text/javascript"></script>`标签中书写js代码

```html
<script type="text/javascript">
js代码
</script>
```

 - 两种方式的区别
   - 使用js文件，可以把js代码单独放置一个文件中，可以统一管理，同时和HTML以及css代码隔开，更容易阅读。

```
注意： 
1. script标签中type是可选属性，如果要写，一定保证type=”text/javascript“
2. script 标签引入位置通常在head头部或者结束body之前(推荐结束body之前)
3. 外链式：不能再script标签中书写js代码，会被引入的xx.js文件中代码覆盖掉
```



### JavaScript的注释

概念: 对代码进行解释性说明，即描述这段代码是来干嘛的，本身对程序没有任何影响。

作用：用于方便代码阅读以及理解

特点：当代码执行时会忽略所有注释

```
单行注释:     // 单行注释  将当前一行为注释
```

```
多行注释: 
作用同单行注释
区别：支持多行注释
使用：/*  多行注释内容 */
```

```
快捷键：      
单行注释： ctrl + /
多行注释： shift + alt + a
```



### JavaScript的输入与输出

###### 3种输出

1. **控制台输出**： console.log("输出内容")  

2. 弹出框输出:    alert("输出内容")

3. 网页输出:   docuement.write("输出内容");

​      注意：如果网页输出的内容是HTML标签代码，那么浏览器会将其变为真正的HTML标签。

​	 输出html代码： document.write("<h1>我是大标题</h1>")

###### 输入

BOM：

```javascript
prompt("提示性文字");

```

- 会以弹出框的形式获取用户通过键盘输入的信息.可以结合输出，将用户的输入的数据输出出来
- 获取的是一个字符串

```javascript
document.write(prompt('请输入银行卡号和密码'));
// 可以使用变量去接受它
let 变量名 = prompt("提示性文字");
```



### JavaScript的变量

1. 背景：当需要子程序里面多次使用同一个数据的时候，每次都需要重新输入，导致程序使用不便。数据重复使用--变量（变化的数据）

2. 概念：指可以保存一个数据的容器，该容器可以多次使用。

3. 作用：解决一个数据多次 重复使用的问题(用于存储程序中临时的数据)。

4. 定义变量

   **定义变量 = 声明变量 + 赋值**

   1）三种声明变量方式： ECMAScript

   ```
   ES5  var				语法： var 变量名；
   ES6  let  				语法： let  变量名；（推荐使用）
   ES6  const				语法： const 变量名；
   ```

   **三种声明变量的方式的区别**：

   ​	var定义变量可以重新声明和赋值

   ​	let定义变量不能重新声明但是可以重新赋值

   ​	const定义变量不能重新声明也不能重新赋值

   2）赋值

   语法： 变量名 = 值;

   ```
   name=‘彭于晏’;
   age = 17;
   sex=‘男’;
   ```

   3）声明变量同时赋值

   语法：  var/let/const 变量名 = 要保存的数据 

   ```
   var name = ‘彭于晏’;
   let age = 17;
   const sex=‘男’;
   ```

   4) 定义多个变量

   使用let同时定义多个变量，变量之间用逗号隔开。

   ```
   let name = ‘彭于晏’,
   		age = 17,
   		sex=‘男’;
   ```

   注意：变量之间是用逗号隔开，**最后一个变量后面要使用分号**。

5. 使用变量

   在需要使用变量的地方直接使用。例如： console.log(已声明的变量)；

   注意： **变量只能定义之后才能使用**

6. 修改变量：即修改变量所保存的数据

```javascript
语法： 已定义的变量名 =  新数据;
```

   注意： 修改变量是不用重新定义的。

7. 变量名规范

- 只能包含 数字、字母、_、$
- 不能以数字开头
- 不能关键字及保留字 (in;class;)
- 不能使用中文命名 (服务器不能识别中文) ，尽量用英文，以及见词达义。比如number total  result   
- 不能使用特殊字符

- 常用的变量名规范写法

  - 大驼峰：每个单词首字母大写， GetArrayMax
    - 用于类名（面向对象）
  - 小驼峰：第一个单词全小写，从第二个单词开始，首字母大写。getArrayMax
    - 一般用于变量名、函数名等





### JavaScript的数据类型

编程语言中数据类型就是给数据进行分类区分，目的是为了让计算机可以进行合理的分配内存和进行数据的运算。

JavaScript中一共包含了8种数据类型：

###### 基本类型（7种）

1. `Number`:数字类型，又分为两种：整数（int）和小数（float）(**int和float不是js的数据类型**)

   1).   整数（int）

   十进制： 日常中使用的数字

   ```
   let num1 = 15; // 十进制表示法
   ```

   八进制： 以0开头的数字（了解）

   ```
   let num2 = 017; // 八进制表示法
   ```

   十六进制： 以0开头的数字（了解）

   ```
   let num3 = 0xF; // 十六进制表示法
   ```

   二进制：以0或者1组成的数字(了解)

   ```
   let num4 = 00000001
   ```

   注意： 程序的输出都会转换为十进制表示法输出。



​		2).     小数（float）： 带有小数点的数字

```
	var  width = 0.79;
```

​		

​		3).    特殊值：

​				NaN（not a number）: 不是一个数字，计算错误，类型转换失败

2. `String`:字符串。

   在程序中字符串表现为一串**被引号所包围的**文字、字符（使用单引号或者双引号都是一样的）。

   ```
   var name = '王二麻子';
   var age = '46'; // 46为数字类型，加了引号'46'就是字符串类型了
   ```

   注意： 相同引号之间不能重复嵌套。

3. `Boolean`:布尔类型

   布尔类型就两个数据。即`true`  `false`，代表真假性。

   - `true`表示程序中逻辑的正确（真）

   - `false`:表示程序中逻辑的错误（假）

     ```
     var isMan = true;
     ```

     注意： 如果true加了引号，就是字符串类型了，而不是布尔类型。

     

4. `undefined`: 未定义（特殊值）

   数据类型undefined就只有一个值，为undefined。

   一个变量声明了但是没有赋值，那么它的默认值就是undefined，这个变量叫做‘未定义变量’。

   ```
   let price；
   console.log(price); // undefined
   ```

   注意： 区分什么是未定义变量和未声明变量

   未声明变量： 变量还未声明就直接使用，那么就会报错。

   未定义变量： 变量声明了但是没有赋值，它有默认值undefined。

   

5. `null`: 空（特殊值）

   数据类型null就只有一个值，为null,表示某个对象是空的状态。

   可以给一个变量赋值为 null 来清除变量的内容从而回收这个变量。

   ```
   let price = 998;
   price = null
   ```



6. `Symbol`: 唯一值

   是ES6新增数据类型，可以提供程序的唯一的数据。常用于设置为对象的属性

   

7. `BigInt`:  超大数

   是ES10新增数据类型，来表示大于 `253 - 1` 的整数，可以表示任意大的整数，常用来表示科学计数。



###### 引用类型( 1种 )

​	`Object`:对象类型

​		可以表示复合型的数据，数组、函数、对象都是对象类型。		



###### 查看基本数据类型方法

语法：typeof  变量名/值

```
console.log( typeof 12 )        //number
console.log( typeof '曹操' )    //string
console.log( typeof true )      //boolean
console.log( typeof undefined ) //undefined
console.log( typeof null )      //object 这是个bug
console.log( typeof Symbol())  //symbol
```

例子：

```
console.log(typeof 0);
console.log(typeof "");
console.log(typeof {});
console.log(typeof []);
console.log(typeof NaN);
console.log(typeof undefined);
console.log(typeof null);
console.log(typeof false);
console.log(typeof function(){});
```



###### 数据类型之间的转换

为什么需要类型转换？因为数据之间的运算只有同类型之间的运算, 如果不同类型之间存在运算的话,需要将其转换为同一种类型后再进行运算。

**强制类型转换(重点)**

1. 将其它类型转为Number类型： parseInt()  parseFloat()  Number()

   1）  parseInt() 

   语法：  parseInt(变量名/值)   

   字符串： 只有**首字符是数字**可以得到具体的数值，否则得到NaN。

   其他类型： NaN。

   ```
   parseInt('20px')//20
   parseInt('3.45px')//3
   parseInt('ak47')//NaN
   parseInt('aaa')//NaN
   parseInt(true)//NaN
   parseInt(undefined)//NaN
   parseInt(null)//NaN
   ```

   2）parseFloat() 

   语法：  parseFloat(变量名/值)   

   字符串： 只有首字符是数字可以得到具体的数值，否则得到NaN。

   其他类型： NaN。

   ```
   parseFloat('20px')//20
   parseFloat('3.45px')//3.45
   parseFloat('ak47')//NaN
   parseFloat('aaa')//NaN
   parseFloat(true)//NaN
   parseFloat(undefined)//NaN
   parseFloat(null)//NaN
   ```

   3)   Number()

   语法：  Number(变量名/值)   

   字符串： **纯数字的字符串**可以得到具体的数值，否则得到NaN。

   boolean: true: 1 false: 0

   undefined: NaN  null: 0

   ```
   Number('20')//20
   Number('20px')//NaN
   Number('3.45px')//NaN
   Number('ak47')//NaN
   Number('aaa')//NaN
   Number(true)//1
   Number(false)//0
   Number(undefined)//NaN
   Number(null)//0
   ```

   

2. 将其它类型转为Boolean类型 : Boolean()

   语法： Boolean(变量名/值)

   只有6个值得到fasle: ""   0   null    undefined    NaN   false

   其他的都得到true。

   ```
   Boolean('20')//true
   Boolean('')// fasle
   Boolean(' ')//true
   Boolean('ak47')//true
   Boolean(true)//true
   Boolean(false)//fasle
   Boolean(undefined)//fasle
   Boolean(null)//fasle
   Boolean(NaN)//fasle
   Boolean(0)//fasle
   Boolean(‘0’)//true
   ```



3. 将其它类型转为String类型： String()

   语法： String(变量名/值)

   ```
   String('20px')//'20px'
   String(20)//'20'
   String(true)//‘true’
   String(undefined)//‘undefined’
   String(null)//‘null’
   ```

   简便语法： 变量名/值 + “”



**自动类型转换**（隐式转换）

运行过程中Javascript会自动进行类型转换，就叫自动类型转换。

```
let num1 = "100";
let num2 = 10;
console.log(num1 - num2); // 90
//减法的语意： 将会按照数字进行运算
```



注意：

1. 其他类型快速转换为字符串类型，可以直接 +"" 。

2. 纯数字的字符串快速转换为数字类型，可以直接 - 0 。




### 运算符

概念：JavaScript中用于**进行运算**的特殊符号统称为运算符

分类：算术运算符、关系运算符(比较运算符)、逻辑运算符、赋值运算符、条件运算符。

###### 算术运算符

- `+`： 加
 - `-`： 减
 - `*`： 乘
 - `/`： 除
 - `%`： 余，取模运算符，除不尽剩下的整数(取余数) 。

注意： 注意： 当`+`号两边有一个是字符串时，那么就成为了**字符串拼接**，会直接将两个数据拼接一起。只有当两边都是数字类型时，才会进行加法运算。



###### 关系运算符(比较运算符)

**最终，返回的是布尔值，正确的话就返回`true`，错误的话就返回`false`**

- `>`： 大于
 - `<`： 小于
 - `==`:  不严格相等，比较值的大小，不比较值的类型 (只比较大小)
 - `===`：严格全等于，比较值的大小，又比较值的类型.(比较大小及类型)
 - `!=`: 不等于，结果和==相反
 - `!==`:  不全等于，结果和===相反
 - `>=`: 大于或等于
 - `<=`: 小于或等于



###### 逻辑运算符

1. `&&`: 并且，逻辑与，多个条件需同时满足,同时满足则为true，否则为false。   一假则假

   语法： 表达式1 && 表达式2

   ```
   console.log(1 === '1' && 5 >= 5 ); // false
   ```

2. `||`: 或者，逻辑或，表示多个条件只需满足其中一个即为true，都不满足才为false。  一真则真

   语法： 表达式1  || 表达式2

   ```
   console.log(1 === '1'  ||  5 >= 5 ); // true
   ```

3. `!`:  取反，逻辑非，原来为true，取反为false。原来为false，取反之后为true。

   语法： !表达式1 

   ```
   console.log(!(1 !== '1')); // false
   ```



###### 赋值运算符

- `=`: 赋值运算符,给变量进行赋值,将`=`号右边表达式的结果赋给左边的变量。

- `-=`:   a -= b 完全等效于 a = a - b,将a-b运算之后的结果再赋值给a。

- `+=`:   a += b 完全等效于 a = a + b,将a+b运算之后的结果再赋值给a。

- `/=`： a /= b 完全等效于 a = a / b,将a/b运算之后的结果再赋值给a。

- `*=`： a *= b 完全等效于 a = a * b,将a*b运算之后的结果再赋值给a。

- `%=`:    a %= b 完全等效于 a = a % b,将a%b运算之后的结果再赋值给a。

- `++`:   a++ 完全等效于a = a + 1，表示自增1. 变量在自身的基础上加1

  - 前置++ ： 

    语法： ++变量名

    运算过程中，先自增1，再参与其他运算。

    ```
    let a = 1, b = 2, c;
    c = ++a + b 
    console.log(c); // 4
    ```

    

  - 后置++

    语法： 变量名++

    运算过程中， 先参与其他运算,再自增1。

    ```
    let a = 1, b = 2, c;
    c = a++ + b 
    console.log(c); // 3
    ```

    

- `--`:   a-- 完全等效于a = a - 1，表示自减1。变量在自身的基础上减1，用法同++



###### 运算符优先级

- 先乘除后加减；
- 赋值优先级最低；
- 优先级相同情况下，从左到右依次计算；
- 使用()可以提升优先级。



### 扩展知识

1.  `&&` :  运算时，遇到false就返回。

   ​	a && b ,如果 a 为true，直接返回b，而不管b为true或者false ；如果 a 为false 那么直接返回a。

   ```
   let a = 0 && 1 && 2; // a = 0
   let b = 1 && 2 && 3; // b = 3
   let c = 1 && 0 && 2; // c = 0
   ```

2.  `||`:  运算时，遇到true就返回。

   a || b ,如果 a 为false，直接返回b，而不管b为true或者false ;如果 a 为true，直接返回a，而不会继续往下执行。

   ```
   let a = 0 || 1 || 2; // a = 1
   let b = 1 || 0 || 3; // b = 1
   ```

3.  **面试题：为什么typeof null得到object而不是null**？

    因为javascript中不同对象在底层都表示为二进制，而javascript 中会把二进制前三位都为0的判断为object类型，而null的二进制表示全都是0，自然前三位也是0，所以执行typeof时会返回'object。

4. 字符编码

   - 为什么会有乱码

     - 由一种字符编码来书写的文件用另一种字符编码去解析，那么就会乱码。比如说在生活中用中文写的东西需要中文的语法去解析。在程序中，用utf-8写的文件，那么就要用utf-8去解析。

   - 什么是字符编码

     - 计算机底层只能够识别0和1，不能直接读取文字，所以为了让计算机能够处理文字。那么就需要定义规则或语法规定计算机0和1 的不同组合表示不同的文字.这个规则就是字符编码。

   - 如何玩转字符编码

     - `ascii`:美国早期的字符编码，也是后续字符编码的基础。在ascii码下，可以表示128种字符，每个字符有对应的ASCII码。比如字符`0`的ASCII码为48,`a`的ASCII码为97。	
       - 缺点：只支持西欧国家的语言以及一些 常见的特殊符号.

   - 在程序中完成字符和ASCII码的切换

     - 获取某个字符的ASCII码

     ```javascript
     var str = "ABC";
     str.charCodeAt(0);
     - 0表示字符在字符串中的位置，以0开始。如果要获取C的ASCII吗，那么就为2
     ```

     - 通过ASCII码获取对应的字符

     ```javascript
     String.fromCharCode();
     //例子
     var code = 48;
     var str = String.fromCharCode(code);
     document.write(str);//0
     ```

   - 常见字符编码

     - `ASCII`
     - 中国
       - `gb2312`
       - `GBK(gb2312的优化)`
     - `utf-8`(推荐使用的)
       - 存放所有已知的文字

5.   二进制和十进制之间的转换

    十进制转二进制：

    语法：

    ```
    变量/数据.toString(2);
    ```

    例如：

    ```
    let num1 = 100
    console.log(num1.toString(2)); // 1100100
    ```

    二进制转十进制：

    语法：

    ```
    parseInt(变量/数据, 2);
    ```

    例如：

    ```
    let num = 00000001;
    console.log(parseInt(num, 2));
    ```

    



