---
title: SVG
categories: 样式
tags: SVG标签
---

# SVG标签

## 一、SVG的简介

## 二、SVG的基本形状
### (1)、矩形 rect
```html
x 左上角x位置，y 左上角y位置，rx 圆角x方位的半径 ，ry 圆角y方位的半径， width 宽度， height 高度
<rect x="10" y="10" width="30" height="30"/>
<rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>

```
### (2)、圆形 circle
```html
r 圆的半径, cx 圆心的x位置, cy 圆心的y位置,
<circle cx="25" cy="75" r="20"/>
```
### (3)、椭圆 ellipse
```html
rx
椭圆的x半径
ry
椭圆的y半径
cx
椭圆中心的x位置
cy
椭圆中心的y位置
<ellipse cx="75" cy="75" rx="20" ry="5"/>
```
### (4)、线条 line
```html
x1
起点的x位置
y1
起点的y位置
x2
终点的x位置
y2
终点的y位置
<line x1="10" x2="50" y1="110" y2="150"/>
```
### (5)、折线 polyline
```html
points 的属性值是由n个点的x坐标和y坐标组合组合成
<polyline points="60 110, 65 120, 70 115, 75 130, 80 125, 85 140, 90 135, 95 150, 100 145"/>
```
### (6)、多边形 polygon
```html
和折线的属性值一样，只是在最后一个坐标后，会自动闭合到第一个坐标，形成闭合形状
<polygon points="50 160, 55 180, 70 180, 60 190, 65 205, 50 195, 35 205, 40 190, 30 180, 45 180"/>
```

### (7)、路径 path
> d （一个点集数列）的属性值 是一个“命令 + 参数 ” 序列

#### 命令包含有

1. `M` 直线命令（动画笔命令） （move to） 大写表示绝对定位  小写表示相对定位  M 只是移动画笔 ，并不画线 经常出现在开始画笔的那个点
2. `L` 画线命令  （Line to）线画到某个点上
3. `H` 绘制水平线 标明在x轴 <span style="color:red">移动到</span> 的位置
4. `V` 绘制垂直线 标明在y轴<span style="color:red">移动到</span> 的位置
5. `Z` 闭合路径命令  Z命令会从当前点画一条直线到路径的起点
    **曲线命令：绘制平滑曲线的命令有三个，其中两个用来绘制贝塞尔曲线，另外一个用来绘制弧形或者说是圆的一部分。**
6. `C` 曲线命令  （三次贝塞尔曲线）  C x1 y1, x2 y2, x y (or c dx1 dy1, dx2 dy2, dx dy) 第一个坐标是起点的控制点，第二个坐标是终点的控制点 第三个坐标是终点坐标 有一个`S` 命令 ，可以延长
   - `S` 曲线 （简写贝塞尔曲线命令）  S x2 y2, x y (or s dx2 dy2, dx dy) 如果S命令跟在一个C或S命令后面，则它的第一个控制点会被假设成前一个命令曲线的第二个控制点的中心对称点。如果S命令单独使用，前面没有C或S命令，那当前点将作为第一个控制点。
7. `Q` 曲线命令 （二次贝塞尔曲线） 只需要一个控制点  Q x1 y1, x y (or q dx1 dy1, dx dy)
   - `T` Q的延长命令  T x y (or t dx dy) <span style="color:red"> 命令前面必须是一个Q命令，或者是另一个T命令</span>，才能达到这种效果。如果T单独使用，那么控制点就会被认为和终点是同一个点，所以画出来的将是一条直线。
8. `A` 弧形命令  A rx ry x-axis-rotation large-arc-flag sweep-flag x y 或者 a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy 
    - rx ry是长轴和短轴半径
    - x-axis-rotation x轴旋转角度
    - large-arc-flag 决定弧线是大于还是小于180度，0表示小角度弧，1表示大角度弧
    - sweep-flag 弧线的方向，0表示从起点到终点沿逆时针画弧，1表示从起点到终点沿顺时针画弧

``` html
<path d="M 20 230 Q 40 205, 50 230 T 90230"/>
<path d="M10 10 h 80 v 80 h -80 Z" fill="transparent" stroke="black"/>
<path d="M130 110 C 120 140, 180 140, 170 110" stroke="black" fill="transparent"/>
S的第一个控制是以（95,80）这个中心对称的（65,10）坐标的对称点
<path d="M10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80" stroke="black" fill="transparent"/>
<path d="M10 80 Q 95 10 180 80" stroke="black" fill="transparent"/>
<path d="M10 80 Q 52.5 10, 95 80 T 180 80" stroke="black" fill="transparent"/>

起点M(80,80) 半径45 没有旋转角度 小角弧 逆时针 终点(125,125) 从终点画直线到(125,80) Z闭合图形
<path d="M80 80 A 45 45, 0, 0, 0, 125 125 L 125 80 Z" fill="green"/>

```

### (8)、填充和边框 Fill 和 Stroke 属性

  1. fill属性设置对象内部的颜色
  2. stroke属性设置绘制对象的线条的颜色 （类似边框的颜色）
  3. fill-opacity控制填充色的不透明度
  4. stroke-opacity控制描边的不透明度
  5. stroke-width属性定义了描边的宽度
  6. stroke-linecap 控制边框终点的形状  有三个值
     -  butt用直边结束线段
     -  square的效果差不多，但是会稍微超出实际路径的范围，超出的大小由stroke-width控制
     -  round表示边框的终点是圆角，圆角的半径也是由stroke-width控制的
  7. stroke-linejoin 控制两条描边线段之间，用什么方式连接
     -  miter 尖角
     -  round 圆角
     -  bevel 斜解
  8. stroke-dasharray 虚线描边 stroke-dasharray="5,10,5"  或 stroke-dasharray="5,5" 格式
        - 第一个例子指定了3个数字，这种情况下，数字会循环两次，形成一个偶数的虚线模式（奇数个循环两次变偶数个）。所以该路径首先渲染5个填色单位，10个空白单位，5个填色单位，然后回头以这3个数字做一次循环，但是这次是创建5个空白单位，10个填色单位，5个空白单位。通过这两次循环得到偶数模式，并将这个偶数模式不断重复。
        - 第二个用来表示非填色区域的长度。所以在上面的例子里，第二个路径会先做5个像素单位的填色，紧接着是5个空白单位，然后又是5个单位的填色。如果你想要更复杂的虚线模式，你可以定义更多的数字。
  9. fill-rule，用于定义如何给图形重叠的区域上色
  10. stroke-miterlimit，定义什么情况下绘制或不绘制边框连接的miter效果
  11. stroke-dashoffset，定义虚线开始的位置

## 三、使用css

 样式放到defs标签内 以及引入外部的css
 ``` html
<?xml version="1.0" standalone="no"?>
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <style type="text/css"><![CDATA[
       #MyRect {
         stroke: black;
         fill: red;
       }
    ]]></style>
  </defs>
  <rect x="10" height="180" y="10" width="180" id="MyRect"/>
</svg>


<?xml version="1.0" standalone="no"?>
<?xml-stylesheet type="text/css" href="style.css"?>

<svg width="200" height="150" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect height="10" width="10" id="MyRect"/>
</svg>
 ```

 ## 四、 渐变

两种渐变都有一个叫做 gradientUnits（渐变单元）的属性
  - userSpaceOnUse 
  - objectBoundingBox 默认值 

 ### (1)、线性渐变    linearGradient
  在defs元素内部，创建一个<linearGradient> 节点
```html
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <linearGradient id="Gradient1">
        <stop class="stop1" offset="0%"/>
        <stop class="stop2" offset="50%"/>
        <stop class="stop3" offset="100%"/>
      </linearGradient>
      <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="50%" stop-color="black" stop-opacity="0"/>
        <stop offset="100%" stop-color="blue"/>
      </linearGradient>
      <style type="text/css"><![CDATA[
        #rect1 { fill: url(#Gradient1); }
        .stop1 { stop-color: red; }
        .stop2 { stop-color: black; stop-opacity: 0; }
        .stop3 { stop-color: blue; }
      ]]></style>
  </defs>

  <rect id="rect1" x="10" y="10" rx="15" ry="15" width="100" height="100"/>
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#Gradient2)"/>

</svg>
```
linearGradient 中有几个stop节点 ，offset 指定位置的偏移 stop-color 指定位置上的渐变颜色  
x1="0" x2="0" y1="0" y2="1" 这些属性定义了渐变路线走向

xlink:href属性 一个渐变的属性和颜色中值（stop）可以被另一个渐变包含引用

```html
 <linearGradient id="Gradient1">
   <stop id="stop1" offset="0%"/>
   <stop id="stop2" offset="50%"/>
   <stop id="stop3" offset="100%"/>
 </linearGradient>
 <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1"
    xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#Gradient1"/>
```
### (2)、径向渐变   radialGradient
```html
<?xml version="1.0" standalone="no"?>
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <radialGradient id="RadialGradient1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
      <radialGradient id="RadialGradient2" cx="0.25" cy="0.25" r="0.25">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>

  <rect x="10" y="10" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient1)"/>
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#RadialGradient2)"/>

</svg>
```

**<span style="color:red">径向渐变有一个中心和焦点 中心点：cx 和cy 焦点 ：fx 和fy 中心点描述渐变的边缘 ， 焦点描述渐变的中心</span>**
**<span style="color:red">径向渐变有一个属性：spreadMethod</span>**
    该属性有三个值
  - pad  渐变到终点，以最终偏移颜色填充剩余部分
  - reflect 渐变到终点，反向渐变 即从100%的颜色到0%的颜色渐变
  - repeat 渐变到终点，又重复渐变 即从0%的颜色到100%的颜色渐变



```html
<?xml version="1.0" standalone="no"?>

<svg width="120" height="120" version="1.1"
  xmlns="http://www.w3.org/2000/svg">
  <defs>
      <radialGradient id="Gradient"
            cx="0.5" cy="0.5" r="0.5" fx="0.25" fy="0.25">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>

  <rect x="10" y="10" rx="15" ry="15" width="100" height="100"
        fill="url(#Gradient)" stroke="black" stroke-width="2"/>

  <circle cx="60" cy="60" r="50" fill="transparent" stroke="white" stroke-width="2"/>
  <circle cx="35" cy="35" r="2" fill="white" stroke="white"/>
  <circle cx="60" cy="60" r="2" fill="white" stroke="white"/>
  <text x="38" y="40" fill="white" font-family="sans-serif" font-size="10pt">(fx,fy)</text>
  <text x="63" y="63" fill="white" font-family="sans-serif" font-size="10pt">(cx,cy)</text>

</svg>



```

## 五、图案 Patterns

>patters 上的属性：
  - width 和height （图案之前的距离） 用户描述在重复下一个图案之前应该跨过多远
  - x 和 y 是开始 的位置
  - patternUnits 属性单元 属性值有 objectBoundingBox（默认值）
  - patternContentUnits 描述了pattern元素基于基本形状使用的单元系统，这个属性默认值为userSpaceOnUse 与patternUnits属性相反 


```html
<?xml version="1.0" standalone="no"?>
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <linearGradient id="Gradient1">
      <stop offset="5%" stop-color="white"/>
      <stop offset="95%" stop-color="blue"/>
    </linearGradient>
    <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
      <stop offset="5%" stop-color="red"/>
      <stop offset="95%" stop-color="orange"/>
    </linearGradient>

    <pattern id="Pattern" x="0" y="0" width=".25" height=".25">
      <rect x="0" y="0" width="50" height="50" fill="skyblue"/>
      <rect x="0" y="0" width="25" height="25" fill="url(#Gradient2)"/>
      <circle cx="25" cy="25" r="20" fill="url(#Gradient1)" fill-opacity="0.5"/>
    </pattern>

  </defs>

  <rect fill="url(#Pattern)" stroke="black" x="0" y="0" width="200" height="200"/>
</svg>
```
## 六、text

>属性：
  - x 和 y 是文本在视口中的位置
  - text-anchor 文本流的方向 ： 属性值有：start ，middle ，end ，inherit
  - fil 填充颜色
  - stroke 描边 
  - 设置字体属性  font-family、font-style、font-weight、font-variant、font-stretch、font-size、font-size-adjust、kerning、letter-spacing、word-spacing和text-decoration

### 相关的子元素 tspan
>属性 ：
  - x 设置绝对 x 坐标 数列
  - dx 从当前位置，用一个水平偏移开始绘制文本
  - y
  - dy
  - rotate 旋转角度
  - textLength ？
### 相关的子元素 tref
> 属性：
  - xlink:href 指向一个元素

### 相关的子元素 textPath
> 属性：
  - xlink:href 取得一个任意路径 把字符对齐到路径 字体会环绕路径，顺着路径走

```html
tspan
<text x="10" y="10">Hello World!</text>
<text>
  <tspan font-weight="bold" fill="red">This is bold and red</tspan>
</text>

tref
<text id="example">This is an example text.</text>

<text>
    <tref xlink:href="#example" />
</text>
textPath
<path id="my_path" d="M 20,20 C 40,40 80,40 100,20" fill="transparent" />
<text>
  <textPath xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#my_path">
    This text follows a curve.
  </textPath>
</text>

```

## 七、基础变形 g <transform ,所有变形都是通过该属性变换的>

#### (1)、平移 translate()
transform="translate(30,40) 表示移动到点(30,40)

#### (2)、旋转 
transform="rotate(45)" 

```html
<g fill="red">
  <rect x="0" y="0" width="10" height="10" />
  <rect x="20" y="0" width="10" height="10" />
  <rect x="0" y="0" width="10" height="10" transform="translate(30,40)" />

</g>

```
#### (3)、斜切  skewX() skewY()

#### (4)、缩放 scale()

#### (5)、用matrix()实现复杂变形

#### (6)、SVG嵌在SVG内部


## 八、剪切和遮罩

### (1)、Clipping <Clipping用来移除在别处定义的元素的部分内容。在这里，任何半透明效果都是不行的。它只能要么显示要么不显示。>

```html
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <clipPath id="cut-off-bottom">
      <rect x="0" y="0" width="200" height="100" />
    </clipPath>
  </defs>

  <circle cx="100" cy="100" r="100" clip-path="url(#cut-off-bottom)" />
</svg>

```

### (2)、Masking  <Masking允许使用透明度和灰度值遮罩计算得的软边缘。>
```html
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <linearGradient id="Gradient">
      <stop offset="0" stop-color="white" stop-opacity="0" />
      <stop offset="1" stop-color="white" stop-opacity="1" />
    </linearGradient>
    <mask id="Mask">
      <rect x="0" y="0" width="200" height="200" fill="url(#Gradient)"  />
    </mask>
  </defs>

  <rect x="0" y="0" width="200" height="200" fill="green" />
  <rect x="0" y="0" width="200" height="200" fill="red" mask="url(#Mask)" />
</svg>

```
### (3)、用opacity定义透明度
```html
<rect x="0" y="0" width="100" height="100" opacity=".5" />

```

## 九、嵌入光栅图像
image 属性：支持PNG、JPG和SVG格式
```html
<svg version="1.1"
     xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
     width="200" height="200">
  <image x="90" y="-65" width="128" height="146" transform="rotate(45)"
     xlink:href="https://developer.mozilla.org/static/img/favicon144.png"/>
</svg>
```
## 十、嵌入XML 。foreignObject 的使用

### foreignObject 元素允许包含不同的XML命名空间元素。
> 属性有：
 - height 和width 
 - x 和 y 坐标
 - 

```html
<svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
  <style>
    polygon { fill: black }

    div {
      color: white;
      font:18px serif;
      height: 100%;
      overflow: auto;
    }
  </style>

  <polygon points="5,5 195,10 185,185 10,195" />

  <!-- Common use case: embed HTML text into SVG -->
  <foreignObject x="20" y="20" width="160" height="160">
    <!--
      In the context of SVG embeded into HTML, the XHTML namespace could
      be avoided, but it is mandatory in the context of an SVG document
    -->
    <div xmlns="http://www.w3.org/1999/xhtml">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit.
      Sed mollis mollis mi ut ultricies. Nullam magna ipsum,
      porta vel dui convallis, rutrum imperdiet eros. Aliquam
      erat volutpat.
    </div>
  </foreignObject>
</svg>
```

## 十一、滤镜效果  Filter 
> Filter 是SVG中创建复杂效果的一种机制
> Filter 是置于defs中

 ###  feGaussianBlur



```html
<svg width="250" viewBox="0 0 200 85"
     xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <!-- Filter declaration -->
    <filter id="MyFilter" filterUnits="userSpaceOnUse"
            x="0" y="0"
            width="200" height="120">

      <!-- offsetBlur -->
      <feGaussianBlur in="SourceAlpha" stdDeviation="4" result="blur"/>
      <feOffset in="blur" dx="4" dy="4" result="offsetBlur"/>

      <!-- litPaint -->
      <feSpecularLighting in="blur" surfaceScale="5" specularConstant=".75"
                          specularExponent="20" lighting-color="#bbbbbb"
                          result="specOut">
        <fePointLight x="-5000" y="-10000" z="20000"/>
      </feSpecularLighting>
      <feComposite in="specOut" in2="SourceAlpha" operator="in" result="specOut"/>
      <feComposite in="SourceGraphic" in2="specOut" operator="arithmetic"
                   k1="0" k2="1" k3="1" k4="0" result="litPaint"/>

      <!-- merge offsetBlur + litPaint -->
      <feMerge>
        <feMergeNode in="offsetBlur"/>
        <feMergeNode in="litPaint"/>
      </feMerge>
    </filter>
  </defs>

  <!-- Graphic elements -->
  <g filter="url(#MyFilter)">
      <path fill="none" stroke="#D90000" stroke-width="10"
            d="M50,66 c-50,0 -50,-60 0,-60 h100 c50,0 50,60 0,60z" />
      <path fill="#D90000"
            d="M60,56 c-30,0 -30,-40 0,-40 h80 c30,0 30,40 0,40z" />
      <g fill="#FFFFFF" stroke="black" font-size="45" font-family="Verdana" >
        <text x="52" y="52">SVG</text>
      </g>
  </g>
</svg>

```









https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial

