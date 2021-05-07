## 控制语句

### 		分支结构

#### 				if_else语句

``` javascript
if(判断条件1) {
   条件1为true的执行语句;
}else if (判断条件2){
   条件2为true的执行语句;
}...{
   ...
}else {
    条件均为flase的执行语句
}
```

#### 		switch语句

- switch用于固定分支的情况，if可以用于任何情况；
- switch分支需要break'来结束，if自动结束
- switch语句更加简洁

``` javascript
switch(表达式) {
     case n:
        代码块
        break;
     case n:
        代码块
        break;
     default:
        默认代码块
} 
```

###     循环结构

#### 				for循环

``` javascript
for(循环变量初始值代码;循环控制条件代码;循环变化量控制代码) {
    循环体内容代码;
}
for(var i=1;i<=100;i++) {
    ......
}
```

#### 		while循环

- 能够与for循环完全相互替换使用，语法和适用场景有所不同

``` javascript
while (循环继续条件) {
    要执行的代码块
}
//循环中的代码将运行一遍又一遍，只要变量（i）小于 10
while (i < 10) {
    text += "数字是 " + i;
    i++;
}
```

### break和continue

#### 	break语句

``` javascript
//break 语句可用于跳出循环。
for (i=0;i<10;i++)
{
    if (i==3)
    {
        break;
    }
    x=x + "The number is " + i + "<br>";
}
```

- break处于嵌套循环中，会结束最近的for循环

####      continue语句

``` javascript
//continue 语句中断循环中的迭代，如果出现了指定的条件，然后继续循环中的下一个迭代
for (i=0;i<=10;i++)
{
    if (i==3) continue;
    x=x + "The number is " + i + "<br>";
}
```



## 运算符

### 		算术运算符

- `+`加法

- `-`减法

- `*`乘法

- `/`除法

- `%`取余

###         比较运算符

- `>`大于
- `<`小于
- `==`只比较数值，不比较数据类型
- `!=`不等于
- `>=`大于等于
- `<=`小于等于
- `===`比较数值和数据类型

###          逻辑运算符

- `&&`与

- `||`或

- `!`非

  取反可以用于判断变量是否有数据，没数据为true，有数据为false

###         赋值运算符

- `=`: x=y
- `+=`: x=x+y 
- `-=`: x=x-y
- `*=`: x=x*y
- `/=`: x=x/y
- `%=`: x=x%y
- `++`
- `--`

## **扩展**

#### 	模板字符串（ES6）

- 加强版的字符串，用反引号 **`**,除了作为普通字符串，还可以用来定义多行字符串，还可以在字符串中加入变量和表达式。

``` javascript
let info=`模板字符串内容`
//用${}在字符串中嵌入变量或者表达式
let name = "Mike";
let age = 27;
let info = `My Name is ${name},I am ${age+1} years old next year.`
console.log(info);
// My Name is Mike,I am 28 years old next year.
```

- 应用：
  - 代替传统的+号字符串的拼接,用于多行字符串或字符串的拼接