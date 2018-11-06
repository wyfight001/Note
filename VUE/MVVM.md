# MVVM

## MVVM

![MVVM](https://raw.githubusercontent.com/Draveness/analyze/master/contents/architecture/images/mvx/MVC-Web-App.jpg)

- 架构方式，开发思想

- M: Model 数据模型 （操作数据的类）
- V：View 视图界面  （HTML）
- VM：ViewModel 视图数据模型   （驱动视图的data数据）

#### M: Model

- 服务端处理数据库中的数据
  - mongoose
  - 设计数据模型
- 客户端要处理服务器的接口交互
  - ajax('地址')
  - GET http://127.0.0.1:3000/users
  - GET http://127.0.0.1:3000/users/1
  - POST http://127.0.0.1:3000/users
  - PATCH http://127.0.0.1:3000/users/1
  - DELETE http://127.0.0.1:3000/users/1
  - 没有表意性
  - a页面 ajax({url:'/users'}) 

#### V: View

#### VM: ViewModel

#### 优点

- 开发效率
- 可维护性
- 原则：模块职责单一