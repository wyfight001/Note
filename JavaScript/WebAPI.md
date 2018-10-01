## API 是一些预先定义的函数

- 目的是提供应用程序与开发人员基于某软件或硬件得以访问一组历程的能力,而又无需访问源码,或理解内部工作机制
- 任何开发语言都有自己的API
- API的特征 输入和输出
- API的使用方法(console.log())

#### 封装函数

```
function getStyle (element, attr) {
	return window.getComputedStyle?window.getComputedStyle(element, null)[attr]:element.currentStyle[attr];
} ------获取任意元素的任意样式 (字符串)

function animate (element, json) {
    clearInterval(element.timeId);
    element.timeId = setInterval(function(){
    	for(var attr in json){
    		var current = parseInt(getStyle(element, attr);
    		var target = json[attr];
    		var step = (target - current)/10;
    		step = step>0?Math.ceil(step):Math:floor(step);
   			current += step;
    		element.style[attr] = current + "px";
    		if (current == target){
				clearInterval(element.timeId);
			}
		}
		console.log("当前位置: "+current+" 目标位置: "+target+" 步进: "+step);    //测试代码
	}, 20)
}-------任意元素任意样式的变化动画
```

## 回调函数 

回调函数就是  -----作为参数的函数-----  (最终所有代码执行完毕再来执行这个函数)