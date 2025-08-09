## CSS
#### CSS的盒模型
HTML中每一个元素都可以看成一个盒子，这个盒子由margin、border、padding、content四个部分组成

目前有两种盒模型：标准盒模型和怪异盒模型，两者的区别主要在于对元素宽高的定义。标准盒模型的宽高指content的宽高，怪异盒模型的宽高指content、padding、border三部分组合的宽高。修改盒模型的方式是通过box-sizing属性来控制

>**BFC盒子**
>
>BFC是块级格式化上下文，例如根元素、overhide设置为hidden scroll等属性的元素、flex布局的元素、块元素或者行内快元素，都可以称为BFC盒子，这种元素的特点是内部布局不会影响到外部布局

#### CSS选择器的优先级
! important > 行内 > id > 类/伪类/属性 > 元素/伪元素 > 全局选择器
 
#### 隐藏元素的方法
display: none 不占据空间
opacity: 0  设置透明度
visibility: hidden  占据空间位置

#### px、rem、em、视口单位
px：绝对单位
em：相对于父元素的字体大小
rem：相对于根元素的字体大小，一般将HTML元素的font-size设置为62.5%，1rem就是10px，便于计算
vh、vw：视口单位，相对于视口的宽高

> **响应式设计**
>
> 一般使用媒体查询，在几个特定的尺寸上，对html的字体大小进行控制，同时对页面中的字体大小、宽高等使用rem，实现响应式布局
> 或者通过JS，添加resize事件监听，动态调整font-size
> 还可以通过elementPlus的栅格系统实现响应式布局

#### 重绘、回流
回流：修改了盒子的位置大小后，布局引擎对页面上所有盒子位置和大小的调整
重绘：改变了盒子的样式，却没有影响到几何属性时，会触发重绘

> **浏览器的渲染机制**
> 
> 解析HTML和CSS，生成DOM树和CSSOM树
> 将DOM树和CSSOM树结合生成渲染树
> 根据渲染树的几何信息，进行回流
> 根据回流的几何信息，得到元素的像素点
> 元素进行展示

>**输入URL后发生了什么**
>
>DNS查询对应IP地址
>向web服务器发送HTTP请求
>服务器进行处理，并返回HTTP相应
>浏览器进行解析渲染

#### 元素水平垂直居中
flex布局
grid布局，align-items、justify-content设置为center
子绝父相，上下左右设置为0，margin设置为auto

#### CSS3 和 HTML5
animation动画
transform转换
渐变
flex和grid布局
文字阴影和盒子阴影

canvas元素
webGIS的API
SEO优化的语义化元素
video和audio元素

#### CSS动画
transition变换，可以添加动画效果并控制动画的时长、生效对象、速度曲线
transform，包括平移、缩放、旋转、形变四类
animation，自定义动画，可以控制关键帧

#### 预处理器
SCSS：嵌套、变量、混入
	一般是使用scss预处理器，相比传统css，提供了嵌套的写法，便于选择器书写
	同时提供了变量，便于统一管理颜色、字体大小等样式，在具体的vue页面中可以通过@import进行导入
	还有混入，是自定义的样式代码片段，可以通过@include进行使用

#### flex布局、grid布局
flex是弹性盒子布局，可以通过flex-dirction控制主轴方向
grid是网格布局，可以通过grid-template-columns控制元素内部分为几列，以及列宽
都是通过display进行设置，都具有align-items和justify-content两个属性

两种布局都可以快速实现左右固定、中间自适应的布局
flex是在父元素上开启flex布局，左右子元素设置宽度，中间元素设置flex属性为1
grid是在父元素上开启grid布局，并设置grid-template-columns为宽度、auto、宽度
