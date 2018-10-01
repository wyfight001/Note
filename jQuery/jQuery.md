# jQuery

## 定义

- JS库: 把一些浏览器兼容性的代码或者是常用的函数封装在一个js文件中,这个文件就是一个JS库-------->jQuery就是JavaScript库中的一种

- Prototype, YUI, Dojo, ExtJS, jQuery等 都是JS库

- 为什么要学jQuery:      Write Less, Do More    

  - DOM中一个简单的功能需要大量的代码
  - DOM中兼容的问题很多  能解决JS的兼容问题, 但是CSS还是有问题的
  - DOM中代码的容错性很差
  - DOM中window.onload也只能有一个

- jQuery的优点: 写得少做的多, 体积小, 功能强大, 链式编程, 隐式迭代, 插件丰富, 开源, 免费

- 学习JS是打造装备的过程,经常需要封装兼容代码----能力检测; 学习jQuery是捡装备的过程

- jQuery的js文件每个版本都有两个, 第一个是正常的, 第二个是压缩的, 上线时用压缩的

  ```
  $("#btn").click(function(){
      $("p").text("我是p");
  })
  ```

- 多库共存  var xy = $.noConflict(); 把$的权利给了xy, $就可以作为其他的用法出现在代码中

## jQuery对象与DOM对象转换

- 浏览器中的顶级对象: window; 页面中的顶级对象: document
- jQuery中的顶级对象: jQuery------可以用$符号来代替, 为了方便 (jQuery的js文件中的所有的东西都是jQuery或者都是$符号下的)
- 如果想要使用jQuery中的属性或者方法, 需要 jQuery.属性或者jQuery.方法()来使用-------------->$.属性或者$.方法
- DOM中注册事件
  - document.getElementById("id属性值").onclick=匿名函数;
- jQuery注册事件
  - $("#id属性值").click(匿名函数)
- 如果通过DOM获取---------就是DOM对象; 如果通过$或者jQuery的方式获取-------jQuery对象    DOM对象和jQuery对象是两个不同的对象 
- DOM对象是不能直接调用jQuery中的方法的! jQuery对象也是不能调用DOM对象的属性和方法   (DOM操作很麻烦, 兼容问题; jQuery操作中, 有些没封装在jQuery中, 通过原生js代码实现功能)
  - DOM对象转成jQuery对象-------->$(DOM对象), 那么就可以使用jQuery中的方法或者属性了; 
  - jQuery对象转DOM对象---------->jQuery对象[0], 或者jQuery.get(0)可以使用DOM对象的属性和方法了
- jQuery对象的事件中的this是当前的DOM对象!
  - jQuery对象.val();----------表示的是获取该元素的value属性值
  - jQuery对象.val("值")---------表示的是设置该元素的属性值

## jQuery对象的方法

- jQuery对象.length--------获取元素个数

- jQuery对象.css("属性名","属性值");--------设置元素的样式属性值-----属性名 DOM写法和css写法都可以

- jQuery对象.css(obj);----------修改多个样式======链式编程  (获取的宽高是字符串类型)

- jQuery对象.width("值"?);-------->  值可以是字符串或数字类型; 没有值则获取宽度值(数字类型)

- jQuery对象.height("值"?);--------->document.getElementById("#dv").offsetHeight

- jQuery对象.innerWidth()-------->无边框的宽

- jQuery对象.outerWidth()--------->有边框的宽

- jQuery对象.offset()--------->对象{left:XX,top:XX}--------同样可以获取和设置

  - jQuery对象.offset().left()-------->获取对象的left值

- jQuery对象.scrollTop()--------->获取元素向上卷曲出去的距离

- jQuery对象.scrollLeft()-------->获取元素向左卷取出去的距离

- jQuery对象.scroll(function(){})--------->注册滚轮移动的事件

- jQuery对象.val()---------获取jQuery对象的value值

- jQuery对象.val("值")---------修改jQuery对象的value值

  ```
  $("select标签").val(num)-------为select标签中value属性是num的这个option标签选中 !!!
  ```

- jQuery对象.text()----------设置或获取jQuery对象的文本内容(成对标签中间的内容)

- jQuery对象.html("<p>一个p</p>")-----在对象中添加p标签语句

- jQuery对象.attr(参数1,参数2)-------设置某个属性的值   参数1为属性名  参数2为属性值

- attr方法主要操作元素的自定义属性,但是也可以操作元素的自带属性;但是,操作元素的选中的checked的时候,不是很合适------->推荐使用prop方法

- jQuery对象.attr(参数1)-------获取某个属性的值

- jQuery对象.removeAttr("属性")---------移除这个自定义属性

- jQuery对象.prop(参数1,参数2)-------设置某个属性的值   参数1为属性名  参数2为属性值(一般为布尔类型)  -----元素选中专用---prop("checked")---布尔值

- 鼠标进入: jQuery对象.mouseenter(function(){});

- 鼠标离开: jQuery对象.mouseleave(function(){});

- 停止: jQuery对象.stop();

- jQuery对象.index();----------获取索引值

- jQuery对象.eq(索引值)-------获取对应索引的标签

- .end()------------方法是修复断链,恢复断链之前的状态

- class操作
  - .addClass("样式名")-------添加一个类或多个(可以链式编程,也可以加空格); 返回的是该对象
  - .removeClass("样式名"?)-----如果没有参数则删除所有的类样式 (可以链式编程,也可以加空格); 返回的是该对象
  - .hasClass("样式名")----------判断有否该样式,返回true或false
  - .toggleClass("样式名")-------判断有否该样式,如果有,就移除;没有,就添加

- 获取兄弟元素
  - .next()----获取下一个兄弟元素
  - .prev()-----获取前一个兄弟元素
  - .siblings()-----获取所有兄弟元素 (除了自己)
  - .nextAll()------获取后面的所有兄弟元素
  - .prevAll()------获取前面的所有兄弟元素

- 动画的相关方法
  - .show()/.hide()------参数1:时间(可以是时间,也可以是"fast"/"slow"/"normal");参数2:回调函数
  - .slideDown()/.slideUp()/slideToggle()-----滑出/滑入/切换滑出滑入   参数1:时间;参数2:回调函数
  - .fadeIn()/.fadeOut()/.fadeToggle()/.fadeTo(时间,结束)-------淡入/淡出/切换  参数1:时间;参数2:回调函数
  - .animate()-----参数1: 最终的样式对象--键值对;参数2:时间;参数3:回调函数

- 动画队列
  - .animate().animate().animate()....
  - .stop()-----停止动画方法------参数1:clearQueue是否清除动画队列?true:false; 参数2:jumpToEnd是否跳转到当前动画的最终效果?true:false

- 隐式迭代------内部帮助我们循环遍历

  每个元素做不同的操作时----each方法   遍历jQuery对象! 但是, 里面的每个对象最开始都是DOM对象

  $("uu>li").each(function(){

  ​	//参数1: index索引; 参数2: 对象

  ​	console.log(argument[0]+"==="+argument[1]);

  });

## 网页加载的不同方式

```
window.onload = function(){
	console.log("哈哈");
};
// jQuery中第一种页面加载事件--------页面全部加载完毕才触发(标签,文字,图片,引入的文件)
$(window).load(function(){
    console.log("哈哈");
});
//jQuery中第二种页面加载事件---------比上面快-----页面中基本元素加载后就触发
$(document).ready(function(){
   console.log("123"); 
});
//jQuery中第三种页面加载事件--------页面中基本元素加载后就出发
jQuery(function(){
  console.log("页面加载了");  
});
$(function(){
    console.log("页面又加载了");
});
```

- 如果有两个window.onload事件, 只执行一个----注册事件,赋值的方式
- $(window).load(function(){})可以执行多个------相当于调用多次方法

## jQuery中获取元素的方式

#### DOM获取元素的方式:

- 根据id------document.getElementById("id属性值");
- 根据标签名字------document.getElementsByTagName("标签名字");
- 根据name属性----document.getElementsByName("name属性值");
- 根据类样式名字document.getElementByClassName("类样式名字")
- 根据选择器-----document.querSelector("选择器")-----id选择器,类选择器,标签选择器.....一个; document.querySelectorAll("选择器")----多个

#### jQuery中获取元素的方式

- $("选择器")--------jQuery对象
  - $("#btn")-------id选择器-----一个
  - $("p")---------标签选择器-------多个元素或一个---$("p").text("都是p")相当于DOM中的.innerText属性---对象.text()是获取;对象.text("值")是赋值
    - 本身没有循环操作,jQuery中内部帮我们循环操作------->隐式迭代
  - $(".cls")------类选择器
  - $("div.cls")------交集选择器
  - $("#dv,p,li")-----并集选择器/多条件选择器
  - 层次选择器
    - $("#dv span")-------获取div父级元素的所有span标签
    - $("#dv>span")------获取div父级元素的直接的子元素
    - $("#dv~span")------获取div父级元素后面的所有兄弟元素
    - $("#dv+span")-----获取的是div后面直接的兄弟元素
  - $("li:odd")----奇数筛选器: 奇数行
  - $("li:even")-----偶数筛选器: 偶数行
  - $("ul").children("li")
  - $("li:eq(索引值)")------>索引选择器: 获取对应索引的元素
  - $("li:lt(索引)")---------->获取小于这个索引的元素;
  - $("li:gt(索引)")---------->获取大于这个缩印的元素
  - $("选择器:last")---------->最后一个
  - $("选择器:first")---------->第一个
  - 当前元素.next()---------->下一个兄弟元素
  - 当前元素.nextAll()--------->后面所有的兄弟元素
  - 当前元素.prev()--------->前一个兄弟元素
  - 当前元素.prevAll()---------->前面所有的兄弟元素
  - 当前元素.siblings()------->所有的兄弟元素(没有自己)
  - 当前元素.parent()--------->父级元素
  - 当前元素.children()--------->当前元素中所有的子元素(直接的)
  - 当前元素.find("选择器")-------->从当前元素中找某个或者是某些元素

- 隐式迭代

  - 设置操作的时候：会给jq内部的所有对象都设置上相同的值
  - 获取的时候：只会返回第一个元素对应的值。

## 创建元素的方式

#### 第一种方法

- var ulObj = $("<ul style='list-style-type:none;cursor:pointer;'></ul>");---------->创建节点

#### 元素创建的另一个方式

- $("#dv").html("<input type='button' value='按钮'>");

#### 元素的添加

- 父级元素.append(子元素);-------$("#dv").append($("<a href='www.baidu.com'>百度</a>"))
- 自己元素.appendTo(父元素);
- 父级元素.prepend(子元素);-------把创建的子元素直接插入到div中的第一个子元素前面<-------->(子元素).prependTo(父级元素)
- $("#dv").after(元素)-------->把元素添加到div的后面,是div的下一个兄弟元素
- $("#dv").before(元素)-------->把元素添加到div的前面,是div的上一个兄弟元素
- 注意问题: 
  1. 获取的元素通过append方法/appendTo方法添加到另一个元素中的时候, 类似于剪切
  2. 获取的元素通过.clone()方法,再append方法添加才是复制

#### 元素的移除方法

- $("#dv").html("")--------移除所有的子元素
- $("#dv").empty()---------清空子元素
- $("#dv").remove()--------自杀,清除自己

## 链式编程

```
$("#uu>li").mouseenter(function(){
    $(this).css("backgroundColor","red");
}).mouseleave(function(){
    $(this).css("backgroundColor","");
}).click(function(){
    $(this).css("backgroundColor","pink").css("border","1px solid balck").css("fontSize","20px");
})
```

- 链式编程: 对象不停地调用方法======>对象.方法().方法().方法().....
- 对象调用方法,如果返回值还是当前这个对象,那么就可以继续调用方法
- 经验: 在jQuery中, 一般情况,对象调用的方法是设置的意义,那么返回来的几乎都是当前的对象,就可以继续的链式编程; 如果是获取的意思, 那么就不能链式变成了

```
function Person(age){
    this.age = age;
    this.sayHi = function(){
        console.log("您好");
        return this;
    };
    this.eat = function(){
        console.log("吃");
    }
};
var per = new Person(10);
per.sayHi().eat();
```



## 元素的选中问题

- 单选框

  ```
  document.getElementById("r3").checked = true;-------DOM操作
  $("#r3")[0].checked = true;--------DOM操作
  $("#r3").attr("checked",true)-------jQuery操作  attr主要针对自定义属性
  console.log($("#r3").attr("checked"))--------是否默认选择?checked:undefined
  ```

  - attr方法针对单选框或者复选框的是否选中问题, 操作起来很麻烦, 几乎不用
  - 推荐使用prop方法------.prop("属性",值); ----值一般是布尔类型,设置选中--------.prop("属性")-----获取值

- 复选框

- 下拉列表

  ```
  $("select标签").val(num)-------选中val为num的option选项
  ```

## 为元素绑定事件/解绑事件

1. #### 对象.事件名字(事件处理函数)
   - $("#btn").mouseenter(function(){});

   ​       $("#btn").mouseleave(function(){});

   - $("#btn").mouseenter(function(){}).mouseleave(function(){});----链式编程    (可以绑定多个相同事件)

     对象必须先创建(存在), 再绑定事件

2. #### 对象.bind("事件名字",事件处理函数);

   - $("#btn").bind("click",function(){});---------bind方法绑定事件  
   - $("#btn").bind("click",function(){}).bind("mouseenter",function(){});---链式编程+bind方法   (也可以绑定多个相同事件)
   - $("#btn").bind({"click":function(){}},"mouseenter":function(){});--------bind方法里面传对象----使用键值对  (绑定多个相同事件时只执行后面的)

   ​       //bind方法内部是调用的另一个方法绑定的事件

   ​       对象必须先创建(存在), 再绑定事件 , 后添加的元素没有事件

3. #### 父级对象.delegate("子级元素","事件名字",事件处理函数);

   - $("#dv").delegate("p","click",function(){});------父级元素调delegate方法, 为子级元素绑定事件------委托代理  (其实delegate方法是调用的on的方法)

     可以先绑定事件, 再创建元素

4. #### 父级对象.on("事件名字","子级元素","事件处理函数");

   - $("#dv").on("click","p",function(){})-----为子级元素绑定事件, 也可以为本身绑定事件
   - 可以先绑定事件,再创建元素



5. #### 用什么方式绑定事件, 最好用对应的方式解绑事件

   - ##### bind对应的解绑事件
     - ###### $("#dv").unbind("click mouseenter");------把所有的点击和鼠标进入事件移除 ---------同时解绑多个事件, 事件名之间用空格.-------也可以用链式编程

     - ###### $("#dv").unbind();----------解绑所有事件

   - ##### delegate对应的解绑事件

     - ###### $("#dv").undelegate();--------把所有子元素的所有事件移除

     - ###### $("#dv").undelegate("p","click mouseenter");----移除子元素p标签的点击和鼠标进入事件

   - ##### on对应的解绑事件

     - ###### $("#dv").off()------父级和子级元素的事件全部解绑

     - ###### $("#dv").off("click mouseenter")-------父级和子级所有的点击&&鼠标进入事件都解除 (中间用空格表示)

     - ###### $("#dv").off("click mouseenter","p")------解绑p的点击事件和鼠标进入事件

     - ###### $("#dv").off("","p")--------解绑p的所有事件

     - ###### $("#dv).off("click","**")--------解绑所有子元素的事件

## 事件冒泡

解决办法: return false

## 事件触发

1. 第一种方式--------对象.事件名字();-------$("#text").focus();
2. 第二种方式--------对象.trigger("focus")------$("#text").trigger("focus");
3. 第三种方式--------对象.triggerHandler("focus")-------$("#text").triggerHandler("focus")--------可以触发事件, 但是不能触发浏览器的默认行为

## 事件参数对象

三个属性

- $("#dv").click(function(e){console.log(e.target)})---------e.target得到的是触发该事件的目标对象 (DOM对象)
- $("#dv").click(function(e){console.log(e.currentTarget)})----------e.currentTarget得到的是触发该事件的当前对象 (DOM对象)
- $("#dv").click(function(e){console.log(e.screenX)})----------得到点击处相对于整个屏幕左上角的横向距离
- e.delegateTarget这个属性得到的是代理的这个对象

```
$("#dv").mousedown(function(e){
    if(e.altKey){
        console.log("按下alt和鼠标");
    }else if(e.shiftKey){
        console.log("按下shift和鼠标");
    }else if(e.ctrlKey){
        console.log("按下ctrl和鼠标");
    }else{
        
    }
});
```

## 包装集

把很多DOM对象进行包装或者是封装------>jQuery对象

jQuery对象-------->DOM对象-----jQuery对象[0]----获取到DOM对象

$("p")[0]-----第一个p标签

##### 如何判断对象存不存在----->看jQuery对象.length属性不等于0的方式

- jQuery对象.length----------->jQuery中如何判断这个元素是否存在,就是通过包装集的length属性来测试的

## jQuery的插件

#### 插件: 就是一个功能, jQuery的插件, 别人把功能写好了,直接拿过来用

#### 使用步骤: 

1. 先下载插件的文件
   - 压缩包: (js文件, css文件, 插件的js文件, index.html文件), 如果没有, 在对应文件夹中找
2. 引入到自己的开发工具中, 先看效果
   - 自己创建一个文件夹-------插件
   - 引入他的js文件-----------jQuery-1.xx.x.js
   - 引入他的css文件
   - 引入他的插件的js文件
   - 把index.html的html代码加入到自己的body中
   - 把index.html文件中的jQuery代码复制到自己的script中即可

#### 自己制作插件

如果希望jQuery对象能够调用这个方法, 那么就把这个方法加入到$.fn.这个位置

## jQuery  UI

- jQuery UI 用户界面
- www.jquery.com---------->plugin