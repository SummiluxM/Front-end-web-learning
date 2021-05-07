# JavaScript进阶-面向对象

任务

- 面对对象的概念
- 面向对象(ES5)
- 对象的操作
- 原型
- 原型链
- this
- 面向对象(ES6)
- 面对对象的三大特性



### 面对对象的概念

###### 面向过程和面向对象

**面向过程**就是分析出解决问题所需要的步骤，然后用函数把这些的步骤一步一步实现，使用的时候一个一个依次调用。

例如打电话：第一步打开手机，第二步输入号码，第三步拨打号码，...。

**面向对象**是把构成问题事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为。

例如造车，我们分析发现车由发动机、骨架、车壳、轮胎、玻璃、座椅、...等等组成，那么我们把这些组成都分解成对象，每个对象由对应的商家去完成极大提高效率。面向对象就可以帮助我们从宏观上把握、从整体上分析整个系统。

也就是说，面向过程是定一个目标，分步骤解决。第一步第二步第三步...。面向对象是把这个目标拆解成不同的小目标，每个目标都是一个对象，每个对象有自己的功能。



###### 面向对象的核心概念

- 类
  - 对具有相同属性和行为的这一类事物的统称。比如，人、汽车、鸟等
- 对象(实例)
  - 类的具体的表现，有具体的属性和行为。比如隔壁的老何，隔壁老王的奔驰车、隔壁老黄的啄木鸟。
- 类和对象之间的关系
  - 类是对象的模板(设计图),对象是类的具体表现(实例)
- 属性和行为
  - 属性：是指类的外在的特征。每个类都有不同的属性。比如人具有姓名、年龄、体重等属性。车这个类具有颜色、型号、车牌号等属性。
    - **属于同一个类的对象具有相同的属性，但属性值不一样**。比如说老王和老黄都是人这个类的对象，都具有姓名、年龄、体重等属性，但他们之间的属性值是不一样的。
  - 行为(方法)：是指对类的一个动作的描述，每个类都具有不同的行为。比如人这个类可以思考、点头、上学、工作等。车这个类具有加速、漂移等行为。
    - **属于同一个类的对象具有相同的行为**



### 面向对象(ES6)

概念：ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过`class`关键字，可以定义类。基本上，ES6 的`class`可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

###### 类和对象的创建(类的实例化)

语法：

```
// 定义类
class 类名{
    //该类的属性和行为
}
// 创建对象
let 对象名 = new 类名();
```



###### 实例属性和行为

如何在类里面添加属性和行为(方法)呢？

添加属性和行为：

```
class Person{
    constructor(){
        //在这里添加属性和行为
        this.属性名1 = 属性值1;
        this.属性名2 = 属性值2;
        //添加行为
        this.属性名3 = function(){
            //该行为要做的事情，即要执行的代码
        }
        this.属性名4 = function(){
            //该行为要做的事情，即要执行的代码
        }
    }
}
// 行为其实本质上在类中就是一个属性，只不过它的值是一个函数，行为只是人为赋予该属性的意义。
// 上面代码定义了一个“Person类”，可以看到里面有一个constructor()方法，这就是构造方法，而this关键字则代表实例对象。
```

通过对象使用属性和行为：

```
let 对象名 = new 类名();
对象名.属性名
对象名.属性名();//使用行为
```

例如：

```
class People{
    constructor(){
        this.name ='张三';
        this.age = 12;
        this.weight = '50kg';
        this.say =function(){
            console.log('张三在吃饭');
        }
    }
}
// 创建对象
var p1 = new People();
console.log(p1.name);
console.log(p1.age);
console.log(p1.weight);
p1.eat();//使用行为，即调用了一次函数
console.log(p1);
```

练习：

```
1. 定义一个学生类，有学号、姓名、年龄、性别等属性，有上学、做作业等行为。创建一个对象并输出以上属性
2. 定义一个商品类，有名称、价格、数量、描述等属性，有加入购物车、立即购买等行为。定义商品对象并输出属性
思考：1. 多创建几个对象，并输出每个对象的属性，有什么缺陷？    构造函数
思考，2. 如果我想在行为里面使用其他属性，怎么办？       this
```

```
// 1.
	class Student{
          constructor(){
              this.snum = '003';
              this.name = "zs";
              this.age = 23;
              this.sex = "男";
              this.goSchool = function(){
                  console.log(`${this.name}去上学了`);
              }
              this.doWork = function(){
                  console.log(`${this.name}在做作业`);
              }
              //输出所有非函数属性
              this.show = function(){
                  console.log(`学号：${this.snum}, 姓名: ${this.name},年龄：${this.age},性别：${this.sex}`);
              }
          
      }
      let s1 = new Student();
      let s2 = new Student();
      s1.show();
      s1.goSchool();
      s1.doWork();
      s2.show();
      s2.goSchool();
      s2.doWork();
```

```
	 class Student{
          constructor(snum,name,age,sex){
              this.snum = snum;
              this.name = name;
              this.age = age;
              this.sex = sex;
              this.goSchool = function(){
                  console.log(`${this.name}去上学了`);
              }
              this.doWork = function(){
                  console.log(`${this.name}在做作业`);
              }
              //输出所有非函数属性
              this.show = function(){
                  console.log(`学号：${this.snum}, 姓名: ${this.name},年龄：${this.age},性别：${this.sex}`);
              }
          }
      }
      //使用构造函数
      var p1 = new Student('003','zs',23,"男");
      var p2 = new Student('004','zrr',18,"男男");
      p1.show();
      p2.show();
```





###### constructor()

- constructor()构造函数是每一个类都必须要有的一个`特殊函数`.主要用来完成新建对象的属性和行为的初始化，即给新建的对象添加属性和行为。

- 作用：

  - 完成新建对象的初始化

- 特点：

  - 如果说定义了一个类确没有定义`constructor`,那么系统会自动添加一个默认的空的构造函数
  - 开发人员可以在构造函数里定义属性和行为

- 使用

  构造函数只能是**新建对象**时由JavaScript自动调用，不能手动调用

  ```
  let 对象名 = new 类名();
  // 在新建对象时，JavaScript会自动调用一次构造函数
  ```

- 无参构造和有参构造

  - 无参构造：是指constructor里没有任何参数

  - 有参构造

    - 在constructor里定义参数。这个可以理解为函数的的形式参数。而构造函数里参数的值在新建对象时传递过去。

      ```
      class People{
          constructor(参数1,参数2,参数N){
              this.属性名1 = 参数1;
              this.属性名2 = 参数2;
              this.属性名n = 参数n;
          }
      }
      创建对象：
      let p1 = new People(数据1,数据2,数据n);
      ```

      JavaScript会将数据传入到顺序对应的参数里。以上的例子中，会将`数据1`放入到构造函数的`参数1`中，`数据2`放入到构造函数中的`参数2`,数据n放入构造函数里的`参数n`,这样，就可以实现，新建不同对象时，可以有不同的属性值。

总结：

1. 通过class 关键字创建类, 类名定义首字母大写
2. 类里面有个constructor 函数,可以接受传递过来的参数,同时返回实例对象（this指向的是new出来的实例对象）。
3. constructor 函数 只要 new 生成实例时,就会自动调用这个函数, 如果我们不写这个函数,类也会自动生成这个函数
4. 生成实例 new 不能省略





###### 类属性和行为

背景：实例属性和行为是每个对象都有的，即对象私享。但有时候我们需要对象共享一个属性。共享属性是指大家用的都是同一个。而面向对象中的共享属性和行为有个别称，即类属性和行为。

概念:类属性和行为是面向对象中的共享属性和行为。即整个类只有一个，并不是对象私享。

定义和使用：

```
class 类名{
    //定义类属性
    static 类属性名 = 类属性值;
    constructor(){}
    //定义类方法
    static 类方法名(){
        //类方法的代码
    }
}
// 使用： 
类名.类属性名来使用
类名.类方法名();
// 注意：普通对象无法直接使用类属性
```

注意： static 是用于修饰类属性的关键字。即表示是个类属性。可以定义多个类属性，

**类方法跟实例方法的区别**：

- 语法上：类方法是通过`static`在构造函数外定义的，而实例方法是在构造函数里通过`this`来定义的
- 使用上:
  - 类方法通过类名来使用
  - 实例方法通过对象名来调用

例子：火车售票，定义一个类，完成火车售票。可以同时多个窗口进行售票。票数一共50张。

```
// 火车售票，定义一个类，完成火车售票。可以同时多个窗口进行售票。票数一共50张。
        class Station{
            static tickets = 50;//定义了一个类属性
            constructor(){
               // this.tickets = 50;//剩余的票数
                //售票
                this.sale = function (){
                    if(Station.tickets >0){
                        Station.tickets--;
                        console.log(`购票成功,剩余${Station.tickets}张票`);
                    }else{
                        console.log('票已售完');
                    }
                    // 在实例方法中也可以使用类方法
                    Station.demo();
                }  
            }
            static demo(){
                console.log('类方法');
            }
        }
        //每个对象都是一个窗口
        var s1 = new Station();
        var s2 = new Station();
        var s3 = new Station();
        // s1.sale();
        // 调用类方法
        Station.demo();
        var timer =   setInterval(() => {
            if(Station.tickets>0){
                s1.sale();
                s2.sale();
                s3.sale();
            }else{
                clearInterval(timer);
            }
        }, 1000);
```

练习：模拟抽奖系统， 有3个窗口可以抽奖，一共20个奖，每次抽奖有30%抽中，利用面向对象来模拟抽奖过程。

```
class Prize{
     static count = 20;//剩余的奖项
     constructor(name){
       //窗口名称
       this.name = name;
       this.draw = function(){
         if(Math.random()<0.3&& Prize.count>0){
           Prize.count--;
           console.log(`恭喜${this.name}窗口的参与者中奖，目前奖池还有${Prize.count}个奖项`)
         }else if(Prize.count>0) {
           console.log('未能中奖,再接再厉');
         }else{
           console.log('没有奖了，请提醒管理员充奖');
         }
       }
     }
   }
   var p1 = new Prize("一号");
   var p2 = new Prize("二号");
   var p3 = new Prize("三号");
 var timer =   setInterval(() => {
     if(Prize.count>0){
      p1.draw();
     p2.draw();
     p3.draw();
     }else{
       clearInterval(timer);
     }
   }, 1000);
```





###### 面向对象中类和类之间的相互调用

一般会在某一个**类的方法里面**定义参数来接受其他类的**对象**来进行操作。

```
class A{
    constructor(){
        //该方法需要接受B类的一个对象和C类的一个对象
        this.show = function(b,c){
            
        }
    }
}
class B{
    constructor(){
        this.name="B";
    }
}
class C{
    constructor(){
        this.name="C";
        this.show = function(a){
            
        }
    }
}
var b1 = new B();
var c1 = new C();
var a = new A();
a.show(b1,c1);类A里面使用类B和类C的对象
c1.show(a)
```

例如：

龟兔赛跑：

```
	var end = 100;//总路程100米
      // 乌龟
      class Tortoise {
        constructor(speed) {
          this.speed = speed;
          this.distance = 0;
          this.climb = function () {
            this.distance += speed;
            console.log(
              `乌龟又爬了${this.speed}米，当前路程为${this.distance}`
            );
          };
        }
      }
      // 乌龟
      class Rabbit {
        constructor(speed) {
          this.speed = speed;
          this.distance = 0;
          this.jump = function () {
            if (Math.random() < 0.3) {
              this.distance += speed;
              console.log(
                `兔子又跳了${this.speed}米，当前路程为${this.distance}`
              );
            } else {
              console.log(`兔子在打盹，睡觉，当前路程为${this.distance}`);
            }
          };
        }
      }
      //游戏类
      class Game{
          constructor(){
              this.game = function(rabbit,tortoise){
                  // 判断是否赢了 
                 var timer = setInterval(() => {
                     rabbit.jump();
                     tortoise.climb();
                    if(rabbit.distance>=end || tortoise.distance >=end){
                      //游戏结束,暂停定时器
                      clearInterval(timer);
                      //兔子赢了
                      if(rabbit.distance>=end &&tortoise.distance >=end){
                          console.log('游戏结束，平局');
                      }else if(rabbit.distance > tortoise.distance){
                          console.log('游戏结束，兔子赢了');
                      }else{
                        console.log('游戏结束，乌龟赢了');
                      }
                  }
                 }, 1000);
              }
          }
        }

      // 测试
        var t = new Tortoise(2);
        var r = new Rabbit(5);
        var g = new Game();
        g.game(r,t);
```



###### 面向对象解题的大致思路：

1. 分析有几个模块(类)，模块内有几个属性和方法
2. 分析方法是否需要其他类的对象
3. 创建对象，调用对象的方法来完成程序。



###### 面向对象的完整语法（ES6）

```
class 类名{
    static 类属性名 = 值;
    constructor(){
        this.实例属性名= 属性值;
        // es5实例方法语法
        this.方法名= function(){
            
        }
    }
   //es6  实例方法语法 推荐
   实例方法名(){
       
   }
   static 类方法名(){
       
   }
}
```



###### 实例属性的新写法

实例属性除了定义在`constructor()`方法里面的`this`上面，也可以定义在类的最顶层。

```
class A{
	 constructor(){
	 	this._x = 1;
	 }
}
// 上面代码中，实例属性this._x定义在constructor()方法里面。另一种写法是，这个属性也可以定义在类的最顶层，其他都不变。
```

```
class A{
	  _x = 1;
	 increment() {
        this._x++;
      }
}
// 上面代码中，实例属性_x与increment()方法，处于同一个层级。这时，不需要在实例属性前面加上this
// 这种新写法的好处是，所有实例对象自身的属性都定义在类的头部，看上去比较整齐，一眼就能看出这个类有哪些实例属性。
```

```
class A {
  x = 1;
  y = 2;

  constructor() {
    // ...
  }
}
// 一眼就能看出，A类有两个实例属性，一目了然,写起来也比较简洁。
```









### 面向对象(ES5)

概念：es5没有专门面向对象的相关语法，但是对象这个概念时一直存在，所以在es6之前的版本，会利用JavaScript自带的特性来模拟面向对象

包含的知识

- 函数
- 原型&原型链（继承）
- call、bind、apply(继承)



###### 创建内置对象

```
let obj = new Object();
obj.name = ’王二麻子’;
obj.age = 17;
```



###### 字面量方式创建自定义对象

例如：

```
let obj = {name:’王二麻子’, age:17, sex: 'man'}; // 对象的格式： { key: value }
```



###### 工厂方式创建自定义对象

**工厂方式是采用函数来封装创建对象的逻辑和细节。**

例如：

```
// 定义一个函数，接受三个参数，这三个包含对象的信息
function person(name,age,sex) {
	let obj = new Object();
	obj.name= name;
	obj.age=age;	
	obj.sex=sex;
	obj.sayName = function() {
		console.log(this.name)
	}
	return obj
}
// 每次调用都会返回包含3个属性和1个方法的对象
let person1 = person('张三',17,'男')；
let person2 = person('李四',18,'女')；
let person3 = person('王二麻子',19,'男')；
console.log(person1)
console.log(person2)
console.log(person3)
```

但是，虽然解决了创建对象时对象相似的问题，但是这只是一个Object类型，而不是一个Person。



###### 构造函数方式创建自定义对象(精通)

在 JavaScript 中，构造器其实就是一个普通的函数。当使用 `new`操作符来作用这个函数时，它就可以被称为构造方法（构造函数）。

js原生中包含了一批构造函数，如Array、Object，我们也可以自定义构造函数，构造函数方式可以在类型实例创建时，同步设置一些必备属性和方法。

例如：

```
function Person(name,age,sex) {
	this.name= name;
	this.age=age;	
	this.sex=sex;
	this.sayName = function() {
		console.log('大家好，我系'+this.name)
	}
}
// 每次调用都会返回包含3个属性和1个方法的对象
let person1 = new Person('张三',17,'男')；
let person2 = new Person('李四',18,'女')；
let person3 = new Person('王二麻子',19,'男')；
console.log(person1.name)
console.log(person2.age)
console.log(person3.sex)
console.log(window.sex)
```

注意：person1、person2、person3都分别保存着Person这个类的不同实例。这三个对象都有一个constructor属性，这个属性指向Person。

```
console.log(person1.constructor === Person) // true
console.log(person2.constructor === Person) // true
console.log(person3.constructor === Person) // true

// 属性constructor(构造函数)来标识类型
console.log(person1 instanceof Person) // true
console.log(person1 instanceof Object) // true
console.log(person2 instanceof Person) // true
console.log(person2 instanceof Object) // true
console.log(person3 instanceof Person) // true
console.log(person3 instanceof Object) // true
```



构造函数和工厂方式的不同：

- 构造函数的函数名**首字母大写**(定义类的标准语法，使用大驼峰命名)
- 构造函数没有显示创建对象
- 属性和方法都赋值给了this
- 没有写return语句，但是最终会返回新实例

构造函数也是一个**函数**，this默认指向window对象。新属性要赋给新实例对象，使用new关键字。

了解扩展： new关键字创建对象的步骤：

1. 首先创建一个空对象obj。
2. 将构造函数的作用域赋给新对象（将this指向新创建的对象obj）
3. 执行构造函数中的函数，为这个对象添加属性
4. 返回新对象



### 对象的操作

###### 创建属性

- 对象.属性名=属性值  // 如果没有这个属性 就会添加这个属性  如果有这个属性 就会修改这个属性值
- 对象[属性名]=属性值  // 方括号运算符 需要注意  里面如果不加引号，那么就会被当成变量



###### 访问属性

- 对象.属性名  // 如果访问的属性名不存在 则返回undefined     它只会当成对象的属性名，而不会去读取成变量

  ```
  let obj = {
  	name: 'pyy'
  }
  let a = 'name';
  
  obj.a   // undefined  因为 它会把a当成一个属性名
  obj[a] //  才会把a当成变量
  obj[name] //  会报错  因为会去找name这个变量，找不到，就会报错
  obj['name'] // ‘pyy’
  ```

  

- 对象[属性名]  // 方括号运算符 需要注意  里面如果不加引号，那么就会被当成变量



###### 修改属性

- 对象.属性名=新的属性值
- 对象[属性名]=新的属性值



###### 删除属性（了解）

delete 对象.属性名



遍历对象

for ...in

for...in是为遍历对象属性而构建的。

语法：

```
for(let key in obj) {
	console.log(key); .// 属性
	console.log(obj.key) // undefined
	console.log(obj[key])// 访问属性值
}
```



###### Object.keys()

获取所有的键， 返回一个数组，数组中存放所有的键名

```
let arr = Object.keys(obj);
arr.forEach(item => {
	item    // 对象的key
	obj[item] // 对象的属性值
});
```



### 原型

使用构造函数方式创建自定义对象的例子

```
function Person(name,age,sex) {
	this.name= name;
	this.age=age;	
	this.sex=sex;
	this.sayName = function() {
		console.log('大家好，我系'+this.name)
	};
	this.sayAge = function() {
		console.log(`我${sayAge}岁,我好累`)
	};
}
```

分析： 每一个类型都拥有共同的特性，要是每一个实例自动拥有就好了。prototype就闪亮登场。



###### prototype(重要)

js中所有的函数类型的对象都有一个prototype属性，prototype自身又是一个对象，因此我们可以给prototype对象添加属性和方法。

也就是说，每个函数都有一个prototype属性，他指向的是一个对象，这个对象的用途是包含所有实例共享的属性和方法。

```
// 定义一个构造器
function Person(name,age,sex) {
}
// 注意： 在js中，函数本身也是一个包含了方法和属性的对象
console.log(Person.length);// => 3      函数的形参个数
console.log(Person.constructor) // =>    ƒ Function()  构造函数
console.log(Person.prototype) //         原型
console.log(Person.prototype instanceof Object) // true   原型的类型
```



###### 原型操作

访问某函数的原型对象：

```
函数名.prototype
```

给原型添加属性和行为(所有该类对象共享的属性和行为)：

```
// 添加属性和行为:
函数名.prototype.属性名= 数据;
函数名.prototype.方法名= function(){}
// 使用： 
对象名.属性名
对象名.方法名();
```

例如：

```
function Fn(){}
console.log( Fn.prototype ); // JavaScript 中的函数永远有一个默认原型属性。

// 给函数的原型对象添加新属性
Fn.prototype.name = "pyy";
console.log( Fn.prototype );

Fn.age = 17;
let fnObj = new Fn();
console.log(fnObj);
console.log(fnObj.age);
console.log(fnObj.name);


```

当创建这个类的实例对象时，原型对象的所有属性和方法都被立即赋予到要创建的对象当中。



###### `__proto__`

每个实例对象（ object ）都有一个私有属性 `__proto__ `,这个属性指向它的构造函数的原型对象（**prototype** ）。

也就是说

```
// 定义一个构造器
function Person(name,age,sex){
}

let person = new Person('zs',18,'男'); // new一个实例对象
console.log(person.__proto__ === Person.prototype); //true
```

完整的描述：每个实例对象（ object ）都有一个私有属性（称之为 `__proto__ `）指向它的构造函数的原型对象（**prototype** ）。该原型对象也有一个自己的原型对象( `__proto__ `) ，层层向上直到一个对象的原型对象为 `null`。根据定义，`null` 没有原型，并作为这个**原型链**中的最后一个环节。



### 原型链

如果说对象自身有一个和原型同名的属性或方法时，会优先使用对象自身的属性或方法。也就是说，访问对象的某个属性或方法时，先在对象本身去找是否有对应的属性和行为，如果有则直接使用。如果没有，则去原型里查找，如果有则使用，如果没有，`则返回undefined-原型链`。

- 本意上是指由原型构成的链条。
- 作用：定义了对象访问属性的顺序
- 流程：
  - 对象在访问某个属性时，会先在本对象里找，如果没有找到，则去对应的原型里找，找到了直接使用，如果还没找到，如果原型对象上还有原型，那么会继续往上一层原型对象中查找，直到原型对象为Object类为止，如果到达Object类对象还没找到，则返回undefined。(对象>构造函数>原型)
  - 所有 JavaScript 中的对象都是位于原型链顶端的 `object` 的实例。

例子：

```
// 让我们从一个函数里创建一个对象o，它自身拥有属性a和b的：
function F() {
   this.a = 1;
   this.b = 2;
}
let o = new F(); // {a: 1, b: 2}

// 在f函数的原型上定义属性
F.prototype.b = 3;
F.prototype.c = 4;

// 不要在 f 函数的原型上直接定义 f.prototype = {b:3,c:4};这样会直接打破原型链
// o.__proto__ === f.prototype
// o.__proto__ 有属性 b 和 c
// o.__proto__.__proto__ 是 Object.prototype.
//  默认情况下，任何函数的原型属性 __proto__ 都是 window.Object.prototype.
// 最后o.__proto__.__proto__.__proto__是null
// 这就是原型链的末尾，即 null，
// 根据定义，null 就是没有__proto__。

// 综上，整个原型链如下: 

// {a:1, b:2} ---> {b:3, c:4} ---> Object.prototype---> null

console.log(o.a); // 1
// a是o的自身属性吗？是的，该属性的值为 1

console.log(o.b); // 2
// b是o的自身属性吗？是的，该属性的值为 2
// 原型上也有一个'b'属性，但是它不会被访问到。
// 这种情况被称为"属性遮蔽"

console.log(o.c); // 4
// c是o的自身属性吗？不是，那看看它的原型上有没有
// c是o.__proto__的属性吗？是的，该属性的值为 4

console.log(o.d); // undefined
// d 是 o 的自身属性吗？不是，那看看它的原型上有没有
// d 是 o.__proto__ 的属性吗？不是，那看看它的原型上有没有
// o.__proto__.__proto__上有吗？ 没有 
// o.__proto__.__proto__.__proto__ 为 null，停止搜索
// 找不到 d 属性，返回 undefined
```









### this

###### 全局this

全局this是指：this指向全局对象(浏览器中的全局对象是 window).

注意：**声明变量时只有是使用var关键字的才是全局变量**。

```
// 全局作用域
console.log(this === window); // true
this.name='pyy'
console.log(window.a); // pyy
console.log(a); // pyy
```



###### 函数this

一般函数都是由window调用，this就是指向window对象。记住一句话： **谁调用，this就指向谁。**

```
function fn() {
	this.name = 'pyy';
	return this;
}
fn();
console.log(name); // name已经成为了全局变量了
console.log(fn() === window); // true
```



###### 对象方法的this

对象方法由对象调用，因此this就指向这个对象。

```
let name = 'zs'
let obj = {
	name: 'pyy',
	age: 17,
	say: function() {
		return `我叫${this.name}我今年${this.age}岁`
	}
}
console.log(obj.say())
```



###### 构造函数中的this

构造函数中的this默认指向新创建的对象。

```
function Person(name,age,sex) {
	this.name= name;
	this.age=age;	
	this.sex=sex;
	this.sayName = function() {
		console.log('大家好，我系'+this.name)
	}
}
let person = new Person('渣渣辉',17,'男');
```



###### call、apply、bind

这三种都是用来改变this的指向，但是用法有所不同。

1. call、apply

   语法：

   ```
   f.call(新的this指向,参数1,参数2,参数2,...)
   f.apply(新的this指向,[参数1,参数2,参数2,...])
   // 两者的唯一区别就是参数，call是直接书写，以逗号间隔，apply是一个数组包裹
   ```

   注意：apply,call会立即执行一次。

   例如：

   ```
   var a = 1; // 注意： 使用了var声明的才是全局变量
   var b = 2;
   let fn = function (c,d) {
   	return this.a + this.b + c + d
   }
   
   console.log(fn(3,4))
   let obj = { a: 100, b: 200 };
   console.log(fn.call(obj,300, 400))
   console.log(fn.apply(obj,[300, 400]))
   ```

2. bind

   语法：

   ```
   f.bind(新的this指向,参数1,参数2,参数2,...)
   ```

   `f.bind()`会创建一个与`f`具有相同函数体和作用域的函数，但是在这个新函数中，`this`将永久地被绑定到了`bind`的第一个参数(也就是我们想要绑定的this指向)，无论这个函数是如何被调用的。也就是说，bind只生效一次。

   ```
   function f(){
     return this.a;
   }
   
   let g = f.bind({a:1});// 创建一个新函数，并且不会立即执行
   console.log(g()); // 1
   
   let h = g.bind({a:2}); // bind只生效一次
   console.log(h()); // 1
   
   let o = {a:3, f:f, g:g, h:h};
   console.log(o.a, o.f(), o.g(), o.h()); // 3, 3, 1, 1
   ```

总结：

- 三个功能相同，区别在于参数的不同或是否立即调用

- 这三者第一个参数都是绑定作用域，修改this的指向。
- call和apply之间唯一区别就是传参的不同。第一个参数仍都是指的执行对象，call方法从第二个参数开始，会将后续的参数当成函数所需的数据。而apply则吧函数所需的数据都放在数组里面，数组作为apply方法的第二个参数。(apply传递参数需要使用数组包裹)
- call和bind之间的区别是call是立即调用所需的函数，只能调用一次。而bind参数跟call是一样的，不过bind不会马上执行，而是将所需要的函数给返回，这样就可以重复的使用所需的函数(apply,call会立即执行一次，bind是创建一个新函数，不会立即执行)
- bind只生效一次。













### 面向对象的三大特性

面向对象具备三大特性：继承、封装和多态。

###### 继承

概念：在程序中，继承是指一个类能够使用另一个类的属性和方法。被继承的那个类称为父类，继承父类属性和方法的那个类叫做子类，即子类能够使用父类里的属性和行为。

ES6 的继承机制实质是先将父类实例对象的属性和方法，加到`this`上面（所以必须先调用`super`方法），然后再用子类的构造函数修改`this`。

语法：

```
class 父类名{
    constructor(参数){
        this.属性名 = 参数;
    }
}
// 子类继承父类
class 子类名 extends 父类名{ // 子类通过extends关键字，继承了父类的所有属性和方法。
    constuctor(参数){
        super(参数);
    }
}

```

super：在子类里面，super是一个特殊作用的关键字，可以利用`super`来调用父类里面的方法或属性。

语法：

```
super.属性名  或   super.方法名();
// 在子类构造函数中，只能使用super() 来表示调用父类的构造函数,让子类拥有父类构造函数里的属性和行为
```

例如：

```
class Father {
	constructor(x,y){
		this.x=x;
		this.y=y;
	}
	a(){
		return '111'
	}
}

class Son extends Father {
	constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)  得到与父类同样的实例属性
    this.color = color; // 放super上面或者注释super都会报错
    // 加上自己的属性
  }

  a() {
    return this.color + ' ' + super.a(); // 调用父类的a()
  }
}
```

注意：子类必须在`constructor`方法中调用`super`方法，且必须是构造函数的第一行，否则新建实例时会报错。这是因为子类自己的`this`对象，必须先通过父类的**构造函数**完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。如果不调用`super`方法，子类就得不到`this`对象。

如果省略了`constructor`,`constructor`会被默认添加。在子类的构造函数中，只有调用`super`之后，才可以使用`this`关键字，否则会报错。这是因为子类实例的构建，基于父类实例，只有`super`方法才能调用父类实例。

例如：

```
	class Father{
            constructor(name,age,sex){
                this.name =name;
                this.age =age;
                this.sex =sex;
                this.show = function(){
                    console.log(`姓名: ${this.name},年龄：${this.age},性别：${this.sex}`);
                }
            }
        }

        class Son extends Father{
            constructor(name,age,sex) {
                super(name,age,sex);
            }
        }
        
        let s1 = new Son('张三',23,'男');
        s1.show();
        let s2 = new Son('李四',34,'女');
        s2.show();
```



父类的静态方法(类方法)，也会被子类继承：

```
	class A {
            static hello() {
                console.log('嘿嘿嘿');
            }
        }

        class B extends A {
        }

        B.hello()  // 嘿嘿嘿
```





**super**

`super`这个关键字，既可以当作函数使用，也可以当作对象使用。在这两种情况下，它的用法完全不同。

1. `super`作为函数调用时，代表父类的构造函数，子类的构造函数必须执行一次`super`函数。且只能用在子类的构造函数之中，用在其他地方就会报错。

```
class A {}

class B extends A {
  constructor() {
    super();
  }
  x() {
    super(); // 报错   用在B类的m方法之中，就会造成语法错误。
  }
}
// 子类B的构造函数之中的super()，代表调用父类的构造函数。这是必须的，否则会报错。
```

**扩展**： 注意，`super`虽然代表了父类`A`的构造函数，但是返回的是子类`B`的实例，即`super`内部的`this`指的是`B`的实例。（理解：子类继承父类，默认情况下拿不到this，所以需要调用super，拿到this）

```
	class A {
            constructor() {
                console.log(this);
            }
        }
        class B extends A {
            constructor() {
                super(); // 在super()执行时，它指向的是子类B的构造函数，而不是父类A的构造函数。也就是说，super()内部的this指向的是B
            }
        }
        new A() // A{}
        new B() // B{}
        
```

2. `super`作为对象时，在普通方法中，指向父类的**原型对象**。（了解）

   ```
   class A {
     x() {
       return 1;
     }
   }
   
   class B extends A {
     constructor() {
       super();
       console.log(super.x()); // 1
     }
   }
   
   let b = new B();
   // 子类B当中的super.x()，就是将super当作一个对象使用。这时，super在普通方法之中，指向A.prototype，所以super.x()就相当于A.prototype.x()。
   ```

   注意，由于`super`指向父类的原型对象，所以定义在父类实例上的方法或属性，是无法通过`super`调用的。

   ```
   	class A {
               constructor() {
                   this.x = 1;
               }
           }
   
           class B extends A {
               y() {
                   return super.x;
               }
           }
   
           let b = new B();
           console.log(b.y());
           // x是父类A实例的属性，super.x就引用不到它。
   ```

   



###### 封装

- 概念：封装再生活中是指对某个事物的内部实现细节进行因此，对外只提供了使用的接口。比如电脑、手机、吹风机。 再程序中，封装是指一种程序的编程技巧，为了能够提高代码的健壮性(安全)、可复用性。

- 作用：

  - 提高代码的健壮性
  - 提高代码的复用性

- JavaScript 的封装体现(私有属性#、存取器属性)

  - `私有属性#`

    - 再es6中，类里面我们可以定义以`#`号开头的属性，JavaScript会自动将其作为**私有属性**（即只能再**类内部**使用）

    - 语法

      ```javascript
      class 类名{
          #私有属性名 =数据;
      }
      ```

      - 只能再类内部中使用。
      - 有兼容性问题，目前就谷歌支持
      - 不能定义再构造函数中

    - 例如：

      ```
      		class B{
                  #age = 1;
                  constructor(){
                     
                      console.log(this.#age); // 1
                  }
                  show(){
                      console.log(this.#age); // 1
                  }
              }
              let b = new B();
              b.show();
              console.log(b.#age); // 报错
      ```

      

  - 存取器属性(JavaScript 封装的最终方案)

    - 概念：是一种特殊的属性，对外而言是一个普通的实例属性，再类内部是有两个方法**get和set**（也叫getter 和 setter 方法）来维护该属性。

    - 语法

      ```javascript
      class 类名{
          constructor(){
              
          }
          // 存取器属性
          get 存取器属性名(){
              
          }
          set 存取器属性名(value){
              
          }
      }
      
      在类外面作为一个普通实例属性来调用
      获取：对象名.存取器属性名 
      设置：对象名.存取器属性名 =新数据
      ```

    - 特点：

      - 存取器属性无论获取或设置都是通过方法来控制的，跟一般的实例属性有很大的区别

    - 作用（体现了封装）

      - 保证了属性的安全性：
      - 隐藏了属性设置或获取的内部实现细节

    - 例如：

      ```
      	class D{
                  constructor(){
                      this._num = 1;
                      this.count = 2;
                  }
                  get num(){
                      return this._num +3;
                  }
                  set num(value){
                      if(typeof value=="number"){
                          this._num=value;
                      }
                  }
              }
              let d = new D();
              console.log(d.num);
              d.num = '王二麻子';
              console.log(d.num);
              console.log(d.count);
              d.count = '嘿嘿嘿';
              console.log(d.count);
      ```

      

- 总结

  - 在JavaScript里，体现封装的方式
    - 函数（比如parse Int、Math.random()）
    - 存取器属性（面向对象中使用）
    - `#`  并 结合存取器属性(未来)







###### 多态

- 概念：一种定义，多种实现。
- 理解：多态是面向对象编程的使用技巧，巧妙的运用了继承以及重写搭配使用能够极大的提高程序的可扩展性。即原来的代码不需改变或极少改变就能够使用新的代码。
- 一般的运用步骤（针对面向对象）
  - 先找到每次更新内容时都会修改的地方
  - 运用继承+重写+instanceof将需要修改的地方进行代码删减
  - 利用instanceof判断对象和类之间的关系。

```
 	// 地图渲染:模拟用户手机里的地图app使用，用户手机里可能有多个地图app。
        //要求：确保该程序能够识别所有的地图app，以及未来可能会加入的新地图app
        // 1. 问题：只要某个类有show方法，那么useMap方法就会执行。期望：只能是地图类才能够执行
        class Map{
            show(){
                console.log('正在使用地图');
            }
        }
        class BaiduMap extends Map{
            show(){
                console.log('正在使用百度地图');
            }
        }
        class GaoDeMap extends Map{
            show(){
                console.log('正在使用高德地图');
            }
        }
        class TencentMap extends Map{
            show(){
                console.log('正在使用腾讯地图');
            }
        }
        class GoogleMap extends Map{
            show(){
                console.log('正在使用谷歌地图');
            }
        }
        // QQ
        class QQ{
            show(){
                console.log('正在使用QQ');
            }
        }

        //模拟用户使用地图app
        //只能时地图类才能够使用
        class User{
            useMap(map){
                //map 必须是地图类的对象才可以
                if(map instanceof Map){
                    map.show();
                }
                
                
            }
        }
        let b = new BaiduMap();
        let g = new GaoDeMap();
        let qq = new QQ();
        let u = new User();
        let t = new TencentMap();
        let google = new GoogleMap();
        //用户正在使用地图
        u.useMap(b);
        u.useMap(g);
        u.useMap(qq);
        u.useMap(t);
        u.useMap(google);
```



### 补充

###### instanceof

概念：可以判断某个对象是否是某个类的实例

语法：

```
对象名 instanceof 类名
// 例子：
var obj = new Object();
console.log(obj instanceof Object);// true
```

- 返回true或false
- 如果右边是本类或着是父类，那么都是返回true



### 扩展

###### 类中的方法

```
	class People{
      constructor(x,y) {
          this.x = x;
          this.y = y;
          this.b = function() {
            console.log(this.x,this.y);
          }
      }
      a(){
            console.log(this.x,this.y);
        }
    }
    let people1 = new People(1,4);
    console.log(people1.a === People.prototype.a); // true
    console.log(people1.b === People.prototype.constructor.b); // false
    console.log(People.prototype); // {constructor: ƒ, a: ƒ}
    console.log(people1); //People{x: 1, y: 4, b: ƒ}
```

构造函数中的this，指向的是实例对象，所以b方法在实例对象当中；类当中的方法，挂载的是类的`prototype`属性上面。

```
class People {
  constructor() {
  }

  a() {
  }

  b() {
  }
}

// 等同于

People.prototype = {
  constructor() {},
  a() {},
  b() {},
};
```



###### super

1. ```
   	class A {
               constructor() {
                   this.x = 1;
                   this.y = 2;
                   this.a = function(){
                       console.log(this.x);
                   }
               }
               a(){
                   return '父a方法';
               }
           }
      
           class B extends A {
              constructor(){
                  super();
              }
              a(){
                  console.log('我拿到的'+super.a());
              }
           }
      
           let b = new B();
           b.a();
   ```

   2.

   ```
        class A {
               constructor() {
                   this.x = 1;
                   this.y = 2;
               }
               a(){
                   return '父a方法';
               }
           }
   
           class B extends A {
              constructor(){
                  super();
              }
              a(){
                  console.log('我拿到的'+super.a());
              }
           }
   
           let b = new B();
           b.a();
   ```

   3.

   ```
    		class A {
               constructor() {
                   this.x = 1;
                   this.y = 2;
               }
               a(){
                   return '父a方法';
               }
           }
   
           class B extends A {
              constructor(){
                  super();
              }
           }
   
           let b = new B();
          console.log(b.a());
   ```

   



###### 手写函数实现new的功能

```
let myNew = function ( func, ...args ){
    //1.新建一个空对象，并将构造函数的原型对象赋给这个空对象
    let obj = Object.create(func.prototype);
    //2.执行构造函数，相应参数被传入，并将this的上下文指向新创建的对象obj
    let result = func.apply(obj,args);
    //3.如果构造函数返回了对象，就舍弃之前创建的对象obj，newObj = result
    if(typeof result === 'object') {return result};
    //4.反之，newObj = obj
    else { return obj };
}
function Person(name){
    this.name = name;
}
let newObj = myNew(Person);
console.log(newObj.name);
```



###### new关键字解释

当执行`let o = new Fn()`时，js实际执行的是：

```
let o = new Object();
o.__proto__ = Fn.prototype;
Fn.call(o);
```



###### Object.create()

ES6中引入了一个新方法Object.create(),可以调用这个方法来创建一个新对象。新对象的原型就是调用 create 方法时传入的第一个参数。

```
var a = {a: 1}; 
// a ---> Object.prototype ---> null

var b = Object.create(a);
// b ---> a ---> Object.prototype ---> null
console.log(b.a); // 1 (继承而来)

var c = Object.create(b);
// c ---> b ---> a ---> Object.prototype ---> null

var d = Object.create(null);
// d ---> null
console.log(d.hasOwnProperty); // undefined, 因为d没有继承Object.prototype
```

注意：Object.create允许一次性地直接设置 `__proto__` 属性，以便浏览器能更好地优化对象。同时允许通过 `Object.create(null) `来创建一个没有原型的对象。





###### Object.getPrototypeOf()

Object.getPrototypeOf(o) === `o.__proto__`

注意： `o.[[Prototype]]` **符号**也是用于指向 `o` 的原型。





###### 对象、函数和数组的原型

```
let o = {a: 1};

// o 这个对象继承了 Object.prototype 上面的所有属性
// o 自身没有名为 hasOwnProperty 的属性
// hasOwnProperty 是 Object.prototype 的属性
// 因此 o 继承了 Object.prototype 的 hasOwnProperty
// Object.prototype 的原型为 null
// 原型链如下:
// o ---> Object.prototype ---> null

var a = ["吃饭", "睡觉", "打豆豆"];

// 数组都继承于 Array.prototype 
// (Array.prototype 中包含 indexOf, forEach 等方法)
// 原型链如下:
// a ---> Array.prototype ---> Object.prototype ---> null

function f(){
  return 'pyy';
}

// 函数都继承于 Function.prototype
// (Function.prototype 中包含 call, bind等方法)
// 原型链如下:
// f ---> Function.prototype ---> Object.prototype ---> null
```



###### JavaScript的ES5继承解决方案(call+原型链)

利用call 和原型链搭配一起实现继承

```
子类名.prototype = new 父类名();
function 子类名(参数1,参数2,参数N){
    父类构造函数.call(this,参数1,参数2,参数N);
}
```

- 设置原型为父类对象是为了实现子类对象能够使用父类原型上的属性和行为
- call方法是为了能够让子类对象拥有父类构造函数里的实例属性和行为。



###### `prototype`、`__proto__`、`constructor`

- `prototype`：是函数专享，该属性指 的是该函数所对应的原型对象。
- `__proto__`: 普通对象有的一个非标准属性，目前绝大多数浏览器都支持。表示该对象所对应构造函数的原型对象，即`对象名.__proto__ === 构造函数名.prototype`
- `constructor`:是原型对象上的属性，指的是原型对象所对应的构造函数本身。
- 三者之间的关系
  - `prototype`是函数专属，而普通对象是有`__proto__`和`constructor`两个属性。
  - 因为JavaScript里一切皆对象，所以函数本身也是一个对象，函数本身同时具有以上三个属性。

