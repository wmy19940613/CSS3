## CSS3知识整理
+ css3的现状
  1. 浏览器的支持程度差，需要添加私有前缀
  2. 移动端支持优于PC端
  3. 不断改进中
  4. 应用相对广泛
+ 如何对待
  1. 坚持渐进增强的原则
  2. 考虑用户群体
  3. 遵照产品的方案
  4. 听boss的
+ css3新增利用属性选择标签
  E[attr] 存在attr属性即可
  E[attr=val] 属性值完全等于val的标签
  E[attr*=val] 属性值包括val，并且在任意位置
  E[attr^=val] 属性值以val开头的值，并且在开始的位置
  E[attr$=val] 属性值以val结束，并且在结束的位置
```
  //div的calss属性里面包含"test"属性的标签。
  div[class*="test"]
  {
  background:#ffff00;
  }
```
+ 伪类
  - 除了以前学过的:link :active :visited :hover外css又新增了很多其他的伪类
    1. 结构（位置）伪类：以某元素（E）相对于父元素或兄弟的位置来获取元素；
        - E:first-child 其父元素的第1个子元素
          E:last-child 其父元素的最后1个子元素
          E:nth-child(n) 其父元素的第n个子元素
          E:nth-last-child(n) 其父元素的第n个子元素（倒着数）
          E:only-child选择的元素是它的父元素的唯一一个了元素；    
     > 值E元素的父元素，并对应位置的子元素必须是E,一旦父元素的子元素不完全是E时，需要以下写法
        - E:nth-of-type()选择指定的元素；
          E:nth-last-of-type()选择指定的元素，从元素的最后一个开始计算；
          E:first-of-type选择一个上级元素下的第一个同类子元素；
          E:last-of-type选择一个上级元素的最后一个同类子元素；
          E:only-of-type选择一个元素是它的上级元素的唯一一个相同类型的子元素；
          E:empty选择的元素里面没有任何内容。(使用并不是很广泛)
    2. 目标伪类：E.target结合锚点进行使用，处于当前锚点的元素会被选中；目标伪类选择器时一个动态选择器，只有存在url指向该匹配元素时候，样式才会生效。
    ```
        <!DOCTYPE html>
        <html>
        <head>
            <title></title>
            <style type="text/css">
                #big-bam-boom:target {
                    color: red;
                }
            </style>
        </head>

        <body>
            <h1 id="big-bam-boom">Kaplow!</h1>
            <a href="#big-bam-boom">Mission Control, we're a little parched up here.</a>
        </body>
        </html>　
        //上述代码的效果是当点击a链接，链接跳转到h1的时候，h1的文字会显示为红色
    ```
+ 排除伪类：
```
  E:not(selector) 除selector（任意选择器）外的元素会被选中；
    div:not(".box"){//除了.box指定的元素之外的剩下的div包括的元素
    }
```
+ 伪元素
  1. E::first-letter:文本的第一个单词或字（如中文，日文，韩文等）     
```
p:first-line
  {
  color:#ff0000;
  font-variant:small-caps;
  }//p标签的第一个单词或者字，为这个样式
```
    2. E::first-line:文本的第一行
```
  p:first-line{
        color:red
    }//p标签的第一行为这个样式
```
    3. E::selection:选择器匹配被用户选取的选取是部分，并且只能向：：selection选择器应用少量CSS属性：有color,backgroud,cursor，outline
```
::selection
{
color:#ff0000;
}

::-moz-selection
{
color:#ff0000;
}
```
    4. E:before和E:after:在E元素内部的开始位置和结束位置创建一个元素，该元素为行内元素，且必须要结合content属性使用。
  + E:after和E:before在旧版本里面时伪元素，css的规范里面说“:”用来表示伪类，“::”用来表示伪元素,但是在高版本浏览器下E:after,E:before会被自动识别为E::after、E::before这样做的目的是为了做兼容处理
  ```
  p:after
  { 
  content:"台词：-";
  background-color:yellow;
  color:red;
  font-weight:bold;
  }//建议用:after,:before,兼容低版本
  ```
+ 颜色 ：-rgba(),a为透明度，不是完全透明的
        - opacity只能针对整个盒子设置透明度，子盒子及内容会继承父盒子的透明度； 
    transparent 不可调节透明度，始终完全透明
+ 文本： text-shadow文字阴影
```
div{
    text-shadow:2px 2px 2px #ccc;
    //第一个表示x轴的偏移，正右负左
    //第二个字表示y轴的偏移，正下负上
    //第三个字为模糊度，只能为正值
    //第四个值为颜色，可以为十六进制，也可以为rgba
}
```
+ 盒模型：
```
- box-sizing: border-box 盒子的大小为width(设置的大小：包括border+padding+content) 
- border-sizing:content-box盒子的大小为width+padding+border.
```
+ 边框：border-radius圆角
```
border-radius:5px //5个角都为5px的圆角
border-radius:5px 6px //左上和右下为5px,右上和左下为6px;
border-radius:3px 4px 5px 6px //依次为左上，右上，右下，左下
```
+ 边框图片：border-image
+ 背景图片：背景在CSS3中也得到很大程度的增强，比如背景图片尺寸、背景裁切区域、背景定位参照点、多重背景等。
   1. background-size:通过background-size设置背景图片的尺寸，就像我们设置img的尺寸一样，在移动端开发中做屏幕适配应用非常广泛
   - background-size:100%,100%(宽高均100%)
   - background-size:cover(设置cover时，会自动调整缩放比例，保证图片始终完整显示在背景区域，如有溢出部分则会被隐藏，显示不全)
   - background-size:contain(设置contain会自动调整缩放比例，保证图片始终完整显示在背景区域)
   2. background-origin：通过background-origin可以设置背景图片定位(background-position)的参照原点
   - border-box以边框做为参考原点；
   - padding-box以内边距做为参考原点；
   - content-box以内容区做为参考点；
   3. background-clip：通过background-clip，可以设置对背景区域进行裁切，即改变背景区域的大小
   - border-box裁切边框以内为背景区域；
   - padding-box裁切内边距以内为背景区域；
   - content-box裁切内容区做为背景区域；
+ 多背景
```
p{background:url(demo.gif) no-repeat; //这是写给不识别下面这句的默认背景图片
background:url(demo.gif) no-repeat ,url(demo1.gif) no-repeat left bottom, url(demo2.gif) no-repeat 10px 15px; //这是高级浏览器的css多重背景，第一个最上面
background-color:yellow; //这是定义的默认背景颜色，全部适合
}
```
+ 渐变：
1. 线性渐变：linear-gradient线性渐变指沿着某条直线朝一个方向产生渐变效果
    包括：方向，起始色，终止色，渐变距离
    - 方向：设置渐变方向，可以用关键字如to top、to right，也可以用角度（正负值均可）如45deg、-90deg等，当以角度做为参数时，可0deg从下往上，90deg从左向右，进而可以推算出180deg从上向下。
  ```
.test {
    background: linear-gradient(#fff, #333);
}
.test2 {
    background: linear-gradient(#000, #f00 50%, #090);
}
.test3 {
    background: linear-gradient(0deg, #000 20%, #f00 50%, #090 80%);
}
.test4 {
    background: linear-gradient(45deg, #000, #f00 50%, #090);
}
.test5 {
    background: linear-gradient(to top right, #000, #f00 50%, #090);
}
  ```
2. 径项渐变：radial-gradient径向渐变指从一个中心点开始沿着四周产生渐变效果
    包括：a) 辐射范围即圆半径 
          b) 中心点 即圆的中心 
          c) 渐变起始色 
          d) 渐变终止色 
          e) 渐变范围
```
radial-gradient(100px, #f00, #ff0, #080); /* 1 */
radial-gradient(100px 100px, #f00, #ff0, #080); /* 2 */
radial-gradient(50px 100px, #f00, #ff0, #080); /* 3 */
代码1：只给出100px，所以被当成是正圆的半径，于是就能确定一个直径为100px的圆；

代码2：给出了2个值，按理应该是要画一个椭圆的，但2个值相等，所以这个椭圆其实此时是个正圆形态。需要注意的是，代码2如果加上 circle，那将是错误语法，因为这是2个值只有椭圆才接受；

代码3：表示了一个水平半径为50px，垂直半径为100px的椭圆
.test {
    background: radial-gradient(circle at center, #f00, #ff0, #080);
}
.test2 {
    background: radial-gradient(circle closest-side, #f00, #ff0, #080);
}
.test3 {
    background: radial-gradient(farthest-side, #f00 20%, #ff0 50%, #080 80%);
}
.test4 {
    background: radial-gradient(at top right, #f00, #ff0, #080);
}
.test5 {
    background: radial-gradient(farthest-side at top right, #f00, #ff0, #080);
}
.test6 {
    background:
                radial-gradient(farthest-side at top right, #f00, #ff0, #080, transparent),
```
+ 过渡（很重要）
  - transition-property设置过渡属性 
    transition-duration设置过渡时间 
    transition-timing-function设置过渡速度（规定过渡效果的时间曲线。默认是 “ease”。） 
    transition-delay设置过渡延时
> Internet Explorer 10、Firefox、Chrome 以及 Opera 支持 transition 属性。
> Safari 需要前缀 -webkit-,Internet Explorer 9 以及更早的版本，不支持 transition 属性,Chrome 25 以及更早的版本，需要前缀 -webkit-。
```
div
{
transition: width 1s linear 2s;
/* Firefox 4 */
-moz-transition:width 1s linear 2s;
/* Safari and Chrome */
-webkit-transition:width 1s linear 2s;
/* Opera */
-o-transition:width 1s linear 2s;
//多个属性过渡用逗号隔开，1s是整个过渡时间为1s,2s是延时2s才开始。
}
```
+ 2D转换（很重要）
  1. 移动translate(x,y)可以改变元素的位置x,y可为负值；
    - a) 移动位置相当于自身原来位置 
      b) y轴正方向朝下 
      c) 除了可以像素值，也可以是百分比，相对于自身的宽度或高度
  2. 缩放scale(x,y)可以对元素进行水平和垂直方向的缩放，x、y的取值可为小数。
  3. 旋转rotate(deg)可以对元素进行旋转，正值为顺时针，负值为逆时针
  4. 倾斜skew(deg,deg)可以使元素按一定的角度进行倾斜，可为负值，第二个参数不写默认为0。
+ 3D转换：用X,Y,Z分别表示空间的三个维度，三条轴互相垂直；
  1. 透视(perspective):电脑显示屏是一个2D平面，图像之所以具有立体感（3D效果），其实只是一种视觉呈现 ，通过透视可以实现此目的，透视可以将一个2D平面，在转换的过程当中，呈现3D效果。（没有perspective，便“没有”Z轴） 
     目前浏览器都不支持 perspective 属性。 
     Chrome 和 Safari 支持替代的 -webkit-perspective 属性。
  2. perspective的两种写法：
     a)作为一个属性，设置给父元素，作用于所有3D转换的子元素
     b)作为transform属性的一个值，作用于元素本身
  3. 左手坐标系：伸出左手，让拇指和食指成“L”形，大拇指向右，食指向上，中指指向前方。这样我们就建立了一个左手坐标系，拇指、食指和中指分别代表X、Y、Z轴的正方向
  4. 左手法则：左手握住旋转轴，竖起拇指指向旋转轴正方向，正向就是其余手指卷曲的方向。
  5. 理解透视距离：透视会产生“近大远小”的效果
  6. 3D呈现（transform-style）:设置内嵌的元素在 3D 空间如何呈现，这些子元素必须为变形元素
       flat：所有子元素在 2D 平面呈现 
       preserve-3d：保留3D空间 
  7. backface-visibility
+ 动画：动画是CSS3中具有颠覆性的特征之一，可通过设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。
  - 必要元素：a.通过@keyframes指定动画序列
           b.通过百分比将动画序列分隔成多个节点
           c. 在各个点中分别定义各属性
           d.通过animation将动画应用于相应元素
  - 关键属性：animation-name:设置动画序列名称
           animation-duration:动画持续时间
           animation-delay:动画延迟时间
           animation-timing-function:动画执行速度，linear,ease等
           animation-play-state:动画播放状态：running,paused等
           animation-direction:动画逆播,alternate等
           animation-fill-mode动画执行完毕后状态，forwards,backwards等
           animation-iteration-count动画执行次数，inifinate等 
           steps(60) 表示动画分成60步完成
         + 参考值的顺序：关于几个值，除了名字，动画时间，延时有严格的要求，其他随意
```
@keyframes myfirst
{
0%   {background: red; left:0px; top:0px;}
25%  {background: yellow; left:200px; top:0px;}
50%  {background: blue; left:200px; top:200px;}
75%  {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}
}

@-moz-keyframes myfirst /* Firefox */
{
0%   {background: red; left:0px; top:0px;}
25%  {background: yellow; left:200px; top:0px;}
50%  {background: blue; left:200px; top:200px;}
75%  {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}
}

@-webkit-keyframes myfirst /* Safari 和 Chrome */
{
0%   {background: red; left:0px; top:0px;}
25%  {background: yellow; left:200px; top:0px;}
50%  {background: blue; left:200px; top:200px;}
75%  {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}
}

@-o-keyframes myfirst /* Opera */
{
0%   {background: red; left:0px; top:0px;}
25%  {background: yellow; left:200px; top:0px;}
50%  {background: blue; left:200px; top:200px;}
75%  {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}

//调用

div
{
animation: myfirst 5s;
-moz-animation: myfirst 5s; /* Firefox */
-webkit-animation: myfirst 5s;  /* Safari 和 Chrome */
-o-animation: myfirst 5s;   /* Opera */
}
//第二种
div
{
animation: myfirst 5s linear 2s infinite alternate;
/* Firefox: */
-moz-animation: myfirst 5s linear 2s infinite alternate;
/* Safari 和 Chrome: */
-webkit-animation: myfirst 5s linear 2s infinite alternate;
/* Opera: */
-o-animation: myfirst 5s linear 2s infinite alternate;
}
```
+ 伸缩布局：CSS3在布局方面做了非常大的改进，使得我们对块级元素的布局排列变得十分灵活，适应性非常强，其强大的伸缩性，在响应式开中可以发挥极大的作用。 
  - 主轴：Flex容器的主轴主要用来配置Flex项目，默认是水平方向
  - 侧轴：与主轴垂直的轴称作侧轴，默认是垂直方向的 
  - 方向：默认主轴从左向右，侧轴默认从上到下
  - 主轴和侧轴并不是固定不变的，通过flex-direction可以互换。
      1. 开启弹性伸缩布局：display:flexbox
      2. 设置布局中元素的排列方式和顺序：flex-direction(可选参数：row,column，row-reverse水平方向，column-reverse垂直方向)
      3. 设置无法容纳时，自动换行：flex-wrap(可选的参数：nowrap默认值都在一行或一列显示，wrap伸缩项目无法容纳时，自动换行，wrap-reverse伸缩项目无法容纳时，方向和wrap相反)
      4. flex-flow:集合了flex-direction和flex-wrap的简写方式
      ```
      display:flex;
      flex-flow:row-reverse wrap;
      ```
      5.justify-content调整主轴对齐
      - 可选的参数: 
        flex-start 伸缩项目以容器的起始点靠齐 
        flex-end 伸缩项目以容器的结束点靠齐 
        center 伸缩项目以容器的中心靠齐 
        space-between 伸缩项目平均分布(类似于老版本的-xxx-box-pack:justify,而且webkit和moz都是通用的) 
        space-around 伸缩项目平均分布,但两边留下伸缩项目之间距离一半的空白
      6. align-items调整侧轴对齐 
       - 可选的参数:
        flex-start元素向侧轴起点对齐。 
        flex-end元素向侧轴终点对齐。 
        center元素向侧轴中间对齐。 
        baseline如弹性盒子元素的行内轴与侧轴为同一条，则该值与’flex-start’等效。其它情况下，该值将参与基线对齐。 
        stretch弹性元素被在侧轴方向被拉伸到与容器相同的高度或宽度。
        7.flex子项目在主轴的缩放比例，不指定flex属性，则不参与伸缩分配
        8.align-content堆栈（由flex-wrap产生的独立行）对齐
        9.order控制子项目的排列顺序，正序方式排序，从小到大
        10.align-self 此属性规定某一个特定的伸缩项元素在次轴上的布局方式，在某个元素上设置该属性会覆盖它的align-items属性。也就是这个属性会让某个元素更有个性，不走寻常路~
