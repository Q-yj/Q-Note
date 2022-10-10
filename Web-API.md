# Web API

API 全称是 Application Programming Interface ，意为应用程序接口

之前的 JS 基础部分，主要是 ECMAScript ，而 Web API 就是浏览器提供得一套操作浏览器功能和页面元素的 API 即 BOM 和 DOM

## 1DOM基础

Document Object Model，文档对象模型，简称DOM ，是W3C组织推荐的处理可扩展标记语言（HTML或者XML）的标准编程接口

W3C已经定义了一系列的DOM接口，通过这些DOM接口可以改变网页的内容、结构和样式

DOM 树：

- 文档：一个页面就是一个文档，DOM中使用 document 表示
- 元素：页面中的所有标签都是元素，DOM中使用 element 表示
- 节点：网页中的所有内容都是节点（标签、属性、文本、注释等），DOM中使用 node 表示

以上都被称之为对象

### 1.1获取元素

DOM 在实际开发中主要用来操作元素，所以需要先获取元素

获取页面中的元素可以使用以下几种方式:

- 根据 ID 获取
- 根据标签名获取
- 通过 HTML5 新增的方法获取
- 特殊元素获取

#### 1.1.1根据ID获取

使用 getElementByld() 方法可以获取带有 ID 的元素对象，并返回一个 Element 对象

#### 1.1.2根据标签名获取

使用 getElementsByTagName() 方法可以返回带有指定标签名的对象的集合

- 返回的是元素对象的集合，以伪数组形式表示
- 可以遍历返回的伪数组
- 得到的元素对象是动态的
- 若没有元素，则返回空的伪数组 []

指定父元素，父元素必须是指定的单个元素

```js
var ol = document.getElementsByTagName('ol');
console.log(ol[0].getElementsByTagName('li'));
```

若给 ol 指定了 id: ol

```js
let ol = document.getElementById('ol');
console.log(ol.getElementsByTagName('li');
```

#### 1.1.3根据HTML5新增的方法获取

根据类名返回元素对象集合：

```js
document.getElementsByClassName('类名');
```

根据指定选择器返回第一个元素对象：

```js
document.querySelector('选择器'); 
```

返回指定选择器的所有元素集合：

```js
document.querySelectorAll('选择器');
```

对于这些获取事件，要不就是返回一个元素对象，要不就是返回一个对象集合

对于返回的对象集合，都可以是作为一种伪数组来表示

#### 1.1.4获取特殊元素

获取 body 元素：

```js
document.body;
```

获取 html 元素：

```js
document.documentElement;
```

### 1.2事件基础

JavaScript 使我们有能力创建动态页面，而事件是可以被 JavaScript 侦测到的行为

网页中的每个元素都可以产生某些可以触发 JavaScript 的事件

例如我们可以在用户点击某按钮时产生一个事件，然后去执行某些操作

#### 1.2.1事件三要素

事件源：事件被触发的对象

```html
<button id="btn">
    唐伯虎
</button>
```

事件类型：如何触发、什么事件

```js
var btn = document.getElementById('btn');
```

事件处理程序：可通过一个函数赋值的方式实现

```js
btn.onclick = function() {
    alert('点秋香');
}
```

#### 1.2.2执行事件的步骤

1. 获取事件源
2. 注册事件（绑定事件）
3. 添加事件处理程序（函数赋值）

### 1.3操作元素

使用 JavaScript DOM 可以改变网页内容、结构和样式

#### 1.3.1改变元素内容

```html
<button>显示当前系统时间</button>
<div>某个时间</div>
```

```js
// 当我们点击了按钮，div里面的文字会发生变化
// 1.获取元素 
var btn = document.querySelector('button');
var div = document.querySelector('div');
// 2.注册事件
btn.onclick = function() {
    div.innerHTML = getDate();
}
// 3.事件处理程序 获取当前系统时间
function getDate() {
   var date = new Date();
   var year = date.getFullYear();
   var month = date.getMonth() + 1;
   var dates = date.getDate();
   var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
   var day = date.getDay();
   return '今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day];
}
```

innerText 和 innerHTML的区别：
1. innerText 不识别html标签 非标准  去除空格和换行
1. innerHTML 识别html标签 W3C标准 保留空格和换行

这两个属性是可读写的  可以获取元素里面的内容

#### 1.3.2修改元素属性

```html
<button id="ldh">刘德华</button>
<button id="zxy">张学友</button> <br>
<img src="images/ldh.jpg">
<script>
    // 修改元素属性  src
    // 1.获取元素
	var ldh = document.getElementById('ldh');
	var zxy = document.getElementById('zxy');
	var img = document.querySelector('img');
	// 2.注册事件  
	// 3.处理程序
	zxy.onclick = function() {
	    img.src = 'images/zxy.jpg';
	}
	ldh.onclick = function() {
	    img.src = 'images/ldh.jpg';
}
</script>
```

#### 1.3.3修改样式属性

我们可以通过 JS 修改元素的大小、颜色、位置等样式

1. element.style：行内样式操作
2. element.className：类名样式操作

```html
<style>
    div {
        width: 200px;
        height: 200px;
        ackground-color: pink;
    }
</style>
<div></div>
<script>
    // 1. 获取元素
    var div = document.querySelector('div');
    // 2. 注册事件 
    // 3. 处理程序
    div.onclick = function() {
        this.style.backgroundColor = 'purple';
        this.style.width = '250px';
    }
</script>
```

注意：

1. Js 里面的样式采取驼峰命名法比如 fontSize、backgroundColor
2. JS修改 style 样式操作，产生的是行内样式，css 权重比较高
3. 如果样式修改较多，可以采取操作类名方式更改元素样式
4. class 因为是个保留字，因此使用 className 来操作元素类名属性
5. className 会直接更改元素的类名，会覆盖原先的类名

#### 1.3.4排他思想

如果有同一组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想算法：

1. 所有元素全部清除样式
2. 给当前元素设置样式
3. 注意顺序不能颠倒

根据这个算法可以用来实现鼠标经过每一行时背景变色

```js
const btns = document.getElementsByTagName('button');
for (let i = 0; i < btns.length; i++) {
    btns[i].onclick = function () {
        for (let j=0;j<btns.length;j++) {
            btns[j].style.backgroundColor = '';
        }
        this.style.backgroundColor = 'pink';
    }
}
```

#### 1.3.5自定义属性

程序员自己添加的属性称为自定义属性

自定义属性目的：

是为了保存并使用数据，有些数据可以保存到页面中而不用保存到数据库中

获取属性：

- element.属性，获取元素自带的属性值
- element.getAttribute('属性')，获取自定义属性

设置属性值：

- element.属性= '值';，设置元素自带的属性值
- element.setAttribute('属性','值');，设置自定义属性

对于 element.setAttribute 方法，若属已存在，则更新该属性值；否则，创建一个新属性

使用 element.属性 获取或设置类名时，要用 className，而对于 element.setAttribute() 方法，直接使用 class，即：div.setAttribute('class', 'footer');

移除属性：

div.removeAttribute('index');

#### 1.3.6H5自定义属性

H5规定自定义属性以 data- 开头作为属性名并赋值

```html
<div data-index="1"></div>
```

兼容性获取 element.getAttribute('data-index')

H5新增方法 element.dataset.index 或 element.dataset['index'] 获取

dataset 是一个集合里面存放了所有以 data- 开头的自定义属性

如果自定义属性里面有多个链接的单词，则使用驼峰命名法获取

### 1.4节点操作

获取元素通常使用两种方式:

- 利用DOM提供的方法获取元素
- 利用节点层级关系获取元素

DOM提供的方法逻辑性不强而且很繁琐，所以可以利用节点获取，虽然兼容性不好，但是逻辑性强

#### 1.4.1节点概述

网页中的所有内容都是节点(标签、属性、文本、注释等），在DOM中，节点使用 node 来表示

HTML DOM 树中的所有节点均可通过 JavaScript 进行访问，所有 HTML 元素（节点）均可被修改，也可以创建或删除

一般地，节点至少拥有 `nodeType` (节点类型)、`nodeName` (节点名称）和 `nodeValue` (节点值）这三个基本属性

三种基本节点类型：

- 元素节点 nodeType 为 1
- 属性节点 nodeType 为 2
- 文本节点 nodeType 为 3（文字、空格、换行）

实际开发中，主要操作的还是元素节点

#### 1.4.2节点层级

##### 1.4.2.1父级节点

node.parentNode

获取离元素最近的父节点，若找不到则返回 null

##### 1.4.2.2子级节点

parentNode.childNodes

包含指定节点的子节点的集合，该集合为即时更新的集合

当中包含了所有的子节点，包括元素节点，文本节点等

如果只想要获得里面的元素节点，则需要专门处理

```js
// 筛选元素节点
for (let i = 0; i < ul.childNodes.length; i++) {
    if (ul.childNodes[i].nodeType === 1) {
        console.log(ul.childNodes[i]);
    }
}
```

一般不提倡使用 childNodes

提倡使用 parentNode.children 获取所有的子元素节点

子节点方法：

获取所有结点中的第一个和最后一个：

- parentNode.firstChild
- parentNode.lastChild

获取元素节点中第一个和最后一个：

- parentNode.firstElementChild
- parentNode.lastElementChild

实际开发的写法（没有兼容性问题）：

- parentNode.children[0]
- parentNode.children[parentNode.children.length -1]

##### 1.4.2.3兄弟节点

node.nextsibling / node.previousSibling 返回当前元素的下/上一个兄弟节点，找不到则返回 null

这个兄弟节点包含元素节点或者文本节点等等

node.nextElementSibling / node.previousElementSibling 返回当前元素下/上一个兄弟元素节点，找不到则返回 null

注意，这两个方法存在兼容性问题，只支持 IE9 以上

```js
// 处理 <IE9 兼容性问题
function getNextElementSibling(node) {
    let n = node;
    while (n = n.nextSibling) {
        if (n.nodeType === 1) {
            return n;
        }
    }
    return null;
}
```

#### 1.4.3节点操作

##### 1.4.3.1创建并添加节点

document.createElement("tagName");

document.createElement() 方法创建由 tagName 指定的 HTML 元素，因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点

在创建了元素节点后，还需要将节点添加到页面中，appendChild() 方法可以给元素节点添加子元素节点，若某元素已存在则重复添加，在页面已存在的元素后面追加新节点

```js
parentNode.appendChild(chileNode);
```

也可以使用 insertBefore() 方法在指定元素的前面插入节点

注意：在一个页面中要添加元素节点，先创建节点，然后添加节点

##### 1.4.3.2删除节点

removeChild(childNode) 

删除一个子节点，并返回删除的节点，其中 childNode 为待删除的子节点

##### 1.4.3.3克隆节点

node.cloneNode([deep]) 方法返回调用该方法的节点的一个副本，也称为复制节点或拷贝节点，其中 node 为被克隆的元素节点

| deep参数 |                     含义                     |
| :------: | :------------------------------------------: |
|   true   |    深拷贝，同时复制节点本身和里面的子节点    |
|  false   | 浅拷贝，只复制节点本身，不复制子节点（默认） |

#### 1.4.4三种动态创建元素的区别

- document.write()：是直接将内容写入页面的内容流，但是当文档流执行完毕，会导致页面全部重绘，即覆盖原本的页面
- innerHTML： 是将内容写入某个 DOM 节点，不会导致页面全部重绘，创建多个元素效率更高，结构稍微复杂（不拼接字符串，采用数组形式拼接）
- createElement()： 创建多个元素效率略低，但是结构更清晰

总结：不同浏览器下，innerHTML 效率要比 createElement 高

### 1.5DOM重点核心

关于 DOM 操作，主要针对元素的操作，主要有 创、增、删、改、查、属性操作、事件操作

创：

- document.write
- innerHTML
- createElement

增：

- appendChild
- insertBefore

删：removeChild

改：修改 DOM 的元素属性

- 修改元素属性：src、href、title 等
- 修改普通元素内容：innerHTML、innerText 
- 修改表单元素：value、type、disabled 等
- 修改元素样式：style、className

查：获取查询 DOM 的元素

- DOM 提供的 API 方法：getElementById、getElementsByTagName 古老用法，不推荐
- H5 提供的新方法：querySelector、querySelectorAll 提倡使用
- 利用节点操作：父（partentNode）、子（children）、兄（previousElementSibling、nextElementSibling）

属性操作：自定义属性

- 设置 DOM 的属性值 setAttribute
- 得到 DOM 的属性值 getAttribute
- 移除属性 removeAttribute

事件操作：事件源 . 事件类型 =事件处理程序

|  鼠标事件   |     触发条件     |
| :---------: | :--------------: |
|   onclick   | 鼠标点击左键触发 |
| onmouseover |   鼠标经过触发   |
| onmouseout  |   鼠标离开触发   |
|   onfocus   | 获得鼠标焦点触发 |
|   onblur    | 失去鼠标焦点触发 |
| onmousemove |   鼠标移动触发   |
|  onmouseup  |   鼠标弹起触发   |
| onmousedown |   鼠标按下触发   |

## 2事件高级

### 2.1注册事件

给元素添加事件，称为注册事件或者绑定事件

注册事件有两种方式：传统方式和事件侦听注册方式

#### 2.1.1传统方式

- 利用on 开头的事件，如 onclick 点击事件
- 特点：注册事件的唯一性
- 同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数

#### 2.1.2事件侦听方式

- w3c 标准推荐方式
- addEventListener() 它是一个方法
- 里面的事件类型是字符串必定加引号而且不带on，如 'click' 点击
- IE9 之前的 IE 不支持此方法，可使用 attachEvent() 代替
- 特点：同一个元素同一个事件可以注册多个侦听器
- 按注册顺序依次执行

```js
eventTarget.addEventListener(type, listener[, useCapture]);
```

eventTarget.addEventListener() 方法将指定的侦听器注册到 eventTarget（目标对象）上

当该对象触发指定的事件时，就会执行事件处理函数

该方法接收三个参数：

- type：事件类型字符串，比如 click 、mouseover，注意这里不要带 on
- listener：事件处理函数，事件发生时，会调用该侦听函数
- useCapture：可选参数，是一个布尔值，默认是 false

### 2.2删除事件

#### 2.2.1传统方式

```js
eventTarget.onclick = null;
```

#### 2.2.2事件侦听方式

```js
eventTarget.removeEventListener(type, listener[, useCapture]);
```

一个对象可能绑定了很多事件，对于 removeEventListener 方法，需要指定要删除的事件 listener，所以在注册事件的时候需要提前将事件函数封装在一个变量里，然后把变量传给 removeEventListener 方法

### 2.3DOM事件流

事件流描述的是从页面中接收事件的顺序

事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即 DOM 事件流

事件流分为三个阶段：

- 捕获阶段
- 当前目标阶段
- 冒泡阶段

事件捕获：网景最早提出，由DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程

事件冒泡：IE 最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点的过程

解释：

假如我们向水里面扔一块石头，首先它会有一个下降的过程，这个过程就可以理解为从 最顶层向事件 发生的 最具体元素 的捕获过程

之后会产生泡泡，会在 最具体元素 之后漂浮到水面上，这个过程相当于事件冒泡

注意：

- JS 代码中只能执行捕获或者冒泡其中的一个阶段
- onclick 和 attachEvent 只能得到冒泡阶段
- addEventListener(type, listener[, useCapture]) 第三个参数如果是 true，表示在事件捕 获阶段调用事件处理程序；如果是 false（默认 false），表示在事件冒泡阶段调用事件处理程序
- 实际开发中很少使用事件捕获，更关注事件冒泡
- 有些事件是没有冒泡的，比如 onblur、onfocus、onmouseenter、onmouseleave

### 2.4事件对象

```js
eventTarget.onclick = function(event) {}
eventTarget.addEventListener('click', function(event) {}）
```

官方解释：event 对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态

简单理解：事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面，这个对象就是事件对象 event，它有很多属性和方法

- event 就是一个事件对象 写到侦听函数的小括号里面当形参来看
- 事件对象只有有了事件才会存在，它是系统自动创建的，不需要传递参数
- 事件对象是事件的一系列相关数据的集合，跟事件相关的，比如鼠标点击就包含了鼠标的相关信息，鼠标坐标等，如果是键盘事件里面就包含的键盘事件的信息，判断用户按下了哪个键
- 这个事件对象可以自己命名，比如 event 、 evt、 e(常用)
- 事件对象也有兼容性问题， ie678 通过 window.event ，兼容性的写法  e = e || window.event;

#### 2.4.1事件对象的常见属性和方法

|   事件对象属性方法   |             说明              |
| :------------------: | :---------------------------: |
|       e.target       |  返回触发事件的对象（标准）   |
|     e.srcElement     | 返回触发事件的对象（非标准）  |
|        e.typ         |         返回事件类型          |
|  e.preventDefault()  |     阻止默认事件（标准）      |
| e.returnValue = true | 阻止默认事件（非标准，IE678） |
| e.stopPropagation()  |       阻止冒泡（标准）        |
|    e.cancelBubble    |   阻止冒泡（非标准，IE678）   |

#### 2.4.2e.target与this的比较

e.target 返回的是触发事件的对象（元素）

this 返回的是绑定事件的对象（元素）

```html
<ul>
    <li>123</li>
    <li>456</li>
    <li>789</li>
</ul>
<script>
    let ul = document.querySelector("ul");
    ul.addEventListener('click', function (e) {
    console.log(e.target); // 返回 li
    console.log(this); // 返回 ul
    })
</script>
```

#### 2.4.3阻止事件默认行为

阻止链接跳转，阻止提交按钮提交

```js
//DOM 标准写法
a.addEventListener ('click', function (e) {
    e.preventDefault();
});
```

```js
//兼容写法
a.onclick = function (e) {
    e.returnValue;
    //或者
    return false;
}
```

### 2.5阻止事件冒泡

事件冒泡本身的特性，会带来的坏处，也会带来的好处，需要灵活掌握

点击了某一个元素节点，这个节点不一定绑定了事件，但是由于 DOM 事件流的冒泡现象，会触发其父节点所绑定的事件

标准写法：利用事件对象里面的 stopPropagation() 方法

```js
e.stopPropagation();
```

非标准写法：IE 6-8 利用事件对象 cancelBubble 属性

```js
e.cancelBubble = true;
```

给相应的子元素节点设置事件的 stopPropagation() 方法，相当于在这个节点阻断了事件冒泡，事件无法继续传递至父节点

举例：

```html
<div class="father">
    <div class="son">son儿子</div>
</div>
<script>
    var son = document.querySelector('.son');
    son.addEventListener('click', function(e) {
        alert('son');
        e.stopPropagation();
        //e.cancelBubble = true; 非标准
    }, false);
    var father = document.querySelector('.father');
    father.addEventListener('click', function() {
        alert('father');
    }, false);
    document.addEventListener('click', function() {
        alert('document');
    })
</script>
```

### 2.6事件委托

事件冒泡本身的特性，会带来的坏处，也会带来的好处，需要灵活掌握

假设有程序，ul 包含很多 li ，需要给每个 li 都注册某个事件，按以往的思维，需要使用 for 循环遍历每一个 li ，这样很麻烦，而且访问 DOM 的次数越多，就会延长整个页面的交互就绪时间，所以，对于此类情况便产生了事件委托

- 事件委托也称为事件代理，在jQuery 里面称为事件委派
- 事件委托原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
- 优点：只操作了一次 DOM ，提高了程序性能

对于上述程序，只需给 ul 注册点击事件，然后利用事件对象的 target 来找到当前点击的 li，因为点击 li，事件会冒泡到ul 上，ul 有注册事件，就会触发事件侦听器

### 2.7常用鼠标事件

#### 2.7.1常用鼠标事件

禁止鼠标右键菜单

contextmenu 主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单

```js
document.addEventListener('contextmenu', function(e) {
    e.preventDefault();
})
```

禁止鼠标选择文字

```js
document.addEventListener('selectstart', function(e) {
    e.preventDefault();
})
```

#### 2.7.2鼠标事件对象

event 对象代表事件的状态，跟事件相关的一系列信息的集合

现阶段我们主要是用鼠标事件对象 MouseEvent 和键盘事件对象 KeyboardEvent

| 鼠标事件对象 |                  说明                   |
| :----------: | :-------------------------------------: |
|  e.clientX   | 返回鼠标相对于浏览器窗口可视区的 X 坐标 |
|  e.clientY   | 返回鼠标相对于浏览器窗口可视区的 Y 坐标 |
|   e.pageX    | 返回鼠标相对于文档页面的 X 坐标IE9+支持 |
|   e.pageY    | 返回鼠标相对于文档页面的 Y 坐标IE9+支持 |
|  e.screenX   |     返回鼠标相对于电脑屏幕的 X 坐标     |
|  e.screenY   |     返回鼠标相对于电脑屏幕的 Y 坐标     |

### 2.8常用键盘事件

#### 2.8.1常用键盘事件

|  键盘事件  |                           触发事件                           |
| :--------: | :----------------------------------------------------------: |
|  onkeyup   |                   某个键盘按键被松开时触发                   |
| onkeydown  |                   某个键盘按键被按下时触发                   |
| onkeypress | 某个键盘按键被按下时触发，但是不识别功能键（ctrl、shif、箭头等） |

onkeypress 已废弃，虽然还是有浏览器支持，但是未来可能会停止支持，使用 keydown 代替

#### 2.8.2键盘事件对象

| 键盘事件对象属性 |               说明               |
| :--------------: | :------------------------------: |
|       key        | 返回物理按键的名称值（推荐使用） |
|     keyCode      |        返回该键的ASCII值         |

keyCode 已废弃:，该特性已经从 Web 标准中删除，虽然一些浏览器目前仍然支持它，但也许会在未来的某个时间停止支持，请尽量不要使用该特性，使用 key 代替

## 3BOM基础

BOM（Browser Object Model）即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window

BOM 由一系列相关的对象构成，并且每个对象都提供了很多方法与属性

BOM 缺乏标准，JavaScript 语法的标准化组织是ECMA，DOM 的标准化组织是 W3C，BOM 最初是Netscape 浏览器标准的一部分

|                   DOM                    |                       BOM                        |
| :--------------------------------------: | :----------------------------------------------: |
|               文档对象模型               |                  浏览器对象模型                  |
| DOM 就是把「文档」当做一个「对象」来看待 |        把「浏览器」当做一个「对象」来看待        |
|        DOM 的顶级对象是 document         |             BOM 的顶级对象是 window              |
|       DOM 主要学习的是操作页面元素       |       BOM 学习的是浏览器窗口交互的一些对象       |
|            DOM 是W3C 标准规范            | BOM 是浏览器厂商在各自浏览器上定义的，兼容性较差 |

BOM 包含了 DOM

### 3.1BOM顶级对象window

window 对象是浏览器的顶级对象，它具有双重角色

它是 JS 访问浏览器窗口的一个接口

它是一个全局对象，定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法，在调用的时候可以省略 window，前面学习的对话框都属于 window 对象方法，如 alert()、prompt() 等

#### 3.1.1window对象常见事件

##### 3.1.1.1窗口加载事件

```js
window.onload = function() {};
window.addEventListener("load", function(){});
```

window.onload 是窗口加载事件,当文档内容完全加载完成会触发该事件（包括图像、脚本文件、CSS文件等）, 就调用的处理函数

注意：

- 有了 window.onload 就可以把 JS 代码写到页面元素的上方，因为onload 是等页面内容全部加载完毕， 再去执行处理函数
- window.onload 传统注册事件方式只能写一次，如果有多个，会以最后一个 window.onload 为准
- 如果使用 addEventListener 则没有限制

```js
document.addEventListener('DOMContentLoaded', function() {});
```

DOMContentLoaded 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等

如果页面的图片很多的话, 从用户访问到 onload 触发可能需要较长的时间, 交互效果就不能实现，必然影响用户的体验，此时用 DOMContentLoaded 事件比较合适

##### 3.1.1.2窗口大小事件

```js
window.onresize = function(){}
window.addEventListener("resize",function(){});
```

window.onresize 是调整窗口大小加载事件, 当触发时就调用的处理函数

注意：

- 只要窗口大小发生像素变化，就会触发这个事件
- 我们经常利用这个事件完成响应式布局
- window.innerWidth 是当前屏幕的宽度

#### 3.1.2定时器

##### 3.1.2.1setTimeout()定时器

```js
window.setTimeout(调用函数 [, 延迟的毫秒数]);
```

setTimeout() 方法用于设置一个定时器，该定时器在定时器到期后执行调用函数

注意：

- window 可以省略。
- 这个调用函数可以直接写函数，或者写函数名或者采取字符串'函数名()' 三种形式，第三种不推荐
- 延迟的毫秒数省略默认是 0，如果写，必须是毫秒
- 定时器可能有很多，所以经常给定时器赋值一个标识符

setTimeout() 这个调用函数我们也称为 回调函数callback，普通函数是按照代码顺序直接调用，而这个函数，需要等待时间，时间到了才去调用这个函数，因此称为回调函数

回调，就是回头调用的意思，上一件事干完，再回头再调用这个函数

element.onclick = function(){} 或者 element.addEventListener(“click”, fn); 里面的函数也是回调函数

```js
window.clearTimeout(timeoutID);
```

clearTimeout() 方法用于取消先前通过调用 setTimeout() 建立的定时器

里面的参数就是定时器的标识符

##### 3.1.2.2setInterval()定时器

```js
window.setInterval(回调函数 [, 间隔的毫秒数]);
```

setInterval() 方法重复调用一个函数，每隔这个时间，就去调用一次回调函数

注意：

- window 可以省略。
- 这个调用函数可以 直接写函数，或者写函数名或者采取字符串'函数名()' 三种形式。
- 间隔的毫秒数省略默认是 0，如果写，必须是毫秒，表示每隔多少毫秒就自动调用这个函数。
- 因为定时器可能有很多，所以我们经常给定时器赋值一个标识符。
- 第一次执行也是间隔毫秒数之后执行，之后每隔毫秒数就执行一次

```js
window.clearInterval(intervalID);
```

clearInterval() 方法取消了先前通过调用 setInterval() 建立的定时器

里面的参数就是定时器的标识符

#### 3.1.3this指向问题

this 的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定 this 到底指向谁，一般情况下的最终指向的是那个调用它的对象现阶段

- 全局作用域或者普通函数中 this 指向全局对象 window（注意定时器里面的 this 指向 window）
- 方法调用中谁调用 this 指向谁
- 构造函数中 this 指向构造函数的实例

### 3.2JS执行队列

JavaScript 语言的一大特点就是单线程，也就是说同一个时间只能做一件事，因为 Javascript 这门脚本语言诞生的使命所致（JavaScript 是为处理页面中用户的交互，以及操作DOM ）

比如我们对 某个DOM 元素进行添加和删除操作，不能同时进行，应该先进行添加，之后再删除

单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务

这样所导致的问题就是，如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉

#### 3.2.1同步与异步

同步：

前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的

同步任务都在主线程上执行，形成一个 执行栈

异步：

在做一件任务时，因为这件任务会花费很长时间，在做这件的同时，还可以去处理其他任务

JS 的异步是通过回调函数实现的，异步任务相关回调函数添加到任务队列中（任务队列也称为消息队列）

异步任务一般有：

- 普通事件， click、resize 等
- 资源加载， load、error 等
- 定时器， setInterval、setTimeout 等

#### 3.2.2JS执行机制

- 先执行 执行栈中的同步任务
- 异步任务（回调函数）放入任务队列中
- 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取 任务队列 中的异步任务，于是被读取的异步务结束等待状态，进入执行栈，开始执行

举例：

```js
console.log(1);
document.addEventListener("click", function  () {
    console.log("click");
});
setTimeout(function () {
    console.log(3);
}, 3000);
console.log(2);
```

若不触发点击事件，结果将依次输出 1、2、3；若点击事件在 3 秒前触发，则依次输出 1、2、click、3；若点击事件在 3 秒后触发，则依次输出 1、2、3、click

### 3.3location对象

window 对象给我们提供了一个 location 属性用于 获取或设置窗体的URL，并且可以用于 解析 URL。因为这个属性返回的是一个对象，所以我们将这个属性也称为 location 对象

#### 3.3.1URL

统一资源定位符（Uniform Resource Locator, URL）是互联网上标准资源的地址

互联网上的每个文件都有 一个唯一的 URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它

格式：protocol://host[:port]/path/[?query]#fragment

|   组成   |                             说明                             |
| :------: | :----------------------------------------------------------: |
| protocol |                    通信协议（http、ftp）                     |
|   host   |                         主机（域名）                         |
|   port   |  端口号（可选），省略时使用方案的默认端口，如http默认端口80  |
|   path   | 路径，由零或多个 `/` 隔开的字符串，一般表示主机上的一个目录或文件地址 |
|  query   |           参数，以键值对的形式，通过 & 符号分隔开            |
| fragment |              片段，# 后面内容，常见于链接、锚点              |

#### 3.3.2location对象的方法

|        方法        |                            返回值                            |
| :----------------: | :----------------------------------------------------------: |
| location.assign()  |        跟 href 一样，可以跳转页面（也称为重定向页面）        |
| location.replace() |        替换当前页面，因为不记录历史，所以不能后退页面        |
| location.reload()  | 重新加载页面，相当于刷新按钮或者 f5 如果参数为 true 强制刷新 ctrl+f5 |

#### 3.3.3location对象的属性

|         属性          |                 返回值                 |
| :-------------------: | :------------------------------------: |
|  location.href(重点)  |          获取或者设置 整个URL          |
|     location.host     |            返回主机（域名）            |
|     location.port     |     返回端口号，未写则返回空字符串     |
|   location.pathname   |                返回路径                |
| location.search(重点) |                返回参数                |
|     location.hash     | 返回片段，# 后面内容，常见于链接、锚点 |

### 3.4navigator对象

navigator 对象包含有关浏览器的信息，它有很多属性，我们最常用的是 userAgent，该属性可以返回由客 户机发送服务器的 user-agent 头部的值

举例：判断用户使用哪个终端打开页面

```js
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = ""; //手机
} else {
    window.location.href = ""; //电脑
}
```

### 3.5history对象

window 对象给我们提供了一个 history 对象，与浏览器历史记录进行交互

该对象包含用户（在浏览器窗口中）访问过的URL

history 对象一般在实际开发中比较少用，但是会在一些OA 办公系统中见到

|   方法    |                         作用                          |
| :-------: | :---------------------------------------------------: |
|  back()   |                   网页地址后退功能                    |
| forward() |                       前进功能                        |
| go(参数)  | 前进后退功能，参数为 1，前进一个页面，-1 后退一个页面 |

## 4PC端网页特效

### 4.1元素偏移量offset

#### 4.1.1offset概述

offset 翻译过来就是偏移量，使用 offset 系列相关属性可以动态的得到该元素的位置（偏移）、大小等

- 获得元素距离带有定位父元素的位置
- 获得元素自身的大小（宽度高度）
- 注意：返回的数值都不带单位

| offset 属性  |                           作用                           |
| :----------: | :------------------------------------------------------: |
| offsetParent | 返回该元素带有定位的父级元素，如果父级没有定位则返回body |
|  offsetTop   |         返回该元素相对带有定位父元素上方的偏移量         |
|  offsetLeft  |         返回该元素相对带有定位父元素左方的偏移量         |
| offsetWidth  |     返回自身 padding、border、width 的宽度，不带单位     |
| offsetHeight |    返回自身 padding、border、height 的高度，不带单位     |

#### 4.1.2offset与style的区别

offset：

- offset 可以得到任意样式表中的样式值
- offset 系列获得的数值是没有单位的
- offsetWidth 包含 padding+border+width
- offsetWidth 等属性是只读属性，只能获取不能赋值
- 所以，想要获取元素大小位置，用 offset更合适

style：

- style 只能得到行内样式表中的样式值
- style.width 获得的是带有单位的字符串
- style.width 获得不包含 padding 和 border 的值
- style.width 是可读写属性，可以获取也可以赋值
- 所以，想要给元素更改值，则需要用 style 改变

#### 4.1.3案例：拖动的模态框

### 4.2元素可视区client

client 翻译过来就是客户端，使用 client 系列的相关属性来获取元素可视区的相关信息

通过client 系列的相关属性可以动态的得到该元素的边框大小、元素大小等

| client 属性  |                           作用                            |
| :----------: | :-------------------------------------------------------: |
|  clientTop   |                   返回元素上边框的大小                    |
|  clientLeft  |                   返回元素左边框大大小                    |
| clientWidth  | 返回自身包括 padding、width ，不含边框，返回数值不带单位  |
| clientHeight | 返回自身包括 padding、height ，不含边框，返回数值不带单位 |

client 和 offsetWidth 最大的区别就是不包含边框

### 4.3元素滚动scroll

scroll 翻译过来就是滚动的，我们使用 scroll 系列的相关属性可以动态的得到该元素的大小、滚动距离等

| scroll 属性  |                     作用                     |
| :----------: | :------------------------------------------: |
|  scrollTop   |   返回被卷上去的上侧距离，返回数值不带单位   |
|  scrollLeft  |   返回被卷上去的左侧距离，返回数值不带单位   |
| scrollWidth  | 返回自身实际宽度，不含边框，返回数值不带单位 |
| scrollHeight | 返回自身实际高度，不含边框，返回数值不带单位 |

如果浏览器的高（或宽）度不足以显示整个页面时，会自动出现滚动条，当滚动条向下滚动时，页面上面被隐藏 掉的高度，我们就称为页面被卷去的头部，滚动条在滚动时会触发 onscroll 事件

可以通过 window.pageYOffset 获得，如果是被卷去的左侧 window.pageXOffset

注意，元素被卷去的头部是 element.scrollTop，左侧 element.scrollLeft

### 4.4一些要点

#### 4.4.1立即执行函数

立即执行函数是指函数定义好后，不需要调用直接执行，即一引入 JS 文件，则该函数自动执行

主要作用：

- 创建一个独立的作用域
- 避免了命名冲突问题

语法：(function() {})() 或者 (function(){}())

举例：

```js
(function () {console.log('hello');})();//hello
(function (a) {console.log(a);})(10);//10
```

#### 4.4.2mouseover和mouseenter的区别

- 当鼠标移动到元素上时就会触发 mouseenter 事件
- mouseover 鼠标经过自身盒子会触发，经过子盒子还会触发
- mouseenter 只会经过自身盒子触发，因为 mouseenter 不会冒泡
- 跟 mouseenter 搭配鼠标离开 mouseleave 同样不会冒泡

### 4.5动画函数封装

#### 4.5.1动画原理

核心原理：通过定时器 setInterval() 不断移动盒子位置

- 获得盒子当前位置
- 让盒子在当前位置加上 1 个移动距离
- 利用定时器不断重复这个操作
- 加一个结束定时器的条件
- 注意此元素需要添加定位（position: absolute），才能使用 element.style.left

#### 4.5.2缓动动画原理

缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来

核心算法：每次移动的距离步长 = (目标值 - 现在的位置) / 10

停止的条件是：让当前盒子位置等于目标位置就停止定时器

注意步长值需要取整

#### 4.5.3封装函数

可以传递三个参数，动画对象 obj 、移动到的距离 target 、回调函数 callback

#### 4.5.4案例：品优购轮播图案例

#### 4.5.5案例：仿淘宝返回顶部案例

#### 4.5.6案例：筋斗云导航栏案例

## 5移动端网页特效

### 5.1触摸事件

移动端浏览器兼容性较好，我们不需要考虑以前JS 的兼容性问题，可以放心的使用原生JS 书写效果，但是移动端也有自己独特的地方

比如触屏事件 touch（也称触摸事件），Android 和IOS 都有

touch 对象代表一个触摸点

触摸点可能是一根手指，也可能是一根触摸笔，触屏事件可响应用户手指（或触控笔）对屏幕或者触控板操作

常见触摸事件：

|    事件    |              说明               |
| :--------: | :-----------------------------: |
| touchstart |  手指触摸到一个 DOM 元素时触发  |
| touchmove  | 手指在一个 DOM 元素上滑动时触发 |
|  touchend  | 手指从一个 DOM 元素上移开时触发 |

#### 5.1.1触摸事件对象

TouchEvent 是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件

这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少等等

touchstart、touchmove、touchend 三个事件都会各自有事件对象

|        列表         |                       说明                       |
| :-----------------: | :----------------------------------------------: |
|       touches       |         正在触摸屏幕的所有手指的一个列表         |
| targetTouches(重点) |     正在触摸当前 DOM 元素上的手指的一个列表      |
|   changedTouches    | 手指状态发生了改变的列表，从无到有，从有到无变化 |

#### 5.1.2移动端拖动元素

拖动元素需要当前手指的坐标值我们可以使用 targetTouches[0] 里面的 pageX 和 pageY

移动端拖动的原理：手指移动中，计算出手指移动的距离。然后用盒子原来的位置+ 手指移动的距离

手指移动的距离：手指滑动中的位置减去手指刚开始触摸的位置

拖动元素：

- 触摸元素 touchstart ：获取手指初始坐标，同时获得盒子原来的位置
- 移动手指 touchmove ：计算手指的滑动距离，并且移动盒子
- 离开手指 touchend

注意：手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动 e.preventDefault();

### 5.2classList使用

classList 属性是 HTML5 新增的一个属性，返回元素的类名，但是 ie10 以上版本支持

该属性用于在元素中添加，移除及切换 CSS 类

添加类：

```js
focus.classList.add('current');
```

移除类：

```js
focus.classList.remove('current');
```

切换类：

```js
focus.classList.toggle('current');
```

### 5.3click延时解决方案

移动端 click 事件会有 300ms 的延时，原因是移动端屏幕双击会缩放（double tap to zoom）页面

（1）禁用缩放

浏览器禁用默认的双击缩放行为并且去掉300ms 的点击延迟

```html
<meta name="viewport" content="user-scalable=no">
```

（2）利用 touch 事件

原理：

- 当我们手指触摸屏幕，记录当前触摸时间
- 当我们手指离开屏幕，用离开的时间减去触摸的时间
- 如果时间小于 150ms，并且没有滑动过屏幕，那么我们就定义为点击

（3）利用 fastclick 插件

使用 fastclick 插件解决300ms 延迟，引入fastclick 插件

官方地址：https://github.com/ftlabs/fastclick

## 6本地存储

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，HTML5 规范提出了相关解决方案

特性：

- 数据存储在用户浏览器中
- 设置、读取方便、甚至页面刷新不丢失数据
- 容量较大，sessionStorage 约5M、localStorage 约20M
- 只能存储字符串，可以将对象 JSON.stringify() 编码后存储

### 6.1sessionStorage

特点：

- 生命周期为 关闭浏览器窗口
- 在同一个窗口（页面）下数据可以共享
- 以键值对的形式存储使用

存储数据：

```js
sessionStorage.setItem(key, value);
```

获取数据：

```js
sessionStorage.getItem(key);
```

删除数据：

```js
sessionStorage.removeItem(key);
```

删除所有数据：

```js
sessionStorage.clear();
```

### 6.2localStorage

特点：

- 生命周期 永久生效，除非手动删除否则关闭页面也会存在
- 可以多窗口（页面）共享（同一浏览器可以共享）
- 以键值对的形式存储使用

存储数据：

```js
localStorage.setItem(key, value);
```

获取数据：

```js
localStorage.getItem(key);
```

删除数据：

```js
loaclStorage.removeItem(key);
```

删除所有数据：

```js
localStorage.clear();
```
