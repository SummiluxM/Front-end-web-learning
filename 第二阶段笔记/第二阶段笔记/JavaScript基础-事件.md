# JavaScript基础-事件

任务：

- 事件概念
- 事件分类及常见事件
- DOM0级事件处理程序
- 事件流
- 事件执行阶段
- DOM2级事件处理程序(指定捕获或冒泡)
- event
- 事件委托/事件代理





### 事件概念

- 事件是指将用户跟页面进行交互的动作或行为统称为事件。比如点击事件。
- 当发生指定事件时，开发人员可以去执行程序。
- 也可以理解为用户和计算机交互的方式方法。
- 事件通常与函数结合使用，函数不会在事件发生前被执行 (如用户点击按钮)。





### 事件分类及常见事件

事件大致可以分为：鼠标事件 、键盘事件、窗口事件 、动画事件、表单事件 、拖动事件、触摸事件等等。

**事件的三要素**：

1. 事件源： 发生事件的对象（事件发生在谁身上,谁就是事件源）。
2. 事件类型： 在事件源上发生了什么类型的事件（点击、移入、拖拽）。
3. 事件处理函数： 事件发生时,需要执行的操作。

例如：

```
点击button按钮，弹出我❤️你。
事件源： button按钮。
事件类型：  点击事件。
事件处理函数：弹出信息。
```



### 鼠标事件 



###### onclick

`onclick`: 点击事件。

语法：

```
// html中
<标签 onclick="做一些想做的事情">

// js中
节点对象.onclick=function(){ "做一些想做的事情" };


<div onclick='fn()'></div>
function fn(){
  console.log('111')
}
```





###### ondblclick

`ondblclick`: 双击事件。

语法：

```
// html中
<标签 ondblclick="做一些想做的事情">

// js中
节点对象.ondblclick=function(){ "做一些想做的事情" };
```



###### onmouseover

onmouseover：当鼠标进入指定标签时触发。

语法：

```
// html中
<标签 onmouseover="做一些想做的事情">

// js中
节点对象.onmouseover=function(){ "做一些想做的事情" };
```



###### onmouseout

onmouseout： 当鼠标离开标签时触发（移出）。

语法：

```
// html中
<标签 onmouseover="做一些想做的事情">

// js中
节点对象.onmouseover=function(){ "做一些想做的事情" };
```



###### onmousemove

onmousemove：鼠标在一个元素上移动持续触发。

语法：

```
// html中
<标签 onmousemove="做一些想做的事情">

// js中
节点对象.onmousemove=function(){ "做一些想做的事情" };
```



###### onmousedown

onmousedown： 单击鼠标任何一个按键都会触发

语法：

```
// html中
<标签 onmousedown="做一些想做的事情">

// js中
节点对象.onmousedown=function(){ "做一些想做的事情" };
```



###### onmouseup

onmouseup： 松开鼠标任何一个按键都会触发

语法：

```
// html中
<标签 onmouseup="做一些想做的事情">

// js中
节点对象.onmouseup=function(){ "做一些想做的事情" };
```



注意：

1. 左边/中间鼠标按钮按下时，会依次执行
   - onmousedown
   - onmouseup
   - onclick
2. 右边鼠标按钮按下时，会依次执行
   - onmousedown
   - onmouseup
   - oncontextmenu



### 键盘事件

###### onkeydown

onkeydown： 当键盘按键按压时触发。

语法：

```
// html中
<标签 onkeydown="做一些想做的事情">

// js中
节点对象.onkeydown=function(){ "做一些想做的事情" };
```

例子1:

```
<input type="text" onkeydown="myFunction()">
function fn(){
	alert("你在输入栏内按下一个键");
}
```

例子2：

```
document.addEventListener("keydown",keydown);
//键盘监听，注意：在非ie浏览器和非ie内核的浏览器
//参数1：表示事件，keydown:键盘向下按；参数2：表示要触发的事件
function keydown(event){
    //表示键盘监听所触发的事件，同时传递参数event
    switch(event.keyCode){
        case 37:
            alert("左键");
            break;
        case 39:
            alert("右键");
            break;
    }
}
```





###### onkeyup

onkeyup： 当键盘按键松开后触发。

语法：

```
// html中
<标签 onkeyup="做一些想做的事情">

// js中
节点对象.onkeyup=function(){ "做一些想做的事情" };
```

例子：

```
<input type="text" onkeyup="myFunction()">
function fn(){
	alert("你在输入栏内松开了一个键");
}
```



###### onkeypress

onkeypress： 当键盘按键被按下并松开一个键时触发。

语法：

```
// html中
<标签 onkeypress="做一些想做的事情">

// js中
节点对象.onkeypress=function(){ "做一些想做的事情" };
```

例子：

```
<input type="text" onkeypress="myFunction()">
function fn(){
	alert("你在输入栏内按了一个键");
}
```

注意： 这三者之间的顺序：

- onkeydown
- onkeypress
- onkeyup



### 表单事件

###### onchange

onchange：会在域的内容改变时发生。

注意：在元素的值改变了且失去焦点时触发（两次的值一样不会触发）

语法：

```
// html中
<标签 onchange="做一些想做的事情">

// js中
节点对象.onchange=function(){ "做一些想做的事情" };
```

例如：

```
<input type="text" onchange="myFunction()">
function fn(){
	alert("输入的内容改变了");
}
```



###### oninput

oninput在`input`或`textarea`的值发生改变时触发，不需要等到元素失去焦点，是实时的。它是HTML5的事件，可用于检测文本类输入框的值。

注意：从JS中修改值不会触发事件。

```
<input oninput='iptOninput()'  />


 function iptOninput() {
       console.log('iptOninput');
  }
```



###### onfocus

onfocus： 元素获得焦点时触发（通常用于 input, select等）。

语法：

```
// html中
<标签 onfocus="做一些想做的事情">

// js中
节点对象.onfocus=function(){ "做一些想做的事情" };
```

例如：

```
<input type="text" onfocus="fn()">
//  注意： focus不能写成函数名
function fn(){
	alert("全场灯光聚焦在你身上了");
}
```



###### onblur

onblur： 对象失去焦点时触发。

语法：

```
// html中
<标签 onblur="做一些想做的事情">

// js中
节点对象.onblur=function(){ "做一些想做的事情" };
```

例如：

```
<input type="text" onblur="myFunction()">
// 注意： 函数名不能写成blur
function fn(){
	alert("失焦了");
}
```



###### onsubmit

onsubmit ：在表单提交时触发。

支持标签：`<form>`, `<keygen>`

语法：

```
// html中
<标签 onsubmit="做一些想做的事情">

// js中
节点对象.onsubmit=function(){ "做一些想做的事情" };
```

例如：

```
<form action="" onsubmit="fn()">
  输入名字: <input type="text" name="fname">
  <input type="submit" value="提交">
</form>

<script>
function fn() {
    alert("表单已提交");
}
</script>
```



###### onreset

onreset：在表单被重置后触发。

语法：

```
// html中
<标签 onreset="做一些想做的事情">

// js中
节点对象.onreset=function(){ "做一些想做的事情" };
```

例子：

```
<form onreset="fn()">
	输入您的名字: <input type="text">
	<input type="reset">
</form>
<script>
function fn() {
    alert("表单已重置");
}
</script>
```





### 框架/对象事件

###### onload 

onload ： 在页面或图像加载完成后触发。

语法：

```
// html中
<body onload="做一些想做的事情">  // 不用

// js中
window.onload=function(){ "做一些想做的事情" };
```

例子1:

```
<img src="xxxx.png" onload="onload()">
<script>
  function onload(){
    alert("图片加载完成");
  }
</script>
```

例子2:

```
<script>
  window.onload= function(){
  	alert('页面加载完成')
  }
</script>
```



###### onresize

onresize:  窗口或框架被重新调整大小时触发。

语法：

```
// html中
<body onresize="做一些想做的事情">  // 不用

// js中
window.onresize=function(){ "做一些想做的事情" };
```

例子：

```
<script>
  window.onresize= function(){
  	alert('页面大小改变了！')
  }
</script>
```





### 事件流

概念：事件流指的当某个事件触发时，该事件在嵌套标签之间的触发的顺序。

根据流向不同事件流分为2类

- 冒泡：事件流顺序为先从具体的子标签开始触发，之后父标签触发事件，一直到顶层标签(html)，之后JavaScript还会让document以及window对象进行触发。由子->父(祖先)

  ```
  span->p->div->body->html->document->window
  ```

  

- 捕获:跟冒泡完全相反，先顶层父标签触发，在JavaScript中，先window对象触发，然后document-》html标签，一直到具体的子标签

  ```
  window->document->html->body->div->p->span
  ```

  



### 事件的传播

一个事件发生后，会在子元素和父元素之间传播。这种传播分成三个阶段。

流程:(三个阶段):

1. 第一阶段(捕获阶段)：从window对象触发，一直到具体的子标签为止，即从`window`对象传导到目标节点（上层传到底层）。
2. 第二阶段(目标阶段)：在目标节点上触发，也就是用户实际触发的标签执行一次事件。（可以理解为第一阶段的末尾，可以理解为第三阶段的开始。）
3. 第三阶段(冒泡阶段):执行一次完整的冒泡，即从具体子标签开始触发，直到window对象为止，即从目标节点传导回`window`对象（从底层传回上层）。触发后。事件执行阶段就结束了。



### DOM0级事件处理

事件处理程序；给某个标签指定某个事件，并指定要执行的代码。

注意： DOM0级事件处理程序**只支持冒泡**。

1. html标签中注册（**不建议使用**）

   语法：

   ```
   <html标签 事件类型 = 事件处理函数></html标签>
   ```

   缺点： 全写在html中，代码冗余且没有分离，不方便后期维护。

2. 节点注册

   语法：

   ```
   节点对象.事件类型 = 事件处理函数
   ```

   例如：

   ```
   box.onclick= function(){}
   ```

   缺点： 同一类型的事件不能注册多次。



```
         <div>
             这是div里的内容
             <p>这是p标签里的内容
                <span>这是span标签的内容</span>
             </p>
         </div>
 
 
 		let span = document.getElementsByTagName('span')[0];
        let p = document.getElementsByTagName('p')[0];
        let div = document.getElementsByTagName('div')[0];
        // dom0级事件处理程序
        div.onclick = function (){
            console.log('div被点击了');
        }
        p.onclick = function (){
            console.log('p被点击了');
        }
        span.onclick = function (){
            console.log('span被点击了');
        }
        //body
        document.body.onclick = function(){
            console.log('body被点击了');
        }
        //html
        document.documentElement.onclick = function(){
            console.log('html被点击了');
        }
        //document
        document.onclick = function(){
            console.log('document被点击了');
        }
        //window 
        window.onclick = function(){
            console.log('window被点击了');
        }
```







### DOM2级事件处理

实现类似onclick的效果，即指定事件处理程序。只不过dom2级可以**指定捕获阶段处理还是冒泡阶段处理**，而dom0级只能在**冒泡阶段**处理。

###### 创建

```
标签变量名.addEventListener("事件名",function(){},布尔型);
// 第一个参数：事件名     一定注意没有on！！！
// 第二个参数：指的事件触发要执行的函数
// 第三个参数（可选）：是否在捕获阶段处理，true表示捕获阶段，false即冒泡阶段处理，不写则默认冒泡阶段处理。
```





```
	<div>
        这是div里的内容
        <p>这是p标签里的内容
            <span>这是span标签的内容</span>
        </p>
    </div>
    
    
       let span = document.getElementsByTagName('span')[0];
        let p = document.getElementsByTagName('p')[0];
        let div = document.getElementsByTagName('div')[0];
        
         //捕获
         span.addEventListener('click',spandemo,true);
         function spandemo(){
             console.log('span被点击了');
         }
         p.addEventListener('click',function(){
             console.log('p被点击了');
         },true);
         div.addEventListener('click',function(){
             console.log('div被点击了');
         },true);
         
         
         
    	//冒泡
        //  span.addEventListener('click',function(){
        //      console.log('span被点击了');
        //  },false);
        //  p.addEventListener('click',function(){
        //      console.log('p被点击了');
        //  },false);
        //  div.addEventListener('click',function(){
        //      console.log('div被点击了');
        //  },false);
        
```



注意： 如果第二个参数是一个函数名，那么需要注意：

```
		<p>段落文字ppppppppppppppppppp</p>

 		let p = document.querySelector('p')
        p.addEventListener('click', function (event) { // 匿名函数
            console.log(1);
        },false);

        p.addEventListener('click', function (event) {
            // 会触发
            console.log(2);
        },false);

        p.addEventListener('click', function (event) {
            // 会触发
            console.log(3);
        },false);

        p.addEventListener('click', function (event) {
            // 会触发
            console.log(4);
        },false);
        
        
        
        p.addEventListener('click', callback, false);
        
        
        // 不会触发
        p.addEventListener('click', callback, false);
        // 会触发
        p.addEventListener('click', callback1, false);
        
        function callback1(event) {
            console.log('callback1');
        }
        function callback(event) {
            console.log('callback');
        }
```





###### 删除

```
标签变量名.removeEventListener("事件名",function(){},布尔型);
// 第一个参数：事件名
// 第二个参数：指的事件触发要执行的函数
// 第三个参数（可选）：是否在捕获阶段处理，true表示捕获阶段，false即冒泡阶段处理，不写则默认冒泡阶段处理。
```

注意：

removeEventListener 会删除通过addEventListener创建的事件处理程序。但是有两个条件

- 所有参数必须一致
- 不能够删除第二个参数是匿名函数。

例如：

```
window.addEventListener(“click”,handler,false);
function handler(){
	console.log('冒泡:点击window了');
}
// 删除
 window.removeEventListener("click",handler,false);
```

```
		 <div>
            这是div里的内容
            <p>这是p标签里的内容
                <span>这是span标签的内容</span>
            </p>
        </div>
        
		
		let span = document.getElementsByTagName('span')[0];
        let p = document.getElementsByTagName('p')[0];
        let div = document.getElementsByTagName('div')[0];
         // dom 2级 
         //捕获
         span.addEventListener('click',spandemo,true);
         function spandemo(){
             console.log('span被点击了');
         }
         p.addEventListener('click',function(){
             console.log('p被点击了');
         },true);
         div.addEventListener('click',function(){
             console.log('div被点击了');
         },true);
         //删除捕获
         span.removeEventListener('click',spandemo,true);
         p.removeEventListener('click',function(){
             console.log('p被点击了');
         },true);
         div.removeEventListener('click',function(){
             console.log('div被点击了');
         },true);
```





### 事件处理小结

###### DOM0级(冒泡)

```
 // HTML标签中  不推荐
 <p on事件名="要执行的代码"></p>
// js中：
节点对象.on事件名 = function(){
}
```



###### DOM2级

```
节点对象.addEventListener()
节点对象.removeEventListener()
```





### event

概念：当某个事件触发时，JavaScript会自动收集该事件的相关信息并包装成一个event原生对象，并自动作为实际参数传入事件处理程序中，我们可以在事件处理程序定义一个形式参数来接收并使用。

event对象常用的属性：

- `target`:保存了触发该事件的具体标签
- `currentTarget`:指的是当前事件执行阶段正在处理的标签，会随着事件执行阶段的进行而变化。
- `preventDefault()`:会取消原有标签的默认行为，比如提交按钮、超链接等
- `stopPropagation()`:取消进一步的冒泡。
- `type`:该事件的类型，返回一个字符串。
- `clientX`:当发生事件时，鼠标相当于窗口的x坐标，以窗口的左上角为原点。
- `clientY`:当发生事件时，鼠标相当于窗口的Y坐标，以窗口的左上角为原点。
- `eventPhase`:  是在事件传播的第几个阶段

注意： 同一个事件只会有一个event对象，event对象可以通过事件流传递给父标签的事件处理程序中。

```
	<div>
        <button>登录</button>
        <a href="http://www.baidu.com" onclick="demo2(event)">百度</a>
    </div>
    
    
    
     	let btn = document.getElementsByTagName('button')[0];
        btn.addEventListener("click",demo,false);
        let div = document.getElementsByTagName("div")[0];
        div.addEventListener("click",demo,false);
        document.body.addEventListener("click",demo,false);
        function demo(e){
            console.log('currentTarget:',e.currentTarget);
            console.log("target",e.target);
        }

        function demo2(e){
            //阻止默认
            e.preventDefault();
            //阻止冒泡
            e.stopPropagation();
            console.log('偏不让你访问百度');
        }
    
```







例子：

```
<div>
  <p>点击</p>
</div>
```

```
let div = document.querySelector('div');
let p = document.querySelector('p');

div.addEventListener('click', callback, true);
p.addEventListener('click', callback, true);
div.addEventListener('click', callback, false);
p.addEventListener('click', callback, false);

function callback(event) {
  let tag = event.currentTarget.tagName;
  console.log(event.type);
  console.log("Tag:'"+tag);
}
// 1
// Tag: 'DIV
// 2
// Tag: 'P
// 2
// Tag: 'P
// 因为addEventListener第三个参数不同，会导致绑定两个监听函数
// 3
// Tag: 'DIV
```

上面代码表示，`click`事件被触发了四次：`<div>`节点的捕获阶段和冒泡阶段各1次，`<p>`节点的目标阶段触发了2次。

1. 捕获阶段：事件从`<div>`向`<p>`传播时，触发`<div>`的`click`事件；
2. 目标阶段：事件从`<div>`到达`<p>`时，触发`<p>`的`click`事件；
3. 冒泡阶段：事件从`<p>`传回`<div>`时，再次触发`<div>`的`click`事件。

其中，`<p>`节点有两个监听函数（`addEventListener`方法第三个参数的不同，会导致绑定两个监听函数），因此它们都会因为`click`事件触发一次。所以，`<p>`会有两次输出。





### 事件委托

由于事件会在冒泡阶段向上传播到父节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件。这种方法叫做事件的代理（也叫事件委托）。

核心思想：

- 给父标签或者祖先标签设置一个事件处理程序，然后利用event对象里的target来判断实际触发事件的标签，然后调用对应的处理代码

作用：减少事件处理程序的代码。

例子1:

```
<div>
    <p>
    <span></span>
    </p>
</div>
需求：都需要设置点击事件
```

分析： 因为div是span、p标签的父标签，给子标签设置点击事件，会因为冒泡机制，父标签也会触发，所以我们可以直接对div设置点击事件，利用event对象来判断实际用户点击的是哪个子标签，然后调用对应 的函数即可。

```
	<div id="box">
        这是div里的内容
        <p>这是p标签里的内容
            <span class="icon">这是span标签的内容</span>
        </p>
    </div>

  		let span = document.getElementsByTagName('span')[0];
        let p = document.getElementsByTagName('p')[0];
        let div = document.getElementsByTagName('div')[0];
        //事件委托进行优化
        document.body.addEventListener('click',handler);
        function handler(e){
            //业务逻辑
            if(e.target == span){
                 console.log('点击了span');
            }else if(e.target == p){
                console.log('点击了p标签');
            }else if(e.target ==div){
                 console.log('点击了div');
            }
        }
        document.body.removeEventListener('click',handler);
```



例子2：

```
	<ul>
        <li>1</li>
        <li>2</li>
    </ul>
    <p>p</p>
    <a>a</a>

document.onclick = function(e){
    // console.log(e.target);
    //对target判断\
    let type =e.target.nodeName;
    if(type=="A"){
    //超链接
    console.log("点击a了");
    }else if(type=="P"){
    console.log("点击p了");
    }else if(type=="LI"){
    console.log("点击Li了");
    }else if(type=="UL"){
    console.log("点击ul了");
    }else if(type=="HTML"){
    console.log("点击html了");
    }
}
```



事件委托应用场景：

```
let ul = document.querySelector('ul');

ul.addEventListener('click', function (event) {
  if (event.target.tagName === 'LI') {
    // xxxxxxx
  }
});

// 上面代码中，click事件的监听函数定义在<ul>节点，但是实际上，它处理的是子节点<li>的click事件。这样做的好处是，只要定义一个监听函数，就能处理多个子节点的事件，而不用在每个<li>节点上定义监听函数。而且以后再添加子节点，监听函数依然有效。
```





### 例子

例子1：

```
<div id="box">哈喽</div>
    <script>
        //获取元素对象
        let box = document.getElementsById('box');

        //注册事件
        /* box.onclick = function(){
            box.style.color = 'red'
        } */

        box.onclick = toColor;
        //box.onclick = toColor();//加():进来就会无条件执行一次  所以不能加
        
        function toColor(){
            box.style.color = 'red'
        } 
    </script>
```



例子2:

```
<input type="text" id='input'>
    <script>     
        //需求： 只允许输入6位字符
        // 1. 输入的时候就应该判断当前输入字符的长度
        // 2. 如果大于6位 ： 截取前6位字符 赋值给自己 
        let input = document.getElementsById("input");
        //注册事件
        input.addEventListener('keyup',function(){      
            //获取当前输入的字符
            if( this.value.length > 6 ){
                //截取前6位的字符赋值给自己 
                this.value = this.value.substr(0, 6)
            }
        })
</script>
```



例子3:

```
		<!-- 
     4.验证用户名长度是否大于等于6位并且小于等于12位，
        如果条件成立提交表单到regsiter.html页面，
        否则弹出提示框注册失败: 不会跳转到regsiter页面
        事件源： form表单
        事件类型：onsubmit 提交之前验证
    -->
    <form id='form' action="./register.html">
        <input id="user" type="text" name="user" >
        <input type="submit" value="注册">
    </form>
    <script>
        
        //获取form标签
        let form = document.getElementsById("form");

        //获取user
        let user = document.getElementById("user");

        //注册事件
        form.onsubmit = function(){
             //满足的条件： user.value.length >= 6 && user.value.length <= 12
            //只判断失败情况
            if(user.value.length < 6  ||  user.value.length > 12){
                //阻止浏览器默认行为
                return false;
            } 
        }
</script>
```

例子4：

阻止表单提交

```
	<form action="success.html" id="loginForm">
        账号: <input type="text" id="user">
        密码: <input type="password" id="pass">
        <button onclick="login(event);">登录</button>
    </form>
    
    
	 function login(e){
            //除非两个输入框都有数据，才允许提交表单
            // 先阻止提交
            e.preventDefault();
            let userinput = document.getElementById('user');
            let passinput = document.getElementById('pass');
            let form = document.getElementById('loginForm');
            if(userinput.value!="" && passinput.value!=""){
                //表单提交
                form.submit();
            }else{
                form.reset();
            }
        }
```





### 补充

###### 自定义属性

有时，需要在HTML元素上附加数据（例如标识： 最常使用的是id），使得在js中使用，很好的一种解决方法就是自定义属性。

```
<div id="box" foo="bar">

let box = document.getElementById('box');
console.log(n.foo); // undefined
console.log(box.getAttribute('foo'));
box.setAttribute('foo', 'baz')
```

这种方法虽然可以达到目的，但是会使得 HTML 元素的属性不符合标准，导致网页代码通不过校验。

更好的解决方法是，使用HTML5提供的`data-`属性。

```
<div id="box" data-foo="bar">
```

然后，使用元素节点对象的`dataset`属性，它指向一个对象，可以用来操作 HTML 元素标签的`data-xxx`属性。

```
let box = document.getElementById('box');
box.dataset.foo // bar
box.dataset.foo = 'baz';
// 通过dataset对象 读写data-foo属性。

```

除了`dataset`属性，也可以用`getAttribute('data-foo')`、`setAttribute('data-foo')`、`removeAttribute('data-foo')`、`hasAttribute('data-foo')`等方法操作`data-xxx`属性。

```
console.log(box.getAttribute('data-foo'));
box.setAttribute('data-foo','barbar')
```





### 扩展

###### 自定义属性

`data-`后面的属性名有限制，只能包含字母、数字、连词线（`-`）、点（`.`）、冒号（`:`）和下划线（`_`)。而且，属性名不应该使用`A`到`Z`的大写字母，比如不能有`data-helloWorld`这样的属性名，而要写成`data-hello-world`。

转成`dataset`的键名时，连词线后面如果跟着一个小写字母，那么连词线会被移除，该小写字母转为大写字母，其他字符不变。反过来，`dataset`的键名转成属性名时，所有大写字母都会被转成连词线+该字母的小写形式，其他字符不变。比如，`dataset.helloWorld`会转成`data-hello-world`。