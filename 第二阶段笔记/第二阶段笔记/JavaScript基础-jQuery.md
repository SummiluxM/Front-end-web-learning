# JavaScript基础-jQuery

任务

- jQuery介绍(了解)
- jQuery对象
- jQuery选择器
- jQuery操作样式
- jQuery操作属性
- jQuery操作方法
- jQuery操作类名
- jQuery中DOM操作
- jQuery遍历
- jQuery事件方法
- jQuery链式调用(理解)
- jQuery动画
- jQuery其他常用方法



### jQuery介绍（了解）

- 背景：用JavaScript 原生 DOM 编写页面交互时，会有一些不方便的地方

  1. 内置函数或属性单词过长，不好记
  2. 获取HTML标签方式繁琐，且返回值类型不统一
  3. 设置 css时，只能是一个一个的设置，效率不高
  4. 在获取子、父、兄弟标签时，各种无脑嵌套的…，繁琐且难以理解
  5. 开发JavaScript 动画，比较繁琐

- 概念

  jQuery是一个第三方的JavaScript函数库，是一个快速、小巧、功能丰富的**js库**，本质上是一个js文件。

- 作用：

  - 用于简化 JavaScript DOM代码

- 版本

  - 目前最新是3.x ，国内用的比较多的是jQuery2.x。jQuery从2.x开始，不再支持ie8、9。
  - 如果要兼容ie8及以下 ，就用jQuery1.x

- 学习：

  -  jQuery文件中暴露了一个jQuery对象给window。
- 这个jQuery对象中封装了很多属性和方法。
  - 学习jQuery就是学习这个jQuery对象中的属性及方法。
  - 学习方法就是查看文档，包括用法及示例，提升查看文档能力。
  - 要想熟练掌握，就要理解基础上多敲+多练。

- 使用：

  - 页面通过`<script src=jQuery.js路径>`引入jQuery.js后，即可使用。

- 排错：

  在操作jQuery对象时，先控制台打印此对象是否找到



### jQuery对象

jQuery对象概念：通过jQuery方式获取标签对象，只能调用jQuery对象属性和方法。

原生对象： 通过原生方式获取的标签对象，只能调用原生属性和方法 。

两者相互转换：

```
原生对象转jQuery对象： $(原生对象)
jQuery对象转原生对象： jq对象.get(0)或者jq对象[0] //原生对象是jq对象索引为0上的值
```

**注意： **  **this是原生对象，而$(this)是jQuery对象。**

例如：

```
<div id='box1' class='red'>我是内容1</div>
<div id='box2' class='green'>我是内容2</div>
<script>
	// 获取原生对象： box1
	let box1 = document.getElementById('box1');
	console.log('原生对象', box1);
	console.log(box1.class);
	console.log(box1.attr('class')); // 报错
	// 原生对象转为jQuery对象
	let $box1 = $(box1);
	console.log(box1.attr('class'));
	
	// 获取jQuery对象： box2
	let $box2 = $('#box2');
	console.log('jQuery对象', $box2);
	console.log($box2.attr('class'));
	console.log($box2.class); // undefined 
	// jQuery对象转为原生对象
	let box2 = $box2[0];
	console.log(box2.class);
</script>
```



### jQuery选择器

选择器：选择那些需要进行操作的dom元素。

语法：

```
$('选择器')  ===  jQuery( ‘选择器’)
```

注意点：用jQuery获取的是经过处理后的`Jquery标签对象`,只能使用jQuery提供的函数，不能使用原生的dom函数,比如innerText、appendChild等都不能用。但jQuery提供了两者切换的方式。

选择器分类：

- 基本选择器
- 层级选择器
- 过滤选择器
- 表单选择器



###### 基本选择器

1. 选择指定id

   语法：

   ```
   $("#id名")；  // 注意，一定要加#  
   // 和原生的区别一下，原生的getDocumentById('')是没有#，直接是id名
   ```

   例如：

   ```
   <div id='box'>我是内容</div>
   
   // 选中元素 添加事件
   $('#box').click(function() {
   	console.log('我被点了')
   });
   // 选中元素 修改样式
   $('#box').css('background','green');
   ```

2. 选择指定class

   语法：

   ```
   $(".class名")；  // 注意要加.
   ```

   例如：

   ```
   <div class='box1'>我是内容1</div>
   
   // 选中元素 添加事件
   $('.box1').click(function() {
   	console.log('我被点了')
   });
   // 选中元素 修改样式
   $('.box1').css('background','green');
   ```

3. 选择所有的某个元素

   语法：

   ```
   $("元素名")；
   ```

   例如：

   ```
   <div>我是内容1</div>
   <div>我是内容2</div>
   <div>我是内容3</div>
   
   // 选中元素 修改样式
   $('div').css('background','green');
   ```

4. 获取多个元素

   语法：

   ```
   $("元素名,.class名,#id名,元素名,...")； // 元素之间 以逗号间隔
   ```

   例如：

   ```
   <div>我是内容1</div>
   <p id='box1'>我是内容2</p>
   <span class='box2'>我是内容3</span>
   <div>我是内容4</div>
   
   // 选中元素 修改样式
   $('div,#box1,.box2').css('background','green');
   ```

   

###### 层级选择器

和css选择器非常类似，根据某一个标签，选择它兄弟或者子孙元素。

```
<header>
	我是内容1
	<div>
		我是子元素1号div
		<p>我是子孙元素1号p</p>
		<p>我是子孙元素2号p</p>
	</div>
	<p>我是子元素1号p</p>
</header>
<p>我是内容2</p>
<span>我是内容3</span>
<div>我是内容4</div>
<div>我是内容5</div>
```



1. 获取元素的所有指定的某个后代元素

   语法：

   ```
   $('元素 后代元素');
   ```

   例子：

   ```
   // 获取所有div元素
   $('body div').css('color', 'red');
   ```

2. 获取元素指定的某个子元素

   语法：

   ```
   $('元素>子元素');
   ```

   例子：

   ```
   // 获取header下面所有p标签
   $('header>p').css('background', 'red');
   ```

3. 获取元素后面紧跟着的某个标签

   语法：

   ```
   $('元素+next元素');
   ```

   例子：

   ```
   // 获取header后面紧跟着的p标签
   $('header+p').css('background', 'red');
   ```

4. 获取元素后的所有指定的某个兄弟元素

   语法：

   ```
   $('元素～元素');
   ```

   例子：

   ```
   // 获取header后面所有兄弟div标签
   $('header～div').css('background', 'red');
   ```

   

###### 过滤选择器

```
<ul>
  <li>第1个li</li>
  <li>第2个li</li>
  <li id='third'>第3个li</li>
  <li>第4个li</li>
  <li>第5个li</li>
  <li>第6个li</li>
</ul>
```



1. 匹配第一个元素

   语法：

   ```
   $('元素:first');
   ```

2. 匹配最后一个元素

   语法：

   ```
   $('元素:last');
   ```

3. 匹配索引是偶数的元素

   语法：

   ```
   $('元素:even');
   ```

4. 匹配索引是奇数的元素

   语法：

   ```
   $('元素:odd');
   ```

5. 匹配索引等于index的元素

   语法：

   ```
   $('元素:eq(index)');
   ```

6. 匹配索引大于index的元素

   语法：

   ```
   $('元素:gt(index)');
   ```

7. 匹配索引小于index的元素

   语法：

   ```
   $('元素:lt(index)');
   ```

8. 集合中去掉某些元素

   语法：

   ```
   $('元素:not()');
   ```

   例如：

   ```
   // 去除li中第一个，得到剩余的
   $('li:not(:first)').css('color', 'green');
   
   // 去除li中id为third的，得到剩余的
   $('li:not(.third)').css('color', 'green');
   ```





### jQuery操作样式

语法：

```
读取样式： jq对象.css('样式名'); // 一次只能读取一个样式
设置样式： 
		单个样式设置： jq对象.css('样式名', '值')
		多个对象样式： jq对象.css({ 
                          '样式名' : '值',
                          '样式名' : '值'
                       })
```



### jQuery操作属性

###### 标准属性

语法：

```
读取标准属性： jq对象.prop('属性名');
设置标准属性： 
		单个样式设置：jq对象.prop('属性名', '值')
		多个对象样式：jq对象.prop({ 
                	'属性名' : '值',
                	'属性名' : '值'
              	})
```



###### 自定义属性

语法：

```
读取自定义属性： jq对象.attr('属性名');
设置自定义属性： 
		单个样式设置：jq对象.attr('属性名', '值')
		多个对象样式：jq对象.attr({ 
                	'属性名' : '值',
                	'属性名' : '值'
              	})
```

例如：

```
<div id='box' class='test' _id='test'></div>

<script src="./jquery.js"></script>
<script>
console.log( $('#box').prop('class') );//获取标准属性
console.log( $('#box').prop('_id') );//不能获取自定义属性

console.log($('#box').attr('class'));//获取标准属性
console.log($('#box').attr('_id'));//获取自定义属性
</script>
```

两者的区别：

  	1. attr用来设置和获取自定义属性
          	2. prop获取和设置标签的原生属性（w3c中定义的属性）



### jQuery操作类名

- 添加类名： addClass()
- 删除指定类名： removeClass(类名)
- 删除所有类名： removeClass()
- 是否含有某类名： hasClass()



###### addClass()

语法：

```
jq对象.addClass('类名')
```



###### removeClass()

语法：

```
jq对象.removeClass('类名'); // 删除指定类名
jq对象.removeClass(); // 删除所有类名
```



例如：

```
 <p class="green">第1个</p>
 <p>第2个</p>
 <p>第3个</p>
 <p>第4个</p>
 <p>第5个</p>
 
 <script src="./jquery.js"></script>
 <script>
 	// 点击所有的p标签，如果是green的类名就删除，否则就添加green类名
 	$('p').click(function() {
 		// 获取当前p标签的class
 		let pClass = $(this).prop('class');
 		console.log(pClass);
 		if(pClass === 'green') {
 			// 如果是green的类名就删除green类名
 			$(this).removeClass('green')
 		} else {
 			// 没有就添加green类名
 			$(this).addClass('green')
 		}
 	})
 </script>
```



###### hasClass()

语法：

```
jq对象.hasClass('类名');
```

例如：

```
 <p class="green red">第1个</p>
 <p>第2个</p>
 <p>第3个</p>
 <p>第4个</p>
 <p>第5个</p>
 
 <script src="./jquery.js"></script>
 <script>
 	// 点击所有的p标签，如果有green的类名就删除，否则就添加green类名
 	$('p').click(function() {
 		// 当前点击的p标签中是否含有类名green
 		let isGreen = $(this).hasClass('green')
 		if(isGreen) {
 			// 如果有green的类名就删除green类名
 			$(this).removeClass('green')
 		} else {
 			// 没有就添加green类名
 			$(this).addClass('green')
 		}
 	})
 </script>
```





### jQuery中DOM操作

###### 查找dom

使用选择器就可以非常快速地完成各种查找。

例如：

```
// 查找id为box的容器的文本内容
$('#box').text();
// 查找id为box的容器的class属性值
$('#box').prop('class')
```

练习：查找id为box下面的span，返回class属性值。



###### 创建节点

语法：

```
 $('html代码') 
```

例如：

```
$('<p id="p1">我是新增加的p</p>')
```



###### 新增节点

1. 在末尾新增节点(最主要的)

   - append()

   - appendTo()

2. 在首位新增节点
   - prepend()
   - prependTo()
3. 指定的节点之后追加
   - after()
   - insertAfter()
4. 指定的节点之前追加
   - before()
   - insertBefore()

例如：

```
<div id='box'>
	<p>p1</p>
	<p>p2</p>
	<p id='third'>p3</p>
	<p>p4</p>
</div>

// 在div中，增加一个p节点
// 1. 创建一个p节点
 let $p = $('<p>新建的p</p>')
 // 2. 增加节点
 $('#box').append($p)// 在box中增加p节点
 $p.appendTo('#box') // 把p节点追加到box中
 
 // 指定的节点之前追加
 $('#third').before($p);
 $p.insertBefore('#third'); // 两种方式完全一样
```



###### 删除节点

- 删除自己： jq对象.remove()
- 删除所有子节点： jq对象.empty()



###### 复制节点

语法：

```
jq对象.clone(true); // 复制节点的同时也复制行为
jq对象.clone(); // 复制节点 但不复制行为
```



###### 筛选节点

1. next()

   next()用于获取后面第一个兄弟节点

2. nextAll()

   nextAll()用于获取后面所有的兄弟节点

3. prev()

   prev()用于获取前面第一个兄弟节点

4. prevAll()

   prevAll()用于获取前面全部兄弟节点

5. siblings()

   siblings()用于获取前后的兄弟的节点

6. children()

   children()用于获取子节点

   语法：

   ```
   jQuery对象名.children('选择器1,选择器2,... ') // 获取所有指定的子节点
   jQuery对象名.children() // 获取所有子节点
   ```

7. find()

   find()是根据css选择器来获取后代标签

   语法：

   ```
   jQuery对象名.find("css选择器");
   ```

8. parent()

   parent()用于获取父元素

9. parents()

   parents()是通过css选择器找到祖先元素。

   语法：

   ```
   jquery对象名.parents(‘父元素选择器’);
   // 例如
   $button.parents('tr');
   ```





### jQuery遍历

###### first()

first()是获取jQuery对象的第一个数据



###### last()

last()是获取jQuery对象的最后一个数据



###### eq()

eq()是获取jQuery对象的指定下标的数据，**下标以0开始**



###### each()

语法:

```
jQuery对象/数组.each(function ( index, elem ){ 
		// elem是索引对应的原生对象
		let $elem = $(elem);//将原生的HTML标签转为jQuery对象
		console.log(index); // 索引
		console.log($elem); // 索引对应的jQuery对象
})
```

注意： each方法中获取的是原生的JavaScript dom对象

例如：

```
<a href="#">第一个a标签</a>
<a href="#">第二个a标签</a>
<a href="#">第三个a标签</a>
<a href="#">第四个a标签</a>
<a href="#">第五个a标签</a>
<a href="#">第六个a标签</a>

let $a = $('a');
console.log($a.first());//第一个a标签
console.log($a.last());//第六个a标签
console.log($a.eq(3));//第四个a标签
// 遍历 each 
$a.each(function(index,elem){
   var $elem = $(elem);//将原生的HTML标签转为jQuery对象
   console.log($elem,index);
});
// 利用for循环完成jQuery对象的遍历
for(var i=0;i<$a.size();i++){
    $a.eq(i);获取第i个数据 类似于$a[i]
}
```





### jQuery事件方法

###### click()

click()是节点的点击事件

语法：

```
jquery对象.click(函数参数);
```

例如：

```
$("button").click(function(e){
    //点击发生时会执行的代码
    一样可以使用event对象，jQuery对它没有任何处理，直接使用即可
    e.clientX,e.clientY
});
```

注意：其他事件都是同理，比如mousemove、keyup、focus、blur等。



###### hover()

语法：

```
jquery对象名.hover(function(){
    鼠标进入标签时会触发
},function(){
    鼠标离开标签时触发
});
```



###### on()

注意： 对于用js动态添加的标签，那么jQuery之前设置的事件代码是无效的。解决方法—on。

on：可以给后代标签设置任意一个事件，对现有标签或动态添加的标签都有效果。

语法：

```
jQuery对象名(父标签).on("事件名","后代标签css选择器",function(){
    事件触发要执行的代码
})；
例如：给所有div设置点击事件，包括动态添加的div，提示ok
$('body').on('click','div',function(e){
             alert('ok');
});
```





### JQuery链式调用

概念：如果对同一个jQuery对象有多个操作，那么jQuery提供了更快捷 的使用方式即链式调用：

语法：

```
jquery对象a.方法1().方法2().方法3().方法n();
```

扩展：

- 方法总是作用左边最近的对象上
- 假设对象a调用方法1,没有产生新的对象. 所以方法2应该作用在a对象上
- 假设a对象调用方法2,产生了**新对象b. 所以方法3应该作用在b对象上**





### JQuery动画

- slideDown:标签带有下拉效果
- slideUp：标签带有上拉效果
- fadeIn：标签带有淡入效果
- fadeOut：标签带有淡出效果
- animate：自定义动画函数

例子：

```
// 以毫秒为单位
jQuery对象名.slideUp(动画持续时间)     以滑动方式隐藏被选元素。
jQuery对象名.slideDown(动画持续时间)   以滑动方式显示隐藏的元素,适用于通过jq隐藏的元素，或在设置为 display:none 的元素

jQuery对象名.fadeIn(动画持续时间)      淡入可见元素
jQuery对象名.fadeOut(动画持续时间)     淡出可见元素



// 自定义动画
jQuery对象名.animate({ // animate一般用于实现移动、2d转换、透明度等动画
    需要动画的css属性属性
},动画持续时间);以毫秒为单位

例子：div向右移动200px，同时opacity为0，持续5s
$('div').animate({
    "margin-left":"200px",
    'opacity':'0'
},2000);
```





### jQuery其他常用方法

注意：要点：没有参数就是获取，有实参就是设置



###### html()

html()设置某标签的内部HTML代码，作用类似于原生的innerHTML。

语法：

```
获取：jquery对象.html()
设置：jquery对象.html(新内容)
```



###### text()

text()类似于innerText

语法：

```
获取：jquery对象.text()
设置：jquery对象.text(新内容)
```



###### val()

val()类似于value



###### removeAttr()

removeAttr()用于删除某个HTML属性

语法：

```
jquery对象.removeAttr("属性名");
```



###### hide()

hide()用于隐藏该jQuery元素

语法：

```
jquery对象.hide();//自己隐藏
```



###### show()

show()用于显示该jQuery元素

语法：

```
jquery对象.show();//显示自己
```





### 扩展

###### 删除节点

删除自身，有两种方法， jq对象.remove()和jq对象.detach()。

- 这两种方法都会返回被删除的节点。

- remove()方法删除元素时候，不保留行为，也就是事件。

- detach()方法删除元素时候，会保留行为。