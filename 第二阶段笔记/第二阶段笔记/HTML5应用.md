# HTML5应用

### 任务

- 本地存储(重要)
- canvas（了解）
-  拖放（熟悉）
- 视频、音频（熟悉）
- 地图（了解）





### 本地存储(重要)

随着Web的发展，数据存储不再是单一的存储在数据库中。浏览器存储的用途也越来越多，最经典的就是“记住用户名”。实现浏览器存储的方式有很多种，HTML5出现之前，最常使用的是cookie，但是cookie存储容量有限（4K ），而且安全性并不高。

本地存储有两种：

- localStorage
- sessionStorage 

###### localStorage

`localStorage`用于**持久化**本地存储，存储在 `localStorage` 的数据可以长期保留,除非用户手动删除，否则数据是永远不会过期的。

localStorage的方法：

- `localStorage.setItem(key,value)`:  指定key和value保存数据。key是保存数据的健，value是保存数据的值。
- `localStorage.getItem（key）`:   通过key获取数据。 key是获取对应数据的键，与setItem中的key对应。
- `localStorage.removeItem(key)`:  通过key删除数据。 key是删除对应数据的键，与setItem中的key对应。
- `localStorage.clear()`:  清除所有数据

例如：

```
localStorage.setItem('name','pyy');
localStorage.getItem('name');
localStorage.removeItem('name');
localStorage.clear();
```

注意：

- 本地存储只支持 string 类型的存储。如果是对象，就需要转换。
- 本地存储也是遵循同源策略的，所以不同的网站直接是不能共用相同的 localStorage。
- 也可以使用localStorage.变量名、localStorage[变量名]去设置和获取值（所以就有三种方式）。

```
localStorage.setItem('age', 17);
console.log(typeof localStorage.getItem('age')); // string
```

```
localStorage.setItem('person', {name: 'pyy'}); // 会自动转化为字符串类型
console.log(typeof localStorage.getItem('person')); // string  

// 解决方案
localStorage.setItem('person', JSON.stringify({name: 'pyy'})); // JSON.stringify转化对象为字符串
console.log( JSON.parse(localStorage.getItem('person'))); // JSON.parse再把这个字符串转换为对象

// 注意： 1. Object类型都需要转换  2. JSON.stringify和JSON.parse要结合使用，不能单独使用。
```

```
<button onclick='btnClick()'>按钮</button>
<span id="pyy"></span>

btnClick = () => {
  if(localStorage.num) {
  	localStorage.num = parseInt(localStorage.num)+1; // 需要转换成number类型
  } else {
  	localStorage.num = 1;
  }
  document.getElementById("pyy").innerHTML = "你已经点击了 " + localStorage.num + " 次"
}
```



###### sessionStorage

`sessionStorage`是用于存储一个会话中的数据，一个会话就是打开网页的那一刻直到网页被关闭的那一刻。

sessionStorage的方法：

- `sessionStorage.setItem(key,value)`:  指定key和value保存数据。key是保存数据的健，value是保存数据的值。
- `sessionStorage.getItem（key）`:   通过key获取数据。 key是获取对应数据的键，与setItem中的key对应。
- `sessionStorage.removeItem(key)`:  通过key删除数据。 key是删除对应数据的键，与setItem中的key对应。
- `sessionStorage.clear()`:  清除所有数据

注意：

- 页面会话在浏览器打开期间一直保持，并且重新加载或恢复页面仍会保持原来的页面会话。
- 打开多个相同的URL的Tabs页面，会创建各自的`sessionStorage`。



sessionStorage和localStorage的总结：

1. `localStorage` 里面存储的数据没有过期时间设置，而存储在 `sessionStorage` 里面的数据在页面会话结束时会被清除（关闭页面的时候）。
2. 两个方式都只能保存字符串形式的键值对。
3. 两个方式大小有的浏览器为5m，有的是无限制。
4. 不同浏览器之间数据不能共享。



```
// 模拟登陆注册
```





### json

###### 概念

- `JSON`对象是 JavaScript 的原生对象，用来处理 JSON 格式数据。它有两个静态方法：`JSON.stringify()`和`JSON.parse()`。

- JSON是JavaScript Object Notation，JavaScript简谱。json本质上是具有一定书写规则的字符串。但JavaScript可以将json转为对象或吧对象转为json进行使用。
- json是一种轻量级的数据交换格式。json一般只使用在数据传输过程中，但无论是在浏览器还是服务器，最终操作的还是对象。

###### 特点

- 占用空间小，方便传输
- 可以直接和对象进行互转
- 支持绝大多数后端语言。java、Python、php等。

###### 语法

- 主要为[]和{}
- 数据都是键值对形式
- []表示数组
- {}表示对象
- json最终必须是一个对象

注意：

1. 字符串必须使用双引号表示，不能使用单引号。
2. 对象的键名必须放在双引号里面。
3. 数组或对象最后一个成员的后面，不能加逗号。



###### json与JavaScript对象之间的转换

- json转对象: JSON.parse()

```javascript
var 对象名 = JSON.parse(json字符串);
```

- 对象转json: JSON.stringify()

```javascript
var 字符串名 = JSON.stringify(对象名);
```







### canvas

###### 常见概念

- `<canvas>`：本质上是HTML5 新增的标签，主要是为JavaScript绘制提供了绘制的空间，绘制图形及图形动画。角色类似于中学时的`黑板`。默认情况下宽高为300*150(px)
- `画笔`:是一个`CanvasRenderingContext2D`类的对象，由JavaScript中的`getContext('2d')`来获取。该对象包含了用于canvas绘制的所有的方法，比如绘制图形、图片等。角色类似于`粉笔`.
- `画布中的坐标系`：默认情况下是以画布标签的左上角为原点,水平为x轴，垂直为y轴，并且向右和向下为正。
- `路径`:由起点到终点的完整的线条称为路径。canvas里`beginPath()`就表示开始一条路径，`closePath`表示路径结束。canvas会自动将起点和终点进行连接，形成一个闭合的路径。这两个是在绘制几何图形时使用
- `子路径`:子路径是指路径中的一部分，具体是指路径中两个点之间的线条。即路径由多条子路径构成。
- `画布中的角度`:`1*(Math.PI/180)` 表示一度 ,`Math.PI`表示180度

注意： 和img不同，**canvas需要结束标签**，如果没写，文档的其余部分会被认为是替代内容，将不会显示出来。

```
// <canvas>简单实例如下:
<canvas id="canvas" width="200" height="100" style="border:1px solid #000000;"></canvas>
// 注意: 标签通常需要指定一个id属性 (通过JavaScript的dom获取), width 和 height 属性定义的画布的大小.
// 使用 style 属性来添加边框
```



###### canvas绘制的大致流程

1. 利用 DOM获取画布以及对应的画笔(获取画布和画笔)

2. 调用画笔对象所提供的api来完成绘制。

   注意：canvas只支持两种形式的图形绘制：**矩形和路径**



###### 画布、画笔的获取

```
// 画布：通过JavaScript dom获取
let canvas = document.getElementById('canvas'); 
// 使用js来控制画布大小： 画布对象名.width 画布对象名.height

//  画笔：在获取画布之后：let 画笔变量名 = 画布对象名.getContext('2d');
let ctx = canvas.getContext('2d');  //getContext("2d") 对象是内建的 HTML5 对象，拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。
```



###### 画布中的坐标系

canvas 是一个二维网格，画布中的坐标系以画布的左上角为原点(0,0),x轴向右为正，y轴向下为正。



###### 移动画笔

`moveTo(x,y) ` ： 将画笔移动到指定的坐标x以及y上。

- 这个函数实际上并不能画出任何东西，就好像在纸上作业，一支钢笔或者铅笔的笔尖从一个点到另一个点的移动过程。

- 常使用`moveTo(x,y) ` 设置新起点。



###### 线

`lineTo(x,y) `： 绘制一条从当前位置到指定x以及y位置的直线。

例如：

```
let canvas=document.getElementById("canvas");
let ctx=canvas.getContext("2d");
ctx.strokeStyle="#FF0000"; // 属性。设置线条的颜色，支持颜色单词，16进制、rgb
ctx.lineWidth = 5; // 属性。设置线条的粗细。以数字为单位，
// strokeStyle、lineWidth要放到stroke之前
ctx.moveTo(0,0); // 定义线条开始坐标
ctx.lineTo(200,100); // 定义线条结束坐标
ctx.stroke(); // 把线条显示在页面上
```



###### 绘制路径

图形的基本元素是路径。路径是通过不同颜色和宽度的线段或曲线相连形成的不同形状的点的集合。一个路径，甚至一个子路径，都是闭合的。使用路径绘制图形需要一些额外的步骤。

1. 创建路径起始点。
2. 然后你使用画布api去画出路径。
3. 封闭路径
4. 描边或填充路径区域来渲染图形

常用函数：

- beginPath()： 开始绘制路径
- closePath():   闭合路径，并会自动将起点和终点进行连接
- stroke():   将勾勒出的线条绘制在画布上
- fill():    填充某个图形

注意：当你调用fill()函数时，所有没有闭合的形状都会自动闭合，所以你不需要调用closePath()函数。但是调用stroke()时不会自动闭合。

例如：

```
// 绘制实体三角形
let canvas=document.getElementById("canvas");
let ctx=canvas.getContext("2d");
ctx.beginPath(); // 开始绘制路径
ctx.moveTo(75, 50); // 移动到左边点
ctx.lineTo(100, 75); // 移动到上点
ctx.lineTo(100, 25); // 移动到下点
ctx.fillStyle = 'red'; // 属性，设置填充颜色。
ctx.fill();
// canvas初始化或者beginPath()被调用后，常会使用moveTo()函数设置起点。
```



###### 绘制圆

arc(): 绘制圆弧或者圆.

语法：

```
arc(x, y, radius, startAngle, endAngle, anticlockwise);
// 该方法有六个参数：x,y为绘制圆弧所在圆上的圆心坐标。radius为半径。startAngle以及endAngle参数用弧度定义了开始以及结束的弧度。这些都是以x轴为基准。参数anticlockwise为一个布尔值。为true时，是逆时针方向，否则顺时针方向。  ===     arc(圆心x，圆心y,半径,开始角度，结束角度，是否逆时针);

// 画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。
```

注意：

- 默认为顺时针，为true表示逆时针
- 表示角的单位是弧度，不是角度。     弧度=(Math.PI/180)\*角度。

例如：

```
// 绘制一个圆
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);
ctx.stroke();
```

```
// 绘制一个笑脸
ctx.beginPath();
ctx.arc(75, 75, 50, 0, Math.PI * 2, true); // 绘制外圆
ctx.moveTo(110, 75);
ctx.arc(75, 75, 35, 0, Math.PI, false);   // 口(顺时针)
ctx.moveTo(65, 65);
ctx.arc(60, 65, 5, 0, Math.PI * 2, true);  // 左眼
ctx.moveTo(95, 65);
ctx.arc(90, 65, 5, 0, Math.PI * 2, true);  // 右眼
ctx.stroke();
```



###### 绘制矩形

三种方法绘制矩形：

- `fillRect(x, y, width, height)`： 绘制一个填充的矩形
- `strokeRect(x, y, width, height)`： 绘制一个矩形的边框
- `clearRect(x, y, width, height)`：清除指定矩形区域，让清除部分完全透明

三种方法参数都一样，x与y指定了矩形的左上角坐标(相对于原点)；width和height设置矩形的尺寸。

例子：

```
 ctx.fillRect(25, 25, 100, 100);
 ctx.clearRect(45, 45, 60, 60);
 ctx.strokeRect(50, 50, 50, 50);
```

`fillRect()`函数绘制了一个边长为100px的黑色正方形。`clearRect()`函数从正方形的中心开始擦除了一个60*60px的正方形，接着`strokeRect()`在清除区域内生成一个50*50的正方形边框。





### 拖放

概念：拖放事件（Drag 和 drop）是HTML5新增的标准特性，绝大多数浏览器都支持，除了ie低版本。

原理：拖放是一种常见的特性，即抓取对象以后拖到另一个位置。在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放。

###### 流程

1. 给需要拖拽的标签设置`draggable=true`

   ```
   <img draggable="true">
   ```

2. 然后，规定当元素被拖动时，会发生什么。给拖拽的标签设置`ondragstart`事件，事件里利用`dataTransfer.setData() `方法设置被拖数据的数据类型和值

   - `setData(‘属性名’,'属性值')`:以键值对方式保存某个数据
   - `getData(‘属性名’)`:获取某个数据

   ```
   <img id='box' draggable="true"  ondragstart="dragstart(event)">
   
   function dragstart(e){
     e.dataTransfer.setData("Text",e.target.id); 
   }
   // Text是表示要添加的拖动数据的类型。值是可拖动元素的 id 
   ```

3. 放到何处。`ondragover` 事件规定在何处放置被拖动的数据。

   默认地，无法将数据/元素放置到其他元素中。如果需要设置允许放置，我们必须阻止对元素的默认处理方式。这要通过调用 ondragover 事件的 event.preventDefault() 方法。

   ```
   <div ondragover="dragover(event)"></div>
   
   function dragover(e){
     e.preventDefault();
   }
   ```

4. 进行放置

   当放置被拖数据时，会发生 drop 事件。

   ```
   <div ondragover="dragover(event)" ondrop="drop(event)"></div>
   
   function drop(e){
       e.preventDefault(); // 调用preventDefault()来避免浏览器对数据的默认处理
       let data=e.dataTransfer.getData("Text"); // 通过dataTransfer.getData("Text") 方法获得被拖的数据。 和第二步setData设置的对应
       e.target.appendChild(document.getElementById(data)); // 把被拖元素追加到放置目标元素中
   }
   ```

完整示例：

```
 <div style="width:350px;height:70px;padding:10px;border:1px solid #aaaaaa;" ondragover="dragover(event)" ondrop="drop(event)"></div>
  <div style="width:350px;height:70px;padding:10px;border:1px solid #aaaaaa;" ondragover="dragover(event)" ondrop="drop(event)">// 定义两个 这样就可以来回拖动
        <span id='box' draggable="true" ondragstart="dragstart(event)">被拖拽的元素</span>
   </div>
  
  <script>

    function dragstart(e) {
      e.dataTransfer.setData("s", e.target.id);
    }
    function dragover(e) {
      e.preventDefault();
    }
    function drop(e) {
      e.preventDefault(); // 调用preventDefault()来避免浏览器对数据的默认处理
      let data = e.dataTransfer.getData("s"); // 通过dataTransfer.getData("Text") 方法获得被拖的数据。 和第二步setData设置的对应
      e.target.appendChild(document.getElementById(data)); // 把被拖元素追加到放置目标元素中
    }

  </script>
```



拖拽相关事件及属性（了解）

- `dragstart`：是个事件。该事件在刚开始拖拽时在拖拽元素上触发。一般会用来设置数据。
- `dragover`：是在拖拽时不断触发的事件，一般会给放置元素设置取消默认的不可放置行为。即表示某个元素可以放置在另一个元素之前或之后。
- `dragleave`:当拖拽元素离开放置元素时触发。给放置元素设置
- `drop`：是放置事件。放置元素进行触发。一般我们会在事件里获取`dragstart`事件里设置的数据，并进行拖拽的dom处理。
- `draggable`：HTML标签属性。设置某个HTML标签是否可拖拽，默认是不可拖拽的-false，布尔型。
- `dataTransfer`：是拖拽相关事件的event对象才有的一个对象属性。可以利用它来实现拖拽的数据传输。一般我们会将拖拽元素的id或class保存到`dataTransfer`中，在`drop`事件中获取该数据并进行处理
  - `setData(‘属性名’,'属性值')`:以键值对方式保存某个数据
  - `getData(‘属性名’)`:获取某个数据
- `offsetX&offsetY`：event对象中的属性。指鼠标相对于放置元素的 偏移量。即鼠标相对于放置元素左上角坐标的偏移量



总结：

​	拖拽一般流程：

1. 给需要拖拽 的标签设置`draggable=true`
2. 给拖拽的标签设置`dragstart`事件，事件里利用`dataTransfer`保存拖拽元素的class或id
3. 给放置元素设置`dragover`事件，事件里取消默认行为，保证该标签可以放置拖拽元素
4. 给放置元素设置`drop`事件，事件里利用`dataTransfer`来获取所保存的数据，并进行业务处理。







### HTML5 地图api&百度地图api

###### HTML 5 自带地理api

概念：HTML5 标准里增强了navigator对象，添加了`geoLocation`属性来获取地理位置相关信息。但是地理位置大多数浏览器有访问限制，且得到的信息不是特别的实用，所以更多的是使用第三方的地图。

语法

```
navigator.geoLocation.getCurrentPosition(success,fail);
需提供两个函数参数，success表示请求地理位置成功，并把地理信息包含在event对象中，fail表示请求失败。
```

- 地理event对象

  - `longtitude`:经度
  - `latitude`:纬度
  - `altitude`:海拔高度
  - `speed`:风速
  - `heading`:方向

- 地理位置只有火狐和ie能够获取，并且一般只有经度和纬度

例如：

```
	function success(e){
            console.log('获取地理位置成功');
            console.log(e);
        }
        function fail(e){
            console.log('获取地理位置失败');
            console.log(e);
        }
        navigator.geolocation.getCurrentPosition(success,fail);
```



###### 百度地图api

- 基本流程
  - [登录百度地图开发平台](http://lbsyun.baidu.com/)
  - 进入控制台，创建应用，获取ak密钥
  - 结合百度api的例子来尝试
- 常见应用
  - 根据指定经纬度来定位地图
  - 在某个位置加上标注，标注加上跳动动画
  - 给标注添加点击事件



```
<style type="text/css"> 
    html{height:100%} 
    body{height:100%;margin:0px;padding:0px} 
    #container{height:100%} 
</style> 
<script type="text/javascript" src="https://api.map.baidu.com/api?v=1.0&type=webgl&ak=6LfziDiCL4Q5Ie17VeZDkVqybFNXGZW4">
</script>



<div id="container"></div>
<script type="text/javascript">
    var map = new BMapGL.Map("container");
    // 创建地图实例 
    var point = new BMapGL.Point(116.404, 39.915);
    // 创建点坐标 
    map.centerAndZoom(point, 15);
    // 初始化地图，设置中心点坐标和地图级别 
</script> 
```



###### 高德地图api

1. 登录网址： https://lbs.amap.com/api/javascript-api/summary
2. 左上角登录，登录成功之后，点击应用管理
3. 在应用管理中，找到我的应用（默认没有，点击新建应用）
4. 新建应用： 应用名称、类型随便写。
5. 应用新建完成，展开点击新建，key名称随便写（符合规范），服务平台选择web端，勾选同意条款（域名白名单不要写）再点击提交。
6. 进入实例中心： https://lbs.amap.com/api/javascript-api/example/geocoder/geocoding 选择自己想要的功能
7. 实例右边，有个源代码编辑器。引入两个script，第一个把我们的key复制进去，第二个就修改一下，修改成我们对应的容器或者是代码。







### 扩展

###### svg

- SVG 指可伸缩矢量图形
- 图像在放大或改变尺寸的情况下其图形质量不会有所损失(不会失真)

面试题：svg和canvas区别

![clipboard.png](https://segmentfault.com/img/bVbv5p9?w=664&h=199)



###### 贝塞尔曲线

- quadraticCurveTo(cp1x, cp1y, x, y)  ： 绘制二次贝塞尔曲线，`cp1x,cp1y`为一个控制点，`x,y为`结束点
- bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)： 绘制三次贝塞尔曲线，`cp1x,cp1y`为控制点一，`cp2x,cp2y`为控制点二，`x,y`为结束点。



![img](https://mdn.mozillademos.org/files/223/Canvas_curves.png)



二次贝塞尔曲线有一个开始点（蓝色）、一个结束点（蓝色）以及一个控制点（红色），而三次贝塞尔曲线有两个控制点。参数x、y在这两个方法中都是结束点坐标。`cp1x,cp1y`为坐标中的第一个控制点，`cp2x,cp2y`为坐标中的第二个控制点。

二次贝塞尔曲线例子：

```
ctx.beginPath();
ctx.moveTo(75, 25);
ctx.quadraticCurveTo(25, 25, 25, 62.5);
ctx.quadraticCurveTo(25, 100, 50, 100);
ctx.quadraticCurveTo(50, 120, 30, 125);
ctx.quadraticCurveTo(60, 120, 65, 100);
ctx.quadraticCurveTo(125, 100, 125, 62.5);
ctx.quadraticCurveTo(125, 25, 75, 25);
ctx.stroke();
```

三次贝塞尔曲线例子：

```
 ctx.beginPath();
 ctx.moveTo(75, 40);
 ctx.bezierCurveTo(75, 37, 70, 25, 50, 25);
 ctx.bezierCurveTo(20, 25, 20, 62.5, 20, 62.5);
 ctx.bezierCurveTo(20, 80, 40, 102, 75, 120);
 ctx.bezierCurveTo(110, 102, 130, 80, 130, 62.5);
 ctx.bezierCurveTo(130, 62.5, 130, 25, 100, 25);
 ctx.bezierCurveTo(85, 25, 75, 37, 75, 40);
 ctx.fill();
```









