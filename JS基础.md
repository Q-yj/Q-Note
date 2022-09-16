# JS

JS，即“JavaScript” 由创始人布兰登·艾奇在1995年用十天的时间完成了JavaScript的设计，网景公司最初命名为LiveScript，后来与Sun公司合作之后将其改为JavaScript

## 1 初识JS

### 1.1 JS是什么

JavaScript是世界上最流行的语言之一，是一种运行在客户端的脚本语言，脚本语言就是不需要编译，运行过程中由js解释器（js引擎）逐行来进行解释并执行，现在也可以基于Nodejs技术进行服务器端编程

### 1.2 JS的作用

- 表单动态校验（密码强度检测）（JS产生的最初目的）

- 网页特效

- 服务器端开发（Node.js）

- 桌面程序（Electron）

- App（Cordova）

- 控制硬件—物联网（Ruff）

- 游戏开发（cocos2d-js）  


### 1.3 浏览器执行JS

浏览器本身并不会执行JS代码，而是通过内置JavaScript引擎来解释JS代码，JS代码执行时逐行解释每一句源码，然后由计算机去执行，所以JavaScript语言为脚本语言

### 1.4 JS三大组成

#### 1.4.1 ECMAScript

ECMAScript是由ECMA国际（原欧洲计算机制造商协会）进行标准化的一门编程语言。这种语言在万维网上应用广泛，它被称为JavaScript或JScript，但实际上后两者时ECMAScript语言的实现和扩展

ECMAScript规定了JS的编程语法和基础核心知识，是所有浏览器厂商共同遵守的一套JS语法工业标准

#### 1.4.2 DOM—文档对象模型

文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标记语言的标准编程接口通过DOM可以对页面上的各种元素进行操作（大小、位置、颜色等）

#### 1.4.3 BOM—浏览器对象模型

浏览器对象模型（Browser Object Model，简称DOM），它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构，通过BOM可操作浏览器窗口，比如弹出框、控制浏览器跳转、获取分辨率等

### 1.5 JS书写方式

#### 1.5.1 行内式

可以将单行或少量JS代码写在HTML标签的事件属性中（以on开头的属性） ，如： onclick
注意单双引号的使用：在HEML中我们推荐使用双引号，JS中我们推荐使用单引号。
可读性差，在html中编写JS大量代码时，不方便阅读；引号易错，引号多层嵌套匹配时，非常容易弄混；
特殊情况下使用

```html
<input type="button" value="click" onclick="alert('Hello, world!')">
```

#### 1.5.2 内嵌式

学习时常用

```html
<script>
    alert("Hello world!");
</script>
```

#### 1.5.3 外部文件

利于HTML页面代码结构化，把大段JS代码独立到HTML页面之外，既美观，也方便文件级别的复用
引用外部JS文件的script标签中间不可写代码
适合于JS代码量比较大的情况

```html
 <script src="newFile.js"></script>
```

### 1.6 JS注释

单行注释：//

多行注释：/* */

### 1.7 JS输入输出语句

输入框：

```js
prompt('请输入你的名字：');
```

警示框：

```js
alert('你好');
```

控制台打印：

```js
console.log('我是程序员能看到的。');
```

## 2 变量

变量是程序在内存中申请的一块用来存放数据的空间

### 2.1 变量的声明

var 是一个JS关键字，用来声明变量（variable变量的意思），使用该关键字声明变量后，计算机会自动为变量分配内存空间，不需要程序员管

age 是程序员定义的变量名，我们要通过变量名来访问内存中分配的空间

```js
var age;
```

### 2.2 变量的初始化

初始化：声明并赋值

```js
var age = 18;
```

### 2.3 声明多个变量

同时声明多个变量可用逗号隔开

```js
var age = 18,
    name = qyj,
    sex = '男';
```

### 2.4 声明但不赋值

输出 undefined

```js
var sex;
console.log(sex);// undefined
```

### 2.5 不声明直接输出

直接报错

```js
console.log(name);//报错
```

### 2.6 不声明直接赋值

变量为全局变量，不提倡

```js
qq = 12345;
console.log(qq);
```

### 2.7 变量命名规范

由字母（A—Za—z）、数字（0—9）、下划线（）、美元符号（5）组成，如： usrAge， num01， name

严格区分大小写，var app；和var App；是两个变量

不能以数字开头，18age是错误的

不能是关键字、保留字，例如： var， for， while

变量名必须有意义

遵守驼峰命名法，首字母小写，后面单词的首字母需要大写，例如 myFirstName

## 3 数据类型

### 3.1 概述

在计算机中，不同的数据所需占用的存储空间是不同的，为了便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型

简单来说，数据类型就是数据的类别型号

变量是用来存储值的所在处，它们有名字和数据类型，变量的数据类型决定了如何将代表这些值的位存储到计算机的内存中

JavaScript是一种弱类型或者说动态语言，这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定

```js
var age = 18;//这是一个数字型
var name = '张三';//这是一个字符串型
```

在代码运行时，变量的数据类型是由JS引擎根据右边变量值的数据类型来判断的，运行完毕之后，变量就确定了数据类型 JavaScript拥有动态类型，同时也意味着相同的变量可用作不同的类型

### 3.2 简单数据类型

| 简单数据类型 |                       说明                       |  默认值   |
| :----------: | :----------------------------------------------: | :-------: |
|    Number    |       数字型，包含整值和浮点值，如21、0.21       |     0     |
|   Boolean    |      布尔值类型，如true、 false，等价于1和0      |   false   |
|    String    | 字符串类型，如'张三' 注意js 里面，字符串都带引号 |    ' '    |
|  Undefined   | var a 声明了变量a但是没有给值，此时a =undefined  | undefined |
|     Null     |          var a = null 声明了变量a为空值          |   null    |

#### 3.2.1 数字型

整数小数都称为数字型

八进制 0~7  在数字前加0 表示八进制

十六进制 0~f  在数字前加0x 表示十六进制

其他进制数直接打印会自动转换为十进制

数字型的最大值 

```js
console.log(Number.MAX_VALUE);
```

数字型的最小值

```js
console.log(Number.MIN_VALUE);
```

infinity 表示无穷大

-infinity 表示无穷小

NaN 表示非数值，Not a Number

#### 3.2.2 字符串型

用引号包含的任意文本，"双引号" 或 '单引号' 都可以，引号可以嵌套使用，比如 "我是 '高富帅' 程序员"

转义符：

| 转义符 |      解释说明       |
| :----: | :-----------------: |
|   \n   | 换行符，n 是newline |
|  \ \   |       表示 \        |
|  \ '   |     表示单引号      |
|  \ "   |     表示双引号      |
|   \t   |    缩进，t 是tab    |
|   \b   |   空格，b 是blank   |

检测获取字符串长度：

```js
var str = 'my name is qyj';
console.log(str.length);
```

字符串拼接：

字符串之间可以用 + 进行拼接，拼接方式为，字符串 + 任意类型 = 新字符串，会把与字符串拼接的任意类型转换成新字符串

#### 3.2.3 布尔型

布尔型只有两个值，true 和 false，true 表示 1，false 表示 0

#### 3.2.4 Undefined和Null

undefined 未定义数据类型：

```js
var str;
console.log(str);//undefined
var variable = undefined;
console.log(variable);//undefined
```

null 空值：

```js
var space = null;
console.log(space);//null
```

### 3.3 获取变量数据类型

typeof variable，获取该变量的数据类型

```js
var num = 10;
console.log(typeof num);//number
var str = 'qiyj';
console.log(typeof str);//string
var flag = true;
console.log(typeof flag);//boolean
var vari = undefined;
console.log(typeof vari);//undefined
```

### 3.4 数据类型转换

使用表单、prompt获取过来的值是字符串型，此时就不能直接进行运算，便需要转换变量的数据类型

#### 3.4.1 转换为字符串型

变量.tostring()：

```js
var num = 10;
var str = num.toString();
console.log(str);
```

String()：

```js
var num = 10;
console.log(String(num));
```

拼接字符串时的转换为，隐式转换

#### 3.4.2 转换为数字型

parseInt()：

如果转换前为小数，则直接取整，如果转换前带单位，则去掉单位

```js
var age = prompt('输入年龄');
console.log(parseInt(age));
console.log(parseInt('3.14'));//3 取整
console.log(parseInt('3.94'));//3 取整
console.log(parseInt('120px'));//120 去掉单位
```

parseFloat()：

```js
console.log(parseFloat('3.14'));//3.14
```

Number()：

```js
var str = '123';
console.log(Number(str));
console.log(Number('3726'));
```

算数运算实现隐式转换：

```js
console.log('12' - 0);
console.log('123' - '120');
```

注意：

'123' + 12 之间进行加法运算，实际上是字符串拼接，其结果还是字符串，要注意加号 + 是拼接字符串

#### 3.4.3 转换为布尔型

Boolean()：

除了以下五种转换为false 其余都是true

```js
console.log(Boolean(''));//false
console.log(Boolean(0));//false
console.log(Boolean(NaN));//false
console.log(Boolean(null));//false
console.log(Boolean(undefined));//false
console.log(Boolean(123));//true
```

## 4 运算符

运算符也被称为操作符，是用于实现赋值、比较和执行算术运算等功能的符号

### 4.1 算数运算符

```js
console.log(1 + 1); // 2
console.log(1 - 1); // 0
console.log(1 * 1); // 1
console.log(1 / 1); // 1 
console.log(4 % 2); // 0
```

注意：

JS中不要直接使用浮点数进行运算，会产生精度误差

```js
console.log(0.1 + 0.2); // 结构为0.30000000000000004
console.log(0.07 * 100); // 结构为7.000000000000001
```

### 4.2 递增递减运算符

如果需要反复给变量加一或减一，可以使用递增（++）和递减（--）运算符，加减号可以放在变量前也可以放在变量后，放在前面称前置，后面称后置

前置：先自加或自减，后参与运算

后置：先原值参与运算，后自加或自减（常用）

### 4.3 比较运算符

比较运算符（关系运算符）是两个数据进行比较时所用的运算符，比较运算后会返回一个布尔值作为比较运算后的结果

```js
console.log(3 >= 5); // false
console.log(2 <= 4); // true
```

程序里面的等于符号 是 ==  默认转换数据类型 会把字符串型的数据转换为数字型 只要求值相等就可以

```js
console.log(3 == 5); // false
console.log('张学友' == '刘德华'); // flase
console.log(18 == 18); // true
console.log(18 == '18'); // true
console.log(18 != 18); // false
```

程序里面有全等，要求两侧的值 还有 数据类型完全一致才可以

```js
console.log(18 === 18);// true
console.log(18 === '18'); // false
```

### 4.4 逻辑运算符

逻辑与 && ：

两侧都为true，结果才是 true，只要有一侧为false，结果就为false 

```js
console.log(3 > 5 && 3 > 2); // false
console.log(3 < 5 && 3 > 2); // true
```

逻辑或 || ：

两侧都为false，结果才是false，只要有一侧为true，结果就是true

```js
console.log(3 > 5 || 3 > 2); // true 
console.log(3 > 5 || 3 < 2); // false
```

逻辑非  ！： 
非，即对结构取反

```js
console.log(!true); // false
```

短路运算（逻辑中断）：

多个表达式进行逻辑运算，当左边的表达式值可以确定最终结果时，不再继续运算右边其余的表达式

```js
console.log(123 && 456); // 456
console.log(0 && 456); //  0
console.log(0 && 1 + 2 && 456 * 56789); // 0
console.log('' && 1 + 2 && 456 * 56789); // ''
```

逻辑与短路运算  如果表达式1 结果为真 则返回表达式2  如果表达式1为假 那么返回表达式1

```js
console.log(123 || 456); // 123
console.log(123 || 456 || 456 + 123); // 123
console.log(0 || 456 || 456 + 123); // 456
```

逻辑或短路运算  如果表达式1 结果为真 则返回的是表达式1 如果表达式1 结果为假 则返回表达式2

### 4.5 赋值运算符

a += 1 相当于 a = a + 1

a -= 1 相当于 a = a - 1

a *= 1 相当于 a = a * 1

a /= 1 相当于 a = a / 1

## 5 流程控制

### 5.1 顺序结构

从上至下依次执行程序

### 5.2 选择结构

#### 5.2.1 if-else

语法结构：

```js
if (条件表达式1) {
    执行语句1
}else if(条件表达式2){
    执行语句2
}else if(条件表达式3){
    执行语句3
}else{
    执行语句4
}
```

#### 5.2.2 三元表达式

语法结构：

```js
条件表达式 ? 表达式1 : 表达式2;
```

如果条件表达式结构为真，则返回表达式1的值，如果为假，则返回表达式2的值

#### 5.2.3 switch-case

语法结构：

```js
switch (表达式) {
    case value1:
        执行语句1;
        break;
    case value2:
        执行语句2;
        break;
    ...    
    default:
        执行最后的语句;
}
```

### 5.3 循环结构

#### 5.3.1 for循环

语法结构：

```js
for (初始化变量; 条件表达式; 操作表达式) {
    循环体
}
```

#### 5.3.2 while循环

语法结构：

```js
while (条件表达式) {
    循环体
}
```

先判断，后执行

#### 5.3.3 do while循环

语法结构：

```js
do {
     循环体
} while (条件表达式)
```

先执行，后判断

#### 5.3.4 break和continue

break 直接退出整个循环，不再进行

continue 退出当前次循环，继续进行下一轮循环

## 6 数组

不同于 C/C++ 等其他语言，JS数组都是动态的创建的，可以自由增加数组长度，也可以存放不同类型的元素

### 6.1 创建数组

利用new 创建数组：

```js
var arr = new Array(); // 创建了一个空的数组
```

利用数组字面量创建数组：

```js
var arr = []; // 创建了一个空的数组
var arr1 = [1, 2, '鸡你太美', true];
```

### 6.2 数组基本操作

#### 6.2.1 遍历数组

遍历就是把数组中的每一个元素都访问一次

```js
for (var i = 0; i < 3; i++) {
    console.log(arr[i]);
}
```

#### 6.2.2 获取数组长度

可将arr.length 应用于遍历数组

```js
console.log(arr.length);
for (var i = 0; i < arr.length; i++){
    console.log(arr[i]);
}
```

#### 6.2.3 新增数组元素

修改length长度：

```js
var arr = ['red', 'green', 'blue'];
console.log(arr.length);
arr.length = 5; // 把我们数组的长度修改为了 5  里面应该有5个元素 
console.log(arr);
console.log(arr[3]); // undefined
console.log(arr[4]); // undefined
```

修改索引号 追加数组元素：

```js
var arr = ['red', 'green', 'blue'];
arr1[3] = 'pink';
console.log(arr);
arr1[4] = 'hotpink';
console.log(arr);
arr1[0] = 'yellow'; // 这里是替换原来的数组元素
console.log(arr);
arr1 = '有点意思';
console.log(arr1); // 不要直接给 数组名赋值 否则里面的数组元素都没了
```

#### 6.2.4 翻转数组

```js
var arr = ['red', 'green', 'blue', 'pink', 'purple', 'hotpink'];
var newArr = [];
for (var i = arr.length - 1; i >= 0; i--) {
    newArr[newArr.length] = arr[i]
}
console.log(newArr);
```

### 6.3 冒泡排序

冒泡排序就是将原本数组里的数据元素按照从大到小或者从小到大的顺序排成一个新的数组

```js
var arr = [4, 1, 2, 3, 5];
for (var i = 0; i <= arr.length - 1; i++) { // 外层循环管趟数 
    for (var j = 0; j <= arr.length - i - 1; j++) { // 里面的循环管 每一趟的交换次数
        // 内部交换2个变量的值 前一个和后面一个数组元素相比较
        if (arr[j] < arr[j + 1]) {
            var temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
console.log(arr);
```

## 7 函数

函数就是封装了一段可被重复调用执行的代码块，通过此代码块可以实现大量代码的重复使用

封装就是把一个或者多个功能通过函数的方式封装起来，对外只提供一个简单的函数接口。

函数的实现有两部分：

```js
//声明函数
function 函数名(形参1,形参2,...) {
    函数体
}
//调用函数
函数名(实参1,实参2,...);
```

- 如果实参的个数和形参的个数一致则正常输出结果

- 如果实参的个数多于形参的个数，会取到形参的个数 

- 如果实参的个数小于形参的个数，多于的形参定义为undefined，最终的结果就是 NaN

- 形参可以看做是不用声明的变量，默认值就是undefined


### 7.1 函数的返回值

格式：

```js
function 函数名() {
    return 需要返回的结果;
}
函数名();
```

注意：

return 会终止函数，后面的代码不会执行

如果有两个以上的形参，return返回最后一个值

### 7.2  arguments的使用

arguments 是所有JS函数内置的对象，但也只有函数具有

```js
function fn() {
    for (var i = 0; i < arguments.length; i++) {
        console.log(arguments[i]);
    }
}
fn(1, 2, 3);
fn(1, 2, 3, 4, 5);
```

- 函数的arguments是伪数组，并不是真正意义上的数组

- 具有数组的 length 属性

- 按照索引的方式进行存储的

- 它没有真正数组的一些方法 pop()  push() 等


### 7.3 函数的声明方式

利用函数关键字自定义函数(命名函数)：

```js
function fn() {
}
fn();
```

函数表达式(匿名函数)：

```js
var fun = function(aru) {
	console.log(aru);
}
fun('鸡你太美');
```

## 8 作用域

JavaScript作用域就是代码名字（变量）在某个范围内起作用和效果，目的是为了提高程序的可靠性更重要的是减少命名冲突

全局作用域：整个script标签或者是一个单独的js文件

- 在全局作用域下声明的变量叫做全局变量（在函数外部定义的变量）

- 全局变量在代码的任何位置都可以使用

- 在全局作用域下var声明的变量是全局变量

- 特殊情况下，在函数内不使用var声明的变量也是全局变量（不建议使用）

局部作用域：在函数内部就是局部作用域，这个代码的名字只在函数内部起效果和作用

- 在局部作用域下声明的变量叫做局部变量（在函数内部定义的变量）

- 局部变量只能在该函数内部使用
- 在函数内部var声明的变量是局部变量
- 函数的形参实际上就是局部变量

作用域链：内部函数访问外部函数的变量，采取的是链式查找的方式来决定取那个值，这种结构我们称为作用域链，采用就近原则

## 9 预解析

我们js引擎运行js 分为两步：  预解析和代码执行

- 预解析：js引擎会把js 里面所有的 var  还有 function 提升到当前作用域的最前面
- 代码执行：按照代码书写的顺序从上往下执行

预解析分为：变量预解析（变量提升）和函数预解析（函数提升）

- 变量提升：就是把所有的变量声明提升到当前的作用域最前面，不提升赋值操作
- 函数提升：就是把所有的函数声明提升到当前作用域的最前面，不调用函数

举例：

```js
f1();
console.log(c);
console.log(b);
console.log(a);
function f1() {
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
// 相当于以下代码
function f1() {
    var a;
    a = b = c = 9;
    // 相当于 var  a  = 9; b = 9; c = 9; b 和 c 直接赋值 没有var 声明 当 全局变量看
    // 集体声明  var a = 9, b = 9, c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
f1();
console.log(c);
console.log(b);
console.log(a);
```

## 10 对象

在JavaScript中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串、数值、数组、函数等

对象是由属性和方法组成的。

- 属性：事物的特征，在对象中用属性来表示（常用名词）
- 方法：事物的行为，在对象中用方法来表示（常用动词）

### 10.1 创建对象

利用对象字面量创建对象：

```js
var obj = {
    uname: '蔡徐坤',
    age: 18,
    sex: '男',
    sing: function() {
        console.log('鸡你太美');
    }
}
//调用对象的属性
console.log(obj.uname);
console.log(obj['age']);
//调用对象的方法
obj.sayHi();
```

利用 new Object 创建对象：

```js
var obj = new Object(); 
obj.uname = '蔡徐坤';
obj.age = 18;
obj.sex = '男';
obj.sing = function() {
        console.log('鸡你太美');
    }
```

### 10.2 利用构造函数创建对象

前面两种创建对象的方式一次只能创建一个对象，但需要多个具有相同属性和方法的对象的时候，就需要使用构造函数来创建

构造函数将相同的属性和方法封装在一个函数里

语法结构：

```js
function 构造函数名() {
    this.属性 = 值;
    this.方法 = function() {}
}
new 构造函数名();
```

- 构造函数名字首字母要大写
- 我们构造函数不需要return 就可以返回结果
- 我们调用构造函数 必须使用 new
- 我们只要new Star() 调用函数就创建一个对象
- 我们的属性和方法前面必须添加 this

```js
function Star(uname, age, sex) {
    this.name = uname;
    this.age = age;
    this.sex = sex;
    this.sing = function (song) {
        console.log(song);
    }
}
var ldh = new Star('蔡徐坤', 18, '男');
console.log(ldh.name);
console.log(ldh['sex']);
ldh.sing('鸡你太美');
```

造函数相当于创建了一个抽象的类，利用构造函数创建对象的过程我们也称为对象的实例化

new 关键字的执行过程：

- new 构造函数可以在内存中创建了一个空的对象 
- this 就会指向刚才创建的空对象
- 执行构造函数里面的代码 给这个空对象添加属性和方法
- 返回这个对象

### 10.3 遍历对象

可以利用 for in 遍历对象：

```js
var obj = {
        name: '蔡徐坤',
        age: 18,
        sex: '男',
        fn: function() {}
}
for (var k in obj) {
    console.log(k);//属性名
    console.log(obj[k]);//属性值 
}
```

## 11 内置对象

JavaScript 中的对象分三种：自定义对象、内置对象、浏览器对象

自定义对象和内置对象是 JS 的基础内容，属于ECMAScript，浏览器对象属于 JS 独有，在JS API细说

内置对象就是指 JS 语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本且必须的功能（属性和方法）

### 11.1 数学对象 Math

Math数学对象不是一个构造函数 ，所以我们不需要new 来调用，而是直接使用里面的属性和方法即可

#### 11.1.1 Math 常用方法

|     方法     |        解释        |
| :----------: | :----------------: |
|   Math.PI    |       圆周率       |
| Math.floor() |      向下取整      |
| Math.ceil()  |      向上取整      |
| Math.round() | 四舍五入，.5往大取 |
|  Math.abs()  |       绝对值       |
|  Math.max()  |       最大值       |
|  Math.min()  |       最小值       |

#### 11.1.2 random 随机数

Math.random() 返回一个位于 [0,1) 之间随机的小数

获取区间 [a,b] 之间的整数：

```js
Math.floor(Math.random() * (b - a + 1)) + a;
```

获取区间 [a,b) 之间的整数：

```js
Math.floor(Math.random() * (b - a)) + a;
```

#### 11.1.3 定义自己的Math对象

```js
// 利用对象封装自己的数学对象  里面有 PI 最大值和最小值
var myMath = {
    PI: 3.141592653,
    max: function() {
        var max = arguments[0];
        for (var i = 1; i < arguments.length; i++) {
            if (arguments[i] > max) {
                max = arguments[i];
            }
        }
        return max;
    },
    min: function() {
        var min = arguments[0];
        for (var i = 1; i < arguments.length; i++) {
            if (arguments[i] < min) {
                min = arguments[i];
            }
        }
        return min;
    }
}
console.log(myMath.PI);
console.log(myMath.max(1, 5, 9));
console.log(myMath.min(1, 5, 9));
```

### 11.2 日期对象 Date

Date 日期对象是一个构造函数，必须使用new 来调用创建我们的日期对象

如果没有参数，则返回当前系统的当前时间

```js
var date = new Date();
console.log(date);
```

如果有参数，参数常用的写法，数字型  2019, 10, 01  或者是 字符串型 '2019-10-1 8:8:8'

```js
var date1 = new Date(2019, 10, 1);
console.log(date1); // 返回的是 11月 不是 10月 
var date2 = new Date('2019-10-1 8:8:8');
console.log(date2);
```

#### 11.2.1 格式化日期

格式化日期，年月日 ：

```js
var date = new Date();
console.log(date.getFullYear()); // 返回当前日期的年
console.log(date.getMonth() + 1); // 月份 返回的月份小1个月
console.log(date.getDate()); // 返回的是 几号
console.log(date.getDay()); // 周一返回的是 1 周六返回的是 6 但是 周日返回的是 0
```

格式化日期，时分秒：

```js
var date = new Date();
console.log(date.getHours()); // 时
console.log(date.getMinutes()); // 分
console.log(date.getSeconds()); // 秒
```

#### 11.2.2 时间戳

获得Date总的毫秒数(时间戳)：

不是当前时间的毫秒数，而是距离1970年1月1号过了多少毫秒数

```js
//通过 valueOf()  getTime()
var date = new Date();
console.log(date.valueOf()); 
console.log(date.getTime());
//简单的写法 (最常用的写法)
var date1 = +new Date();
console.log(date1);
//H5新增的
console.log(Date.now());
```

#### 11.2.3 倒计时

```js
function countDown(time) {
    var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
    var inputTime = +new Date(time); // 返回的是用户输入时间总的毫秒数
    var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
    var d = parseInt(times / 60 / 60 / 24); // 天
    d = d < 10 ? '0' + d : d;
    var h = parseInt(times / 60 / 60 % 24); //时
    h = h < 10 ? '0' + h : h;
    var m = parseInt(times / 60 % 60); // 分
    m = m < 10 ? '0' + m : m;
    var s = parseInt(times % 60); // 秒
    s = s < 10 ? '0' + s : s;
    return d + '天' + h + '时' + m + '分' + s + '秒';
}
console.log(countDown('2022-9-10 18:00:00'));
var date = new Date();
console.log(date);
```

### 11.3 数组对象

#### 11.3.1 检测是否为数组

instanceof 运算符，它可以用来检测是否为数组

```js
var arr = [];
console.log(arr instanceof Array);
```

Array.isArray(参数);  H5新增的方法

```js
var arr = [];
console.log(Array.isArray(arr));
```

#### 11.3.2 添加或删除数组元素

push() 在我们数组的末尾添加一个或者多个数组元素，参数直接写

```js
var arr = [1, 2, 3];
console.log(arr.push(4, '鸡你太美'));
console.log(arr);
```

unshift() 在我们数组的开头添加一个或者多个数组元素，参数直接写

```js
var arr = [1, 2, 3];
console.log(arr.unshift('唱', '跳'));
console.log(arr);
```

pop() 它可以删除数组的最后一个元素，无参数，返回被删除的元素

```js
var arr = [1, 2, 3];
console.log(arr.pop());
console.log(arr);
```

shift() 它可以删除数组的第一个元素，无参数，返回被删除的元素

```js
var arr = [1, 2, 3];
console.log(arr.shift());
console.log(arr);
```

#### 11.3.3 数组排序

翻转数组：reverse()

```js
var arr = ['pink', 'red', 'blue'];
arr.reverse();
console.log(arr);
```

数组排序（冒泡排序）：sort()

```js
var arr = [13, 4, 77, 1, 7];
 arr1.sort(function(a, b) {
     //  return a - b; 升序的顺序排列
     return b - a; // 降序的顺序排列
 });
 console.log(arr);
```

#### 11.3.4 数组索引

返回数组元素索引号方法：indexOf()、lastIndexOf()

- 作用就是返回该数组元素的索引号
- 它只返回第一个满足条件的索引号
- 它如果在该数组里面找不到元素，则返回的是 -1

```js
var arr = ['red', 'green', 'blue', 'pink', 'blue'];
console.log(arr.IndexOf('blue')); //从前面开始查找  2
console.log(arr.lastIndexOf('blue'));//从后面开始查找  4
```

#### 11.3.4 数组去重

举例：

遍历旧数组， 然后拿着旧数组元素去查询新数组， 如果该元素在新数组里面没有出现过， 我们就添加， 否则不添加

利用 新数组.indexOf() 如果返回时 - 1 就说明 新数组里面没有改元素

```js
function unique(arr) {
    var newArr = [];
    for (var i = 0; i < arr.length; i++) {
        if (newArr.indexOf(arr[i]) === -1) {
            newArr.push(arr[i]);
        }
    }
    return newArr;
}
var demo = unique(['c', 'a', 'z', 'a', 'x', 'a', 'x', 'c', 'b'])
console.log(demo);
```

#### 11.3.5 数组转换为字符串

toString()：

```js
var arr = [1, 2, 3];
console.log(arr.toString());
```

join(分隔符)：

```js
var arr1 = ['green', 'blue', 'pink'];
console.log(arr1.join()); // green,blue,pink
console.log(arr1.join('-')); // green-blue-pink
console.log(arr1.join('&')); // green&blue&pink
```

### 11.4 字符串对象

#### 11.4.1 基本包装类型

- 对象才有属性和方法
- 复杂数据类型才有属性和方法
- 那么为什么简单数据类型有 length 属性呢？
- 基本包装类型：把简单数据类型包装成复杂数据类型，这样基本数据类型也有了属性和方法

```js
// 1. 简单数据类型包装成复杂数据类型
let temp = new String('aaa');
// 2. 把临时变量赋值给 str
str = temp;
// 3. 销毁临时变量
temp = null;
```

#### 11.4.2 根据位置返回字符

charAt(index)：

```js
var str = 'andy';
console.log(str.charAt(3));
```

charCodeAt(index)：返回相应索引号的字符ASCII值，目的是判断用户按下了那个键

```js
console.log(str.charCodeAt(0));
```

str[index]：H5 新增的

```js
console.log(str[0]);
```

#### 11.4.3 字符串操作方法

字符串拼接：concat('字符串1','字符串2'....)

```js
var str = 'andy';
console.log(str.concat('red'));
```

字符串截取：substr('截取的起始位置', '截取几个字符')

```js
var str1 = '改革春风吹满地';
console.log(str1.substr(2, 2));
```

字符串替换：replace('被替换的字符', '替换为的字符')

```js
var str = 'andyandy';
console.log(str.replace('a', 'b'));
```

字符转换为数组：split('分隔符')

```js
var str1 = 'red, pink, blue';
console.log(str2.split(','));
var str2 = 'red&pink&blue';
console.log(str3.split('&'));
```

#### 11.4.4 查找某个字符出现的次数

算法：先查找第一个 o 出现的位置，然后 只要indexOf 返回的结果不是 -1 就继续往后查找，因为indexOf 只能查找到第一个，所以后面的查找，一定是当前索引加1，从而继续查找

```js
var str = "oabcoefoxyozzopp";
var index = str.indexOf('o');
var num = 0;
// console.log(index);
while (index !== -1) {
    console.log(index);
    num++;
    index = str.indexOf('o', index + 1);
}
console.log('o出现的次数是: ' + num);
```

#### 11.4.5 统计出现最多的字符

算法：利用 charAt(） 遍历这个字符串，把每个字符都存储给对象， 如果对象没有该属性，就为1，如果存在了就 +1

遍历对象，得到最大值和该字符

```js
var str = 'abcoefoxyozzopp';
var o = {};
for (var i = 0; i < str.length; i++) {
    var chars = str.charAt(i); // chars 是 字符串的每一个字符
    if (o[chars]) { // o[chars] 得到的是属性值
        o[chars]++;
    } else {
        o[chars] = 1;
    }
}
console.log(o);

var max = 0;
var ch = '';
for (var k in o) {
    // k 得到是 属性名
    // o[k] 得到的是属性值
    if (o[k] > max) {
        max = o[k];
        ch = k;
    }
}
console.log(max);
console.log('最多的字符是' + ch);
```
