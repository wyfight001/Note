## BOM----->Browser Object Model 

- 浏览器对象模型,操作浏览器的
- 浏览器顶级对象:window-------皇上
- 页面中顶级对象:document------总管太监
- 页面中所有内容都是属于浏览器的,页面中的内容也都是window的,window是可以省略的
- window下面没有write方法,window.document.write();

window.name;

top和window是同一个东西, 名字不一样

- window.alert(); 测试的时候使用,不能设置样式,页面加载过程
- window.prompt(); 
- window.confirm(); 点确定,返回true;点取消,返回false
- window.onload=function(){};只要页面加载完毕,这个事件就会触发  window.可以省略  important
- window.onunload=function(){};页面关闭后才触发的事件
- window.onbeforeunload=function(){};页面关闭前才触发的事件

### location对象: 地址栏上的地址操作

###### 地址:协议(http://)+主机(localhost:)+端口号+路径

```
window.location.hash------>地址栏上#及后面的内容(锚)
window.location.host----->主机名及端口号(端口号负责通信)
window.location.hostname-------->主机名
window.pathname-------->文件路径--相对路径
window.port---------->端口号
window.protocol---------->协议(http:)
window.search----------->?及后面的内容(搜索的内容)
location.href="www.jd.com"------>设置跳转的页面地址 (属性)  重要!!!
location.assign("www.jd.com);------->设置跳转页面地址 (方法)
location.reload();------->重新加载 (刷新)
location.replace("www.jd.com");-------->跳转页面(没有历史记录)
```

### history对象: 历史记录的后退和前进

```
window.history.forward()------->前进
window.history.back()-------->后退
window.history.go(int)-------->正数为前进,负数为后退
```

 

### navigator对象: 获得系统和浏览器信息

```
window.navigator.platform------->判断系统平台类型
window.navigator.userAgent------->浏览器
```

### BOM中有两个定时器----计时器

1. 定时器1 setInterval(function(){},num);表示页面加载完毕后!!!,每隔num(单位:ms)执行一次函数,返回值就是定时器的id值....

   清除定时器 clearInterval(定时器id);  alert有断言功能 应该使用清理掉定时器

2. 定时器2(一次性的) window.setTimeout(函数,时间);和定时器1的参数和返回值一样, 但是是一次性的!(占空间,应该清理)

### 三大系列

##### offset

如果样式的代码是在style的标签中设置,则外部是获取不到的!在body中的属性style中可以获取 (不用)

用offset系列可以获取,数字类型,没有px: 

- offsetWidth-----获取元素的宽
- offsetHeight
- offsetLeft-----父级元素的margin+父级元素padding+父级元素border+自己的margin,如果脱离文档流,主要是自己的left和自己的margin
- offsetTop, 