# JS高级

## 1JavaScript面向对象

### 1.1面向对象编程介绍

有两大编程思想：面向过程编程和面向对象编程

#### 1.1.1面向过程编程

面向过程编程，即POP（Process-oriented programming），面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用即可

- 优点：性能比面向对象高，适合跟硬件联系很紧密的东西，例如单片机就采用的面向过程编程
- 缺点：没有面向对象易维护、易复用、易扩展

#### 1.1.2面向对象编程

面向对象编程，即 OOP（Object Oriented Programming），面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作

在面向对象程序开发思想中，每—个对象都是功能中心，具有明确分工， 面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目

面向对象的特性：封装性、继承性、多态性

- 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护
- 缺点：性能比面向过程低

### 1.2ES6中的类和对象

#### 1.2.1类

在 ES6 中新增加了类的概念，可以使用 class 关键字声明—个类，之后以这个类来实例化对象

类 抽象了对象的公共部分，它泛指某一大类（class）

对象 特指某一个，通过类实例化一个具体的对象

面向对象的思维特点：

- 抽取(抽象)对象共用的属性和行为组织(封装)成—个类（模板）
- 对类进行实例化,获取类的对象

#### 1.2.2对象

在现实生活中，万物皆对象，对象是 一个具体的事物，看得见摸得着的实物，例如一本书、一辆汽车、一个人，一个数据库、一张网页、一个与远程服务器的连接也可以是“对象”

在 JavaScript 中，对象是一组无序的相关属性和方法的集合，所有的事物都是对象，例如字符串、数值、数组、函数等

对象是由属性和方法组成的：

- 属性：事物的 特征，在对象中用属性来表示（常用名词）
- 方法：事物的 行为，在对象中用方法来表示（常用动词）

#### 1.2.3创建类和对象

class 创建类：

```js
class Star {
    constructor(uname, age) {
        this.uname = uname;
        this.age = age;
    }
}
```

利用类创建对象：

```js
var star1 = new Star('qyj', 18);
var star2 = new Star('QYJ', 20);
```

注意：

- 通过 class 关键字创建类，类名习惯性定义首字母大写
- 类里面 constructor 函数，可以接受传递过来的参数，同时返回实例对象
- constructor 函数，只要 new 生成实例时，就会自动调用这个函数,，如果不写这个函数，类也会自动生成这个函数
- 生成实例 new 不能省略
- 注意语法规范，创建类时类名后面不要加小括号，生成实例时类名后面加小括号，构造函数不需要加 function

#### 1.2.4类中添加方法

直接在类中写方法名即可：

```js
class Star {
    constructor(uname, age) {
    this.uname = uname;
    this.age = age;
}
    sing(){
        console.log(this.uname + '爱唱歌')
    }
}
```

创建实例对象：

```js
var star1 = new Star('qyj', 18);
star1.sing(); //qyj爱唱歌
```

注意：

- 类里面所有的函数不需要写 function
- 多个函数方法之间不需要添加逗号分隔

### 1.3类的继承

#### 1.3.1继承

在现实中的继承，子承父业，比如我们都继承了父亲的姓

在程序中的继承，子类可以继承父类的—些属性和方法

语法：使用 extends 关键字

```js
class Father {
    constructor() {
    }
    money() {
        console.log(100);
    }
}
class Son extends Father {
}
var son = new Son();
son.money(); //100
```

#### 1.3.2super关键字

super 关键字用于访问和调用对象父类上的函数，可以调用父类的构造函数，也可以调用父类的普通函数

举例：

```js
class Father {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }
    sum() {
        console.log(this.x + this.y);
    }
}
class Son extends Father {
    constructor(x, y) {
        //super调用父类的构造函数
        super(x, y);
        this.x = x;
        this.y = y;
    }
    //子类继承父类方法的同时扩展自己的方法
    subtract() {
        console.log(this.x - this.y);
    }
}
var son = new Son(5, 3);
son.subtract(); //2
son.sum(); //8
```

```js
class Father {
    say() {
        return '我是爸爸';
    }
}
class Son extends Father {
    say() {
        //super调用父类普通函数
        console.log(super.say() + '的儿子');
    }
}
var son = new Son();
son.say(); //我是爸爸的儿子
```

#### 1.3.3使用类的注意事项

- 必须先定义类，才能通过类实例化对象
- 类里面的共有属性和方法一定要加 this 使用
- constructor 里面的 this 指向实例对象, 方法里面的 this 指向这个方法的调用者

举例：

```js
let that;
class Star {
    constructor (uname, age) {
        that = this;
        this.uname = uname;
        this.age = age;
        // btn按钮调用sing方法
        this.btn = document.querySelector("button");
        this.btn.onclick = this.sing;
        // constructor 里面的this 指向的是 创建的实例对象
        console.log("constructor: ", this);
    }
    sing() {
        // 这个sing方法里面的 this 指向的是 btn 这个按钮，因为这个按钮调用了这个函数
        console.log("sing:", this); // button
        console.log(that.uname); // that里面存储的是constructor里面的this
    }
    dance() {
        // 这个dance里面的this 指向的是实例对象 ldh 因为ldh 调用了这个函数
        console.log("dance:", this);
    }
}
let rick = new Star("Rick", 20);
rick.dance();
```

## 2构造函数和原型

### 2.1构造函数和原型

#### 2.1.1概述

在典型的面向对象语言中（如 Java），都存在类的概念，类就是对象的模板，对象就是类的实例，但在 ES6 之前， JS 中并没用引入类的概念

在 ES6 之前 ，对象不是基于类创建的，而是用一种称为 构建函数 的特殊函数来定义对象和它们的特征

创建对象可以通过以下三种方式：

- 对象字面量
- new Object()
- 自定义构造函数

#### 2.1.2构造函数

构造函数 是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与 new 一起使用

我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面

在 JS 中，使用构造函数时要注意以下两点：

- 构造函数用于创建某一类对象，其首字母要大写
- 构造函数要和 new 一起使用才有意义

new 在执行时会做四件事情：

- 在内存中创建一个新的空对象
- 让 this 指向这个新的对象
- 执行构造函数里面的代码，给这个新对象添加属性和方法
- 返回这个新对象（所以构造函数里面不需要 return）

#### 2.1.3静态成员和实例成员

JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的 this 上添加

通过这两种方式添加的成员，就分别称为静态成员和实例成员

- 静态成员：在构造函数本上添加的成员称为静态成员，只能由构造函数本身来访问
- 实例成员：在构造函数内部创建的对象成员称为实例成员，只能由实例化的对象来访问

#### 2.1.4构造函数原型

构造函数方法很好用，但是 存在浪费内存的问题

函数内容一样的函数，会在内存中产生两份，占两份空间，我们希望所有的对象使用同一个函数，这样就比较节省内存，于是就有了构造函数原型 prototype

JavaScript 规定，每一个构造函数都有一个 prototype 属性，指向另一个对象，注意这个 prototype 就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有

我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法

举例：

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype.sing = function () {
        console.log('我会唱歌');
}
var ldh = new Star('刘德华', 18);
var zxy = new Star('张学友', 19);
console.log(ldh.sing === zxy.sing); // true，sing方法已被共享
```

#### 2.1.5对象原型

对象都会有一个属性 __ proto __ 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 原型对象的属性和方法，就是因为对象有 __ proto __ 原型的存在

__ proto __ 对象原型和构造函数的原型对象 prototype 是等价的

__ proto __ 对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是 它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象 prototype

举例：

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype.sing = function() {
    console.log('我会唱歌');
}
var ldh = new Star('刘德华', 18);
console.log(ldh.__proto__ === Star.prototype); //true
```

#### 2.1.6原型constructor

对象原型（__ proto __）和构造函数（prototype）原型对象里面都有一个属性 constructor 属性 ，constructor 我们称为构造函数，因为它指回构造函数本身，constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数

一般情况下，对象的方法都在构造函数的原型对象中设置，如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor 就不再指向当前构造函数了，此时我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数

举例：

```js
function Star(uname, age) {
    this.uname = uname;
    this.age = age;
}
Star.prototype = {
    constructor: Star,//指向Star
    sing: function() {
        console.log('我会唱歌');
    },
    movie: function() {
        console.log('我会演电影');
    }
}
var ldh = new Star('刘德华', 18);
console.log(ldh.__proto__.constructor);//Star
```

#### 2.1.7原型链

- 只要是对象就有 __ proto __ 原型, 指向原型对象
- 原型对象里面的 __ proto __ 原型指向的是 Object.prototype
- Object.prototype 原型对象里面的 __ proto __ 原型指向为 null

成员查找：

- 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性
- 如果没有就查找它的原型（也就是 __ proto __ 指向的 prototype 原型对象）
- 如果还没有就查找原型对象的原型（Object）的原型对象）
- 依此类推一直找到 Object 为止（null）
- __ proto __ 对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线

#### 2.1.8原型对象中this的指向

构造函数中的 this 指向我们实例对象，原型对象里面放的是方法，这个方法里面的 this 指向的是这个方法的调用者, 也就是这个实例对象

#### 2.1.9扩展内置对象

可以通过原型对象，对原来的内置对象进行扩展自定义的方法

举例：给数组增加自定义求偶数和的功能

```js
Array.prototype.sum = function() {
    var sum = 0;
    for (var i = 0; i < this.length; i++) {
        sum += this[i];
    }
    return sum;
};
var arr = [1, 2, 3];
console.log(arr.sum());//6
var arr1 = new Array(11, 22, 33);
console.log(arr1.sum());//66
```

### 2.2继承

ES6之前并没有给我们提供 extends 继承，我们可以通过 ”构造函数+原型对象“ 模拟实现继承，被称为组合继承

#### 2.2.1call方法

功能：调用这个函数, 并且修改函数运行时的 this 指向

举例：

```js
function fn(x, y) {
    console.log(this);
}
var obj = {
    name: 'andy'
};
fn.call(obj, 1, 2);//此时这个函数的this 就指向了obj这个对象
```

#### 2.2.2借用构造函数继承父类属性

通过 call() 把父类型的 this 指向子类型的 this ，这样就可以实现子类型继承父类型的属性

举例：

```js
function Father(uname, age) {
    // this 指向父构造函数的对象实例
    this.uname = uname;
    this.age = age;
}
function Son(uname, age, score) {
    // this 指向子构造函数的对象实例
    Father.call(this, uname, age);
    this.score = score;
}
var son = new Son('刘德华', 18, 100);
```

#### 2.2.3借用原型对象继承父类方法

一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法

这个时候原型对象就起了作用，我们可以令子类构造函数的原型对象等于父类构造函数的原型对象，这样子类也可以使用父类构造函数的原型对象上的成员方法了

但是这样指定之后，子类构造函数和父类构造函数的对象原型 prototype 就指向同一个内存地址了，也就是说在子类原型对象上绑定其特有的成员方法，父类上也会有，显然这是不合理的

解决方法就是利用父类的实例对象：

- 将子类所共享的方法提取出来
- 子类原型对象等于是实例化父类，因为父类实例化之后 另外开辟空间，就不会影响原来父类原型对象
- 将子类的 constructor 重新指向子类的构造函数

举例：

```js
// 1. 父构造函数
function Father(uname, age) {
    // this 指向父构造函数的对象实例
    this.uname = uname;
    this.age = age;
}
Father.prototype.money = function() {
    console.log(100000);
};
// 2 .子构造函数 
function Son(uname, age, score) {
    // this 指向子构造函数的对象实例
    Father.call(this, uname, age);
    this.score = score;
}
// Son.prototype = Father.prototype;  这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化
Son.prototype = new Father();
// 如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数
Son.prototype.constructor = Son;
// 这个是子构造函数专门的方法
Son.prototype.exam = function() {
    console.log('孩子要考试');
}
var son = new Son('刘德华', 18, 100);
console.log(son);
console.log(Father.prototype);
console.log(Son.prototype.constructor);
```

#### 2.2.4类的本质

类的本质其实还是一个函数 我们也可以简单的认为 类就是 构造函数的另外一种写法

特点：

- 类有原型对象prototype 
- 类原型对象prototype 里面有constructor 指向类本身
- 类可以通过原型对象添加方法
- 类创建的实例对象有__ proto __ 原型指向类的原型对象

所以 ES6 的类它的绝大部分功能，ES5 都可以做到，新的 class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已

ES6 的类其实就是一种语法糖

语法糖：语法糖就是一种便捷写法，简单理解，有两种方法可以实现同样的功能，但是一种写法更加清晰方便，那么这个方法就是语法糖

### 2.3ES5新增方法

#### 2.3.1forEach方法

forEach 方法用于遍历数组，不对原数组进行修改

语法：

```js
array.forEach(function(currentValue, index, arr), thisArg);
```

该方法接收一个函数 function 参数，其中，该函数内又有三个参数：

- currentValue：数组当前项的值
- index：数组当前项的索引
- arr：数组对象本身

一般可以省略后面回调函数中后两个参数和 thisArg 参数

#### 2.3.2filter方法

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组，注意它返回一个新数组

语法：

```js
array.filter(function(currentValue, index, arr));
```

- currentValue：数组当前项的值
- index：数组当前项的索引
- arr：数组对象本身

#### 2.3.3some方法

some() 方法用于检测数组中的元素是否满足指定条件

通俗的说查找数组中是否有满足条件的元素

注意它返回值是布尔值，如果查找到这个元素，就返回 true，如果查找不到就返回 false

语法：

```js
array.some(function(currentValue, index, arr));
```

- currentValue：数组当前项的值
- index：数组当前项的索引
- arr：数组对象本身

#### 2.3.4trim方法

trim() 方法会从一个字符串的两端删除空白字符

trim() 方法并不影响原字符串本身，它返回的是一个新的字符串

#### 2.3.5Object.keys方法

Object.keys() 用于获取对象自身所有的属性，返回一个数组

- 效果类似 for...in
- 返回一个由属性名组成的数组

#### 2.3.6Object.defineProperty方法

Object.defineProperty() 定义对象中新属性或修改原有的属性

语法：

```js
Object.defineProperty(obj, prop, descriptor)
```

- obj：必需，目标对象
- prop：必需，需定义或修改的属性的名字
- descriptor：必需，目标属性所拥有的特性

```js
Object.defineProperty(obj, prop, {
    value: undefined,
    writable: false,
    enumerable: false,
    configurable: false
})
```

- value：设置属性的值 默认为 undefined
- writable：值是否可以重写，默认为 false
- enumerable：目标属性是否可以被枚举，默认为 false
- configurable：目标属性是否可以被删除或是否可以再次修改特性，默认为 false

## 3函数进阶

### 3.1函数的定义和调用

#### 3.1.1函数的定义方式

function 声明式（命名函数）：

```js
function fn() { };
```

函数表达式（匿名函数）：

```js
var fun = function () { };
```

Function 生成函数：

```js
var f = new Function('a', 'b', 'console.log(a + b)');
f(1, 2);
```

- Function 里面参数都必须是字符串格式
- 第三种方式执行效率低，也不方便书写，因此较少使用
- 所有函数都是 Function 的实例化对象
- 函数也属于对象

#### 3.1.2函数的调用方式

- 普通函数：直接加括号，fn()
- 对象的方法：加小数点方式， obj.fn()
- 构造函数：new 构造函数
- 绑定事件函数：触发相应事件，例如 click 点击触发函数
- 定时器函数：setInterval，每隔一段时间调用函数
- 立即执行函数：(function() {})()，自动调用，直接执行

### 3.2this的指向

#### 3.2.1函数内部this的指向

|   调用方式   |                 this 指向                  |
| :----------: | :----------------------------------------: |
|   普通函数   |                   window                   |
|   构造函数   | 实例对象，原型对象里面的方法也指向实例对象 |
|  对象的方法  |               该方法所属对象               |
| 绑定事件函数 |                绑定事件对象                |
|  定时器函数  |                   window                   |
| 立即执行函数 |                   window                   |

#### 3.2.2改变函数内部this的指向

call 方法：

call() 方法调用一个对象，简单理解为调用函数的方式，但是它可以改变函数的 this 指向

```js
fun.call(thisArg, arg1, arg2, ...);
```

参数：

- thisArg：在 fun 函数运行时指定的 this 值
- arg1，arg2：传递的其他参数
- 返回值就是函数的返回值，因为它就是调用函数
- 因此当我们想改变 this 指向，同时想调用这个函数的时候，可以使用 call，比如继承

apply 方法：

apply() 方法调用一个函数，简单理解为调用函数的方式，但是它可以改变函数的 this 指向

```js
fun.apply(thisArg, [argsArray])
```

参数：

- thisArg：在fun函数运行时指定的 this 值
- argsArray：传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数
- 因此 apply 主要跟数组有关系，比如使用 Math.max() 求数组的最大值

bind 方法：

bind() 方法不会调用函数，但是能改变函数内部 this 指向

```js
let fn = fun.bind(thisArg, arg1, arg2, ...)
```

参数：

- thisArg：在 fun 函数运行时指定的 this 值
- arg1，arg2：传递的其他参数
- 返回由指定的 this 值和初始化参数改造的原函数拷贝
- 因此当我们只是想改变 this 指向，并且不想调用这个函数的时候，可以使用 bind

### 3.3严格模式

#### 3.3.1什么是严格模式

JavaScript 除了提供正常模式外，还提供了 严格模式（strict mode）

ES5 的严格模式是采用具有限制性 JavaScript 变体的一种方式，即在严格的条件下运行 JS 代码

严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略

严格模式对正常的 JavaScript 语义做了一些更改：

- 消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为
- 消除代码运行的一些不安全之处，保证代码运行的安全
- 提高编译器效率，增加运行速度
- 禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class, enum, export, extends, import, super 不能做变量名

#### 3.3.2开启严格模式

为脚本开启严格模式：

为整个脚本文件开启严格模式，需要在所有语句之前放一个特定语句：在所有语句之前放一个特定语句 "use strict";（或'use strict';）

```html
<script>
    'use strict';
</script>
```

由于 "use strict" 加了引号，所以老版本的浏览器会把它当作一行普通字符串而忽略

有的 script 基本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中，这样独立创建一个作用域而不影响其他 script 脚本文件

```html
<script>
    (function (){
        "use strict";
        var num = 10;
    })();
</script>
```

为函数开启严格模式：

要给某个函数开启严格模式，需要把 "use strict";（或 'use strict';）声明放在函数体所有语句之前

将 "use strict" 放在函数体的第一行，则整个函数以 "严格模式" 运行

```js
function fn() {
    'use strict';
    // 下面的代码按照严格模式执行
}
```

#### 3.3.3严格模式中的变化

严格模式下变量的规定：

在正常模式中，如果一个变量没有声明就赋值，默认是全局变量，严格模式禁止这种用法，变量都必须先用 var （let、const）命令声明，然后再使用

严格模式下严禁删除已经声明变量，例如：delete x; 语法是错误的

严格模式下 this 的指向：

- 以前在全局作用域函数中的 this 指向 window 对象
- 严格模式下全局作用域中函数中的 this 是 undefined
- 以前构造函数时不加 new 也可以 调用,当普通函数，this 指向全局对象
- 严格模式下,如果 构造函数不加 new 调用, this 指向的是 undefined 如果给他赋值则会报错
- new 实例化的构造函数指向创建的对象实例
- 定时器 this 还是指向 window
- 事件、对象还是指向调用者

严格模式下函数的变化：

函数不能有重名的参数

函数必须声明在顶层，新版本的 JavaScript 会引入 “块级作用域”（ ES6 中已引入），为了与新版本接轨，不允许在非函数的代码块内声明函数

更多严格模式可参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode

### 3.4高阶函数

高阶函数是对其他函数进行操作的函数，它 接收函数作为参数或将函数作为返回值输出

举例：

```js
function fn(callback){
    callback&&callback();
}
fn(function(){alert('hi')}
```

举例：

```js
function fn(){
    return function() {}
}
 fn();
```

上面的 fn 就是一个高阶函数

函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用

最典型的就是作为回调函数，同理函数也可以作为返回值传递回来

### 3.5闭包

#### 3.5.1闭包的概念

闭包（closure）指有权访问另一个函数作用域中变量的函数——《JavaScript 高级程序设计》

简单理解就是，一个作用域可以访问另外一个函数内部的局部变量

举例：

```js
function fn() {
    var num = 10;
    function fun() {
        console.log(num);
    }
    fun();//fun 这个函数作用域 访问了另外一个函数 fn 里面的局部变量 num
}
fn();
```

#### 3.5.2闭包的作用

闭包的主要作用就是延伸变量的作用范围

举例：

```js
function fn() {
    var num = 10;
    return function() {
        console.log(num);
    }
}
var f = fn();
f();
```

### 3.6递归

#### 3.6.1递归的概念

如果 一个函数在内部可以调用其本身，那么这个函数就是 递归函数

简单理解就是，函数内部自己调用自己, 这个函数就是递归函数

递归函数的作用和循环效果一样

由于递归很容易发生 “栈溢出” 错误（stack overflow），所以必须要加退出条件 return

举例：

```js
function fn(n) {
    if (n == 1) {
        return 1;
    }
    return n * fn(n - 1);
}
console.log(fn(3));
console.log(fn(4));
```

#### 3.6.2浅拷贝与深拷贝

- 浅拷贝只是拷贝一层, 更深层次对象级别的只拷贝引用（修改目标对象的值，源对象的值也会改变，因为对象属性指向同一地址）
- 深拷贝拷贝多层，每一级别的数据都会拷贝
- Object.assign(target, ...sources) es6 新增方法可以 浅拷贝

## 4正则表达式

### 4.1正则表达式概述

正则表达式（ Regular Expression ）是用于匹配字符串中字符组合的模式，在 JavaScript 中，正则表达式也是对象

正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文（匹配）

此外，正则表达式还常用于过滤掉页面内容中的一些敏感词（替换），或从字符串中获取我们想要的特定部分（提取）等 

特点：

- 灵活性、逻辑性和功能性非常的强
- 可以迅速地用极简单的方式达到字符串的复杂控制
- 实际开发，一般都是直接复制写好的正则表达式，但是要求会使用正则表达式并且根据实际情况修改正则表达式

### 4.2正则表达式在JS中的使用

#### 4.2.1创建正则表达式

通过调用 RegExp 对象的构造函数创建：

```js
var regexp = new RegExp(/表达式/); 
```

通过字面量创建：

```js
var regexp = /表达式/;
```

#### 4.2.2测试正则表达式

test() 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串

```js
regexObj.test(str);
```

- regexObj 是写的正则表达式
- str 我们要测试的文本
- 检测 str 文本是否符合我们写的正则表达式规范

### 4.3正则表达式中的特殊字符

一个正则表达式可以 由简单的字符构成，比如 /abc/，也可以是 简单和特殊字符的组合，比如 /ab*c/

其中特殊字符也被称为 元字符，在正则表达式中是具有特殊意义的专用符号，如 ^ 、$ 、+ 等

更多关于正则表达式的信息可参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

#### 4.3.1边界符

正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符 ^ 和 $

| 边界符 |              说明              |
| :----: | :----------------------------: |
|   ^    | 表示匹配行首的文本（以谁开始） |
|   $    | 表示匹配行尾的文本（以谁结束） |

如果 ^ 和 $ 在一起，表示必须是 精确匹配（不能多不能少，只能是这些）

举例：

```js
var reg = /^abc/;
console.log(reg.test('abc')); // true
console.log(reg.test('abcd')); // true
console.log(reg.test('aabcd')); // false
var reg1 = /^abc$/;
console.log(reg1.test('abc')); // true
console.log(reg1.test('abcd')); // false
console.log(reg1.test('aabcd')); // false
console.log(reg1.test('abcabc')); // false
```

#### 4.3.2字符类

字符类表示有一系列字符可供选择，只要匹配其中一个就可以了，所有可供选择的字符都放在方括号内

举例：

```js
var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
console.log(rg.test('andy')); // true
console.log(rg.test('baby')); // true
console.log(rg.test('color')); // true
console.log(rg.test('red')); // false
var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
console.log(rg1.test('aa')); // false
console.log(rg1.test('a')); // true
console.log(rg1.test('b')); // true
console.log(rg1.test('c')); // true
console.log(rg1.test('abc')); // false
var reg = /^[a-z]$/; // 26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围
console.log(reg.test('a')); // true
console.log(reg.test('z')); // true
console.log(reg.test(1)); // false
console.log(reg.test('A')); // false
var reg1 = /^[a-zA-Z0-9_-]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
console.log(reg1.test('a')); // true
console.log(reg1.test('B')); // true
console.log(reg1.test(8)); // true
console.log(reg1.test('-')); // true
console.log(reg1.test('_')); // true
console.log(reg1.test('!')); // false
var reg2 = /^[^a-zA-Z0-9_-]$/;// 如果中括号里面有^ 表示取反的意思
console.log(reg2.test('a')); // false
console.log(reg2.test('B')); // false
console.log(reg2.test(8)); // false
console.log(reg2.test('-')); // false
console.log(reg2.test('_')); // false
console.log(reg2.test('!')); // true
```

#### 4.3.3量词符

量词符用来设定某个模式出现的次数

简单理解，就是让下面的a这个字符重复多少次

| 量词  |       说明       |
| :---: | :--------------: |
|   *   |   重复次数 ≥ 0   |
|   +   |   重复次数 ≥ 1   |
|   ?   | 重复 0 次或 1 次 |
|  {n}  |    重复 n 次     |
| {n,}  |   重复次数 ≥ n   |
| {n,n} | 重复 n 次到 m 次 |

举例：

```js
var reg1 = /^a*$/; //  * 相当于 >= 0 可以出现0次或者很多次 
console.log(reg1.test('')); //true
console.log(reg1.test('a')); //true
console.log(reg1.test('aaaa')); //true
var reg2 = /^a+$/; //  + 相当于 >= 1 可以出现1次或者很多次
console.log(reg2.test('')); // false
console.log(reg2.test('a')); // true
console.log(reg2.test('aaaa')); // true
var reg3 = /^a?$/; //  ?  相当于 1 || 0
console.log(reg3.test('')); // true
console.log(reg3.test('a')); // true
console.log(reg3.test('aaaa')); // false
var reg4 = /^a{3}$/; //  {3 } 就是重复3次
console.log(reg4.test('')); // false
console.log(reg4.test('a')); // false
console.log(reg4.test('aaaa')); // false
console.log(reg4.test('aaa')); // true
var reg5 = /^a{3,}$/; //  {3, }  大于等于3
console.log(reg5.test('')); // false
console.log(reg5.test('a')); // false
console.log(reg5.test('aaaa')); // true
console.log(reg5.test('aaa')); // true
var reg6 = /^a{3,6}$/; //  {3,16}  大于等于3 并且 小于等于16
console.log(reg6.test('')); // false
console.log(reg6.test('a')); // false
console.log(reg6.test('aaaa')); // true
console.log(reg6.test('aaa')); // true
console.log(reg6.test('aaaaaaa')); // false
```

#### 4.3.4预定义类

| 预定类 |                             说明                             |
| :----: | :----------------------------------------------------------: |
|   \d   |            匹配 0-9 之间的任一数字，相当于 [0-9]             |
|   \D   |           匹配所有 0-9 以外的字符，相当于 [ ^0-9 ]           |
|   \w   |      匹配任意的字母、数字和下划线，相当于 [A-Za-z0-9_]       |
|   \W   |  除所有字母、数字和下划线以外的字符，相当于 [ ^A-Za-z0-9_ ]  |
|   \s   | 匹配空格（包括换行符、制表符、空格符等），相等于[ \t\r\n\v\f ] |
|   \S   |           匹配非空格的字符，相当于 [ ^\t\r\n\v\f ]           |

#### 4.3.5替换

replace() 方法可以实现替换字符串操作，用来替换的参数可以是一个字符串或是一个正则表达式

```js
stringObject.replace(regexp/substr,replacement)
```

- 第一个参数：被替换的字符串 或者 正则表达式
- 第二个参数：替换为的字符串
- 返回值：一个替换完毕的新字符串

当 replace 中第一个参数为正则表达式的时候，还有一个 switch 参数可选

```js
/表达式/[switch]
```

switch（也称为修饰符）按照什么样的模式来匹配. 有三种值：

- g：全局匹配
- i：忽略大小写
- gi：全局匹配 + 忽略大小写
