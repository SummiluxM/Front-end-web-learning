# JavaScript基础-BOM

任务：

- JavaScript的组成（理解）
- DOM和BOM介绍
- Window对象
- Screen对象（了解）
- History对象（理解）
- Navigator对象
- Location对象





### JavaScript的组成

JavaScript由三部分组成

- ECMAScript： ecma组织定义的JavaScript核心语法，简称ES。跟使用环境无关。
- BOM： 浏览器对象模型，操作浏览器窗口本身。比如新建、关闭窗口或前进、后退或刷新页面等功能
- DOM： 文档对象模型，用于操作网页，对HTML标签的增删查改以及修改css样式等等。

注意：

- BOM中包含的对象提供了很多用于操作浏览器的属性和方法。
- DOM中包含的对象提供了很多用于操作网页文档的属性和方法。
- BOM包含了DOM  、 DOM是BOM子级。
- BOM/DOM只是模型,只是一个概念一个称呼而已。



### BOM组成

概念：BOM(browser Object model-浏览器对象模型)，整个**浏览器**窗口，我们可以运用该对象里的api来控制标签页，比如刷新、前进、后退、改变页面地址、检测浏览器设备类型等操作。

BOM是由以下几个对象组成：

注意：

- BOM的顶层对象就是**window**。
- window对象有六个属性，这六个属性又分别是一个对象。
- Document：DOM的顶层对象， 也就是网页文档。
- History：浏览器的历史记录。
- Location：用于获得当前页面的地址。
- Navigator：包含有关访问者浏览器的信息。
- Screen：包含有关用户屏幕的信息。





### Window

- Window对象是BOM的顶层对象。

- 所有浏览器都支持 window 对象，它表示**浏览器窗口**。

- 所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员；全局变量是 window 对象的属性；全局函数是 window 对象的方法。

- 每个标签页都有一个window对象，里面包含了操作页面所需要的所有api。包括我们学习的DOM核心-document对象实际上是作为window对象的一部分（document 是 window 对象的属性之一）。

- 在使用window对象的各种属性和方法时可以省略`window.`前缀。

  ```
  window.alert();   ===   alert(); // 追溯到了对window对象的访问,省略了window.前缀
  ```

小细节：

```
// 访问未声明的变量会抛出错误，但是通过查询 window 对象，可以知道某个可能未声明的变量是否存在。
console.log(a); // 报错：a is not defined
console.log(window.a); // undefined
```



###### window常用方法

- alert() 
- comfirm() 
- prompt()
- 定时器
- close()：关闭当前窗口
- open():  打开一个新的浏览器窗口



###### alert() 

 window.alert() 显示带有一段消息和一个确认按钮的警告框。



###### confirm() 

 window.confirm()方法用于显示一个带有指定消息和确认及取消按钮的对话框，所有主要浏览器都支持 confirm() 方法。

如果访问者点击"确定"，此方法返回true，否则返回false。

例如：

```
function myFunction(){
    var x;
    var r=confirm("按下按钮!");
    if (r==true){
        x="你按下了\"确定\"按钮!";
    }
    else{
        x="你按下了\"取消\"按钮!";
    }
    console.log(x)
}
```



###### prompt()

window.prompt()方法用于显示可提示用户进行输入的对话框。

这个方法返回用户输入的**字符串**。

语法：

```
prompt(msg,defaultText)
```

参数msg： 可选。要在对话框中显示的纯文本（不是 HTML 格式的文本）。

参数defaultText：可选。默认的输入文本。



###### close()

window.close() 方法用于关闭浏览器窗口。



###### open()

window.open() 方法用于打开一个新的浏览器窗口。

语法：

```
window.open(URL);
```

参数URL：可选。打开指定的页面的URL。如果没有指定URL，打开一个新的空白窗口。



### 定时器(重点)



###### setTimeout()

延时定时器

 `setTimeout`方法是用来设置一个定时器，该定时器在定时器到期后执行一个函数或指定的一段代码。（不推荐执行代码，存在安全性问题）

语法：

```
let timeoutID = setTimeout(Function, delay);
```

参数Function：  

- 是你想要在到期时间(`delay`毫秒)之后执行的函数。

参数delay：

- 延迟的毫秒数 (一秒等于1000毫秒)，函数的调用会在该延迟之后发生。
- 如果省略该参数，delay取默认值0，意味着“马上”执行，或者尽快执行。
- **但是**，不管是哪种情况，实际的延迟时间可能会比期待的(delay毫秒数) 值长。
- 因为在浏览器中，`setTimeout()`的每调用一次定时器的最小间隔是4ms。

注意： 

1. setTimeout()是一个**异步函数**

2. setTimeout函数的返回值timeoutID表示定时器的编号，这个值可以传递给`clearTimeout`来取消该定时器。



例如：

```
// 3秒后输出我错了
setTimeout(function() {
	console.log('我错了')
}, 3000);
```



```
	// 每隔1s, 输出1-5之间的数字(模拟setInterval)
	let num = 0;// 定义变量保存要输出的数字    
  function fn() {      
    num++; // 自增1       
    console.log(num);// 输出数字    
    let timeoutID = setTimeout(fn, 1000);// 调用定时器，拿到定时器的编号timeoutID，也就是定时器id
    //判断之后停止计时器
    if(num === 5) clearTimeout( timeoutID )// 数字为5的时候，就取消定时器
  }
  fn();
```



###### setInterval()

间隔定时器

setInterval方法是**重复**调用一个函数或执行一个代码段，在每次调用之间具有固定的时间延迟（不推荐执行代码，存在安全性问题）。

语法：

```
let intervalID = setInterval(Function, delay);
```

参数Function： 

- 要重复调用的函数。 每经过指定 `延迟（delay）` 毫秒后执行的函数。该函数不接受任何参数，也没有返回值。

参数delay：

- 是每次延迟的毫秒数 (一秒等于1000毫秒)，函数的每次调用会在该延迟之后发生。
- 如果这个参数值小于10，则默认使用值为10（这个参数每个浏览器都有默认的最小值）。

注意： 

1. setInterval()也是一个异步函数。

2. setInterval函数的返回值intervalID表示定时器的编号，这个值可以传递给`clearInterval`来取消该定时器。

例如：

```
    // 每隔1s, 输出1-5之间的数字
    let  num = 0;//定义变量保存输出的数字
    let intervalID = setInterval(function(){       
        num++;
        console.log( num );//停止计时器
        if( num === 5) clearInterval( intervalID );    
		},1000);
```





### Screen(了解)

window.screen 对象包含有关用户屏幕的信息。

###### screen.availWidth

screen.availWidth 属性返回访问者屏幕的宽度，以像素计，减去界面特性，比如窗口任务栏（可用的屏幕宽度）。

例如：

```
document.write("可用宽度: " + screen.availWidth);
```



###### screen.availHeight

screen.availHeight属性返回访问者屏幕的高度，以像素计，减去界面特性，比如窗口任务栏（可用的屏幕高度）。

例如：

```
document.write("可用高度: " + screen.availHeight);
```





### History（理解）

window.history 对象包含浏览器的历史。

###### history.back()

history.back() 方法加载历史列表中的前一个 URL，与在浏览器点击**后退**按钮相同。



###### history.forward()

history forward()方法加载历史列表中的下一个 URL，与在浏览器中点击**向前**按钮相同。



###### history.go()

history.go()方法可以实现向前，后退的功能。

语法：

```
history.go(n)
```

参数n：

- 表示跳转页面的个数
- 为正时，表示前进n个页面
- 为负时，表示后退n个页面
- 为0时，表示刷新当前页面。



###### history.length

history.length属性返回历史列表中的网址数。



### Navigator

window.navigator 对象包含有关访问者浏览器的信息，所有浏览器都支持该对象。

应用：浏览器环境监测(是pc还是移动端)。能够实现根据用户设备类型显示对应的页面。

重要属性：

```
navigator.userAgent // 客户机器发送到服务器的user-agent头部的值，即用户代理。
```

其他属性(了解)：

- navigator.cookieEnabled: 浏览器是否启用了cookie。

- navigator.appName： 浏览器名称
- navigator.appVersion： 浏览器版本
- navigator.appCodeName： 浏览器代号
- navigator.platform： 硬件平台
- navigator.systemLanguage： 用户代理语言



### Location(重点)

window.location 对象用于获得当前页面的地址 (URL)，并把浏览器重定向到新的页面。

**组成(精通)**：

- href: 当前页面完整的URL地址
- protocol:  协议部分,包括":"符号。如：`https:`
- host: 主机名和端口
- hostname: 主机名部分,如： `www.baidu.com`
- port: 端口,如：`8080` 
- pathname:  路径名，包含页面文件名称
- search: 参数部分。
- hash:  锚点，包含‘#’

例如：

```
https://www.baidu.com:3000/js/bom/index.html?name=pyy&age=17#maodian;
协议(protocol):   https:
域名（host）：    www.baidu.com:3000
主机名（hostname）： www.baidu.com
端口（port）：  8080
路径名(pathname):   /js/bom/index.html
参数(search):   ?name=pyy&age=17
锚点(hash):   #maodian
```



###### location.href

location.href 属性返回当前页面的 URL。

- 获取当前页面地址： location.href 
- **设置当前页面地址**：  location.href = "新地址";





###### location.assign()    （了解）

location.assign() 方法加载新的文档。

例如：

```
location.assign("https://www.baidu.com")
```



###### location.reload()    （了解）

location.reload()方法用来刷新页面

语法：

```
location.reload()
location.reload(true); // 不使用缓存
```

### 扩展知识

###### window

全局变量不能通过 delete 操作符删除；而 window 属性上定义的变量可以通过 delete 删除

```
var num=123;
window.str="string";
delete num;
delete str;
console.log(num); //123

console.log(str); //str is not defined
//全局变量不能通过 delete 删除，因为通过 var 定义全局变量会有一个名为 [Configurable] 的属性，默认值为 false，所以这样定义的属性不可以通过 delete 操作符删除
```



###### Location

页面地址中的中文乱码可以使用`decodeURIComoponet()`来处理乱码,只对页面地址有效。

```
decodeURIComoponet(location.href);
```

