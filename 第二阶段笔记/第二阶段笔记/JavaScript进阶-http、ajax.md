# JavaScript进阶-http、ajax

### ajax

###### 概念

- 背景：传统页面，我们访问服务器上的数据是通过表单或直接修改网页地址来实现。问题在于在数据返回之前页面是属于不可操作状态(转圈)，导致用户会花费等待时间。解决方案-ajax
- ajax(异步JavaScript 和xml)，是指在不刷新页面的情况下可以利用JavaScript发生请求以及接受响应，这样的话在等待数据接收时，用户可以继续操作页面。
- JavaScript中 要实现ajax需借助`xmlHttpRequest`对象以及其提供的方法来实现。
- ajax的作用：利用JavaScript发送请求和接受响应。

###### ajax使用的方法（XMLHTTPRequest类的实例方法）

1. `open()`:设置请求的地址以及请求的方式
2. `send()`:发送请求
3. `status`:表示返回的响应的状态。即状态码。请求发送以及接受完毕为200
4. `readyState`:表示请求的当前状态
   - `0`:表示xmlhttprequest对象被创建
   - `1`:open()已被调用
   - `2`:send方法已被调用，已经获取响应头信息
   - `3`:正在接受响应数据
   - `4`:响应数据接收完毕（通信成功时，状态值为4）
5. `onreadyStateChange`:当readyState属性发生变化时会触发。
6. `responseText`:保存了响应数据

###### ajax的使用流程

1. 新建一个xmlhttprequest对象
2. 调用open()方法
3. 指定`onreadyStateChange`事件，判断当readyState ==4 && status==200 时，说明数据接收完毕。响应数据会作为实际参数传递到该事件中.
4. 调用send方法，来发送请求
5. 会使用xmlhttprequest对象的responseText属性来获取响应数据



例如：

```
 function Ajax(type,url,success){
 	var xhr = new XMLHttpRequest();
 	 xhr.open(type,url);
 	 xhr.onreadystatechange = function(){
            if(xhr.status==200 && xhr.readyState==4){
                success(xhr.responseText);
            }
      }
      xhr.send(null);
 }
 
 Ajax('get','./data.json',success);
 function success(data){
 	console.log(data);
 	console.log(JSON.parse(data))
 }
```



###### jQuery中使用ajax

- $.ajax

  ```javascript
  $.ajax({
      url:'http://www.baidu.com',// 请求的地址
      type:'get',//请求的方式,
      data:{
          name:'admin'
      },//要发送的数据
      dataType:'json',//发送数据的格式,非必须，不写jQuery会自动匹配类型。如果接收的是json，那么会自动转为对象进行使用，省略了JSON.parse()
      success:function(res){
          //响应接收完毕时会使用的方法，数据保存在res中
      }
  });
  ```

  - 这里面data和dataType属性都是非必须。

    

- $.get

- $.post







### MockJs

##### 数据交互流程梳理

###### 前后端交互及分离

1. 前后端交互：一般web项目会分为前端和后端。
   - 前端：负责界面的实现，以及用户交互、数据渲染。并保证用户的体验
   - 后端：负责开发服务器端程序。包括数据处理以及接受请求及发送响应数据。并最终吧数据保存到数据库中。
   - 前端需要把后端返回的数据渲染在页面上



##### 本地Mockjs拦截ajax请求并生成随机数据

###### 概念：

mockjs本质上是一个第三方的模拟服务器端的工具，能够拦截前端发出的ajax请求并生成随机数据当成响应数据返回给浏览器。

###### 作用：

- 用于拦截ajax请求
- 生成随机数据充当响应

###### mockjs引入

1. 安装mockjs-一般是针对脚手架项目。
2. 在浏览器端引入Mock.js文件，即可使用.一般是针对纯前端项目或个人项目

###### mockj使用

```javascript
Mock.mock(url,type,{
    //生成随机数据并直接吧该对象作为响应数据返回给浏览器
    属性名:属性值,
    属性名:属性值
});
```

- ajax响应就接收的就是mock中传入的对象

###### mock基础语法

```javascript
1. 数字
  指定范围的随机整数：'price|20-30':1
  指定范围带小数的随机数字：'price|20-30.1-3':2  20到30之间，小数位数为1~3位的随机数字
  随机的一个整数:  'price':`@integer`
2. 字符串
  随机一个名字：   'name':'@cname'
  随机一段文字描述：'text':'cword(50)'
  随机一个邮箱：  'email':'@email'
  随机一个日期：  'birth':'@date'
  随机一个性别：  'sex|1':['男','女']
3. 随机验证码
  "imgUrl":Mock.Random.dataImage('50x50',Mock.mock({'reg':/^\w{5}$/}.reg))
4. 数组
 随机数量的数组:
  'goods|20-30':[{
      'name':'@name',
      'price|20-100':2,
      'des':'@cword(20)',
      'count|10-100':1,
      'url|1':['1.jpg','2.jpg','3.jpg']
  }]
```

- 其中@是占位符，指mockjs中已经定义好的数据模板。

###### Mockjs 处理业务请求

```javascript
Mock.mock('/login','post',function(query){
    //query是一个对象，里面包含了url、body、method三个属性。请求所提交的数据在body属性中
     //业务代码
    return 响应数据;
})
```

- mockjs会吧函数的返回值作为响应数据







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



### http

##### 基础概念

###### 网络协议概念

- 是为了实现计算机之间能够传输数据而达成的一种约定或规定。只要计算机遵守协议，那么无论计算机是哪个厂商开发的，以及不同操作系统的电脑都可以实现数据传输
- 实现网络数据传输的协议：TCP/IP 协议族
  - TCP/IP:是指以tcp和ip协议为主的用于实现网络通信的一整套网络协议的集合。

###### tcp/ip 协议族及分层(了解)

- 主要分为4层：
- 应用层：吧应用程序的数据按照指定的协议进行包装。比如发送的是邮件，采用邮件的协议进行包装-SMTP，如果发送的是文件，会用FTP(File Transfer protocol).如果是网页，就用HTTp进行包装。
- 传输层
- 网络层
- 数据链路层(网络接口层)

###### HTTP数据交互流程 *

	### 浏览器获取网络资源的流程

- 浏览器要发送请求到服务器用于请求某个资源（可能是HTML页面、css文件、js文件、图片之类的），服务器接收到请求之后经过处理，将要返回的数据包装成一个响应，最后服务器会将响应传回给浏览器。浏览器用http解析响应并渲染对应的数据在页面上。
- 浏览器一个请求只能请求一个资源。即一次只能拿到一个文件，可能是HTML、或js、或css、图片等。也有可能只是一段文字，比如判断登录。

###### 客户端：

- 在http这块，客户端就指的是浏览器。

###### 服务器

- 处理请求并发送响应的电脑。

###### http&https对比 

###### http :

hyper-text transfer protocol (超文本传输协议)

- 是运行在应用层上的一个协议。规定了两台主机的网页数据，如何传输。
- 特点：
  - 对于数据传输，http协议并没有做安全认证、不能识别接收数据的服务器身份，同时对于一些数据，是明文传输。

###### HTTPS: 

hyper-text transfer protocol over secure socket layer：建立在安全套接字上的超文本传输协议

- 安全版本的http协议。 
- HTTPS比http多了一层ssl/tsl.专门负责数据的加密和解密及身份验证。
- 传输效率不如http，但增加了安全性，同时也增加了身份认证。



##### 请求和响应

###### 请求和响应概念

- 当浏览器发送请求时，会吧请求相关的信息和要发送的数据包装成一个请求数据块发送给服务器，服务器接收请求并处理之后，也会吧要返回的数据包装成响应数据块传回给浏览器，浏览器解析数据并展示在页面上。
- 手动发送请求的两种方式
  - 通过网页地址
  - JavaScript

###### 请求

一个普通的请求包含了四个部分：请求行、请求头、空行、请求数据

 - 请求行： 由请求方法、URL和HTTP协议版本3个字段组成，它们用空格分隔。例如，GET /index.html HTTP/1.1(HTTP请求报文)。

- 请求头：包含了对数据属性的描述以及请求本身的配置信息。由关键字/值对组成，每行一对，关键字和值用英文冒号“:”分隔，请求头部通知服务器有关于客户端请求的信息。
  
  - `content-type`：请求体的数据类型
  
  - `Accept`:期望接收的数据类型
  - `User-Agent` ：浏览器端浏览器型号和版本
  - `host`:发送请求的域名
  - `content-Length`:请求体的数据字符长度，无请求体为0
  - `connection`:浏览器和服务器的连接方式：keep-alive: 长连接
  - `Cache-Control`:是否启动缓存
  - `Accept-Encoding`:支持的扩展数据类型。比如支持压缩
  
- 空行： 最后一个请求头之后是一个空行，发送回车符和换行符，通知服务器以下不再有请求头。

- 请求数据（请求体）：包含了要发送给服务器的用户数据。一般是post请求会有，get请求没有。

- 请求的方式：
  - `GET`:一般是指获取数据，不发送数据。

    get最常见的一种请求方式，当点击网页上的链接或者通过在浏览器的地址栏输入网址来浏览网页的，使用的都是GET方式。使用GET方法时，请求参数和对应的值附加在URL后面，利用一个问号（“?”）代表URL的结尾与请求参数的开始，传递参数长度受限制（一般不超过2kb）。例如，/index.html?name=pyy&age=17,这样通过GET方式传递的数据直接表示在地址中。

  - `POST`：提交数据。一般是需要提交用户数据时使用。比如登录、注册、添加数据。
    
    通过GET发送的请求，地址中”?”之后的部分就是请求数据。这种方式不适合传送私密数据。另外，由于不同的浏览器对地址的字符限制也有所不同，一般最多只能识别1024个字符，所以如果需要传送大量数据的时候，也不适合使用GET方式，所以就可以使用POST方式。因为使用POST方法可以允许客户端给服务器提供信息较多。POST方法将请求参 数封装在HTTP请求数据中，以名称/值的形式出现，可以传输大量数据，这样POST方式对传送的数据大小没有限制，而且也不会显示在URL中。
    
    - 请求包含请求体，要发送的数据就保存在请求体里
    - 大小无限制。
    - post一般会发生两次请求。第一次是发送一个请求头，当服务器接收并响应时，才发送包含数据的第二个请求到服务器。
    - 数据没有包含在地址里。
    
  - `PUT`：修改数据。

  - `Delete`：删除数据时用。

- 指定请求的方式：
  - `<form >`里有个`method`属性可以指定请求方式
  - JavaScript修改
  - 默认情况下，通过地址栏发送的请求都是get请求

**GET和POST请求总结**：

1. GET提交，请求的数据会附在URL之后，以?分割URL和传输数据，多个参数用&连接。POST提交：把提交的数据放置在是HTTP包的包体＜request-body＞中。因此，GET提交的数据会在地址栏中显示出来，而POST提交，地址栏不会改变。
2. 浏览器和服务器对URL长度有限制，因此对于GET提交时，传输数据就会受到URL长度的限制。POST请求由于不是通过URL传值，所以数据不受限。
3. POST的安全性要比GET的安全性高。



###### 响应

- 包含了状态行、响应头、响应体
  - 状态行：包含了服务器的地址，版本号，响应状态码
  - 响应头：包含了该响应的配置信息
  - 响应体：服务器要发送的数据
- 状态码：表示该请求处于什么阶段。
  - `200`:表示该请求已处理完毕，浏览器已接收完响应
  - `304`:数据未修改
  - `400`:浏览器端语法 错误
  - `401`:浏览器没有经过授权
  - `403`:请求被服务器拒绝
  - `404`:服务器没有找到该资源
  - `500`:服务器发生崩溃性错误
  - `503`:服务器临时错误。







### 扩展

原生ajax发送post请求：

和get请求不同，post请求需要设置请求头。

```
 function Ajax(type,url,success){ 
	 var xhr = new XMLHttpRequest();
 	 xhr.open(type,url);
 	 xhr.onreadystatechange = function(){
            if(xhr.status==200 && xhr.readyState==4){
                success(xhr.responseText);
            }
      }
      // 设置请求头
      xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded")
      xhr.send('name=pyy&age=17');
 }
```













