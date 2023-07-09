---
title: CSS
categories: 样式
tags: CSS
---
## css3

### border-radius 圆角的设置

*四个值 - border-radius: 15px 50px 30px 5px;*（依次分别用于：左上角、右上角、右下角、左下角）：

### border-image 边框图像属性

border-image: 边框图像   |     在哪里裁切图像  |  定义中间部分应重复还是拉伸

```css
border-image: url(border.png) 30 round;
```

### background-image  多重背景

```css
background-image: url(flower.gif), url(paper.gif);
background-position: right bottom, left top;
background-repeat: no-repeat, repeat;
```

<span style="color:#83AE70;font-weight:700">background:url(flower.gif)  right  bottom  no-repeat ,  url(paper.gif)  left  top  repeat;</span>

**background-size 背景图像大小**  

- 长度，百分比
- contain  关键字将背景图像缩放为尽可能大的尺寸（但其宽度和高度都必须适合内容区域）。这样，取决于背景图像和背景定位区域的比例，可能存在一些未被背景图像覆盖的背景区域。
- cover 关键字会缩放背景图像，以使内容区域完全被背景图像覆盖（其宽度和高度均等于或超过内容区域）。这样，背景图像的某些部分可能在背景定位区域中不可见。

定义多个背景图像的尺寸

```css
background-size: 50px, 130px, auto;
```

**background-origin 属性** ：背景图像的位置

三个不同的值： 

1. border-box，背景图片从边框的左上角开始
2. padding-box ，从内边框边缘的左上角开始（默认）
3. content-box ， 从内容左上角开始

**background-clip 属性**  ：属性指定背景的绘制区域。

- border-box - 背景绘制到边框的外部边缘（默认）
- padding-box - 背景绘制到内边距的外边缘
- content-box - 在内容框中绘制背景



### 颜色

#### RGBA颜色

**rgba(*red*, *green*, *blue*, *alpha*)。 *alpha* 参数是介于 0.0（完全透明）和 1.0（完全不透明）之间的数字。**

#### HSL颜色

HSL 指的是色相、饱和度和亮度（Hue、Saturation 以及 Lightness）。

#### HSLA颜色

HSLA 颜色值由以下参数规定：hsla(hue, saturation, lightness, alpha)，其中 alpha 参数定义不透明度。 alpha 参数是介于 0.0（完全透明）和 1.0（完全不透明）之间的数字。

### 渐变

1. 线性渐变（向下、向上、向左、向右、对角线）
2. 径向渐变（由其中心定义）

```css
线性渐变
background-image: linear-gradient(direction, color-stop1, color-stop2, ...);
径向渐变
background-image: radial-gradient(shape size at position, start-color, ..., last-color);
```

例子：background-image: linear-gradient(to right, red , yellow);

 background-image: radial-gradient(red, yellow, green);

#### **重复线性渐变** ：repeating-linear-gradient() 函数用于重复线性渐变：

```css
background-image: repeating-linear-gradient(red, yellow 10%, green 20%);
```

#### 重复径向渐变 ：repeating-radial-gradient() 函数用于重复径向渐变：

```css
background-image: repeating-radial-gradient(red, yellow 10%, green 15%);
```

### 阴影效果

1. text-shadow
2. box-shadow

```css
text-shadow: 2px 2px 5px red;  水平阴影 垂直阴影 模糊效果 阴影颜色
text-shadow: 0 0 3px #FF0000, 0 0 5px #0000FF; 多个阴影
```

```css
box-shadow: 10px 10px 5px grey; 水平阴影 垂直阴影 模糊效果 阴影颜色
box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
```

### 文本效果 CSS 文本溢出、整字换行、换行规则以及书写模式

#### text-overflow 文字溢出

```css
overflow: hidden;
text-overflow: clip;  裁剪
text-overflow: ellipsis;  呈现省略号
```

#### word-wrap  字换行    使长文字能够被折断并换到下一行。

```css
word-wrap: break-word; 允许长单词被打断换行到下一行
```

#### word-break   换行规则  

```css
word-break: keep-all;  此行将连字符打断
word-break: break-all; 将在任何字符处中断
```

#### writing-mode  书写模式 

```css
writing-mode: horizontal-tb; 水平放置 
writing-mode: vertical-rl;  垂直放置
```

### 字体

### 2D转换

**transform 2D转换**

- translate()  `transform: translate(50px, 100px);`  从其当前位置移动元素（根据为 X 轴和 Y 轴指定的参数）
- rotate() `transform: rotate(20deg);`   根据给定的角度顺时针或逆时针旋转元素
- scaleX() 
- scaleY()
- scale() ` transform: scale(2, 3);`   增加或减少元素的大小（根据给定的宽度和高度参数）
- skewX() `transform: skewX(20deg);`  使元素沿 X 轴倾斜给定角度。
- skewY()  `transform: skewY(20deg);`  使元素沿 Y 轴倾斜给定角度。
- skew() `transform: skew(20deg, 10deg);`  使元素沿 X 和 Y 轴倾斜给定角度。
- matrix() `transform: matrix(1, -0.3, 0, 1, 0, 0);`   把所有 2D 变换方法组合为一个。

matrix(scaleX(),skewY(),skewX(),scaleY(),translateX(),translateY()) 

matrix() 方法可接受六个参数，其中包括数学函数，这些参数使您可以旋转、缩放、移动（平移）和倾斜元素。

### 3D转换

transform属性：

- rotateX()
- rotateY()
- rotateZ()



### 过渡

```css
transition: width 2s;   可设置多个值
transition: width 2s linear 1s;
```

#### 指定过渡的速度曲线

transition-timing-function 属性规定过渡效果的速度曲线。

transition-timing-function 属性可接受以下值：

- ease - 规定过渡效果，先缓慢地开始，然后加速，然后缓慢地结束（默认）
- linear - 规定从开始到结束具有相同速度的过渡效果
- ease-in -规定缓慢开始的过渡效果
- ease-out - 规定缓慢结束的过渡效果
- ease-in-out - 规定开始和结束较慢的过渡效果
- cubic-bezier(n,n,n,n) - 允许您在三次贝塞尔函数中定义自己的值

#### 延迟过渡效果

transition-delay 属性规定过渡效果的延迟（以秒计）。

#### 过渡 + 转换

```css
transition: width 2s, height 2s, transform 2s;
```

### 动画  @keyframes

- animation-duration 属性定义需要多长时间才能完成动画。
- animation-delay 属性规定动画开始的延迟时间。
- animation-iteration-count 属性指定动画应运行的次数。 <span style="color:#83AE70;font-weight:700">infinite ，使动画永远持续下去</span>
- animation-direction 属性指定是向前播放、向后播放还是交替播放动画。
  - normal - 动画正常播放（向前）。默认值
  - reverse - 动画以反方向播放（向后）
  - alternate - 动画先向前播放，然后向后
  - alternate-reverse - 动画先向后播放，然后向前
- animation-timing-function 属性规定动画的速度曲线。
  - ease - 指定从慢速开始，然后加快，然后缓慢结束的动画（默认）
  - linear - 规定从开始到结束的速度相同的动画
  - ease-in - 规定慢速开始的动画
  - ease-out - 规定慢速结束的动画
  - ease-in-out - 指定开始和结束较慢的动画
  - cubic-bezier(n,n,n,n) - 运行您在三次贝塞尔函数中定义自己的值
- animation-fill-mode 改变动画不会在第一个关键帧播放之前或在最后一个关键帧播放之后影像元素这一行为
  - none - 默认值。动画在执行之前或之后不会对元素应用任何样式。
  - forwards - 元素将保留由最后一个关键帧设置的样式值（依赖 animation-direction 和 animation-iteration-count）。
  - backwards - 元素将获取由第一个关键帧设置的样式值（取决于 animation-direction），并在动画延迟期间保留该值。
  - both - 动画会同时遵循向前和向后的规则，从而在两个方向上扩展动画属性。

```css
animation: example 5s linear 2s infinite alternate; 名称  时间  动画速度曲线  开始延迟时间  动画次数  是否反向等
```

### 工具提示

```html
<style>
/* Tooltip 容器 */
.tooltip {
  position: relative;
  display: inline-block;
  border-bottom: 1px dotted black; /* 如果需要在可悬停文本下面显示点线 */
}

/* Tooltip 文本 */
.tooltip .tooltiptext {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  padding: 5px 0;
  border-radius: 6px;
 
  /* 定位工具提示文本 - 请看下面的例子 */
  position: absolute;
  z-index: 1;
}

/* 将鼠标悬停在工具提示容器上时，显示工具提示文本 */
.tooltip:hover .tooltiptext {
  visibility: visible;
}
</style>

<div class="tooltip">Hover over me
  <span class="tooltiptext">Tooltip text</span>
</div>
```



### 图片滤镜

filter 属性把视觉效果（如模糊和饱和度）添加到元素。 Internet Explorer 或 Edge 12 不支持 filter 属性。

```css
 filter: grayscale(100%);
```

### object-fit 属性  **用于规定应如何调整 <img> 或 <video> 的大小来适应其容器。**

- fill - 默认值。调整替换后的内容大小，以填充元素的内容框。如有必要，将拉伸或挤压物体以适应该对象。
- contain - 缩放替换后的内容以保持其纵横比，同时将其放入元素的内容框。
- cover - 调整替换内容的大小，以在填充元素的整个内容框时保持其长宽比。该对象将被裁剪以适应。
- none - 不对替换的内容调整大小。
- scale-down - 调整内容大小就像没有指定内容或包含内容一样（将导致较小的具体对象尺寸）



### 多列

- column-count     该属性规定元素应被划分的列数。
- column-gap    属性规定列之间的间隔。
- column-rule-style  属性规定列之间的规则样式
- column-rule-width    属性规定列之间的规则宽度
- column-rule-color   属性规定列之间的规则的颜色
- column-rule    column-rule: 1px solid lightblue; 
- column-span   属性规定元素应跨越多少列。
- column-width   属性为列指定建议的最佳宽度。

### css在媒体查询中使用变量

```css
@media screen and (min-width: 450px) {
  .container {
    --fontsize: 50px;
  }
   :root {
    --blue: lightblue;
  }
}

@media not|only mediatype and (mediafeature and|or|not mediafeature) {
  CSS-Code;
}

```

### box-sizing   属性允许我们在元素的总宽度和高度中包括内边距（填充）和边框。

box-sizing: border-box;，则宽度和高度会包括内边距和边框 

### flexbox布局模块

父级元素

<span style="color:#83AE70;font-weight:700">display:flex</span>

- [flex-direction](https://www.w3school.com.cn/css/css3_flexbox.asp) 属性定义容器要在哪个方向上堆叠 flex 项目。
- [flex-wrap](https://www.w3school.com.cn/css/css3_flexbox.asp)   属性规定某个 flex 项目相对于其余 flex 项目将增长多少。
- [flex-flow](https://www.w3school.com.cn/css/css3_flexbox.asp)  属性是用于同时设置 flex-direction 和 flex-wrap 属性的简写属性。
- [justify-content](https://www.w3school.com.cn/css/css3_flexbox.asp)  属性有center，flex-start，flex-end， space-around ，space-between
- [align-items](https://www.w3school.com.cn/css/css3_flexbox.asp)  属性：center，flex-start，flex-end，stretch（拉伸flex项目以填充容器），baseline （使 flex 项目基线对齐）
- [align-content](https://www.w3school.com.cn/css/css3_flexbox.asp)  



#### flex-direction 属性

```css
flex-direction: column; 设置垂直堆叠 flex 项目 （从上到下）
flex-direction: column-reverse; 值垂直堆叠 flex 项目（但从下到上）
flex-direction: row; 水平堆叠 flex 项目（从左到右）
flex-direction: row-reverse;  水平堆叠 flex 项目（但从右到左）
```

#### flex-wrap 属性

```css
flex-wrap: wrap;  规定 flex 项目将在必要时进行换行
flex-wrap: nowrap;  规定将不对 flex 项目换行（默认）
flex-wrap: wrap-reverse;  定如有必要，弹性项目将以相反的顺序换行
```

#### flex-flow 属性  用于同时设置 flex-direction 和 flex-wrap 属性的简写属性

```css
flex-flow: row wrap;   
```

#### justify-content 属性

```css
justify-content: center; flex 项目在容器的中心对齐
justify-content: flex-start; 将 flex 项目在容器的开头对齐（默认）
justify-content: flex-end; 将 flex 项目在容器的末端对齐
justify-content: space-around;  显示行之前、之间和之后带有空格的 flex 项目
justify-content: space-between;  显示行之间有空格的 flex 项目 
```

#### align-items 属性

```css
align-items: center;  将 flex 项目在容器中间对齐
align-items: flex-start;  将 flex 项目在容器顶部对齐
align-items: flex-end; 将弹性项目在容器底部对齐
align-items: stretch; 拉伸 flex 项目以填充容器（默认）
align-items: baseline;   使 flex 项目基线对齐 
```

#### align-content 属性

```css
align-content: space-between;   显示的弹性线之间有相等的间距
align-content: space-around;   显示弹性线在其之前、之间和之后带有空格
align-content: stretch;   拉伸弹性线以占据剩余空间（默认）
align-content: center;   值在容器中间显示弹性线
align-content: flex-start;  值在容器开头显示弹性线
align-content: flex-end;  值在容器的末尾显示弹性线 
```

#### order 属性  可以改变 flex 项目的顺序：

```html
<div class="flex-container">
  <div style="order: 3">1</div>
  <div style="order: 2">2</div>
  <div style="order: 4">3</div> 
  <div style="order: 1">4</div>
</div>
```

#### flex-grow 属性   规定某个 flex 项目相对于其余 flex 项目将增长多少

#### flex-shrink 属性    规定某个 flex 项目相对于其余 flex 项目将收缩多少 

#### flex-basis 属性规定 flex 项目的初始长度。

#### flex 属性是 flex-grow、flex-shrink 和 flex-basis 属性的简写属性。

#### align-self 属性规定弹性容器内所选项目的对齐方式。



















