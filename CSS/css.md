## 多类名选择器：

- 标签中写class="属性1 属性2" class的值为class名、空格、class名，就可以同时调用两个类名选择器

- 样式显示效果跟HTML元素中的类名先后顺序，受css样式书写的上下顺序有关

- 多个类名之间用空格隔开

- 多类名选择器在后期布局比较复杂的情况下，还是较多使用的

  <div class="nav">
  div:hover ==  .nav:hover

- class相当于名字，id相当于身份证号,两者最大区别就是class可以使用多次，但是id只能用1次

- id和class不相互排斥，用的最多的还是class

## 字体风格  

- font-size大小 font-family字体 font-weight粗细 font-style 风格
- font-weight:normal | bold | bolder | lighter | number 没有单位
- normal 相当于 400； bold 相当于700  
- font-style: normal | italic | oblique

1. 网页普遍使用14px+
2. 尽量使用偶数的数字字号
3. 各种字体之间必须使用英文状态的逗号隔开
4. 中文字体需要加英文状态下的引号，英文字体一般不用加引号
5. 如果字体中包含空格、#、$等符号，则改字体必须加英文状态下的引号，如"Times New Roman"
6. 尽量使用系统默认字体
7. 浏览器按照font-size先后顺序显示字体
8. 使用unicode写字体兼容性最好 "\5FAE\8F6F\96C5\9ED1" == "微软雅黑"    "5B8B\4F53" == "宋体"

##### 字体连写 （要按顺序）

###### font: font-style font-weight font-size/line-height font-family 

##### 字体外观设置

###### font color line-height text-align text-indent

- color: RGB代码，如红色可以表示rgb(255,0,0)或rgb(100%,0%,0%)  百分比时取值为0百分号也不能掉
- #ff0000 === #f00 必须两两相同才能缩写
- line-height:一般比字号大7,8个像素
- text-align: 让盒子里面的文字！！对齐
- text-decoration: none | underline | overline | line-through == s/del标签

## 标签显示模式 ：display

1. 块级元素 （block-level）p h1-h6 霸道 独占一行 可设置宽高、对齐方式 div是最典型的块元素
2. 行内元素 （inline-level） <span> 和相邻行内元素在一行上  设置宽高无效，但水平方向的padding和margin可以设置   默认宽度就是它本身内容宽度   行内元素只能容纳文本或其他行内元素
3. 行内块元素 （inline-block） <img /> <input type="text">  <td>

行内元素  可以改宽高 （综合1.2） 默认宽度是它本身内容的宽度

高度、行高、外边距、内边距都可以控制  两个行内块之间有缝隙


行内元素只能容纳文本或其他行内元素 （a特殊 a里面可以放块级元素 仅限于a）

p h1 不能放块状元素

a里面不要放a链接

## css三大特性

1. 层叠性
2. 继承性   某些属性可以继承   如height不能继承
3. 优先级   权重计算

#### 权重计算

- 标签选择器：  0001
- 类/伪类选择器 0010
- ID选择器	  0100
- 行内选择器	  1000
- important     ∞
- css谁的权重大，显示谁的属性，一样的话，遵循就近原则
- 权重不能进位
- 继承的权重为0

### css背景

1. background-image
2. background-repeat
3. background-position :   后面可以接方位名字 没有先后顺序

​                          如果只有一个值，另一个默认居中
                          可以接px值  但是有先后顺序，前面是x，后面是y

4. background-color
5. background-attachment: scroll | fixed

- background: 背景颜色 背景图片 背景平铺 背景滚动 背景位置 一般以此顺序，但是顺序没有先后顺序
- css3 背景透明
- background-color: rgba(255,255,255,0.5); red green blue alpha(透明度0-1)

## css三大重点  盒子  定位  浮动

#### 1. Box ：border padding margin

​           border: border-width || border-style || border-color
           border-style: none || solid || dashed
           border: 1px solid black; 一般
           table-collapse: collapse； 合并相邻边框

```
padding: xpx; 一个值表示上下左右padding，两个值表示上下padding和左右padding，三个值表示上padding、左右padding和下padding，四个值分别表示上右下左padding  顺时针

margin: xpx; 一个值表示上下左右margin，两个值表示上下margin和左右margin，三个值表示上margin、左右margin和下margin，四个值分别表示上右下左margin

测试时：里面的蓝色为实体颜色，浅绿色为padding，橘黄色是border，暗红色是margin

盒子水平居中，只用设置左右margin值为auto
要让盒子居中对齐，必须满足两个条件 1.必须是块级元素 2.盒子必须有宽度

插入图片。用的最多  比如产品展示类

背景图片我们一般用于小图标背景或者超大背景图片

    * 相邻块元素垂直外边距的合并
    * 嵌套块元素垂直外边距的合并
       1.可以为父元素定义1像素的上边框或上内边距
       2.可以为父元素添加overflow：hidden。

外盒尺寸=content width + padding + border + margin
内盒尺寸=content width + padding + border

如果一个盒子没有给定宽度/高度或者继承父亲的宽度/高度，则padding不会影响本盒子大小

盒子布局稳定性
width(最稳定) > padding(会撑开盒子) > margin(盒子垂直分布时的外边距合并问题，嵌套时子盒子加margin-top父盒子也会有margin-top)

border-radius: Xpx; 类似margin，可以有1、2、3、4个值，4个值分别是左上、右上、右下、左下

box-shadow: h-shadow | v-shadow | blur |  spread |color | inset 水平阴影、垂直阴影、模糊距离(虚实)、阴影尺寸(阴影大小)、阴影颜色、内/外阴影 
```
#### 2. Float       

- 标准流（普通流）：就是网页标签正常由上而下、由左而右排列顺序的意思，比如块级元素独占一行，行内元素按顺序排
- 浮动 : 文字环绕，任何盒子一行排列（浮动布局） left | right | none 
  - 浮动特性：只有左右浮动
  - 脱标：不占位置 会影响它下面的标准流
  - 浮动跨越不了内边距、边框 
  - 一个父盒子中的一个子盒子浮动，则其他的也应该浮动
  - 浮动有隐藏模式转换，会让元素默认转换为行内块元素

##### 怎么排列！！！

###### float  浮 漏 特  

- 浮：加了浮动的元素是扶起来的
- 漏：加了浮动的盒子，不占位置，它浮起来，原来的位置漏给了标准流的盒子    
- 特：特别注意，首先浮动的盒子需要和标准流的父级搭配使用，其次，浮动会使元素显示模式体现为行内块元素

##### 布局流程：

1. 确定页面版心（可视区）  
2. 分析页面中的行模块，以及每个行模块中的列模块  
3. 制作HTML结构   4.CSS初始化，然后开始运用盒子模型的原理，通过DIV+CSS布局来控制页面各个模块

- 左右布局用float：left | right
- 注意优先级
- 清除浮动 方法 ： 1.额外标签法     2.overflow清除浮动    3.after伪元素清除浮动    4.双伪元素清除浮动

#### 3. position (定位！！！最为麻烦)  css离不开定位，特别是后面的js特效！！！ 可以越过父盒子

* 定位属性主要包括 定位模式  和  边偏移(top/bottom,left/right)  两部分

* 定位模式  position:属性值 （static|relative|absolute|fixed）

* ##### static 所有元素的默认定位方式  唯一用处：就是取消定位

* ##### relative(自恋型) 

    1.以自己的左上角为基准点偏移  也是压住别人
    2.位置走了，但是原来位置继续占有

* ##### absolute(拼爹型) 压着别人都要用absolute

    1.不占位置 ！！
    2.若所有父元素都没有定位，则以浏览器当前屏幕为基准定位
    3.若最近的父元素有定位，则以该父元素为基准定位

子绝父相！！！  自己是绝对定位的话，父级要用相对定位 （最合适的搭配）

浮动并不是完全脱标（文字和图片没有脱标！），而绝对定位是完全脱标！

绝对定位的盒子水平/垂直居中
    1.首先left50%，父盒子一般大小
    2.然后走自己外边距负一半值就可以了margin-left

* ##### fixed(认死理型)   

    1.与父亲没有关系，只认浏览器
    2.完全脱标，不占有位置

背景图片不能撑开盒子，插入图片才会撑开盒子

z-index  默认为0，不加单位，只有相对、绝对、固定定位的盒子才有此属性，越大越在上
font-weight也没有单位

相对定位、绝对定位、固定定位都脱标，比标准流高一级，会浮在它们上面

##### 显示与隐藏 

- display: none; 隐藏某元素，不占有位置   display: block   常用！！！
- visibility: hidden; 隐藏某元素，占有位置  visibility: visible 显示

##### 溢出部分

- overflow: hidden|visible|auto|scroll

##### 用户界面  

- cursor鼠标样式   default小白|text文本|move移动|pointer小手
- outline轮廓线 0|none  针对表单(input)
- resize防止文本域拖拽 none
- vertical-align和行内块搭配使用（img默认和基线对齐和input）

##### 溢出的部分显示省略号

1. 文字一行显示white-space: nowrap;
2. 溢出部分隐藏overflow: hidden;
3. 超出部分省略号text-overflow:ellipsis;

##### css精灵图（sprite）为了减少服务器的请求次数

- 把多个小背景图片放到一张大图上 background-position

##### 字体图标！ icomoon  iconfont

- 是文字
- 打开网站icomoon或iconfont，选图标，下载，拷贝font文件夹到HTML文件中，建立链接

```
@font-face { 
    font-family: "icomoon";  /*我们自己起名字可以*/
    src:  url('fonts/icomoon.eot?7kkyc2');
    src:  url('fonts/icomoon.eot?7kkyc2#iefix') format('embedded-opentype'),
      url('fonts/icomoon.ttf?7kkyc2') format('truetype'),
      url('fonts/icomoon.woff?7kkyc2') format('woff'),
      url('fonts/icomoon.svg?7kkyc2#icomoon') format('svg');
    font-style: normal;  /*倾斜字体正常*/
}
```



##### 引字体

- 如 span {font-family: icomoon;},   打开下载的文件夹里的demo.html文件，然后复制相应文字图片
- 如果需要自制图标，则需要svg格式的图片，在icomoon中上传，然后下载
- 如果需要追加图标，则在icomoon中上传之前的selection.json，然后追加，再重新下载
- 小问题： 注意img, input 等行内块结构默认与文字基线对齐！
- width: 100% 是使宽度和父元素相同（哪怕父元素的宽也是百分比）