## JS分三个部分: ECMAScript标准, DOM(Document Object Model), BOM(Browser Object Model)

- 所有语言都离不开 增 删 改 查
- 字符串判断比数字判断效率低

DOM: 文档对象模型   把页面看成文档进行操作

DOM对象: 通过DOM方式获取的元素得到的对象

xml文件也可以看成是一个文档

- HTML: 展示信息, 展示数据的
- XML: 侧重于存储数据 标签名随便写,大多数都是成对的, 不需要任何工具就能打开 

1. 文档(document): 一个页面就是一个文档
2. 元素(element): 页面中每个标签,都是一个元素(element),每个元素都可以看成是一个对象
   - 标签可以嵌套,标签中有标签,元素中有元素
3. 节点(node): 页面中所有的内容都是节点  (标签,属性,文本)    
   - root: 根
   - 根元素(html标签)

页面就是文档--document,文档中有根元素:html 

DOM树: 由文档及文档中所有元素组成的一个树形结构图,叫树状图,也叫DOM树

### 事件: 有触发和响应,事件源  (大多数事件用on开头)

先有按钮,才能获取,获取之后才能注册事件 

##### 常见获取元素方法

```
function my$(id){
	return document.getElementById(id);
}
document.body
document.getElementsByName("name1"); 根据name值获取元素
document.getElementById("btn"); 根据id获取元素  常用
document.getElementsByTagName("p")  根据标签名获取,返回一个伪数组 [p,p,p,p...]  常用
document.getElementByClassName("cls") 根据类样式的名获取元素----->h5
document.querySelector("#btn"); 根据选择器的方式获取元素----->h5
document.querySelectorAll(".cls"); 获取多个---->h5
```

##### 常用事件

```
onclick, onmouseover, onmouseout, onfocus, onblur(失去焦点), onmousedown, onmouseup
```

###### for循环在页面加载的时候执行, 事件是事件触发的时候执行

###### 规律: 在表单中,如果表单属性和值相同(checked,select,disabled,readonly), 那么在DOM操作时,属性值是布尔类型就可以了  

- 表单标签常用属性: name,value,type,checked,selected,disabled,readonly
- 表单中  value属性和innerText在页面中的效果相同
- 凡是css中属性多个单词的写法,在js DOM操作时,把-干掉,后面的单词首字母大写即可
- 在js中DOM操作时,设置元素的类样式,不用class关键字,而是用className
- 阻止超链接的默认跳转: return false; (在事件中有return false)

### innerText和textContent,innerHTML

1. 设置标签中间的文本内容,应该使用textContent属性(标准), chrome, firefox支持, IE8不支持, IE里面有些属性是定制的
2. innerText属性都支持, IE8的标准, 谷歌,火狐,IE8都支持
3. 前两者都是写text的,<会用&lt;,>会用&gt;解析,设置标签内容,是没有标签的效果

- 而innerHTML可以设置文本内容,设置标签内容是有标签效果的,浏览器都兼容.....主要作用是在标签中设置新的html标签内容
- 想要设置标签内容,使用innerHTML,想要设置文本内容,innerText或者textContent或者innerHTML
- 想要获取标签内容,innerText可以获取标签中间的文本内容,标签中如果还有标签,那么最里面的标签文本内容也能获取,而innerHTML获取的是标签中的所有html内容

###### 总结: 想要标签及文本内容,用innerHTML;想要设置标签, 使用innerHTML;想要设置文本,用innerText或者innerHTML或者textContent

兼容代码: 任何浏览器,如果不支持某属性,则该属性的类型是undefined

##### 标签属性 ≠ DOM对象属性

- 用getAttribute("自定义属性的名字")才能 获取 这个属性的值
- 用setAttribute("自定义属性的名字","自定义属性的值") 设置 自定义属性   (html标签中也有这个属性)
- 用removeAttribute("属性名字")来移除某个属性
- 自定义属性是无法用DOM获取的

文档:document

元素:页面中所有的标签,元素-----element, 标签-----元素-----对象

节点:页面中所有的内容(标签,属性,文本),node

根元素:html标签

### 节点的属性

- (可以使用标签--元素.点出来,可以使用属性节点.出来,文本节点.出来)

1. nodeType:节点的类型  1---标签,2---属性,3---文本
2. nodeName:节点的名字  标签节点---大写的标签名字,属性节点---小写的属性名字,文本节点---#text
3. nodeValue:节点的值   标签节点---null,属性节点---属性值,文本节点---文本内容

- 只有标签可以作为父节点
- obj.parentNode 获取父节点
- 元素创建: 3种方式

```
12行代码:
obj.parentNode;
obj.parentElement;
obj.childNodes;
obj.children;
obj.firstChild;
obj.firstElementChild;
obj.lastChild;
obj.lastElementChild;
obj.previousSibling;
obj.previousElementSibling;
obj.nextSibling;
obj.nextElementSibling;
```

###### 凡是获取节点的代码在谷歌和火狐得到的都是 相关的节点

###### 凡是获取元素的代码在谷歌和火狐得到的都是 相关的元素

###### 从子节点和兄弟节点开始,凡是获取节点的代码在IE8中得到的是元素,获取元素的相关代码,在IE8中得到的是undefined---元素的代码IE8不支持

### 创建元素的三种方法

1. document.write(元素标签和内容)---->如果在页面加载之后写入,则原页面内容被覆盖

2. obj.innerHTML(元素标签和内容)

3. document.createElement("标签")---->对象, 只负责创建元素

   创建元素----->把元素追加到父元素objParent.appendChild(document.createElement("p"))

##### 元素相关方法

```
obj.appendChild()-----追加子元素
obj.inserrBefore(newChild,refChild)-----在前面插入
obj.replaceChild(newChild,refChild)-----替换子元素
obj.removeChild(obj.firstElementChild)------移除元素
```

##### 为同一个元素绑定多个事件(DOM), 用什么方式绑定事件,就应该用对应的方式解绑事件!!!

三种方法:

```
1. obj.on+事件名=函数<-------->obj.on+事件名=null
2. obj.addEventListener(1,2,3)<----------->obj.removeListener(1,2,3)
3. obj.attachEvent(1,2)<--------->obj.detach(1,2)
```

###### obj.addEventListener(1,2,3)-----谷歌火狐支持,IE8不支持

###### 参数1: 事件的类型----事件的名字,没有on

###### 参数2: 事件处理函数----函数(命名函数,匿名函数)

###### 参数3: 布尔类型----目前就写false (控制事件是冒泡,还是捕获)

- this指向绑定事件的元素
- 解绑事件: 
  1. obj.onclick=null; 
  2. obj.removeEventListener(1,2,3) 解绑事件的时候需要在绑定事件的时候,使用命名函数

###### IE8中是 (谷歌火狐不支持,IE8支持)

###### obj.attachEvent(1,2)   

###### 参数1: 事件类型---带on; 

###### 参数2: 事件处理函数  (有一个对象参数:事件处理参数对象)  

- this指向window
- 解绑事件: obj.detachEvent(1,2); 命名函数

### 事件冒泡

多个元素嵌套,有层次关系,这些元素都注册了相同的事件,如果里面的元素的事件触发了,外面的元素的该事件自动地触发了
事件冒泡是从里向外

如何阻止事件冒泡:

```
window.event.cancelBubble=true; (属性)  IE,谷歌用

 e.stopPropagation(); (方法)谷歌火狐用

window.event和e都是事件参数对象,只是IE中没有e
```

###### forEach方法按升序为数组中含有效值的每一项执行一次callback函数, 有三个参数:(数组当前项的值,数组当前项的索引,数组对象本身)

事件有三个阶段  (冒泡和捕获不可能同时发生, 通过obj.eventPhase属性可以知道当前事件是什么阶段,一般默认都是冒泡阶段)

1. 事件捕获阶段  :  从外向内
2. 事件目标阶段  :  目标
3. 事件冒泡阶段  :  从里向外

addEventListener(事件类型,事件处理函数,控制事件阶段(true捕获,false冒泡)

```
document.body, document.title, document.documentElement
```

### 事件参数对象 

```
###### element.onmousemove = function(){console.log(argument[0]);}

###### 事件处理函数中实际上是有一个参数的, 这个参数和事件有关系,是一个对象-------->事件参数对象
IE8中没有事件参数对象, 可以用window.event替代
```

- e.clientX 可视区域的横坐标
- e.clientY 可视区域的纵坐标

### 三大系列

1. ##### offset

   - offsetWidth--------->获取元素的宽
   - offsetHeight
   - offsetTop
   - offsetLeft
   - offsetParent---------->定位的父级 

2. ##### scroll

   - scrollWidth------->元素中内容的实际的宽
   - scrollHeight------->元素中内容的实际的高
   - scrollTop---------->向上卷取出去的距离
   - scrollLeft---------->向左卷曲出去的距离

3. ##### client

   - clientWidth------->可视区域的宽 (没有边框), 边框内部
   - clientHeight--------->可视区的高 (没有边框), 边框内部
   - clientLeft------------->左边框的宽度
   - clientTop------------->上边框的宽度
   - clientX-------------->可视区域横坐标
   - clientY-------------->可视区域纵坐标
   - pageX-------------->相对于页面顶部的坐标
   - pageY

   ```
   //使文本不选中
   window.getSelection?window.getSelection().removeAllRanges():document.selection.empty();
   ```

   ### 元素隐藏

   my$("dv").style.display = "none";   //不占位

   my$("dv").style.visibility = "hidden";  //占位

   my$("dv").style.opacity = 0; //占位