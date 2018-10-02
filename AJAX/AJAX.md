# AJAX

## 概述

- 在此之前, 我们可以通过以下几种方式让浏览器发出对服务端的请求
  - 地址栏输入地址
  - 特定元素的href或src属性
  - 表单提交

## API

- XMLHttpRequest --------->ajax的核心构造函数

  ```
  var xhr = new XMLHttpRequest();
  xhr.open('get','./test.php',true);
  xhr.send(null);
  xhr.responseType('json');
  xhr.onreadystatechange = function(){
      if(this.readyState!==4) return;
      console.log(this.responseText);   //永远获取的是字符串的相应格式
      console.log(this.response);    //会根据this.responseType的变化而变化
      console.log(this.status);     //状态码
      console.log(this.statusText);    //状态信息
  }
  ```

兼容代码

```
var xhr = XMLHttpRequest? new XMLHttpRequest(): new ActiveXObject('Microsoft.XMLHTTP');
```



## 封装

```
function ajax(method, url, params, callback){
    var xhr = new XMLHttpRequest()
    method = method.toUpperCase()
    var arr = [];
    if(params.instanceOf(Object)){
        for(var key in params){
            var newStr = key + '=' + params[key];
            arr.push(newStr);
        }
        params = arr.join('&')
    }
    if(method === 'GET') {
        url += '?'+params
    }
    xhr.open(method,url)
    var data = null
    if(method === 'POST'){
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        data = params
    }
    
    xhr.onreadystatechange = function(){
        if(this.readyState !==4) return
        callback(this.responseText)
    }
    xhr.send(data)   
}
```

## jQuery的ajax

```
$.ajax({
	url: 'xxxxx',
    type: 'get',
    data: {id: 1, name: 'zhangsan'},
    dataType: 'json',
    success: fn
})

$.get('json.php',{id: 1}, fn);          //{id:1}在url里传递
$.post('json.php',{id: 1}, fn);         //{id:1}在请求报文里传递
$.getJSON('json.php',{id: 1}, fn);      //无须服务端设置Content-Type为application/json (默认为GET请求)

$('selector').load(url selector,data,fn);  //局部加载

$(document).ajaxStart(function(){
})
$(document).ajaxStop(function(){
})
```



## 进度条API-------NProgress

引入NProgress的js,css文件

$(document).ajaxStart(function(){

​	NProgress.start();

}).ajaxStop(function(){

​	NProgress.stop();

})