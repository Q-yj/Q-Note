# Web移动端

移动端常见浏览器：

UC浏览器，QQ浏览器，百度手机浏览器，360安全浏览器，谷歌浏览器，搜狗手机浏览器，猎豹浏览器，以及其他杂牌浏览器

国内的UC和QQ，百度等手机浏览器都是根据 Webkit 修改过来的内核，国内尚无自主研发的内核，就像国内的手机操作系统都是基于Android修改开发的一样

总之，兼容移动端主流浏览器，处理 Webkit 内核浏览器即可

在移动端开发时，可以使用浏览器的模拟手机界面以及调试

视口：视口（viewport）就是浏览器显示页面内容的屏幕区域

理想视口：

- 为了使网站在移动端有最理想的浏览和阅读宽度而设定
- 理想视口个对设备来讲，是最理想的视口尺寸
- 需要手动添写 meta 视口标签通知浏览器操作

视口标签：

```html
 <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0,minimum-scale=1.0, user-scalable=no">
```

|        语句        |        解释说明        |
| :----------------: | :--------------------: |
| width=device-width | 视口宽度与设备保持一致 |
| initial-scale=1.0  | 视口的默认的缩放比1.0  |
| maximum-scale=1.0  |  最大允许的缩放比1.0   |
| minimum-scale=1.0  |  最小允许的缩放比1.0   |
|  user-scalable=no  |     不允许用户缩放     |

二倍图：

- 准备的图片比实际大小大 2 倍，这就是二倍图
- 在实际开发中，通常需要图片进行缩放使用，但是直接放大图片会导致图片模糊，所以便需要二倍图甚至多倍图
- 即我们准备的图片就比需要的大小大2倍或多倍，当我们在缩放时，就是正常的图片

背景缩放：

background size属性规定背景图像的尺寸

```html
background-size: 背景图片宽度 背景图片高度 百分比 cover  contain;
```

- 只写一个参数肯定是宽度高度省略了会 等比例缩放
- 单位可以给百分比
- cover 完全覆盖盒子，图片可能有部分显示不全
- contain 是盒子完全包含图片，图片拉伸到最大

移动端 css 初始化：

移动端初始化推荐使用 normalize.css

官方网址： https://necolas.github.io/normalize.css/

## 1 流式布局

流式布局，就是百分比布局，也称非固定像素布局

通过盒子的宽度设置成百分比来根据屏幕的宽度来进行伸缩，不受固定像素的限制，内容向两侧填充

流式布局方式是移动web开发使用的比较常见的布局方式

[京东移动端首页]: C:/Users/Q/Desktop/web前端/前端学习/移动端Web/流式布局-京东移动端首页/index.html

## 2 flex布局

在移动端布局页面或者不用考虑兼容性的pc端布局，更适合用flex来布局

flex 是 flexible Box 的缩写，意为 “弹性布局”，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为 flex 布局

为父盒子设为 flex 布局后，子元素的 float、clear、vertical-align属性将失效

采用 flex 布局的元素，称为 flex容器（flex container），简称 “容器”，它的所有子元素自动成为容器成员，称为 flex项目（flex item），简称 “项目”

flex项目本身也可以成为容器，称为子容器。则上一级则称为父容器

子容器可以横向排列也可以纵向排列

### 2.1 父项常见属性

- flex-direction：设置主轴方向
- justify-content：设置主轴上的子元素排列方式
- flex-wrap：设置子元素是否换行
- align-items：设置侧轴上的子元素排列方式（单行）
- align-content：设置侧轴上的子元素的排列方式（多行）
- flex-flow：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

#### 2.1.1 flex-direction

作用：设置主轴方向

在 flex 布局中，分为主轴和侧轴两个方向

默认主轴方向为 x 轴方向，水平向右

默认侧轴方向为 y 轴方向，垂直向下

子元素是靠主轴来排列的

|     属性值     |       说明       |
| :------------: | :--------------: |
|      row       | 默认值，从左到右 |
|  row-reverse   |     从右到左     |
|     column     |     从上到下     |
| column-reverse |     从下到上     |

#### 2.1.2 justify-content

作用：设置主轴上子元素排列方式

使用此属性之前一定要确定好主轴是哪个

|    属性值     |                    说明                     |
| :-----------: | :-----------------------------------------: |
|  flex-start   | 默认值，从头部开始，若主轴是x轴，则从左到右 |
|   flex-end    |               从尾部开始排列                |
|    center     |   在主轴居中对齐（若主轴是x，则水平居中）   |
| space-around  |                平分剩余空间                 |
| space-between |    先向两边贴紧，再平分剩余空间（重要）     |

#### 2.1.3 flex-wrap

作用：设置子元素是否换行

默认情况下，项目都排在一条线上，flex 布局中默认是不换行的

若父盒子一行上装不开，则会缩小子元素的宽度，从而仍然一行显示

|    属性值    |      说明      |
| :----------: | :------------: |
|    nowrap    | 默认值，不换行 |
|     wrap     |      换行      |
| wrap-reverse |    反向换行    |

#### 2.1.4 align-items

作用：设置侧轴上的子元素排列方式（单行）

该属性控制子项在侧轴上的排列方式，在子项为单项的时候使用

|   属性值   |         说明         |
| :--------: | :------------------: |
| flex-start |       从上到下       |
|  flex-end  |       从下到上       |
|   center   | 挤在一起（垂直居中） |
|   strech   |    拉伸（默认值）    |

#### 2.1.5 align-content

作用：设置侧轴上的子元素的排列方式（多行）

设置子项在侧轴上的排列方式并且 只能用于子项出现换行的情况（多行），在单行下是没有效果的

|    属性值     |                  说明                  |
| :-----------: | :------------------------------------: |
|     flex      |      默认值，在侧轴的头部开始排列      |
|   flex-end    |          在侧轴的尾部开始排列          |
|    center     |             在侧轴中间显示             |
| space-around  |         子项在侧轴平分剩余空间         |
| space-between | 子项在侧轴先分布在两头，再平分剩余空间 |
|    strech     |   设置子项元素高度任意平分父元素高度   |

#### 2.1.6 flex-flow

作用：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

### 2.2 子项常见属性

#### 2.2.1 flex

作用：定义子项目分配剩余空间，用 flex表示占多少份数

flex的值可以是整数，可以是百分数

例如要平分一个盒子，则不给定子元素宽度（高度），然后给每一个子元素设置属性：flex: 1

#### 2.2.2 align-self

作用：控制子项自己在侧轴上的排列方式

允许单个项目有与其他项目不一样的对齐方式

可覆盖 align-items 属性

|   属性值   |                 描述                  |
| :--------: | :-----------------------------------: |
|    auto    | 默认值，继承父盒子的 align-items 值。 |
|   strech   |        元素被拉伸以适应容器。         |
|   center   |          元素位于容器的中心           |
| flex-start |          元素位于容器的开头           |
|  flex-end  |          元素位于容器的结尾           |

#### 2.2.3 order

作用：定义项目的排列顺序

数值越小，排列越靠前，默认为 0

### 2.3 案例

[携程移动端首页]: C:\Users\Q\Desktop\web前端\前端学习\移动端Web\flex布局-携程移动端首页\index.html

## 3 rem布局

rem（root em）是一个单位，类似于 em 

em 是相对于父元素字体大小

rem 的基准是相对于html元素的字体大小、

使用rem 通过修改html元素字体的大小来改变页面中元素的大小从而整体控制整个页面

### 3.1 媒体查询

媒体查询（Media Query）是 CSS3 的新语法

- 使用 @media 查询，可以针对不同的媒体类型定义不同的样式
- @media 可以针对不同屏幕尺寸设置不同的样式
- 重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面
- 目前针对很多苹果手机、安卓手机、平板等设备都用到媒体查询

#### 3.1.1 语法规范

```css
@media mediatype and|not|only (media feature) {
    CSS3-Code;
}
```

#### 3.1.2 mediatype 查询类型

将不同终端设备划分成不同的类型，称为媒体类型

|  类型  |              解释说明              |
| :----: | :--------------------------------: |
|  all   |            用于所有设备            |
| print  |        用于打印机和打印浏览        |
| screen | 用于电脑屏幕，平板电脑，智能手机等 |

#### 3.1.3 关键字

关键字将媒体类型特性连接到一起作为媒体查询的条件

| 关键字 |                         解释说明                         |
| :----: | :------------------------------------------------------: |
|  and   | 可以将多个类型或多个媒体类型连接到一起成为媒体查询的条件 |
|  not   |      排除某个媒体类型，相当于 “非” 的意思，可以省略      |
|  only  |             指定某个特定的媒体类型，可以省略             |

#### 3.1.4 媒体特性

每种媒体类型都具体各自不同的特性，根据不同媒体类型的媒体特性设置不同的展示风格

|    值     |                解释                |
| :-------: | :--------------------------------: |
|   width   |  定义输出设备中页面可见区域的宽度  |
| min-width | 定义输出设备中页面最小可见区域宽度 |
| max-width | 定义输出设备中页面最大可见区域宽度 |

举例：

```css
@media screen and (max-width: 800px) {
    body {
        background-color: pink;
    }
}
@media screen and (max-width: 500px){
    body {
        background-color: purple;
    }
}
```

### 3.2 元素大小动态变化

rem 单位是跟着 html 来走的，有了 rem ，页面元素可以设置不同大小尺寸媒体查询可以根据不同设备宽度来修改样式

举例：

```html
<html>
	<head>
    	<style>
			@media screen and (min-width: 320px) {
    			html {
        			font-size: 50px;
    			}
			}
			@media screen and (min-width: 640px) {
    			html {
        			font-size: 100px;
    			}
			}
			div {
     			height: 1rem;
     			font-size: .5rem;
                background-color: green;
            	color: #fff;
     			text-align: center;
     			line-height: 1rem;
			}
		</style>
	</head>
    <body>
        <div>鸡你太美</div>
    </body>
</html>

```

### 3.3 引入资源

当样式比较繁多的时候，我们可以针对不同的媒体使用不同 CSS 样式

直接在 link 中判断设备的尺寸，然后引用不同的 CSS 文件

```html
<!-- 当屏幕宽度大于等于320px时调用style320.css -->
<!-- 当屏幕宽度大于等于640px时调用style640.css -->
<link rel="stylesheet" href="style320.css" media="screen and (min-width: 320px)">
<link rel="stylesheet" href="style640.css" media="screen and (min-width: 640px)">
```

### 3.4 Less

CSS 是一门非程序式语言，没有变量、函数、作用域等概念

- CSS 需要书写大量看似没有逻辑的代码，CSS 冗余度是比较高的
- 不方便维护及扩展，不利于复用
- CSS 没有很好的计算能力
- 非前端开发工程师来讲，往往会因为缺少 CSS 编写经验而很难写出组织良好且易于维护的 CSS 代码项目

由此产生了Less

#### 3.4.1 Less 简介

Less（Leaner Style Sheets的缩写）是一门 CSS 扩展语言，也称为 CSS 预处理器

作为CSS的一种形式的扩展，它并没有减少 CSS 的功能，而是在现有的 CSS 语法上，为 CSS 加入程序式语言的特性

它在CSS的语法基础之上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了CSS的编写，并且降低了CSS的维护成本

Less中文网址： https://less.bootcss.com/

Less是一门 CSS 预处理语言，它扩展了 CSS 的动态特性

#### 3.4.2 Less 变量

变量是指没有固定的值，CSS 中一些颜色和数值经常使用

```less
@变量名:值;
```

注意：

变量名必须有 @ 前缀，不能包含特殊字符，不能以数字开头，且大小写敏感

举例：

```less
@color: pink;
@font14: 14px;
body {
    background-color: @color;
}
div {
    background-color: @color;
    font-size: @font14;
}
```

#### 3.4.3 Less 编译

本质上，Less包含一套自定义的语法及一个解析器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的CSS文件

我们需要把我们的less文件，编译生成为css文件，这样我们的html页面才能使用

在 VS Code 中，使用 Easy Less 插件可以即时编译生成 CSS 文件，再引入即可

#### 3.4.4 Less 嵌套

类似于html元素之间的嵌套，Less 里也可以把选择器嵌套

```less
#header {
    .logo {
        width: 100px;
    }
}
//相当于
#header .logo {
     width: 100px;
}
```

#### 3.4.5 Less 中的伪类伪元素

要在 less 中写伪类、交集选择器、伪元素选择器，则要在内层选择器的前面加上 &

- 内层选择器前面没有 &，则它被解析为父选择器的后代；
- 若有 &，则被解析为父元素自身或父元素的伪类

```less
a {
    &:hover {
        color: red;
    }
}
```

#### 3.4.6 Less 运算

任何数字、颜色或者变量都可以参与运算，Less 提供了加（+）、减（-）、乘（*）、除（/）算数运算

注意：

- 运算符的作用左右两侧要有空格
- 运算数若只有一个带有单位，则最后结果以此为单位
- 若有多个单位，则以第一个单位为准

### 3.5 rem 适配方案

让一些不能等比自适应的元素，达到当设备尺寸发生改变的时候，等比例适配当前设备

使用媒体查询根据不同设备按比例设置 html 的字体大小，然后页面元素使用 rem 做尺寸单位，当 html 字体大小变化元素尺寸也会发生变化，从而达到等比缩放的适配

实际开发中，按照设计稿与设备宽度的比例，动态计算并设置html根标签的font-size大小

CSS中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为rem为单位的值

#### 3.5.1 rem 适配方案技术使用

方案一：Less，媒体查询，rem

方案二：flexible.js，rem

两种方案目前都存在，方案二更简单，推荐使用

#### 3.5.2 方案一使用

常见设计稿尺寸：

|   设备    |                           常见宽度                           |
| :-------: | :----------------------------------------------------------: |
| iphone45  |                            640px                             |
| iphone678 |                            750px                             |
|  Android  | 常见320px、360px、375px、384px、400px、720px（大部分4.7~5寸的安卓设备为720px） |

一般情况下，我们以一套或两套效果图适应大部分的屏幕，放弃极端屏或对其优雅降级，牺牲一些效果，现在基本以750为准

动态设置字体大小：

- 首先确定好设计稿尺寸，例如750px
- 后将屏幕划分为一定的等分（划分标准不一定，15等分或20等分）
- 用 屏幕尺寸 除以 划分的份数，得到 html 里面的文字尺寸大小，此时不同屏幕下的字体大小是不同的
- 页面元素的 rem 值 = 页面元素在750像素下的 px 值 / html里面的文字大小

#### 3.5.2 方案二使用

方案一使用的效果很好，但是比较繁琐，方案二简洁高效

- flexible.js，是手机淘宝团队出的简洁高效移动端适配库
- 我们再也不需要在写不同屏幕的媒体查询，因为里面 JS 做了处理
- 它的原理是把当前设备划分为10等份，但是不同设备下，比例还是一致的
- 我们只需要确定好我们当前设备的html文字大小就可以了

flexible.js项目地址：https://github.com/amfe/lib-flexible

flexible官方文档地址：https://github.com/amfe/article/issues/17

### 3.6 案例

[苏宁移动端首页]: C:\Users\Q\Desktop\web前端\前端学习\移动端Web\rem布局-苏宁移动端首页\index.html

## 4 响应式布局

### 4.1 响应式布局概述

响应式布局，就是使用媒体查询针对不同宽度的设备进行布局和样式的设置，从而达到适配不同设备的目的

响应式布局需要一个父级作为容器，来配合自己元素来实现变化效果

平时我们的响应式尺寸可以按以下划分（但是我们也可以根据实际情况自己定义划分）

|         设备划分         |      尺寸区间       | 宽度设定 |
| :----------------------: | :-----------------: | :------: |
|     超小屏幕（手机）     |      w < 768px      |   100%   |
|     小屏设备（平板）     | 768px <= w < 992px  |  750px   |
|  中等屏幕（桌面显示器）  | 992px <= w < 1200px |  970px   |
| 宽屏设备（大桌面显示器） |     w >= 1200px     |  1170px  |

代码：

```css
/* 超小屏幕 */
@media screen and (max-width: 767px) {
    .container {
        width: 100%;
    }
}
/* 小屏幕 */
@media screen and (min-width: 768px) {
    .container {
        width: 750px;
    }
}
/* 中等屏幕 */
@media screen and (min-width: 992px) {
    .container {
        min-width: 970px;
    }
}
/* 大屏幕 */
@media screen and (min-width: 1200px) {
    .container {
        width: 1170px;
    }
}
```

### 4.2 Bootstrap 前端开发框架

#### 4.2.1 Bootstrap 简介

Bootstrap 来自 Twitter，是目前最受欢迎的前端框架

Bootstrap 是基于HTML、CSS 和JAVASCRIPT 的，它简洁灵活，使得Web 开发更加快捷

官方网址：https://getbootstrap.com/

中文网址：https://www.bootcss.com/

框架：顾名思义就是一套架构，它有一套比较完整的网页功能解决方案，而且控制权在框架本身，有预制样式库、组件和插件

使用者要按照框架所规定的某种规范进行开发

Bootstrap 优点：

- 标准化的 html + css 编码规范
- 提供了一套简洁、直观、强悍的组件
- 有自己的生态圈，不断的更新迭代
- 让开发更简单，提高了开发的效率

#### 4.2.2 Bootstrap 使用

步骤：

- 创建文件夹结构

按照原先的创建形式，index.html、css 文件夹、images 文件夹等，再加上从官网下载的 Bootstrap 文件夹，里面包含了 css 、fonts 、js 等文件夹

- 创建 html 骨架结构

```html
<!--要求当前网页使用IE浏览器最高版本的内核来渲染-->
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<!--视口的设置：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放-->
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">
<!--[if lt IE 9]>
<!-- 解决ie9以下浏览器对html5新增标签的不识别，并导致CSS不起作用的问题 -->
<script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
<!--解决ie9以下浏览器对css3 Media Query 的不识别-->
<script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
<!--[endif]-->
```

- 引入相关样式文件

```html
<!-- Bootstrap 核心样式-->
<link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
```

- 书写内容

1. 直接拿 Bootstrap 预先定义好的样式来使用
2. 修改 Bootstrap 原来的样式，注意权重问题
3. 学好 Bootstrap 的关键在于知道它定义了哪些样式，以及这些样式能实现什么样的效果

#### 4.2.3 布局容器

Bootstrap 需要为页面内容和栅格系统包裹一个 .container 容器，它提供了两个作此用处的类

1. container 类

   响应式布局的容器固定宽度

   大屏( >=1200px) 宽度定为1170px

   中屏( >=992px) 宽度定为970px

   小屏( >=768px) 宽度定为750px

   超小屏(100%)

2. container-fluid 类

   流式布局容器百分百宽度

   占据全部视口（viewport）的容器

### 4.3 Bootstrap 栅格系统

栅格系统英文为 “grid systems”，也有人翻译为 “网格系统”，它是指将页面布局划分为等宽的列，然后通过列数的定义来模块化页面布局

Bootstrap 提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列

#### 4.3.1 栅格选型

栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，内容就可以放入这些创建好的布局中

- 按照不同屏幕划分为 1~12 等份
- 行（row）可以去除父容器作用15px的边距
- 列（column）大于12，多余的 “列（column）”所在的元素将被作为一个整体另起一行排列
- xs-extra small：超小，sm-small：小，md-medium：中等，lg-large：大
- 每一列默认有左右15像素的 padding
- 可以同时为一列指定多个设备的类名，以便划分不同份数例如 class="col-md-4 col-sm-6"

代码案例：

```html
<!-- 有12个，则可以占满一行 -->
<div class="row">
    <div class="col-lg-3 col-md-4 col-sm-6 col-xm-12">1</div>
    <div class="col-lg-3 col-md-4 col-sm-6 col-xm-12">2</div>
    <div class="col-lg-3 col-md-4 col-sm-6 col-xm-12">3</div>
    <div class="col-lg-3 col-md-4 col-sm-6 col-xm-12">4</div>
</div>
<!-- 有12个，则可以占满一行，不同份数表示了所占比例 -->
<div class="row">
    <div class="col-lg-1">1</div>
    <div class="col-lg-2">2</div>
    <div class="col-lg-3">3</div>
    <div class="col-lg-6">4</div>
</div>
<!-- 不足12个，则空出多余 -->
<div class="row">
    <div class="col-lg-3">1</div>
    <div class="col-lg-3">2</div>
    <div class="col-lg-3">3</div>
    <div class="col-lg-2">4</div>
</div>
<!-- 超出12个，则放到下一行 -->
<div class="row">
    <div class="col-lg-3">1</div>
    <div class="col-lg-3">2</div>
    <div class="col-lg-3">3</div>
    <div class="col-lg-4">4</div>
</div>
```

#### 4.3.2 列嵌套

栅格系统内置的栅格系统可以将内容再次嵌套

就是一个列内再分成若干份小列

可以通过添加一个新的 .row 元素和一系列 .col-sm-* 元素到已经存在的 .col-sm-* 元素内

代码案例：

```html
<div class="container">
    <div class="row">
        <div class="col-md-4">
            <div class="row">
                <div class="col-md-6">第一小列</div>
                <div class="col-md-6">第二小列</div>
            </div>
        </div>
        <div class="col-md-4">第二列</div>
        <div class="col-md-4">第三列</div>
    </div>
</div>
```

#### 4.3.3 列偏移

使用 .col-md-offset-* 类可以将列向右侧偏移

这些类实际是通过使用 * 选择器为当前元素增加了左侧的边距（margin）

```html
<div class="container">
    <div class="row">
        <div class="col-md-4">1</div>
        <div class="col-md-4 col-md-offset-4">2</div>
    </div>
    <div class="row">
        <div class="col-md-8 col-md-offset-2">0</div>
    </div>
</div>
```

#### 4.3.4 列排序

通过使用 .col-md-push-* 和 .col-md-pull-* 类就可以很容易的改变列的顺序

可以实现左右盒子交换位置

代码案例：

```html
<div class="container">
    <div class="row">
        <div class="col-md-4">左侧盒子</div>
        <div class="col-md-8">右侧盒子</div>
    </div>
    <div class="row">
        <div class="col-md-4 col-md-push-8">左侧盒子</div>
        <div class="col-md-8 col-md-pull-4">右侧盒子</div>
    </div>
</div>
```

#### 4.3.5 工具

为了加快对移动设备友好的页面开发工作，利用媒体查询功能，并使用这些工具类可以方便的针对不同设备展示或隐藏页面内容

.visible-  和 .hidden- 可以实现在不同大小设备下展示和隐藏

代码案例：

```html
<div class="container">
    <div class="row">
        <div class="col-xs-3">
            <span class="visible-lg">我会显示</span>
        </div>
        <div class="col-xs-3">2</div>
        <div class="col-xs-3 hidden-md hidden-xs">我会隐藏</div>
        <div class="col-xs-3">4</div>
    </div>
</div>
```

### 4.4 案例

[阿里百秀移动端首页]: C:\Users\Q\Desktop\web前端\前端学习\移动端Web\响应式布局-阿里百秀首页\index.html
