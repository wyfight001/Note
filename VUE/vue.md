# VUE

## 1. 单页面应用程序

- Single Page Application (SPA)
- 从字面意义来看就是一个网站一个页面
  - coding
  - 网易云音乐
  - 极致用户体验,就像native app一样
- 优点
  - 分离前后端关注点, 前端负责界面显示, 后端负责数据存储和计算, 各司其职, 不会把前后端的逻辑混杂在一起
  - 减轻服务器压力, 服务器只用出数据即可, 不用管展示逻辑和页面合成, 吞吐能力会提高几倍
  - 同一套后端程序代码, 不用修改就可以用于Web界面, 手机, 平板等客户端
- 缺点
  - 致命缺点: SEO问题, 搜索引擎优化
  - 前进, 后退, 地址栏等, 需要程序进行管理
  - 书签, 需要程序来提供支持
- Hash (网页内部定位)

#### 1.1 简单的单页面程序

- `hash`
- `window.onhashchange`事件
- 当hash改变的时候, 根据不同的hash做不同的处理

#### 1.2 主流前端JavaScript框架

- Angular   (09年 原来是个人开发, 后来被google收购)
- React       (诞生于Facebook公司内部)
- Vue.js      (尤雨溪  中国江苏无锡人 12年左右 中文文档)
- 目前在公司中, BAT级别的企业, React > Angular > Vue.js. 在中小型公司, Vue.js更多一些

## 2. Vue.js介绍

- 是什么
  - 前端JS框架
- 为什么用它
  - 能帮助提升网站应用程序开发效率
- 一般什么情况使用它
  - 一般是需要开发SPA应用程序的时候去用
  - 但是VUE是渐进式的, Vue其实可以融入到不同的项目中
    - 可以和传统的网站开发架构融合在一起, 例如可以简单的把它当做一个类似jQuery的库来使用
    - 也可以使用它开发大型的SPA单页面应用程序
- 发展历史
  - 作者: 尤雨溪(微博: 尤小右)
  - 作者尤雨溪最初在2013年12月8号在GitHub上发布了v0.6版
  - 2015年10月份正式发布1.0版本
    - 真正火起来是在15年的1.0版本发布之后
  - 2016年10月份正式发布2.0版
- 相关资源  (别买书)
  - Github
  - http://cn.vuejs.org
  - 官方教程

## 3. 起步

#### 3.1 安装

安装: `npm install vue`默认安装最新稳定版

发布日志: https://github.com/vuejs/vue/releases

#### 3.2 Vue实例

- el
- data
- methods

总结:

- VUE的最大好处: 不需要DOM操作
- VUE其实就是一个更高级的模板引擎
  - 在页面中具有被Vue管理的程序入口 (不能使html和body)
  - `new Vue`出Vue应用程序
  - 把页面所有需要操作的DOM, 都通过数据绑定的方式来处理
    - 在data中声明
    - 在模板中通过特殊的语法来使用
      - `{{}}`使用在非表单元素, h1, p, strong
      - `v-model=""`使用在表单元素
    - 处理事件的方式
      - 在methods中定义方法
      - 在模板中通过`v-on:事件名称="事件处理函数"`的方式来注册特定的事件处理函数
    - 通过`el`选项来声明被Vue管理的模板入口
      - 不能是html, body
  - 在Vue中, 通过模板绑定的数据都是响应式的
    - 数据如果一旦变化, 则绑定该数据的视图元素也会改变

#### 3.3 数据绑定渲染

普通数据绑定

`{{}}`

- mustache语法 (胡子)

标签节点属性绑定  (v-bind可以省略)

- 语法:  `v-bind:属性名称="data中的数据成员名"`
- 简写: `:属性名称:"data中的数据成员名"`

#### 3.4 表单数据双向绑定

- 双向数据绑定
  - 数据的变化
  - 视图的变化
- 文本
- 多行文本
- 复选框
- 单选按钮
- 选择列表

#### 3.5 事件处理

- 定义事件处理函数
- 绑定事件处理函数
  - `v-on:事件名称="事件处理函数"`
  - 缩写: `@事件名称="事件处理函数"`
- methods
  - 不要有和data中重名的成员, 否则报错

#### 3.6 v-if  v-for

```javascript
<div id="app">
    <input type="checkbox" v-model="seen">显示/关闭盒子
    <div v-if="seen" class="box"></div>
    <h1>列表渲染</h1>
    <ul>
        <li v-for="item in fruits">
            {{ item }}
        </li>
    </ul>
</div>
<script>
	var app = new Vue({
		el: '#app',
		data: {
			seen: true,
			fruits: ['苹果','香蕉','橘子']
		},
	})
</script>
```

## json-server

- 这个工具已经在服务端处理了跨域的问题
- 真正的场景是需要在客户端解决跨域（通用解决方案就是代理服务器）

`npm i -g json-server`安装

`json-server --watch db.json`启动结构服务

增删改查：

- `GET/list`查询所有
- `GET/list/id`查询单个
- `POST/list`添加
- `DELETE/list/id`根据id删除
- `PATCH/list/id`根据id修改

## 接口测试工具： POSTMAN

## http-server

安装`npm i http-server`

查看帮助`hs -h`

基本使用

```
#默认占用8080端口启动一个服务器，直接打开浏览器
hs -o

#指令占用端口开启服务器
hs -p 3001 -o

#不启用缓存开启
hs -c-1 -p 3001 -o
```

