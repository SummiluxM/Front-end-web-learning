# JavaScript基础-DOM

任务：

- DOM的简介(了解)

- DOM节点的操作



### DOM的简介

###### DOM 概念

DOM(Document Object model-文档对象模型)。 指将HTML页面或xml页面解析成对象模型，能够利用一些内置api在程序中操作页面上的标签。DOM核心在于学会运用内置的api来完成程序(js代码)和页面之间的交互.DOM是一种技术标准，并不属于任何一种编程语言，只是JavaScript内置了 DOM的实现，即JavaScript内置了可以操作HTML页面的api，JavaScript DOm部分的api 都放在内置的`document`对象中。

- DOM是一种标准，跟语言无关，只是JavaScript实现了DOM
- JavaScript 内置了 操作页面的api，放在内置的document原生对象中



###### DOM发展

DOM发展分为三个阶段

- DOM 0级&1级：早期用js操作HTML标签是浏览器厂商自己实现的，没有统一标准。到98年 才形成了第一个标准：DOM1级。

```
- dom1级可以对HTML标签进行增删查改。
```

- DOM 2级： 添加了dom对事件以及css的进一步支持，也是普及的版本。ie9+支持。

- DOM 3级：将dom内容进行模块化，添加了很多新特性，大多数是针对xml部分。



###### document对象

- JavaScript内置的原生对象。也是 JavaScript DOM的核心，包含了绝大多数JavaScript dom 所需要使用的api以及属性。

- 当浏览器载入 HTML 文档, 它就会成为 **Document 对象**。

- Document 对象是 HTML 文档的根节点。

- Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。

- Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

- document 常用的属性和方法

  ```
  document.body:能够快捷的获取页面上的<body>标签;
  document.documentElment: 能够快捷的获取页面上的<html>标签;
  document.title:能够快捷的获取页面名字;
  document.URL: 能够获取页面的地址;
  ```

  

  

###### Node对象

HTML的每个成员都是一个节点对象，节点对象具有自己的属性和方法。

有一句话：一切都是节点Node，一切皆是对象（Node也是对象）。

例如： 获取`<body>`标签内容高度

```
let body = document.body; // 获取页面上的<body>标签;
console.log(body.clientHeight) // 获取内容高度;
```



###### DOM树

```
1. DOM会将整个文档看成"一颗倒挂的树",其“树枝”和"叶子"就是页面上的某个HTML标签，我们称这样的树为“DOM”树。
2. 整个DOM树在程序中被抽象为document对象而存在。DOM树会按照标签的层级关系来进行展示，根标签为<html>标签。页面上其他的标签(也包括了HTML标签里的文字和属性)都会作为DOM树上的一个节点而存在。
3. 目前所学的所有关于DOM的函数或属性(getElementById 、innerHTML、appendChild等)都是用于操作DOM树节点-Node的。
4. DOM树会吧页面上的每个HTML标签以及HTML标签里的属性和文本都会当成一个节点来看待。
```



### 查询节点

方法：

- getElementById()
- getElementsByTagName()
- getElementsByClassName()
- querySelector()
- querySelectorAll()



属性：

- parentNode
- childNodes
- previousSibling
- nextSibling
- firstChild
- lastChild

##### 方法：

###### getElementById()

getElementById() 方法是通过id找到元素节点。

语法：

```
let 变量名 = document.getElementById(id);
```

注意：

- 如果没有指定 ID 的元素就返回 *null*
- 如果存在多个指定 ID 的元素则返回第一个。
- 参数id是元素的id属性值（HTML标签中的id属性值）。
- 获取的是**一个元素节点**，而不是元素集合。



###### getElementsByClassName() 

IE9以下不支持该方法。

getElementsByClassName() 方法是返回带有指定类名对象的数组

语法：

```
let 变量名 =document.getElementsByClassName(classname);  // 整个文档下面获取指定类名
// 参数classname：必须；需要获取的HTML标签的class属性值。   
// 多个类名使用空格分隔，如 "my test"。
let 变量名 =obj.getElementsByTagName(classname); // 指定对象下面获取指定类名
```

例如：

```
// 获取所有包含 red 和 my class名的元素
document.getElementsByClassName('my test');

// 获取 id 为 main 的元素的所有包含一个 test class名的后代元素：
document.getElementById('main').getElementsByClassName('test');
```

返回值：NodeList 对象，NodeList 对象代表一个有顺序的节点列表，也是一个数组，里面包含了满足条件的HTML标签对象。顺序跟HTML代码书写顺序一致的。



###### getElementsByTagName()

getElementsByTagName() 方法是通过**标签名**获取元素对象**集合**。

语法：

```
let 变量名 = document.getElementsByTagName("标签名")
```

返回值：返回一个数组，包含页面上所有同类型的标签。



###### 通过css选择器

获取一个： querySelector()

获取多个： querySelectorAll()

语法：

```
document.querySelector("css选择器")； // 获取满足条件的第一个标签
document.querySelectorAll("css选择器")； // 获取满足条件的所有标签，返回一个数组
```





##### 属性：

###### parentNode

parentNode 属性返回节点的**父节点**，如果节点没有父节点则返回 *null* 。

语法：

```
node.parentNode
```

例如：

```
// 获取id为box的父节点
document.getElementById("box").parentNode;
```



###### childNodes

childNodes属性返回所有子节点的集合。

语法：

```
node.childNodes
```

例子：

```
// 获取 body 元素的子节点集合
document.body.childNodes;
```



###### previousSibling

previousSibling属性返回上一个兄弟节点（处于同一层级）

语法：

```
node.previousSibling
```

例子：

```
// 获取id为box的上一个兄弟节点
document.getElementById("box").previousSibling;
```



###### nextSibling

nextSibling属性返回下一个兄弟节点（处于同一层级）(查找的是Node节点)

语法：

```
node.nextSibling
```

例子：

```
// 获取id为box的上一个兄弟节点
document.getElementById("box").nextSibling;
```



###### firstChild

firstChild属性返回元素的第一个子节点(Node节点)。

语法：

```
node.firstChild
```

例子：

```
// 返回文档节点的第一个子节点
document.firstChild;
```



###### lastChild

lastChild属性返回元素的最后一个子节点。

语法：

```
node.lastChild
```

例子：

```
// 返回文档节点的最后一个子节点
document.lastChild;
```







### 节点信息(了解)

###### nodeName

nodeName属性返回当前节点的节点名称（大写的）。

语法： 

```
node.nodeName
```



###### nodeType

nodeType属性返回元素的节点类型。

语法： 

```
node.nodeType
```

- 如果节点是一个元素节点，nodeType 属性返回 1。

- 如果节点是属性节点, nodeType 属性返回 2。

- 如果节点是一个文本节点，nodeType 属性返回 3。

- 如果节点是一个注释节点，nodeType 属性返回 8。



###### nodeValue

nodeValue属性返回或设置当前节点的值。

语法：

```
str = node.nodeValue; // 获取当前节点的值。
node.nodeValue = str; // 设置当前节点的值。
```

- 对于文档节点来说, `nodeValue`返回`null`。
- 对于text, comment, 和 CDATA 节点来说, `nodeValue返回该节点的文本内容`。
- 对于 attribute 节点来说, 返回该属性的属性值。



### 创建节点

只有document才有这个权限去创建。

###### createElement() 

createElement() 方法用于创建一个**元素节点**。

语法：

```
let element = document.createElement(tagName);
```

参数tagName： 要创建元素的类型（字符串）。

返回值element： 新建的元素。

例如：

```
// 创建一个新的 <div> 
let newDiv = document.createElement("div"); 
```



###### createTextNode() 

createTextNode() 方法用于创建一个**文本节点**。

语法：

```
let text = document.createTextNode(data);
```

参数data：一个字符串，包含了要放入文本节点的内容。

返回值text： 一个文本节点。

例如：

```
// 创建文本节点
let newContent = document.createTextNode("我是新建的文本"); 
```



### 属性的操作

注意： 有些 HTML 属性名是 JavaScript 的保留字，在js中，必须改名。主要是：

1. `for`属性改为`htmlFor`
2. **`class`属性改为`className`**

HTML 元素包括标签名和若干个键值对，这个键值对就称为“属性”（attribute）。

###### 元素的标准属性

HTML 元素的标准属性（即在**标准中定义的属性**），会自动成为元素节点对象的属性。

```
<div id="box" class="mydivclass" title="mydivtitle"></div>

let box = document.getElementById('box');
console.log(box.className);
console.log(box.title);
// div元素标签的属性class和title和id，自动成为节点对象的属性。
// 并且这些属性都是可写的。

```

```
<div id="box" class="mydivclass" title="mydivtitle"></div>

let box = document.getElementById('box');
box.className = 'newClass';
console.log(box)
```

属性操作的标准方法：

元素节点提供四个方法，用来操作属性(主要掌握前面两个)。

1）适用性

对所有属性（包括用户自定义的属性）都适用。

2）属性名

这些方法只接受属性的标准名称，不用改写保留字，比如`for`和`class`都可以直接使用。另外，这些方法对于属性名是大小写不敏感的。



###### getAttribute()

getAttribute()方法用于获取某个节点属性的值，如果指定的属性不存在，则返回  `null` 或 `""`。

语法：

```
let attribute = element.getAttribute(attributeName);
```

参数attributeName： 想要获取的属性值的属性名称。

返回值attribute： 一个包含 `attributeName` 属性值的字符串。

例如：

```
let div1 = document.getElementById("div1");
let align = div1.getAttribute("align");
alert(align); 
```



###### setAttribute()

setAttribute()方法用于给某个节点添加一个属性。如果属性已经存在，则更新该值；否则，使用指定的名称和值添加一个新的属性。

语法：

```
element.setAttribute(name, value);
```

参数name：属性名称。

参数value：属性的值/新值。

例如：

```
let div = document.getElementById("box");
div.setAttribute("name", "myName");
div.setAttribute('class', 'myClass');
div.className=
```



```
 // 创建一个新的 div 元素
  let newDiv = document.createElement("div"); 
  // 给它一些内容
  let newContent = document.createTextNode("Hi there and greetings!"); 
  // 添加文本节点 到这个新的 div 元素
  newDiv.appendChild(newContent); 

  // 将这个新的元素和它的文本添加到 DOM 中
  let currentDiv = document.getElementById("box"); 
  document.body.insertBefore(newDiv, currentDiv);
```

练习： 

	1.  点击按钮，用于切换div的背景颜色红色--蓝色切换
 	2. 页面上有一个输入框、按钮、img标签。输入框输入要修改的图片名字；按钮点击时修改图片(本地的)。
	3. 页面上有一个按钮、img标签。按钮点击时添加随机图片(本地的)。



###### hasAttribute()

`hasAttribute`方法返回一个布尔值，表示当前元素节点是否包含指定属性。

```
let box = document.getElementById('box');

 if (box.hasAttribute('class')) {
       box.setAttribute('class', 'mydivclass');
  }
// 检查div节点是否含有class属性。如果有，则设置为mydivclass。
```

###### removeAttribute()

`removeAttribute`方法用于从当前元素节点移除属性。

```
let box = document.getElementById('box');
box.removeAttribute('class');
```







### 增加节点

###### appendChild()

appendChild()方法为元素添加一个新的子元素（向节点的子节点列表的**末尾添加**新的子节点）。

语法：

```
let element =父元素节点.appendChild(要添加的子元素);
```

参数node：要添加的节点。

返回值element： 添加的节点。

例如：

```
document.getElementById("box").appendChild('<span>www</span>'); //  Failed to execute 'appendChild' on 'Node': parameter 1 is not of type 'Node'.   参数不是一个Node对象
```

```
// 元素通常是由元素节点和文本节点组成。例如创建一个p标签, 你必须创建p元素节点和文本节点。
let p=document.createElement("p")
let t=document.createTextNode("我是文本节点");
p.appendChild(t);
```



注意：可以使用 appendChild() 方法移除元素到另外一个元素。

例如：

```
<ul id="box1"><li>咖啡</li><li>茶</li></ul>
<ul id="box2"><li>水</li><li>牛奶</li></ul>
let node = document.getElementById("box2").lastChild;
document.getElementById("box1").appendChild(node);
```





练习：

1. 点击一个按钮，每点一次，页面上id为box的div中，添加一个空的p标签。
2. 点击一个按钮，每点一次，页面上id为box的div中，添加一个p，p标签有文本，文本随便写（需要创建）。

   



###### insertBefore()

insertBefore()方法是现有的子元素**之前**插入一个新的子元素。

语法：

```
let element = 父元素节点.insertBefore(要插入的节点,现有的子元素)
```

参数newnode：要插入的节点。

参数existingnode： 现有的子元素（要添加新的节点前的子节点）。

例如：

```
<ul id="myList"><li>咖啡</li><li>茶</li></ul>
function fn(){
	var newItem=document.createElement("li")
	var textnode=document.createTextNode("水")
	newItem.appendChild(textnode)
	var list=document.getElementById("myList")
	list.insertBefore(newItem,list.childNodes[0]);
}
```

注意：也可以使用 insertBefore() 方法来移除已存在的元素。

例如：

```
<ul id="myList1"><li>咖啡</li><li>茶</li></ul>
<ul id="myList2"><li>水</li><li>牛奶</li></ul>
function fn(){
	var node=document.getElementById("myList2").lastChild;
	var list=document.getElementById("myList1");
	list.insertBefore(node,list.childNodes[0]);
}
```





### 删除节点

###### removeChild()

removeChild()方法是用于删除一个子元素。如删除成功，此方法可**返回被删除的节点**，如失败，则返回 NULL。

语法：

```
let node = node.removeChild(node)
```

参数node：要移除的节点。

返回值node：移除的节点。

例如：

```
<ul id="myList"><li>咖啡</li><li>茶</li><li>牛奶</li></ul>
function fn(){
	var list=document.getElementById("myList");
	list.removeChild(list.childNodes[0]);
}
```



练习： 

```
 <div id="box">
     <p>一个p标签</p>
     <p>一个p标签</p>
     <p>一个p标签</p>
     <p>一个p标签</p>
  </div>
  // 1. 删除第一个p标签
  // 2. 删除所有的p标签
```



### 修改节点

###### replaceChild()

replaceChild()方法是用于替换子节点。

语法：

```
let node = node.replaceChild(newnode,oldnode)
```

参数newnode：要插入的节点

参数oldnode： 要移除的节点

返回值node： 替换的节点

例如：

```
<ul id="myList"><li>咖啡</li><li>茶</li><li>牛奶</li></ul>
function fn(){
	var textnode=document.createTextNode("水");
	var item=document.getElementById("myList").childNodes[0];
	item.replaceChild(textnode,item.childNodes[0]);
}
// 注意：只是将节点的文本节点“咖啡”替换为“水”,而不是整个li元素,这也是替换节点的一种备选。
```





### innerHTML与innerText

###### innerHTML

innerHTML属性是设置或者返回元素的内容。

语法：

```
// 操作元素对象中的HTML代码（带有标签的文本）
获取：  HTML标签节点.innerHTML 
设置： HTML标签节点.innerHTML = '新的内容'
```

例如：

```
<div id="box">文本内容<p>段落文字</p></div> 
<script>
	let box = document.getElementsById('box'); // 获取div节点
	console.log( box.innerHTML );// 获取box中的HTML代码，会包含标签
	box.innerHTML = '<p>新的段落文字</p>'; // 会解析标签
</script>
```



###### innerText

innerText属性是设置或者返回渲染文本的内容（不带标签的纯文本）。

语法：

```
// 操作元素对象中的文本（不带有标签的纯文本）
获取：  HTML标签节点.innerText 
设置： HTML标签节点.innerText = '新的内容'
```

例如：

```
<div id="box">文本内容<p>段落文字</p></div> 
<script>
	let box = document.getElementsById('box'); // 获取div节点
	console.log( box.innerText );// 获取box中的普通文本，不会包含标签
	box.innerText = '<p>新的段落文字</p>'; // 不会解析标签
</script>
```



### 综合应用

###### 获取节点例子

```
<div>
	p>第一个子元素</p>
	<p>第二个子元素</p>
	<p id='third'>第三个子元素</p>
	<p>第四个子元素</p>
</div>

<script>
	let third = document.getElementById("third");//获取id为third的节点 第三个子元素
	console.log(third.previousSibling);//获取third节点的上一个兄弟节点
	console.log(third.nextSibling );//获取third节点的下一个兄弟节点
	let parent = third.parentNode;//通过third查找父节点
	let children = parent.childNodes;//通过parent查找所有的子节点
	console.log(parent.firstChild);//获取parent第一个子节点
	console.log(parent.lastChild );//获取parent最后一个子节点
</script>
```



###### 创建节点例子

```
<div>
	p>第一个子元素</p>
	<p>第二个子元素</p>
	<p id='third'>第三个子元素</p>
	<p>第四个子元素</p>
</div>

<script>
  // 创建节点
  let addp = document.createElement("p");// 1. 创建节点
  addp.setAttribute("color", "green")// 2. 创建属性节点
  addp.class= 'newPClass'; // 2. 创建属性节点
  addp.innerHTML = "我是新的字元素";// 3. 添加文本内容
  // 追加节点
  let third = document.getElementById("third");//4. 获取id为third的节点 第三个子元素
  let parent = third.parentNode;//通过third查找父节点  或者直接给父节点一个id
  parent.insertBefore(addp, third);   // 在第三个子元素之前添加（移动节点，不是复制节点）
</script>
```



###### 修改节点例子

```
<div>
	p>第一个子元素</p>
	<p>第二个子元素</p>
	<p id='third'>第三个子元素</p>
	<p>第四个子元素</p>
</div>
<script>
	let textnode=document.createTextNode("我是第三个子元素修改之后的值");
	let third = document.getElementById("third");//获取id为third的节点 第三个子元素
	third.replaceChild(textnode,third.childNodes[0]);
</script>
```





###### 删除节点例子：

```
<div>
	p>第一个子元素</p>
	<p>第二个子元素</p>
	<p id='third'>第三个子元素</p>
	<p>第四个子元素</p>
</div>
<script>
	let third = document.getElementById("third");//获取id为third的节点 第三个子元素
	let parent = third.parentNode;//通过third查找父节点  或者直接给父节点一个id
	parent.removeChild(third);
</script>

```



### 获取和修改CSS样式

###### 获取和设置行内样式

1. 获取标签的css属性

   语法：

   ```
   标签变量名.style.css属性名 ;
   ```

2. 修改HTML标签的某个css属性

   语法：

   ```
   标签变量名.style.css属性名 = css属性值;
   ```

   例如：

   ```
   let div = document.getElementById('box');
   div.style.color="red";// 修改文本颜色为红色
   div.style.backgroundColor ="blue";//修改背景颜色为蓝色
   ```

   注意：这种方式只能获取行内样式，通过外联或内联写的样式该方式不能获取。所以修改的css属性在页面会以行内样式而存在。

###### 获取其他样式

getComputedStyle()

该内置函数可以获取某个标签的页面最终所使用的所有的样式。**返回一个对象**，每个css属性都是该对象里的一个属性。

语法：

```
let 变量名 = getComputedStyle(标签变量名,null);// 该变量就保存了函数所返回的对象
```

例如：

```
let div = document.getElementById('box');
let style = getComputedStyle(div,null);
style.css属性名
// 获取文本颜色
style.color
// 获取背景颜色
style.backgroundColor
```



### 练习

1. 页面上有一个输入框、按钮、img标签。输入框输入要修改的图片名字；按钮点击时修改图片。



### 补充

###### 多选框

在js中，可以通过`标签变量名.checked`来获取和设置多选框的选中状态。

语法：

```
获取：  标签变量名.checked
设置： 标签变量名.checked = true 或 false;
```



###### 输入框input

通过js获取输入框的值方法：

1. 获取input节点

   ```
    let input = document.getElementById('input');
   ```

   

2. 获取值

   ```
   let value = input.value;
   ```

   



###### 点击事件

在需要实现点击的标签添加一个`onclick`HTML标签属性，其值就是当点击该HTML标签时要执行的js代码或者执行一个函数。

语法：

```
<div onclick = "alert(0)">mydiv</div>
<button onclick = "fn()">喜欢我，就点我吧</button>

<script>
	function fn() {
		console.log('你点到我了！')
	}
</script>
```



###### eval()

eval ()函数可以把某段字符串作为js代码并执行，最终返回执行的结果。

语法：

```
let 执行结果= eval(待执行的代码字符串)；
```

例如：

```
let num = eval("1+2");
console.log(num);3 // 代码的执行结果
```



###### subStr&&subString

作用：都是获取字符串中的一部分

语法：

```
字符串.substr(子字符串的开始下标,子字符串的字符数量);
字符串.substring(子字符串的开始下标,子字符串的结束下标);// 不包含结束下标
```

注意： 这两个方法如果是从某个位置一直到字符串末尾，第二个参数可以省略不写





###### 常用dom操作的流程

- 如何实现点击

  - 添加一个`onclick`,其值会作为当点击发生时要执行的js代码。一般推荐使用函数

- 如何修改一个标签的内容或属性

  - 通过id或class找到该标签
  - 利用`变量名.innerHTML`来设置标签的内容
  - 利用`变量名.getAttribute`来获取标签的某个属性,利用`变量名.setAttribute()`来设置某个属性

- 如何完成批量添加标签

  - 思路: 先完成添加一个标签，再利用循环完成批量操作
  - 添加一个标签
    - 利用`document.createElement`在程序中新增一个标签
    - 再对新标签进行添加属性、修改内容、修改css等操作
    - 利用`appendChild`将新标签添加到页面上

- 删除一个标签

  - 获取待删除的标签
  - 获取其父标签
  - 父标签调用`removeChild`来删除

- 删除所有标签

  - 利用倒序遍历来依次删除每一个被选中的标签

- 获取标签自身-利用this。`固定用法`

  - 比如获取点击标签本身

  ```
  <img onclick="demo(this)">function demo(elem){    elem指的就是被点击的img元素本身}
  ```

- 如何插入一个标签

- 如何获取或修改css样式

- 如何给标签追加class，而非覆盖

  - 追加

  ```
  标签变量名.classList.add("新class名");
  ```

  - 删除

  ```
  标签变量名.classList.remove("待删除的class名");
  ```





### 扩展

1. 回车，空格也是文本节点Text。

2. 文本节点,`nodeName`属性会返回`"#text"`,而`tagName`属性会返回`undefined`。