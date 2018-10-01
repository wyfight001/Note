# JavaScript

## 简介

#### 分三部分

1. ECMAScript标准-----基础的语法
2. DOM
3. BOM

JS是一门脚本语言，是一门解释性语言，是一门弱类型语言，是一门基于对象的语言，是一门动态类型的语言

动态页面：页面由html+css+Js

向服务器发送请求，服务器那边没有页面，是动态的生成，返回给客户端

#### 编程思想

- 面向过程：所有的事情都是亲力亲为，注重的是过程
- 面向对象：提出需求，找对象，对象解决，注重的是结果  不是面向过程的替代，而是面向过程的封装（面向对象编程：Object Oriented Programming---OOP), 有类(class)的概念
- 面向对象的特性：** 封装，继承，多态 **
  1. 封装：就是包装，把一些重用的内容进行包装，在需要的时候，直接使用
  2. 继承：类与类之间的关系，JS中没有类的概念，js中有构造函数的概念，是可以有继承的，是基于原型
  3. 多态：同一个行为，针对不同的对象，产生了不同的效果
- JS不是一门面向对象的语言(没有class),JS是一门基于对象的语言,因为面向对象的思想适合于人的想法,编程起来会更加的方便,及后期的维护. JS可以通过构造函数来模拟类的概念(class)

## 封装

- 就是包装
- 一个值存储在一个变量中----封装
- 一坨重复代码放在一个函数中-----封装
- 一系列的属性放在一个对象中-----封装
- 一些功能类似的函数(方法)放在一个对象中------封装
- 好多相类似的对象放在一个js文件中------封装

## 继承: 为多态服务

### 原型链:是一种关系,实例对象和原型对象之间的关系,关系是通过原型(__proto__)来联系的

#### 构造函数---原型对象---实例对象  (原型)

```
function Person(sex, age){
    this.sex = sex;
    this.age = age;
}
//通过构造函数的原型添加方法和属性, 数据共享, 实例对象可以直接访问
Person.prototype = {
	constructor: Person,  //必须要加,手动修改构造器的指向
    sayHi : function(){
        console.log("您好");
    },
    height: "188",
    weight : "55kg"
};
var per = new Person("男", 16);
//实例对象中有两个属性（这两个属性是通过构造函数来获取的），和__proto__这个属性
//构造函数中并没有sex和age这两个属性
```

- 实例对象中有个属性，____proto____, 也是对象，叫原型，不是标准的属性，浏览器使用的，IE8不支持
- 构造函数中有一个属性，prototype，也是对象，叫原型，是标准属性，程序员使用
- 可以通过原型对象向内置对象添加方法

##### 原型------>______proto______, 或者prototype, 都是原型对象

##### 原型的作用-------->	共享数据, 节省内存空间

- 构造函数中的prototype属性, 是构造函数的原型对象
- 构造函数的原型对象(prototype)中有一个constructor构造器, 这个构造器指向的就是自己所在的原型对象所在的构造函数
- 实例对象的原型对象(____proto____)指向的是该构造函数的原型对象
- 构造函数的原型对象(prototype)中的方法是可以被实例对象直接访问的
- 实例对象可以直接访问原型对象中的属性或者方法
- 属性或方法如果在实例对象中找不到, 才会去实例对象所指向的构造函数的原型中找
- 我们可以为系统的对象的原型中添加方法, 相当于在改变源码
- 原型链: 实例对象和原型对象之间的关系,关系是通过原型(____proto____)来联系的

![三者之间的关系](C:\Users\user\Desktop\htmlfiles\4.javascript高级\03-JavaScript-高级-第1天\三者之间的关系.png)

##### 把局部变量变成全局变量, 把局部变量给window就可以了

```
一次性函数
(function(win){   ---------形参
	var num = 10;
	//js是一门动态类型的语言, 对象没有属性, 点了就有了
	win.num = num;
})(window);       ---------实参
```

```
(function(win){
	function Random(){}  //创建构造函数
    Random.prototype.getRandom = function(min,max){
        return ((max-min)*Math.random()+min);
    }   //构造函数的原型getRandom方法
    win.Random = Random; //将Random对象暴露给window,外部可以直接访问
})(window)
var random = new Random();
console.log(random.getRandom(0,5));
```

- 实例对象的原型_____proto_____指向的是该对象所在的构造函数的原型对象
- 构造函数的原型对象(prototype)指向如果改变了,实例对象的原型(______proto______)指向也会发生改变
- 实例对象的______proto______对象------->构造函数的prototype  的______proto______--------->Object的prototype

#### 继承

- 首先继承是一种关系,类(class)与类之间的关系,JS中没有类,但是可以通过构造函数模拟类,然后通过原型来实现继承

##### 原型的另一个作用------->为了实现继承  :  父类级别与类级别的关系

```;;
//人的构造函数
function Person(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Person.prototype.eat = function(){
    console.log("人会吃");
}
Person.prototype.play = function(){
    console.log("会玩");
}
//学生的构造函数
function Student(score){
    this.score = score;
}
//继承
Student.prototype = new Person("小明",10,"男");
Student.prototype.study = function(){
    console.log("学习");
}
var stu = new Student(100);
console.log(stu.name);
console.log(stu.sex);
console.log(stu.age);
console.log(stu.score);
stu.eat();
stu.play();
stu.study();
```

##### 原型继承: 改变原型的指向

- 缺陷: 因为改变原型指向的同时实现继承,直接初始化了属性,继承过来的属性的值都是一样的,这就是问题

- 解决方案:继承的时候,不用改变原型的指向,直接调用父级的构造函数的方式来为属性复制就可以了 

##### 借用构造函数继承: 主要解决属性的问题

-  构造函数名字.call(当前对象,属性,属性,属性,...);
  1. 解决了属性继承,并且值不重复
  2. 缺陷: 父级类别中的方法不能继承

##### 组合继承

- 原型继承+借用构造函数继承

```
function Person(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Person.prototype.sayHi = function(){
    console.log("你好");
}
//借用构造函数继承属性
function Student(name,age,sex,score){
    Person.call(this,name,age,sex);
    this.score = score;
}
//原型继承方法
Student.prototype = new Person();
Student.prototype.eat = function(){
    console.log("吃");
}
var stu = new Student("小明",12,"男",99);
console.log(stu.name);
console.log(stu.sex);
console.log(stu.score);
stu.sayHi();
stu.eat();
```

##### 拷贝继承

- 把一个对象中的属性或者方法直接复制到另一个对象中

- var obj2 = obj1;  //仅仅改变指向

- ```
  var obj2 = {};
  for(var key in Person.prototype){
      obj2[key] = Person.prototype[key];
  }          //真正的拷贝继承
  ```

## 函数进阶

#### 函数定义

- ##### 函数声明

function f1(){

​	console.log("函数");

};

函数声明如果放在if-else的语句中,在IE8的浏览器中会出现问题

- ##### 函数表达式

var ff = function(){

​	console.log("函数");

};

以后宁愿用函数表达式,都不要用函数声明

#### 函数中的this指向

- 普通函数的this是谁?------>window
- 定时器中的this是谁?------->window
- 构造函数的this是谁?-------->实例对象
- 对象的方法中的this是谁?-------->实例对象
- 原型对象的方法中的this是谁?------->实例对象

#### 严格模式

"use strict"  //严格模式

#### 函数的调用方式

- 普通函数----f1();
- 构造函数----var ff = new F1(); //通过new来调用,创建对象
- 对象方法函数----var per = new Person(); per.play();

#### 函数是对象

- 函数是对象,对象不一定是函数. 函数中既有prototype,也有______proto______, 一个东西既有prototype,又有______proto______,那它就是函数; 对象中有______proto______
- 函数对象中有______proto______原型, 所以是对象; 函数中有prototype原型, 是对象
- 所有的函数实际上都是Function的构造函数创建出来的实例对象
  - var f1 = new Function("num1","num2","return num1+num2");
  - console.log(f1(10,20));

#### 函数中的几个成员

1. name属性------->函数的名字,name属性只读,不能修改
2. arguments属性-------->实参的类数组
3. length属性----------->形参的个数
4. caller----------->调用者

```
 function f1(x,y) {
      console.log(f1.name);
      console.log(f1.arguments.length);
      console.log(f1.length);
      console.log(f1.caller);//调用者
    }
   // f1.name="f5";
   // f1(10,20,30,40);
   // console.dir(f1);

    function f2() {
      console.log("f2函数的代码");
      f1(1,2);
    }
    f2(); //f2函数的代码   f1   2   2   f2(){...}
```

#### 函数作为参数使用

```
f1(function(){
    console.log("哈哈");
});   //传入匿名函数

function f2(){
    console.log("f2的函数");
}
f3(f2);   //命名函数,那么只传入命名函数的名字,没有括号!

function f4(fn){
    setInterval(function(){
        console.log("开始");
        fn();
        console.log("结束");
    },1000);
}
f4(function(){
    console.log("好困啊");
})
```

#### 函数作为返回值使用

Object.prototype.toString.call(参数) ---------------->参数的类型

```
function getType(type){
    return function(obj){
        return Object.prototype.toString.call(obj)===type;
        //return Object.prototype.toString.apply(obj)===type;
        //return Object.prototype.toString.bind(obj)()===type;
    }
}
var ff = getType("[object Array]");
var result = ff([1,2,3]);
console.log(result) //true
```

```
	   //按日期,size或名字排序
       function File(name, size, time) {
            this.name = name;//电影名字
            this.size = size;//电影大小
            this.time = time;//电影的上映时间
        }

        var f1 = new File("jack.avi", "400M", "1997-12-12");
        var f2 = new File("tom.avi", "200M", "2017-12-12");
        var f3 = new File("xiaosu.avi", "800M", "2010-12-12");
        var arr = [f1, f2, f3];

        function fn(attr) {
            return function (obj1,obj2) {
                if (obj1[attr] < obj2[attr]) {
                    return -1;
                } else if (obj1[attr] == obj2[attr]) {
                    return 0;
                } else {
                    return 1;
                }
            }
        }
        var ff = fn("size");
        arr.sort(ff);
        for (var i = 0; i < arr.length; i++) {
            console.log(arr[i].name + "=====" + arr[i].size + "=====" + arr[i].time);
        }
```



## 正则表达式

##### 定义:

- 也叫规则表达式, 按照一定的规则组成的一个表达式, 这个表达式的作用主要是匹配字符串的
- 主要作用: 匹配字符串, 或者批量处理字符串
- 在大多数编程语言中都可以使用

##### 组成

- 由元字符或是限定符组成的一个式子

##### 元字符

- . 表示除\n之外的任意的单个字符
- \r\n回车换行
- [][0-9] [0-9] 0到9(包含)中的一个数字 [a-zA-Z]
- [] 另一个含义: 把正则表达式中元字符的意义干掉
- [0-9]|[a-z]  数字或数目
- ()  分组  提升优先级 

限定符 

- {m,n}表示该限定符前面的表达式出现了m-n次 [a-z]{3}  [a-z0-9]{1,6}  .{9,}
- {,9}是错误的
- *表示前面的表达式  出现0到多次------{0,}
- +表示前面的表达式  出现1到多次-----{1,}
- ? 表示前面的表达式  出现0次到1次----------{0,1}
- ^ 表示的是以开始,或者是取反  ------^[0-9] 以数字开头; [ ^0-9]取反, 非数字
- $ 表示的是以什么结束  -------[[ 0-9][ a-z ]][a-z] $ 必须以小写字母结束 ----^[0-9]$相当于严格模式
- \d------[0-9]  数字中的一个
- \D------非数字中的一个
- \s-------空白符中的一个 space/tab
- \S-------非空白符
- \W-------特殊符号   ----[ ^0-9a-zA-Z_]    "__不算特殊符号"
- \w-------非特殊符号 [0-9a-zA-Z_] 
- \b--------单词的边界

##### 邮箱的正则表达式

```
[0-9a-zA-Z_.-]+[@][0-9a-zA-Z_.-]+([.][a-zA-Z]+){1,2}
```

##### 汉字的正则表达式

```
[\u4E00-\u]
eacape('汉字'); ----->"%u6C49%u5B57"
unescape('%u6C49%u5B57')-------->"汉字"
```

正则表达式的方法

- g表示所有, i表示忽略大小写

- reg.test(str)--------->判断str中是否有reg

- str.match(/\d+/g)-------->(match的参数是正则表达式) str中所有的数字都拿出来放在一个数组中   g指的是全局匹配

- str.replace(/RegExp/g, "str") --------->全部替换  (没有g就是只替换第一个)   (str.replace(/\s+/g,""))----->删除所有的空格

- str.replace(/[h]/gi,"S");------>将字符串中的大小写H都换成S

- reg.exec(str) --------->匹配输出结果  

  ```
  var str = "中国移动:10086;中国联通:10010;中国电信:10000";
  var reg = /\d{5}/g;
  var array = reg.exec(str);
  while (array != null){
      console.log(array);
      array = reg.exec(str);
  }  // 三个数组  (exec是遍历)
  ```

##### 创建正则表达式对象

1. 通过构造函数创建对象

   var reg = new RegExp(/\d{5}/);

   var str = "我的电话是10086";

   console.log(reg.test(str));

2. 字面量的方式创建对象

   var reg = /\d{5}/;

   console.log(reg.test("电话是10080"));

## apply, call和bind的使用

#### apply和call方法

- apply和call方法也是函数的调用方式

- apply和call都可以改变this的指向

- apply和call方法中如果没有传入参数,或者是传入的是null,那么调用该方法的函数对象中的this就是默认的window

- apply和call都可以让函数或者方法来调用,传入参数和函数自己调用的写法不一样,但是效果是一样的,apply是传入数组参数,call是一个一个传入参数

- apply和call方法实际上并不存在函数这个实例对象中,而是在Function的prototype中

- 返回值即为函数或方法的返回值

  ```
  function f1(num1,num2){
      console.log("结果是:"+(num1+num2)+this);
  }
  f1.apply(null,[100,200]) //结果是:300[object Window]
  f1.call(null,100,200)
  
  var obj = {
      sex: "男",
      age: 10
  }
  f1.apply(obj,[10,20]);  //结果是:30[object Object]
  f1.call(obj,10,20)   //同上
  ```

- apply和call的作用: 改变this的指向

- 不同的地方: 参数传递的方式是不一样的

- apply的使用语法

  - 函数名字.apply(对象,[参数1,参数2,...]);
  - 方法名字.apply(对象,[参数,参数2,...]);

- call的使用语法

  - 函数名字.call(对象,参数1,参数2,...);
  - 方法名字.call(对象,参数1,参数2,...);

#### bind方法

```
function f1(x, y){
    console.log((x+y)+"====>"+this)
}
// var ff = f1.bind(null,10,20);
var ff = f1.bind(null);
ff(10,20);
```

- 复制了一份的时候,把参数传入到f1函数中,null就是this,默认为window
- bind方法就是复制的意思,参数可以在复制的时候传进去,也可以在复制之后调用的时候传入进去
- bind是复制一个方法或者函数,是在复制的同时改变了this的指向
- apply和call是调用的时候改变this指向;bind方法是复制一份的时候,改变了this的指向
- 使用语法
  - 函数名字.bind(对象,参数1,参数2,...);---->返回值是复制之后的这个函数
  - 方法名字.bind(对象,参数1,餐数2,...);----->返回值是复制之后的这个方法

##### bind的应用

- 改变定时器中的this指向
- 与apply和call不同,bind方法返回的是一个函数, 还需要调用才有效

## 作用域

#### 变量-------->局部变量和全局变量

- 作用域: 就是变量的使用范围
- js中没有块级作用域

```
while(true){
    var num = 10;
    break;
}
console.log(num);  //10

{var num2 = 100;}
console.log(num2); //100

if(true){
    var num3 = 300;
}
console.log(num3) //300   都是全局变量
```

- 作用域链: 变量的使用,从里向外,层层搜索,搜索到了就可以直接使用了
- 预解析: 就是在浏览器解析代码之前,把变量的声明和函数的声明提前到该作用域的最上面

## 闭包

- 闭包的概念:

- 闭包的作用: 缓存数据, 延长作用域链

- 闭包的优点和缺点: 缓存数据 (既是有点, 又是缺点)

- 闭包的模式

  - 函数模式的闭包

    ```
    function f1(){
        var num = 10;
        function f2(){
            console.log(num);
        }
        f2();
    }
    f1();   // 10
    ```

  - 对象模式的闭包: 函数中有个对象, 这个对象可以访问函数中的变量

    ```
    function f3(){
        var num = 10;
        var obj = {
            age : num
        };
        console.log(obj.age);
    }
    f3();
    ```

- 闭包的应用

  ```
  function f1(){
      var num = 10;
      num++;
      console.log(num);
  }
  f1();   //11
  f1();   //11
  f1();   //11
  
  function f2(){
      var num = 10;
      return function(){
          num++;
          console.log(num);
      }
  }
  var ff = f2();
  ff();   //11
  ff();   //12
  ff();   //13
  ```

## 沙箱 : 环境, 黑盒

- 在一个虚拟的环境中模拟真实世界,做实验,实验结果和真实世界的结果是一样的,但是不会影响真实世界

- 自调用函数就是一个沙箱

- 主要作用: 避免命名冲突

  ```
  (function(){
   	var str = "小黑喜欢小红";
      str.substr(2);
      console.log(str);
  }())  //沙箱
  ```

  

## 递归

- 递归: 函数中调用函数自己,此时就是递归,递归一定要有结束的条件,否则就是死循环
- 递归轻易不要用,效率很低

```
//斐波拉契数列
function getSum(x){
    if(x==1 || x==2){
        return 1;
    }
    return getSum(x-1)+getSum(x-2);
}
getSum(5) //5
getSum(7) //13

//求数字每个位数之和
function getEverySum(x){
    if(x<10){
        return x;
    }
    return x%10 + getEverySum(parseInt(x/10));
}
```

## 拷贝

##### 浅拷贝: 拷贝就是复制,就相当于把一个对象中的所有的内容,复制一份给另一个对象,直接复制,或者说,就是把一个对象的地址给了另一个对象,他们指向相同,两个对象之间有共同的属性或者方法,都可以使用

```
var obj1 = {
    name:"张三",
    sex: "男",
    age: 10
};
var obj2 = {};
for(var key in obj1){
    obj2[key] = obj1[key];
}    // 浅拷贝
```

##### 深拷贝:拷贝还是复制,深: 把一个对象中所有的属性或者方法,一个一个的找到,并且在另一个对象中开辟相应的空间,一个一个地存储到另一个对象中

## 伪数组和数组

伪数组和数组的区别

- 真数组的长度是可变的, 伪数组的长度是不可变的
- 数组实例对象的______proto______------->Array的prototype, 真数组能调用数组里的方法
- 伪数组实际上是对象 , 里面有0,1,2,...属性和length属性