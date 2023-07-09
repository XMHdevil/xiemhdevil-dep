---
title: Canvas
categories: 样式
tags: 动画
---
## Canvas

> Canvas 标签只有两个属性：
>  width 和 height
> 初始化宽度为300 高度为150
> <canvas>元素与<img>标签的不同之处在于，就像<video>，<audio>，或者 <picture>元素一样，很容易定义一些替代内容。

```html

<canvas id="tutorial" width="150" height="150"></canvas>


<html>
 <head>
  <script type="application/javascript">
    function draw() {
      var canvas = document.getElementById("canvas");
      if (canvas.getContext) {
        var ctx = canvas.getContext("2d");

        ctx.fillStyle = "rgb(200,0,0)";
        ctx.fillRect (10, 10, 55, 50);

        ctx.fillStyle = "rgba(0, 0, 200, 0.5)";
        ctx.fillRect (30, 30, 55, 50);
      }
    }
  </script>
 </head>
 <body onload="draw();">
   <canvas id="canvas" width="150" height="150"></canvas>
 </body>
</html>

```
## 一、使用canvas来绘制图形

> 和SVG不同的是，canvas只有两种形式绘制图形：矩形和路径

### (1)、绘制矩形
> 三种方法绘制矩形
    1. fillRect(x, y, width, height) 绘制一个填充的矩形
    2. strokeRect(x, y, width, height) 绘制一个矩形的边框
    3. clearRect(x, y, width, height) 清除指定矩形区域，让清除部分完全透明。

### (2)、绘制路径
  创建路径起点 ----> 调用绘制路径的函数 ----> 封闭路径  --->  填充
  1. beginPath() 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。
  2. closePath() 闭合路径之后图形绘制命令又重新指向到上下文中。
  3. stroke() 通过线条来绘制图形轮廓。使用描边则不会闭合路径
  4. fill() 通过填充路径的内容区域生成实心的图形。
   
  - moveTo(x,y) 绘制的起点
  - lineTo(x,y) 绘制直线
  - arc arc(x, y, radius, startAngle, endAngle, anticlockwise) 绘制圆弧 x,y是圆心坐标 ，radius是半径，startAngle开始弧度，endAngle 结束弧度 ，`弧度=(Math.PI/180)*角度,三点时刻是0°的角度`anticlockwise 属性值为 true则是逆时针，属性值为false 则是顺时针
  - arcTo arcTo(x1, y1, x2, y2, radius)  两端的坐标和半径
  - quadraticCurveTo(cp1x, cp1y, x, y) 绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点。
  - bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y) 绘制三次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。
  - rect(x, y, width, height) 绘制一个左上角坐标为（x,y），宽高为width以及height的矩形。
#### 绘制一个三角形
```js
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    ctx.moveTo(75, 50);
    ctx.lineTo(100, 75);
    ctx.lineTo(100, 25);
    ctx.fill();
  }
}
```
#### 绘制一个圆形圆弧
```js
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext){
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    ctx.arc(75, 75, 50, 0, Math.PI * 2, true); // 绘制
    ctx.moveTo(110, 75);
    ctx.arc(75, 75, 35, 0, Math.PI, false);   // 口(顺时针)
    ctx.moveTo(65, 65);
    ctx.arc(60, 65, 5, 0, Math.PI * 2, true);  // 左眼
    ctx.moveTo(95, 65);
    ctx.arc(90, 65, 5, 0, Math.PI * 2, true);  // 右眼
    ctx.stroke();
  }
}

function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext){
    var ctx = canvas.getContext('2d');

    for(var i = 0; i < 4; i++){
      for(var j = 0; j < 3; j++){
        ctx.beginPath();
        var x = 25 + j * 50; // x 坐标值
        var y = 25 + i * 50; // y 坐标值
        var radius = 20; // 圆弧半径
        var startAngle = 0; // 开始点
        var endAngle = Math.PI + (Math.PI * j) / 2; // 结束点
        var anticlockwise = i % 2 == 0 ? false : true; // 顺时针或逆时针

        ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise);

        if (i>1){
          ctx.fill();
        } else {
          ctx.stroke();
        }
      }
    }
  }
}


```


#### 二次贝塞尔曲线及三次贝塞尔曲线
```js
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    // 二次贝塞尔曲线
    ctx.beginPath();
    ctx.moveTo(75, 25);
    ctx.quadraticCurveTo(25, 25, 25, 62.5);
    ctx.quadraticCurveTo(25, 100, 50, 100);
    ctx.quadraticCurveTo(50, 120, 30, 125);
    ctx.quadraticCurveTo(60, 120, 65, 100);
    ctx.quadraticCurveTo(125, 100, 125, 62.5);
    ctx.quadraticCurveTo(125, 25, 75, 25);
    ctx.stroke();
   }
}

function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext){
    var ctx = canvas.getContext('2d');

     //三次贝塞尔曲线
    ctx.beginPath();
    ctx.moveTo(75, 40);
    ctx.bezierCurveTo(75, 37, 70, 25, 50, 25);
    ctx.bezierCurveTo(20, 25, 20, 62.5, 20, 62.5);
    ctx.bezierCurveTo(20, 80, 40, 102, 75, 120);
    ctx.bezierCurveTo(110, 102, 130, 80, 130, 62.5);
    ctx.bezierCurveTo(130, 62.5, 130, 25, 100, 25);
    ctx.bezierCurveTo(85, 25, 75, 37, 75, 40);
    ctx.fill();
  }
}

```

### (3)、Path2D 对象
 > 记录绘制路径，封存路径，多次使用
 >还可以使用 SVG paths

```js
new Path2D();     // 空的Path对象
new Path2D(path); // 克隆Path对象
new Path2D(d);    // 从SVG建立Path对象

function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext){
    var ctx = canvas.getContext('2d');

    var rectangle = new Path2D();
    rectangle.rect(10, 10, 50, 50);

    var circle = new Path2D();
    circle.moveTo(125, 35);
    circle.arc(100, 35, 25, 0, 2 * Math.PI);

    ctx.stroke(rectangle);
    ctx.fill(circle);
  }
}

// 复用SVG里面的路径 M10 10 是起点， h 80 是右移动80 v 80 是下移动80 ，h -80 左移动 80 Z 回到起点
var p = new Path2D("M10 10 h 80 v 80 h -80 Z");

```

## 二、使用样式和颜色
> 给绘制的图形上色 主要有两个属性：
> fillStyle 和 strokeStyle  fillStyle是设置填充的颜色 ， strokeStyle是设置轮廓的颜色


```js
// 这些 fillStyle 的值均为 '橙色'
ctx.fillStyle = "orange";
ctx.fillStyle = "#FFA500";
ctx.fillStyle = "rgb(255,165,0)";
ctx.fillStyle = "rgba(255,165,0,1)";

```

### (1)、透明度Transparency
> 通过设置globalAlpha属性或者使用一个半透明颜色作为轮廓或填充的样式

```js
// 指定透明颜色，用于描边和填充样式
ctx.strokeStyle = "rgba(255,0,0,0.5)";
ctx.fillStyle = "rgba(255,0,0,0.5)";

function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  // 画背景
  ctx.fillStyle = '#FD0';
  ctx.fillRect(0,0,75,75);
  ctx.fillStyle = '#6C0';
  ctx.fillRect(75,0,75,75);
  ctx.fillStyle = '#09F';
  ctx.fillRect(0,75,75,75);
  ctx.fillStyle = '#F30';
  ctx.fillRect(75,75,75,75);
  ctx.fillStyle = '#FFF';

  // 设置透明度值
  ctx.globalAlpha = 0.2;

  // 画半透明圆
  for (var i=0;i<7;i++){
      ctx.beginPath();
      ctx.arc(75,75,10+10*i,0,Math.PI*2,true);
      ctx.fill();
  }
}

function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  // 画背景
  ctx.fillStyle = 'rgb(255,221,0)';
  ctx.fillRect(0,0,150,37.5);
  ctx.fillStyle = 'rgb(102,204,0)';
  ctx.fillRect(0,37.5,150,37.5);
  ctx.fillStyle = 'rgb(0,153,255)';
  ctx.fillRect(0,75,150,37.5);
  ctx.fillStyle = 'rgb(255,51,0)';
  ctx.fillRect(0,112.5,150,37.5);

  // 画半透明矩形
  for (var i=0;i<10;i++){
    ctx.fillStyle = 'rgba(255,255,255,'+(i+1)/10+')';
    for (var j=0;j<4;j++){
      ctx.fillRect(5+i*14,5+j*37.5,14,27.5)
    }
  }
}

```

### (2)、线型 Line styles
  1. `lineWidth = value` 线的宽度
  2. `lineCap = type`  线末端样式 
      - butt 一条直线 
      - round 凸出的半圆
      - square 端点处加上了等宽且高度为一半线宽的方块
  3. `lineJoin = type` 线与线之间的接合处的样式
      - round 圆角
      - bevel 直线
      - miter 尖角
  4. `miterLimit = value`  限制当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。
      - 被等效定义为线条内外连接点距离（miterLength）与线宽（lineWidth）的最大允许比值（因为路径点是内外连接点的中点）
  5. `getLineDash()` 返回一个包含当前虚线样式，长度为非负偶数的数组。
  6. `setLineDash(segments)`设置当前虚线样式。
      - setLineDash 方法接受一个数组 ，来指定线段与间隙的交替
  7. `lineDashOffset = value` 设置虚线样式的起始偏移量。

```js
// lineCap属性
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  var lineCap = ['butt','round','square'];

  // 创建路径
  ctx.strokeStyle = '#09f';
  ctx.beginPath();
  ctx.moveTo(10,10);
  ctx.lineTo(140,10);
  ctx.moveTo(10,140);
  ctx.lineTo(140,140);
  ctx.stroke();

  // 画线条
  ctx.strokeStyle = 'black';
  for (var i=0;i<lineCap.length;i++){
    ctx.lineWidth = 15;
    ctx.lineCap = lineCap[i];
    ctx.beginPath();
    ctx.moveTo(25+i*50,10);
    ctx.lineTo(25+i*50,140);
    ctx.stroke();
  }
}

// 使用虚线 --- 基本动画
var ctx = document.getElementById('canvas').getContext('2d');
var offset = 0;

function draw() {
  ctx.clearRect(0,0, canvas.width, canvas.height);
  ctx.setLineDash([4, 2]);
  ctx.lineDashOffset = -offset;
  ctx.strokeRect(10,10, 100, 100);
}

function march() {
  offset++;
  if (offset > 16) {
    offset = 0;
  }
  draw();
  setTimeout(march, 20);
}

march();


```

### (3)、渐变 Gradients 
> 有线性或者径向渐变 来填充或描边
>  1. createLinearGradient(x1, y1, x2, y2) createLinearGradient 方法接受 4 个参数，表示渐变的起点 (x1,y1) 与终点 (x2,y2)。
>  2. createRadialGradient(x1, y1, r1, x2, y2, r2) createRadialGradient 方法接受 6 个参数，前三个定义一个以 (x1,y1) 为原点，半径为 r1 的圆，后三个参数则定义另一个以 (x2,y2) 为原点，半径为 r2 的圆。
>  3. gradient.addColorStop(position, color) addColorStop 方法接受 2 个参数，position 参数必须是一个 0.0 与 1.0 之间的数值，表示渐变中颜色所在的相对位置。例如，0.5 表示颜色会出现在正中间。color 参数必须是一个有效的 CSS 颜色值（如 #FFF， rgba(0,0,0,1)，等等）。



```js
var lineargradient = ctx.createLinearGradient(0,0,150,150);
var radialgradient = ctx.createRadialGradient(75,75,0,75,75,100);

var lineargradient = ctx.createLinearGradient(0,0,150,150);
lineargradient.addColorStop(0,'white');
lineargradient.addColorStop(1,'black');


```

### (4)、图案样式 Patterns
>  
>  1. createPattern(image, type) 该方法接受两个参数。Image 可以是一个 Image 对象的引用，或者另一个 canvas 对象。Type 必须是下面的字符串值之一：repeat，repeat-x，repeat-y 和 no-repeat。

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  // 创建新 image 对象，用作图案
  var img = new Image();
  img.src = 'https://mdn.mozillademos.org/files/222/Canvas_createpattern.png';
  img.onload = function() {

    // 创建图案
    var ptrn = ctx.createPattern(img, 'repeat');
    ctx.fillStyle = ptrn;
    ctx.fillRect(0, 0, 150, 150);

  }
}

```

### (5)、阴影 Shadows

> 1. `shadowOffsetX = float`
shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离，它们是不受变换矩阵所影响的。负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0。
> 2. `shadowOffsetY = float`
shadowOffsetX 和 shadowOffsetY 用来设定阴影在 X 和 Y 轴的延伸距离，它们是不受变换矩阵所影响的。负值表示阴影会往上或左延伸，正值则表示会往下或右延伸，它们默认都为 0。
> 3. `shadowBlur = float`
shadowBlur 用于设定阴影的模糊程度，其数值并不跟像素数量挂钩，也不受变换矩阵的影响，默认为 0。
> 4. `shadowColor = color`
shadowColor 是标准的 CSS 颜色值，用于设定阴影颜色效果，默认是全透明的黑色。

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  ctx.shadowOffsetX = 2;
  ctx.shadowOffsetY = 2;
  ctx.shadowBlur = 2;
  ctx.shadowColor = "rgba(0, 0, 0, 0.5)";

  ctx.font = "20px Times New Roman";
  ctx.fillStyle = "Black";
  ctx.fillText("Sample String", 5, 30);
}

```

### (6)、Canvas填充规则 fill
  两个值：
> `nonzero`  
> `evenodd`

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  ctx.beginPath();
  ctx.arc(50, 50, 30, 0, Math.PI*2, true);
  ctx.arc(50, 50, 15, 0, Math.PI*2, true);
  ctx.fill("evenodd");
}

```
## 三、绘制文本
> 渲染文本有两种方法
> 1. `fillText(text, x, y[, maxWidth])` 在指定的(x,y)位置填充指定的文本，绘制的最大宽度是可选的
> 2. `strokeText(text, x, y [, maxWidth])` 在指定的(x,y)位置绘制文本边框，绘制的最大宽度是可选的

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  ctx.font = "48px serif";
  ctx.strokeText("Hello world", 10, 50);
}
```
### (1)、有样式的文本
  1. font = value 默认值是 10px sans-serif
  2. textAlign = value 文本对齐选项
      - start 默认值
      - end
      - left
      - right
      - center
  3. textBaseline = value 基线对齐选项 
      - top
      - hanging
      - middle
      - alphabetic 默认值
      - ideographic
      - bottom
  4. direction = value
      - ltr
      - rtl
      - inherit 默认值

### (2)、预测量文本宽度
  1. measureText() 将返回一些TextMetrics对象的宽度、所在像素，这些提现文本特性的属性。
...... 等等


## 四、使用图像

HTMLImageElement
这些图片是由Image()函数构造出来的，或者任何的<img>元素
HTMLVideoElement
用一个HTML的 <video>元素作为你的图片源，可以从视频中抓取当前帧作为一个图像
HTMLCanvasElement
可以使用另一个 <canvas> 元素作为你的图片源。
ImageBitmap
这是一个高性能的位图，可以低延迟地绘制，它可以从上述的所有源以及其它几种源中生成。

详细看文档

## 五、变形 Transformations
> 两个在开始绘制复杂图形时必不可少的方法
>   1. `save() ` 保存画布的所有状态
>   2. `restore()` 恢复canvas状态

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  ctx.fillRect(0,0,150,150);   // 使用默认设置绘制一个矩形
  ctx.save();                  // 保存默认状态

  ctx.fillStyle = '#09F'       // 在原有配置基础上对颜色做改变
  ctx.fillRect(15,15,120,120); // 使用新的设置绘制一个矩形

  ctx.save();                  // 保存当前状态
  ctx.fillStyle = '#FFF'       // 再次改变颜色配置
  ctx.globalAlpha = 0.5;
  ctx.fillRect(30,30,90,90);   // 使用新的配置绘制一个矩形

  ctx.restore();               // 重新加载之前的颜色状态
  ctx.fillRect(45,45,60,60);   // 使用上一次的配置绘制一个矩形

  ctx.restore();               // 加载默认颜色配置
  ctx.fillRect(60,60,30,30);   // 使用加载的配置绘制一个矩形
}

```

### (1)、移动Translating
  `translate(x,y)`  x 为左右偏移量 y 为上下偏移量
   调用restore方法比手动恢复原先的状态要简单得多。

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  for (var i = 0; i < 3; i++) {
    for (var j = 0; j < 3; j++) {
      ctx.save();
      ctx.fillStyle = 'rgb(' + (51 * i) + ', ' + (255 - 51 * i) + ', 255)';
      ctx.translate(10 + j * 50, 10 + i * 50);
      ctx.fillRect(0, 0, 25, 25);
      ctx.restore();
    }
  }
}

```

### (2)、旋转Rotating
> 以原点中心旋转canvas
  `rotate(angle)` 画圆  angle 为旋转角度，它是一个顺时针方向，以弧度为单位的值

```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  ctx.translate(75,75);

  for (var i=1;i<6;i++){ // Loop through rings (from inside to out)
    ctx.save();
    ctx.fillStyle = 'rgb('+(51*i)+','+(255-51*i)+',255)';

    for (var j=0;j<i*6;j++){ // draw individual dots
      ctx.rotate(Math.PI*2/(i*6));
      ctx.beginPath();
      ctx.arc(0,i*12.5,5,0,Math.PI*2,true);
      ctx.fill();
    }

    ctx.restore();
  }
}

```

### (3)、缩放 Scaling
> 变形都是以左上角为原点，向右边为负数
> 向下边为y轴的正数
> 如果参数为负实数， 相当于以x 或 y轴作为对称轴镜像反转（例如， 使用`translate(0,canvas.height); scale(1,-1);` 以y轴作为对称轴镜像反转， 就可得到著名的笛卡尔坐标系，左下角为原点）。
  `scale(x,y)`  x 为水平缩放因子，y 为垂直缩放因子 <1 为缩放 ，>1 则放大 

### (4)、变形Transforms
> 允许对变形矩阵直接修改
  #### ` transform(a,b,c,d,e,f) ` 
  1. a 水平方向的缩放
  2. b 竖直方向的倾斜偏移
  3. c 水平方向的倾斜偏移
  4. d 竖直方向的缩放
  5. e 水平方向的移动
  6. f 竖直方向的移动
  #### `setTransform(a,b,c,d,e,f)`
```js
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  var sin = Math.sin(Math.PI/6);
  var cos = Math.cos(Math.PI/6);
  ctx.translate(100, 100);
  var c = 0;
  for (var i=0; i <= 12; i++) {
    c = Math.floor(255 / 12 * i);
    ctx.fillStyle = "rgb(" + c + "," + c + "," + c + ")";
    ctx.fillRect(0, 0, 100, 10);
    ctx.transform(cos, sin, -sin, cos, 0, 0);
  }

  ctx.setTransform(-1, 0, 0, 1, 100, 100);
  ctx.fillStyle = "rgba(255, 128, 255, 0.5)";
  ctx.fillRect(0, 50, 100, 100);
}
```

## 六、组合Compositing
> 对于组合图形，绘制顺序会有限制 可通过globalCompositeOperation设置

  1. ` globalCompositeOperation = type` 设定了在画新图形时采用的遮盖策略，其值是一个标识12种遮盖方式的字符串
   1. - `source-over`  默认值： 在画布上下文之上绘制图形
   2. - `source-in` 新图形只在新图形和目标画布重叠的地方绘制。其他地方都是透明
   3. - `source-out` 在不与现有画布重叠的地方绘制图形
   4. - `source-atop`新图形只在与现有画布内容重叠的地方绘制
   5. - `destination-over `在现有画布内容后面绘制新图形
   6. - `destination-in `现有画布内容保持在新图形和现有画布内容重叠的位置。其他的都是透明
   7. - `destination-out `现有内容保持在新图形不重叠的地方
   8. - `destination-atop `现有的画布只保留与新图形重叠的部分，新的图形是在画布内容后面绘制的。
   9. - `lighter `两个重叠图形的颜色是通过颜色值相加来确定的。
   10. - `copy `只显示新图形。
   11. - `xor `图像中，那些重叠和正常绘制之外的其他地方是透明的。
   12. - `multiply `将顶层像素与底层相应像素相乘，结果是一幅更黑暗的图片。
   13. - `screen `像素被倒转，相乘，再倒转，结果是一幅更明亮的图片。
   14. - `overlay `multiply和screen的结合，原本暗的地方更暗，原本亮的地方更亮。
   15. - `darken `保留两个图层中最暗的像素。
   16. - `lighten `保留两个图层中最亮的像素。
   17. - `color-dodge`将底层除以顶层的反置。
   18. - `color-burn`将反置的底层除以顶层，然后将结果反过来。
   19. - `hard-light`屏幕相乘（A combination of multiply and screen）类似于叠加，但上下图层互换了。
   20. - `soft-light`用顶层减去底层或者相反来得到一个正值。
   21. - `difference `一个柔和版本的强光（hard-light）。纯黑或纯白不会导致纯黑或纯白。
   22. - `exclusion`和difference相似，但对比度较低。
   23. - `hue` 保留了底层的亮度（luma）和色度（chroma），同时采用了顶层的色调（hue）。
   24. - `saturation`保留底层的亮度（luma）和色调（hue），同时采用顶层的色度（chroma）。
   25. - `color`保留了底层的亮度（luma），同时采用了顶层的色调(hue)和色度(chroma)。
   26. - `luminosity`保持底层的色调（hue）和色度（chroma），同时采用顶层的亮度（luma）。

### (1)、裁切路径


## 七、基本动画

### (1)、步骤
  1. `clearRect` 清空canvas 
  2. 保存canvas状态 
  3. 绘制动画图形（animated shapes) =====>重绘动画帧
  4. 恢复canvas状态

### (2)、操作动画
  > 我们只能在脚本执行结束后才能看到结果，我们可以通过下面两个定时器来控制动画
  1. setInterval 
  2. setTimeout

### (3)、更新动画
> 可以用window.setInterval(), window.setTimeout(),和window.requestAnimationFrame()来设定定期执行一个指定函数。
  1. `setInterval(function,delay)`  定期执行
  2. `setTimeout(function,delay)` 
  3. `requestAnimationFrame(callback)` 在重绘之前，执行一个特定的函数来更新动画






