# AJAX

## 概述

在此之前, 我们可以通过以下几种方式让浏览器发出对服务器的请求, 获得服务端的数据

- 地址栏输入地址, 回车, 刷新
- 特定元素的href或src属性
- 表单提交

无法通过或很难通过代码的方式进行编程(对服务端发出请求并且接受服务端返回的响应), 如果可以通过JS直接发送网络请求, 那么Web的可能就会更多

AJAX就是浏览器提供的一套API, 可以通过JS调用, 从而实现通过代码控制请求与响应, 实现网络编程

AJAX是一套API核心提供的类型: XMLHttpRequest

涉及到AJAX操作的页面"不能"使用文件协议访问

## API

- XMLHttpRequest ---------->核心, 构造函数!!!!!

  初始化-------->建立连接------->接收到响应头-------->响应体加载中------>加载完成

  ```
  var xhr = new XMLHttpRequest();                 //初始化
  xhr.open("GET","/time.php");   //设置请求行      //建立连接
  xhr.setRequestHeader('Foo','Bar')   //设置一个请求头Foo: Bar
  xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")   //一旦请求体是urlencoded格式的内容, 一定要设置请求头中的Content-Type
  xhr.send('key1=value1&key2=value2');   //以urlencoded格式设置请求体
  //onreadystatechange并不是只在响应时触发, 是在状态改变就触发
  xhr.onreadystatechange = function () {
  	switch(this.readyState){
          case 1: console.log(this.respondText);break;  //建立连接后
          case 2: console.log(this.respondText);break;  //接收到响应头
          case 3: console.log(this.respondText);break;  //响应体加载中
          case 4: console.log(this.respondText);        //加载完成
  	}
  }
  xhr.onload = function(){     //相当于readyState == 4的时候, 需要浏览器支持H5
      console.log(this.responseText);
  }
  ```

  因为响应需要时间, 所以无法通过返回值的方式返回响应; 所以AJAX API采用事件的机制 (通知的感觉)...     

   xhr.onreadystatechange = function(){}

  - readyState  的 值 
    - 0    -----> UNSENT    创建xhr
    - 1   ------> OPENED    xhr.open("GET","XXXX")之后
    - 2  -------> HEADERS_RECEIVED 获取响应头之后
    - 3   -------> LOADING 正在下载响应体
    - 4   -------> DONE 下载完毕

- getAllResponseHeaders() --------->获取响应头(返回字符串)

- getResponseHeader("Date")   ---------->获取响应头里的信息

- onload()   ------------->  是HTML5中提供的XMLHttpRequest version2.0定义的

- 当表单格式是"multipart/form--data", 出现Request Payloaded

## GET&POST

- http中约定报文的内容就是字符串, 而我们需要传递给客户端的信息是一个有结构的数据, 这种情况下我们一般采用JSON作为数据格式( json_encode()不带空格)

## jQuery中的AJAX

```
$.ajax({
    url: 'time1.php',
    type: 'get',
    beforeSend: function(xhr){
        //在所有发送请求的操作(open,send)之前执行
        console.log('beforeSend',xhr)
    },
    //只有请求成功, 状态码是200时, 才会执行这个函数
    success: function(res){        //响应体
        console.log(res)
    },
    error: function(xhr){
    //只有请求不正常(状态码不为200),才会执行
        console.log(xhr)
    },
    complete: function(xhr){
        console.log(xhr)
    }
})
```

高度封装的函数 (jQuery)

```
$.get('time.php', {id: 1}, function(res){   //get请求放在url地址里
    console.log(res)
})
$.post('time.php', {id, 1}, function(res){   //post请求放在请求体里
    console.log(res)
})
$.
```

# 跨域 

## 同源策略 

- 同源协议是浏览器的一种安全策略, 所谓同源是指域名, 协议, 端口完全相同, 只有同源的地址才可以相互通过AJAX的方式请求
- 同源或者不同源说的是两个地址之间的关系, 不同源地址之间请求称之为跨域请求
- 同源策略: 不同源地址之间, 默认不能相互发送AJAX请求
- XMLHttpRequest不支持跨域请求

## 跨域请求

- localhost指的是虚拟主机上的第一个站点根目录

- 不同源地址之间如果需要相互请求, 必须服务端和客户端配合才能完成

- 发送请求的方式   (尝试跨域请求, 校验目标 : 1---能发出去; 2----能收回来)

  - img         img可以发送不同源地址之间的请求, 无法拿到响应结果

    ```
    var img = new Image()
    img.src = 'http://www.xxxxxxx'   (直接请求, 不需要append到页面中)
    ```

  - link (真正的定义是链入一个文档, 通过rel属性声明链入的文档与当前文档的关系)      可以发送不同源地址之间的请求, 无法拿到响应内容

    ```
    var link = document.creatElement('link')
    link.rel = 'stylesheet'       必须要加rel才能发请求
    link.href = 'http://XXXXXXX'
    document.body.appendChild(link)
    ```

  - script  (和link类似写法)    可以发送不同源地址之间的请求, 无法拿到响应结果. 

    借助于JS代码可以执行, 可以获取响应内容 (JSONP)

    ```
    var script = document.creatElement('script')
    script.src = 'http://XXXXXX'
    document.body.appendChild(script)
    function foo(res){      //相当于请求的回调
        console.log(res)
    }
    //服务端 中echo出 foo({$json});  在json格式字符串外面包裹函数的调用
    ```

  - iframe

## JSONP  (json with padding)

- 通过script标签请求一个服务端的PHP文件, 这个文件返回的结果是一段JS, 作用是调用我们事先定义好的一个函数, 从而将服务端想要给客户端发过去的数据发送给客户端 (和ajax无关)

  ```
  封装代码
  
  ```

## CORS (Cross Origin Resource Share)

- ajax支持跨域访问  (需要在服务端设置响应头"Access-Control-Allow-Origin: * ")

  ```
  客户端
  $.get('http://localhost/cors.php',{},function(res){
      console.log(res)
  })
  服务端
  header('Access-Control-Allow-Origin: *');
  ```

  