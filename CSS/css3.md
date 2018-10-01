## css3新增

#### 结构伪类选择器

- :first-child
- :last-child
- :nth-child(n)

#### 属性伪类选择器

- div[class] {} 选中所有带class属性的标签
- div[class=test] {}  == test
- div[class^=test] {} 选中所有test开头的标签
- div[class$=test] {} 选中所有test结尾的标签
- div[class*=test] {} 选中所有带有test的标签

#### 伪元素

- p::first-letter {}  第一个字
- p::first-line {}    第一行
- p::selection {}     选中
- after和before！！！
  - div::before   必须有一个属性content:"";  在内部内容的前面插入

#### 动画：过渡动画  帧动画

##### transition: (transition property) (transition duration) (transition-timing-function) (transition delay)

###### 1. 2D变形 transform  过渡动画

- 移动translate(x,y) 缩放scale(x,y) 旋转rotate(deg)  倾斜（skew）
- transform: translate(x,y) | scale(x,y) | rotate(xdeg)
- transform-origin 调整旋转原点

- 动画 animation  帧动画

  - animation: 动画名称 动画时间 运动曲线 何时开始 播放次数 是否反向 运行或暂停

  ```
  animation-name animation-duration animation-timing-function animation-delay animation-iteration-count animation-direction animation-play-state
  animation：move 3s ease 0s infinite alternate; 调用动画
  @keyframes move { from { } to { } }  声明动画  （关键帧） 
  ```

  

###### 2. 伸缩布局（css3）

- 父盒子 display: flex; flex-direction: row | column 子盒子 flex: 2 占两份
- 文字阴影  text-shadow 水平阴影 垂直阴影 模糊距离 阴影颜色
- 背景缩放 background-size: x y; 长度或百分比，如果只设置一个值，则第二个值默认为auto。 如果设置为cover 则等比例缩放到完全填满背景区域。如果设置为contain，则等比例缩放到宽填满背景区域
- 背景渐变 只能加浏览器前缀！-webkit- -moz- -o- -ms-
  - background: -webkit-linear-gradient(top,green,red);
  - background: -webkit-linear-gradient(渐变起始位置，颜色 位置，颜色 位置...)
- 多背景 background: url(xxxx) no-repeat top left,(逗号隔开）url(xxxx) no-repeat right bottom;

###### 3. 三维动画 transform: rotateX(xdeg) rotateY(xdeg)

- 如果需要出现透视效果，则需要将母盒子设置perspective: 500px;数值越大，效果越不明显。