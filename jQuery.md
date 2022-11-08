# jQuery

## 1jQuery入门

### 1.1jQuery概述

#### 1.1.1JavaScript库

JavaScript 库：即 library，是一个封装好的特定的集合（方法和函数），从封装一大堆函数的角度理解库，就是在这个库中，封装了很多预先定义好的函数在里面，比如动画 animate、hide、show、获取元素等

简单理解：就是一个JS文件，里面对我们原生js代码进行了封装，存放到里面，这样我们可以快速高效的使用这些封装好的功能了

比如 jQuery，就是为了快速方便的操作 DOM，里面基本都是函数（方法）

常见的 JavaScript 库：

- jQuery
- Prototype
- YuI
- Dojo
- Ext JS
- 移动端的zepto

这些库都是对原生JavaScript的封装，内部都是用 JavaScript 实现的，我们主要学习的是jQuery

#### 1.1.2jQuery的概念

jQuery 是 一个快速、简洁的 JavaScript 库，其设计的宗旨是 “write Less , Do More”，即倡导写更少的代码，做更多的事情

j 就是 JavaScript；Query 查询；意思就是查询js，把 js 中的 DOM 操作做了封装，我们可以快速的查询使用里面的功能

jQuery 封装了 JavaScript 常用的功能代码，优化了 DOM 操作、事件处理、动画设计和 Ajax 交互

学习 jQuery 本质∶就是学习调用这些函数（方法）

jQuery 出现的目的是加快前端人员的开发速度，我们可以非常方便的调用和使用它，从而提高开发效率

#### 1.1.3jQuery的优点

- 轻量级，核心文件才几十kb，不会影响页面加载速度
- 跨浏览器兼容。基本兼容了现在主流的浏览器
- 链式编程、隐式迭代
- 对事件、样式、动画支持，人大简化了 DOM 操作
- 支持插件扩展开发。有着丰富的第三方的插件，例：树形菜单、日期控件、轮播图等
- 免费、开源

### 1.2jQuery的基本使用

#### 1.2.1jQuery下载与使用

官网：https://jquery.com

版本：

- 1x：兼容IE678等低版本浏览器，官网不再更新
- 2x：不兼容IE 678等低版本浏览器，官网不再更新
- 3x：不兼容IE 678等低版本浏览器，是官方主要更新维护的版本

使用：将下载的 JS 脚本引入 HTML 即可

#### 1.2.2jQuery入口函数

方法一（推荐）：

```js
$(function () {
    // 此处是页面DOM加载完成的入口
});
```

方法二：

```js
$(document).ready(function () {
    // 此处是页面DOM加载完成的入口
});
```

- 等着 DOM 结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery 帮我们完成了封装
- 相当于原生 js 中的 DOMContentLoaded
- 不同于原生 js 中的 load 事件是等页面文档、外部的js文件、css文件、图片加载完毕才执行内部代码
- 更推荐使用第一种方式

#### 1.2.3jQuery的顶级对象

- $ 是jQuery的别称，在代码中可以使用jQuery代替 $，但一般为了方便，通常都直接使用 $
- $ 是jQuery的顶级对象，相当于原生 JavaScript 中的 window，把元素利用 $ 包装成jQuery对象，就可以调用jQuery的方法

#### 1.2.4jQuery对象和DOM对象

1.对比：

- 用原生 JS 获取来的对象就是 DOM 对象
- jQuery 方法获取的元素就是 jQuery 对象
- jQuery 对象本质：通过 $ 把 DOM 元素进行了包装，返回的形式是 伪数组形式
- jQuery 对象只能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 属性和方法
- DOM 对象不能使用 jQuery 里面的 hide 等方法，jQuery 对象不能使用原生 JS 的属性和方法

2.联系：

DOM 对象与 jQuery 对象之间是可以相互转换的

因为原生 js 比 jQuery 更大，原生的一些属性和方法 jQuery 没有给我们封装

要想使用这些属性和方法需要把 jQuery 对象转换为 DOM 对象

DOM 对象转换为 jQuery 对象直接使用 $(DOM对象)；jQuery 对象是一种伪数组的形式，可通过索引转换为 DOM 对象

DOM对象转换为 jQuery 对象：

```js
$("div")
```

jQuery 对象转换为 DOM 对象：

```js
$("div")[index]
$("div").get(index)
```

## 2jQuery常用API

### 2.1jQuery选择器

#### 2.1.1jQuery基础选择器

原生 JS 获取元素方式很多，很杂，而且兼容性情况不一致，因此 jQuery 给我们做了封装，使获取元素统一标准

```js
$('选择器'）//里面选择器直接写CSS选择器即可，但是要加引号
```

|    名称    |      用法       |           描述           |
| :--------: | :-------------: | :----------------------: |
| ID 选择器  |    $("#id")     |    获取指定 ID 的元素    |
| 全选选择器 |     $("*")      |       匹配所有元素       |
|  类选择器  |   $(".class")   | 获取同一类 class 的元素  |
| 标签选择器 |    $("div")     | 获取同一类标签的所有元素 |
| 并集选择器 |  $("div,p,li")  |       选取多个元素       |
| 交集选择器 | $("li.current") |         交集元素         |

#### 2.1.2jQuery层级选择器

|    名称    |    用法    |                             描述                             |
| :--------: | :--------: | :----------------------------------------------------------: |
| 子代选择器 | $("ul>li") | 使用 > 号，获取亲儿子层级的元素（注意，并不会获取孙子层级的元素） |
| 后代选择器 | $("ul li") | 使用空格，代表后代选择器，获取 ul 下的所有 li 元素，包括孙子等 |

#### 2.1.3jQuery隐式迭代

遍历内部 DOM 元素（伪数组形式存储）的过程就叫做 隐式迭代

简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用

例如：

```html
<div>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
<script>
    $('div div').css('color', 'red');//给每一个div都变成红色
</script>
```

#### 2.1.4jQuery筛选选择器

|    语法    |     用法      |                             描述                             |
| :--------: | :-----------: | :----------------------------------------------------------: |
|   :first   | $("li:first") |                      获取第一个 li 元素                      |
|   :last    | $("li:last")  |                     获取最后一个 li 元素                     |
| :eq(index) | $("li:eq(2)") | 获取到的 li 元素中，选择索引号为 2 的元素，索引号 index 从 0 开始 |
|    :odd    |  $("li:odd")  |          获取到的 li 元素中，选择索引号为奇数的元素          |
|   :even    | $("li:even")  |          获取到的 li 元素中，选择索引号为偶数的元素          |

#### 2.1.5jQuery父子兄筛选方法

|            语法            |              用法              |                           描述                           |
| :------------------------: | :----------------------------: | :------------------------------------------------------: |
|      parent()（重点）      |       $('li').parent();        |                         查找父级                         |
| children(selector)（重点） |     $('ul').children('li')     |           相当于 $('ul>li')，最近一级(亲儿子)            |
|   find(selector)（重点）   |      $('ul').find('li');       |              相当于 $('ul li')，后代选择器               |
| siblings(selector)（重点） |  $('.first').siblings('li');   |               查找兄弟节点，不包括自己本身               |
|      nextAll([expr])       |      ('.first').nextAll()      |              查找当前元素之后所有的同辈元素              |
|      prevtAll([expr])      |      $('.last').prevAll()      |              查找当前元素之前所有的同辈元素              |
|      hasClass(class)       | $('div').hasClass('protected') | 检查当前的元素是否含有某个特定的类，如 果有，则返回 true |
|     eq(index)（重点）      |         $('li').eq(2);         |          相当于 $('li:eq(2)' )，index从 0 开始           |
|         parents()          |   $('div').parents('.one');    |          获取元素所有父级，然后指定其中一个父级          |

#### 2.1.6jQuery里的排他思想

排他思想：当前元素（$(this)）设置样式，其余的兄弟元素（$(this).siblings()）清除样式

```js
$('button').mouseover(function () {
    // 设置自己的属性
    $(this).css('background-color', 'pink')
    // 消灭其他元素的属性
    $(this).siblings().css('background-color', '');
})
```

#### 2.1.7链式编程

链式编程是为了节省代码量，看起来更优雅

```js
$('button').mouseover(function () {
    // 先设置自己的属性，然后消灭其他兄弟的属性
    $(this).css('background-color', 'pink').siblings().css('background-color', '');
})
```

### 2.2jQuery样式操作

#### 2.2.1操作CSS方法

jQuery 可以使用 CSS 方法来修改简单元素样式； 也可以操作类，修改多个样式

参数只写属性名，则是返回属性值

```js
$(this).css('color');
```

参数是 属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号

```js
$(this).css('color', 'red');
```

参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号

```js
$(this).css({ 'color':'white','font-size':'20px'});
```

#### 2.2.2设置类样式方法

作用等同于以前的 classList，可以操作类样式， 注意 操作类里面的参数不要加点

添加类：

```js
$('div').addClass('current');
```

移除类：

```js
$('div').removeClass('current');
```

切换类：

```js
$('div').removeClass('current');
```

#### 2.2.3类操作与className区别

- 原生 JS 中 className 会覆盖元素原先里面的类名
- jQuery 里面类操作 只是对指定类进行操作，不影响原先的类名

### 2.3jQuery效果

#### 2.3.1显示隐藏效果

1.显示效果

语法：

```js
show([speed, [easing], [fn]])
```

2.隐藏效果

语法：

```js
hide([speed, [easing], [fn]])
```

3.切换效果

语法：

```js
toggle([speed, [easing], [fn]])
```

参数：

- 参数都可以省略， 无动画直接显示
- speed：三种预定速度之一的字符串（'slow', 'normal', or 'fast'）或表示动画时长的毫秒数值(如：1000)
- easing：(Optional) 用来指定切换效果，默认是 'swing'，可用参数 'linear'
- fn: 回调函数，在动画完成时执行的函数，每个元素执行一次

#### 2.3.2滑动效果

1.下滑效果

语法：

```js
slideDown([speed,[easing],[fn]])
```

2.上滑效果

语法：

```js
slideUp([speed,[easing],[fn]])
```

3.滑动效果

语法：

```js
slideToggle([speed,[easing],[fn]])
```

参数：

- 参数都可以省略，无动画直接显示
- speed：三种预定速度之一的字符串（'slow', 'normal', or 'fast'）或表示动画时长的毫秒数值(如：1000)
- easing：(Optional) 用来指定切换效果，默认是 'swing'，可用参数 'linear'
- fn: 回调函数，在动画完成时执行的函数，每个元素执行一次

#### 2.3.3事件切换

语法：

```js
hover([over],out)
```

参数：

- over：鼠标移到元素上要触发的函数（相当于 mouseenter）
- out：鼠标移出元素要触发的函数（相当于 mouseleave）
- 如果只写一个函数，则鼠标经过和离开都会触发它

#### 2.3.4动画队列停止排队

动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行

```js
stop()
```

- stop() 方法用于停止动画或效果
- 注意：stop() 写到动画或者效果的 前面， 相当于停止结束上一次的动画

#### 2.3.5淡入淡出效果

1.淡入效果

语法：

```js
fadeIn([speed,[easing],[fn]])
```

2.淡出效果

语法：

```js
fadeOut([speed,[easing],[fn]])
```

3.切换效果

语法：

```js
fadeToggle([speed,[easing],[fn]])
```

参数：

- 参数都可以省略
- speed：三种预定速度之一的字符串('slow','normal', or 'fast')或表示动画时长的毫秒数值(如：1000)
- easing：（Optional）用来指定切换效果，默认是 'swing'，可用参数 'linear'
- fn: 回调函数，在动画完成时执行的函数，每个元素执行一次

4.不透明度

语法：

```js
fadeTo([[speed],opacity,[easing],[fn]])
```

参数：

- opacity：透明度必须写，取值 0~1 之间
- speed：三种预定速度之一的字符串（'slow','normal', or 'fast'）或表示动画时长的毫秒数值(如：1000)，必须
- easing：（Optional）用来指定切换效果，默认是 'swing'，可用参数 'linear'
- fn: 回调函数，在动画完成时执行的函数，每个元素执行一次

#### 2.3.6自定义动画

语法：

```js
animate(params,[speed],[easing],[fn])
```

参数：

- params: 想要更改的样式属性，以对象形式传递，必须写。 属性名可以不用带引号， 如果是复合属性则需要采取驼峰命名法 
- borderLeft。其余参数都可以省略
- speed：三种预定速度之一的字符串（'slow','normal', or 'fast'）或表示动画时长的毫秒数值（如：1000）
- easing：（Optional）用来指定切换效果，默认是 'swing'，可用参数 'linear'
- fn: 回调函数，在动画完成时执行的函数，每个元素执行一次

### 2.4jQuery属性操作

#### 2.4.1设置或获取元素固有属性值

所谓元素固有属性就是元素本身自带的属性

比如 < a > 元素里面的 href，比如 < input > 元素里面的 type

获取：

```js
prop("属性")
```

设置：

```js
prop("属性"，"属性值")
```

#### 2.4.2设置或获取元素自定义属性值

用户自己给元素添加的属性，我们称为自定义属性

比如给 div 添加 index ='1'

获取：

```js
attr("属性") //类似原生 getAttribute()
```

设置：

```js
attr("属性","属性值") //类似原生 setAttribute()
```

改方法也可以获取 H5 自定义属性

#### 2.4.3数据缓存

data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构

一旦页面刷新，之前存放的数据都将被移除

获取：

```js
date("name") // 向被选元素获取数据
```

附加：

```js
data("name","value") // 向被选元素附加数据
```

还可以读取 HTML5 自定义属性 data-index ，得到的是数字型

### 2.5jQuery文本属性值

主要针对元素的内容还有表单的值操作

#### 2.5.1普通元素内容

相当于原生 innerHTML

获取：

```js
html()
```

设置：

```js
html("内容")
```

#### 2.5.2普通元素文本内容

相当与原生 innerText

获取：

```js
text()
```

设置：

```js
text("内容")
```

#### 2.5.3表单的值

相当于原生 value

获取：

```js
val()
```

设置：

```js
val("内容")
```

### 2.6jQuery元素操作

主要是遍历、创建、添加、删除元素操作

#### 2.6.1遍历元素

jQuery 隐式迭代是对同一类元素做了同样的操作

如果想要给同一类元素做不同操作，就需要用到遍历

1.each()

```js
$("div").each(function (index, domElem) {
    $(domElem);
});
```

- each() 方法遍历匹配的每一个元素，主要用 DOM 处理，each 每一个
- 里面的回调函数有 2 个参数：index 是每个元素的索引号；demElem 是每个DOM元素对象，不是jquery对象
- 要想使用 jquery 方法，需要给这个 dom 元素转换为 jquery 对象：$(domElem)

2.$.each()

```js
$.each(object，function (index, element) { })
```

- $.each() 方法可用于遍历任何对象，主要用于数据处理，比如数组，对象
- 里面的函数有 2 个参数：index 是每个元素的索引号； element 遍历内容

其中，object 对象可以是 DOM 对象，数组，一般对象等：

（1）当 object 为 DOM 对象：

```js
$.each($('li'), function (i, domElem) {
    $(domElem); // 转换为 jQuery 对象
})
```

（2）当 object 为数组：

```js
$.each(arr, function(inbdex, value) {
    // arr 为原数组
    // index 为当前索引
    // value 为当前数组值
})
```

（3）当 object 为一般对象：

```js
$.each(obj, function(key, value) {
    console.log(key, value);
    // obj: 对象
    // key: 对象的键
    // value: 对象的值
})
```

#### 2.6.2创建元素

```js
$('<li></li>'); //动态的创建了一个 <li>
```

#### 2.6.3添加元素

1.内部添加

把内容放入匹配元素内部最后面，类似原生 appendChild

```js
element.append('内容')
```

把内容放入匹配元素内部最前面

```js
element.prepend('内容')
```

- 内部添加元素，生成之后，它们是父子关系

2.外部添加

把内容放入目标元素后面

```js
element.after('内容')
```

把内容放入目标元素前面

```js
element.before('内容')
```

- 外部添加元素，生成之后，他们是兄弟关系

#### 2.6.4删除元素

删除匹配的元素

```js
element.remove() //删除元素本身
```

删除匹配的元素集合中所有的子节点

```js
element.empty()
```

清空匹配的元素内容

```js
element.html('div')
```

empt() 和 html(" ") 作用等价，都可以删除元素里面的内容，只不过 html 还可以设置内容

### 2.7jQuery尺寸位置操作

#### 2.7.1jQuery尺寸

|                 语法                 |                        用法                         |
| :----------------------------------: | :-------------------------------------------------: |
|          width() / height()          |     取得匹配元素宽度和高度值只算 width / height     |
|     innerWidth() / innerHieght()     |        取得匹配元素宽度和高度值包含 padding         |
|     outerWidth() / outerHeight()     |    取得匹配元素宽度和高度值包含 padding、border     |
| outerWidth(true) / outerHeight(true) | 取得匹配元素宽度和高度值包含 padding、borde、margin |

- 以上参数为空，则是获取相应值，返回的是数字型
- 如果参数为数字，则是修改相应值
- 参数可以不必写单位

#### 2.7.2jQuery位置

位置主要有三个： offset()、position()、scrollTop() / scrollLeft()

1.offset() 设置或获取元素偏移

offset() 方法设置或返回被选元素相对于文档的偏移坐标，跟父级没有关系

该方法有2个属性 left、top

offset().top 用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离

```js
offset({ top: 10, left: 30 })
```

2.position() 获取元素偏移

position() 方法用于返回被选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为准

该方法有2个属性 left、top

position().top 用于获取距离定位父级顶部的距离，position().left 用于获取距离定位父级左侧的距离

该方法只能获取

3.scrollTop() / scrollLeft() 设置或获取元素被卷去的头部或左侧

scrollTop() 方法设置或返回被选元素被卷去的头部

不跟参数是获取，参数为不带单位的数字则是设置被卷去的头部

```js
$('.back').click(function () {
    $('body, html').stop().animate({
        scrollTop: 0
    });
}); //返回顶部
```

## 3jQuery事件

### 3.1事件注册

```js
element.事件(function () {})
```

```js
$('div').click(function () { 事件处理程序 })
```

其他事件和原生基本一致

比如 mouseover、mouseout、blur、focus、change、keydown、keyup、resize、scroll 等

### 3.2事件处理

#### 3.2.1绑定事件

on() 方法在匹配元素上绑定一个或多个事件的事件处理函数

语法：

```js
element.on(events, [selector], fn)
```

- events：一个或多个用空格分隔的事件类型，如 'click' 或 'keydown'
- selector：元素的子元素选择器
- fn：回调函数，即绑定在元素身上的侦听函数

1.绑定多个事件

可以绑定多个事件，多个处理事件处理程序

```js
 $('div').on({
    mouseover: function(){},
    mouseout: function(){},
    click: function(){}
});
```

```js
$('div').on('mouseover mouseout', function() {
    $(this).toggleClass('current');
}); 
```

2.事件委派

事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素

这样就不需要给多个子元素多次绑定事件了

```js
$('ul').on('click', 'li', function() {
    alert('hello world!');
});
```

在此之前有 bind()、 live()、delegate() 等方法来处理事件绑定或者事件委派，最新版本的请用 on() 来替代

3.给动态元素绑定事件

动态创建的元素（暂时还没创建未来即将创建），click() 没有办法绑定事件，而 on() 可以给动态生成的元素绑定事件

```js
$('div').on('click', 'p', function(){
    alert('俺可以给动态生成的元素绑定事件')
});
$('div').append($('<p>我是动态创建的p</p>'));
```

#### 3.2.2解绑事件

off() 方法可以移除通过 on() 方法添加的事件处理程序

```js
$('p').off() // 解绑p元素所有事件处理程序
$('p').off( 'click') // 解绑p元素上面的点击事件
$('ul').off('click', 'li') // 解绑事件委托
```

如果有的事件只想触发一次， 可以使用 one() 来绑定事件

#### 3.2.3自动触发事件

有些事件希望自动触发,

比如轮播图自动播放功能跟点击右侧按钮一致，可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发

1.简写形式

```js
element.click()
```

2.自动触发模式

```js
element.trigger('click')
element.triggerHandler('click') //不会触发元素的默认行为
```

### 3.3事件对象

事件被触发，就会有事件对象的产生

```js
element.on(events,[selector],function(event) {})
```

阻止冒泡：event.stopPropagation()

## 4jQuery其他方法

### 4.1jQuery拷贝对象

如果想要把某个对象拷贝给另外一个对象使用，此时可以使用 $.extend() 方法

语法：

```js
$.extend([deep], target, object1, [objectN])
```

- deep: 如果设为 true 为深拷贝，不写则为浅拷贝
- target：要拷贝的目标对象
- object1：待拷贝到第一个对象的对象
- objectN：待拷贝到第 N 个对象的对象

浅拷贝是把被拷贝的 对象复杂数据类型 中的地址拷贝给目标对象，修改目标对象会影响被拷贝对象，对于简单数据类型属性，则不会拷贝地址

深拷贝，前面加 true， 完全克隆（拷贝的对象,而不是地址），修改目标对象不会影响被拷贝对象

### 4.2多库共存

Query 使用 $ 作为标示符，随着 jQuery 的流行,其他 js 库也会用这 $ 作为标识符， 这样一起使用会引起冲突

要让 jQuery 和其他的 js 库不存在冲突，可以同时存在，这就叫做多库共存

解决方案：

1.把里面的 $ 符号 统一改为 jQuery，比如 jQuery('div')

2.jQuery 变量规定新的名称：$.noConflict()

```js
var suibian = $.noConflict();
suibian('div');
```

### 4.3jQuery插件

jQuery 功能比较有限，想要更复杂的特效效果，可以借助于 jQuery 插件完成

这些插件也是依赖于 jQuery 来完成的，所以必须要先引入 jQuery 文件，因此也称为 jQuery 插件

jQuery 插件库：http://www.jq22.com/

jQuery 之家：http://www.htmleaf.com/
