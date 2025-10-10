## CSS

#### CSS 的盒模型

HTML 中每一个元素都可以看成一个盒子，这个盒子由 margin、border、padding、content 四个部分组成

目前有两种盒模型：标准盒模型和怪异盒模型，两者的区别主要在于对元素宽高的定义。标准盒模型的宽高指 content 的宽高，怪异盒模型的宽高指 content、padding、border 三部分组合的宽高。修改盒模型的方式是通过 box-sizing 属性来控制

> **BFC 盒子**
>
> BFC 是块级格式化上下文，例如根元素、overhide 设置为 hidden scroll 等属性的元素、flex 布局的元素、块元素或者行内快元素，都可以称为 BFC 盒子，这种元素的特点是内部布局不会影响到外部布局

#### CSS 选择器的优先级

! important > 行内 > id > 类/伪类/属性 > 元素/伪元素 > 全局选择器

#### 隐藏元素的方法

display: none 不占据空间
opacity: 0 设置透明度
visibility: hidden 占据空间位置

#### px、rem、em、视口单位

px：绝对单位
em：相对于父元素的字体大小
rem：相对于根元素的字体大小，一般将 HTML 元素的 font-size 设置为 62.5%，1rem 就是 10px，便于计算
vh、vw：视口单位，相对于视口的宽高

> **响应式设计**
>
> 一般使用媒体查询，在几个特定的尺寸上，对 html 的字体大小进行控制，同时对页面中的字体大小、宽高等使用 rem，实现响应式布局
> 或者通过 JS，添加 resize 事件监听，动态调整 font-size
> 还可以通过 elementPlus 的栅格系统实现响应式布局

#### 重绘、回流

回流：修改了盒子的位置大小后，布局引擎对页面上所有盒子位置和大小的调整
重绘：改变了盒子的样式，却没有影响到几何属性时，会触发重绘

> **浏览器的渲染机制**
>
> 解析 HTML 和 CSS，生成 DOM 树和 CSSOM 树
> 将 DOM 树和 CSSOM 树结合生成渲染树
> 根据渲染树的几何信息，进行回流
> 根据回流的几何信息，得到元素的像素点
> 元素进行展示

> **输入 URL 后发生了什么**
>
> DNS 查询对应 IP 地址
> 向 web 服务器发送 HTTP 请求
> 服务器进行处理，并返回 HTTP 相应
> 浏览器进行解析渲染

#### 元素水平垂直居中

flex 布局
grid 布局，align-items、justify-content 设置为 center
子绝父相，上下左右设置为 0，margin 设置为 auto

#### CSS3 和 HTML5

animation 动画
transform 转换
渐变
flex 和 grid 布局
文字阴影和盒子阴影

canvas 元素
webGIS 的 API
SEO 优化的语义化元素
video 和 audio 元素

#### CSS 动画

transition 变换，可以添加动画效果并控制动画的时长、生效对象、速度曲线
transform，包括平移、缩放、旋转、形变四类
animation，自定义动画，可以控制关键帧

#### 预处理器

SCSS：嵌套、变量、混入
一般是使用 scss 预处理器，相比传统 css，提供了嵌套的写法，便于选择器书写
同时提供了变量，便于统一管理颜色、字体大小等样式，在具体的 vue 页面中可以通过@import 进行导入
还有混入，是自定义的样式代码片段，可以通过@include 进行使用

#### flex 布局、grid 布局

flex 是弹性盒子布局，可以通过 flex-dirction 控制主轴方向
grid 是网格布局，可以通过 grid-template-columns 控制元素内部分为几列，以及列宽
都是通过 display 进行设置，都具有 align-items 和 justify-content 两个属性

两种布局都可以快速实现左右固定、中间自适应的布局
flex 是在父元素上开启 flex 布局，左右子元素设置宽度，中间元素设置 flex 属性为 1
grid 是在父元素上开启 grid 布局，并设置 grid-template-columns 为宽度、auto、宽度
