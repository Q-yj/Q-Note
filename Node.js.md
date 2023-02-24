# Node.js

## 1初识Node.js与内置模块

### 1.1初识Node.js

到目前为止，已经掌握了 HTML、CSS 以及 JavaScript 的相关知识

其中，浏览器中的 JavaScript 组成部分是 JS 核心语法和 WebAPI

JS 核心语法中，学习了变量、数据类型、循环、分支、函数、作用域等相关知识；WebAPI 中，学习了 DOM、BOM 等相关知识

#### 1.1.1概述

JavaScript 之所以可以在浏览器中被执行，是因为浏览器具有 JavaScript 解析引擎，不同的浏览器使用的 JavaScript 解析引擎是不相同的

- Chrome 浏览器：V8
- Firefox 浏览器：OdinMonkey
- Safri 浏览器：JSCore
- IE 浏览器：Chakra

其中，Chrome 浏览器的 V8 引擎性能最好

JavaScript 之所以可以操作 DOM 和 BOM，是因为灭个浏览器都内置了 DOM、BOM 这样的 API 函数，JavaScript 可以调用它们

浏览器中的 JavaScript 运行环境：

- 运行环境是指代码正常运行所需的必要环境
- V8 引擎负责解析和执行 JavaScript 代码
- 内置 API（DOM、BOM 等）是由运行环境提供的特殊接口，只能在所属的运行环境中被调用

#### 1.1.2Node.js简介

Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境

Node.js 官方中文网址：https://nodejs.org/zh-cn/

Node.js 中的 JavaScript 运行环境：

- 浏览器是 JavaScript 的前端运行环境，Node.js 是 JavaScript 的后端运行环境
- 包含 V8 引擎和内置 API（fs、path、http 等）
- Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API

Node.js 作为一个 JavaScript 的运行环境，仅仅提供了基础的功能和 API

然而，基于 Node.js 提供的这些基础功能，很多强大的工具和框架如雨后春笋，层出不穷，所以学会了 Node.js ，可以让前端程序员胜任更多的工作和岗位：

- 基于 Express 框架（http://www.expressjs.com.cn/），可以快速构建 Web 应用
- 基于 Electron 框架（https://electronjs.org/），可以构建跨平台的桌面应用
- 基于 restify 框架（http://restify.com/），可以快速构建 API 接口项目
- 读写和操作数据库、创建实用的命令行工具辅助前端开发

#### 1.1.3了解终端

终端（Terminal）是专门为开发人员设计的，用于实现人机交互的一种方式

常用终端命令：

- 清屏：clear    (cmd窗口清屏用cls)

- 自动补全命令：输入命令的前几个字母，按 Tab 键，进行提示或补全

- 查找历史命令：按 ↑ 上 ↓ 下键
- 切换目录：cd xxx    直接切换到xxx文件夹；cd ..       切换到上级目录；cd \     直接回到根目录
- 调用 node 程序，运行某个js文件：node 空格 某个js文件 

### 1.2fs文件系统模块

fs 模块是 Node.js 官方提供的、用来操作文件的模块

它提供了一系列的方法和属性，用来满足用户对文件的操作需求

- fs.readFile() 方法，用来读取指定文件中的尼内容
- fs.writeFile() 方法，用来向只当的文件中写入内容

如果要在 JavaScript 代码中使用 fs 模块来操作文件，则需要先导入它

```js
const fs = require('fs')
```

#### 1.2.1readFile方法

语法：

```js
fs.readFile(path[,options],callback)
```

参数：

- path，必选参数，字符串，表示文件的路径
- options，可选参数，表示以什么格式来读取文件，默认值是 utf8
- callback，必选参数，文件读取完成后，通过回调函数拿到读取的结果

举例：

```js
const fs = require('fs');
fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
  if (err) {
    return console.log('读取文件失败！' + err.message);
  }
  console.log('读取文件成功！' + dataStr);
})
```

#### 1.2.2writeFile方法

语法：

```js
fs.writeFile(file,data[,options],callback)
```

参数：

- file，必选参数，需要指定一个文件路径的字符串，表示文件的存放路径
- data，必选参数，表示要写入的内容
- options，可选参数，表示以什么格式写入文件内容，默认值是 utf8
- callback，必选参数，文件写入完成后的回调函数

举例：

```js
const fs = require('fs')
fs.writeFile('./files/4.txt', 'Hello Node.js!!', function(err) {
  if (err) {
    return console.log('文件写入失败！' + err.message)
  }
  console.log('文件写入成功！')
})
```

#### 1.2.3路径动态拼接的问题

在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题

是因为，在代码在运行的时候，会以执行 node 命令时所处的目录，动态拼接出被操作文件的完整路径

解决方案是，在使用 fs 模块操作文件时，直接提供完整的路径，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题

可以直接使用 __dirname 来拼接字符串

__dirname 表示当前文件所处的目录

### 1.3path路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块

它提供了一系列的方法和属性，用来满足用户对路径的处理
需求

- path.join() 方法，用来将多个路径片段拼接成一个完整的路径字符串
- path.basename() 方法，用来从路径字符串中，将文件名解析出来
- path.extname()方法，可以获取路径中的扩展名部分

如果要在 JavaScript 代码中使用 path 模块来处理路径，则需要先导入它

```js
const path = require('path')
```

#### 1.3.1join方法

语法：

```js
path.join([...paths])
```

参数：

- ...paths < string >，路径片段的序列
- 返回值：< string >

举例：

```js
const pathStr1 = path.join('/a','/b/c','../','./d','e');
console.log(pathStr1);//输出 \a\b\d\e
const pathStr2 = path.join(__dirname,'./file/1.txt');
console.log(pathStr2);//输出 当前所在目录下\file\1.txt
```

以后涉及到路径拼接操作，就使用 path.join() 方法进行处理，尽量不使用加号 + 进行字符串拼接

#### 1.3.2basename方法

语法：

```js
path.basename(path[,ext])
```

参数：

- path < string >，必选参数，表示一个路径的字符串
- ext < string >，可选参数，表示文件扩展名
- 返回值：< string >，表示路径中最后一部分

举例：

```js
const fpath = '/a/b/c/index.html';
var fullName = path.basename(fpath);
console.log(fullName);//输出 index.html
var nameWithoutExt = path.basename(fpath,'.html');
console.log(nameWithoutExt);//输出 index
```

#### 1.3.3extname方法

语法：

```js
path.extname(path)
```

参数：

- paths < string >，必选参数，表示一个路径的字符串
- 返回值：< string >，返回得到的扩展名字符串

举例：

```js
const path = require('path');
const fpath = '/a/b/c/index.html';
const fext = path.extname(fpath);
console.log(fext);//输出 .html
```

### 1.4http模块

在网络节点中，负责消费资源的电脑，叫做客户端

负责对外提供网络资源的电脑，叫做服务器

http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块

通过 http 模块提供的 http.createServer() 方法，就
能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务

如果要希望使用 http 模块创建 Web 服务器，则需要导入它

```js
const http = require('http')
```

服务器和普通电脑的区别在于，服务器上安装了 web 服务器软件，例如：IIS、Apache 等

通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器

在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件，因为我们可以基于 Node.js 提供的 http 模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务

#### 1.4.1服务器相关概念

1. IP 地址

IP 地址就是互联网上每台计算机的唯一地址，因此 IP 地址具有唯一性

如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信

IP 地址的格式，通常用“点分十进制”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0~255 之间的十进制整数

注意：

- 互联网中每台 Web 服务器都有自己的 IP 地址
- 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在浏览器中输入 127.0.0.1 这个 IP 地址，就可以将自己的电脑当作一台服务器进行访问了

2. 域名和域名服务器

尽管 IP 地址能够唯一地标记网络上的计算机，但 IP 地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，即域名（Domain Name）地址

IP 地址和域名是一一对应的关系，这份对应关系存放在一种叫做域名服务器(DNS，Domain name server)的电脑中，使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现

因此，域名服务器就是提供 IP 地址和域名之间的转换服务的服务器

注意：

- 单纯使用 IP 地址，互联网中的电脑也能够正常工作，但是有了域名的加持，能让互联网的世界更方便
- 在开发测试期间，127.0.0.1 对应的域名是 localhost，它们都代表我们自己这台电脑，使用上没有区别

3. 端口号

 在一台电脑中，可以运行成百上千个 Web 服务，每个 web 服务都对应一个唯一的端口号

客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 Web 服务进行处理

注意：

- 每个端口号不能同时被多个 Web 服务占用
- 在实际应用中，URL 中的80端口可以被省略

#### 1.4.2创建最基本的Web服务器

步骤：

- 导入 http 模块

  ```js
  const http = require('http')
  ```

- 创建 Web 服务器实例

  调用 http.createServer() 方法

  ```js
  const server = http.createServer()
  ```

- 为服务器实例绑定 request 事件，监听客户端的请求

  使用服务器实例的 on() 方法，为服务器绑定一个 request 事件

  ```js
  server.on('request',(req,res) => {
      
  })
  ```

- 启动服务器

  调用服务器实例的 listen() 方法，启动当前 Web 服务器实例

  ```js
  server.listen(80,() => {
      
  })
  ```

在绑定 request 事件时，想在事件处理函数中访问与客户端相关的数据或属性，可以使用 req

req 是请求对象，它包含了与客户端相关的数据和属性

- req.url 是客户端请求的 URL 地址
- req.method 是客户端的 method 请求类型

在 request 事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用 res

res 是响应对象，它包含了与服务器相关的数据和属性

res.end 向客户端发送指定的内容，并结束这次请求的处理过程

解决中文乱码问题：

当调用 res.end() 方法向客户端发送中文内容时，会出现乱码问题，此时需要手动设置内容的编码格式

```js
//设置响应头
res.setHeader('Content-Type','text/html; charset=utf-8')
```

#### 1.4.3根据不同的url响应不同的页面

举例：

```js
const http = require('http');
const server = http.createServer();
server.on('request', (req, res) => {
  // 1. 获取请求的 url 地址
  const url = req.url;
  // 2. 设置默认的响应内容为 404 Not found
  let content = '<h1>404 Not found!</h1>';
  // 3. 判断用户请求的是否为 / 或 /index.html 首页
  // 4. 判断用户请求的是否为 /about.html 关于页面
  if (url === '/' || url === '/index.html') {
    content = '<h1>首页</h1>';
  } else if (url === '/about.html') {
    content = '<h1>关于页面</h1>';
  }
  // 5. 设置 Content-Type 响应头，防止中文乱码
  res.setHeader('Content-Type', 'text/html; charset=utf-8');
  // 6. 使用 res.end() 把内容响应给客户端
  res.end(content);
})
server.listen(80, () => {
  console.log('server running at http://127.0.0.1');
})
```

## 2模块化

### 2.1模块化基本概念

#### 2.1.1概述

模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程

对整个系统来说，模块是可组合、分解和更换的单元

在编程领域中，模块化就是遵守固定的规则，把一个大文件拆成独立并互相依赖的多个小模块

优点：

- 提高了代码的复用性
- 提高了代码的可维护性
- 可以实现按需加载

#### 2.1.2模块化规范

模块化规范就是对代码进行模块化的拆分组合时，需要遵守的规则，比如使用什么样语法格式来引用模块，在模块中使用什么样语法格式向外暴露成员

模块化规范的好处：

大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己

### 2.2Node.js中模块化

#### 2.2.1Node.js中模块的分类

根据模块来源的不同，分为三大类：

- 内置模块（由 Node.js 官方提供的，例如 fs、path、http 等）
- 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
- 第三方模块（由第三方开发出来的模块，使用前需要先下载）

#### 2.2.2加载模块

使用 require() 方法

```js
const fs = require('fs');//内置 fs 模块
const custom = require('./custom.js');//自定义模块
const moment = require('moment');//第三方模块
```

#### 2.2.3Node.js中的模块作用域

模块作用域和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制就叫做模块作用域

模块作用域的好处：

防止了全局变量污染的问题

#### 2.2.4向外共享模块作用域中的成员

1. module 对象

在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息

2. module.exports 对象

在自定义模块中，可以使用 module.exports 对象将模块内的成员共享出去，供外界使用

外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象

3. 共享成员时的注意点

使用 require() 方法导入模块时，导入的结果永远以 module.exports 指向的对象为准

4. exports 对象

由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 exports 对象

默认情况下，exports 和 module.exports 指向同一个对象，最终共享的结果，还是以 module.exports 指向的对象为准

5. exports 和 module.exports 的使用误区

在使用 require() 模块时，得到的永远是 module.exports 指向的对象

为了防止混乱，尽量不要在同一个模块中同时使用 exports 和 module.exports

#### 2.2.5Node.js中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖

CommonJS 规定：

- 每个模块内部，module 变量代表当前模块
- module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口
- 加载某个模块，其实是加载该模块的 module.exports 属性，require() 方法用于加载模块

### 2.3npm与包

#### 2.3.1包

Node.js 中的第三方模块又叫做包

不同于 Node.js 中的内置模块于自定义模块，包是由第三方个人或团队开发出来的，免费供所有人使用

由于 Node.js 的内置模块仅提供了一些底层的 API，导致在基于内置模块进行项目开发时效率很低

包是基于内置模块封装出来的，提供了更高级、更方便的 API，极大的提高了开发效率

包和内置模块之间的关系，类似于 jQuery 和浏览器内置 API 之间的关系

npm,Inc 公司旗下的著名网站，全球最大的包共享平台 https://www.npmjs.com/，可以从这个网站搜索需要的包

npm,Inc 公司提供一个地址为 https://registry.npmjs.org/ 的服务器，用来对外共享所有的包，可以从这个服务器上下载需要的包

nmp,Inc 公司提供了一个包管理工具，可以使用这个包管理工具从服务器下载需要的包到本地来使用，这个包管理工具叫 Node Package Manager（简称 npm 包管理工具），在安装 Node.js 时已经同时被安装在了用户电脑

在终端执行 npm -v 命令可以查看所安装的 npm 包管理工具的版本号

#### 2.3.2npm体验

1. 格式化时间的传统做法

- 创建格式化时间的自定义模块
- 定义格式化时间的方法
- 创建补零函数
- 从自定义模块中导出格式化时间的函数
- 导入格式化时间的自定义模块
- 调用格式化时间的函数

```js
function dateFormat(dtStr) {
  const dt = new Date(dtStr);
  const y = dt.getFullYear();
  const m = padZero(dt.getMonth() + 1);
  const d = padZero(dt.getDate());
  const hh = padZero(dt.getHours());
  const mm = padZero(dt.getMinutes());
  const ss = padZero(dt.getSeconds());
  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
}
// 定义补零的函数
function padZero(n) {
  return n > 9 ? n : '0' + n;
}
module.exports = {
  dateFormat
}

// 导入自定义的格式化时间的模块
const TIME = require('./15.dateFormat');
// 调用方法，进行时间的格式化
const dt = new Date();
const newDT = TIME.dateFormat(dt);
console.log(newDT);
```

2. 格式化时间的高级做法

- 使用 npm 包管理工具，在项目中安装格式化时间的包 moment
- 使用 require() 导入格式化时间的包
- 参考 moment 官方 API 文档对时间进行格式化

```js
const moment = require('moment');
const dt = moment().format('YYYY-MM-DD HH:mm:ss');
console.log(dt);
```

3. 在项目中安装包

在项目中安装指定名称的包，需要运行如下命令：

```shell
npm install 包的完整名称
```

可以简写为：

```shell
npm i 包的完整名称
```

还可以安装指定版本的包，例如：

```shell
npm i moment@2.22.2
```

4. 初次安装后

初次安装完成后，在项目文件夹下多了一个 node_modules 的文件夹和 package-lock.json 的配置文件

其中：

- node_modules 文件夹用来存放所有已安装到项目中的包，require() 导入第三方包时就是从这个目录中查找并加载包
- package-lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名称、版本号、下载地址等

注意：不要手动修改它们里的任何代码，npm 包管理工具会自动维护它们

#### 2.3.3包管理配置文件

1. npm 规定

在项目根目录中，必须提供一个叫做 package.json 的包管理配置文件，用来记录与项目有关的一些配置信息

- 项目名称、版本号、描述等
- 项目中都用到了哪些包
- 哪些包只在开发期间用到
- 哪些包在开发和部署时都会用到

2. 快速创建 package.json

npm 包管理工具提供了快捷命令，可以在执行命令时所处的目录中快速创建 package.json 这个包管理配置文件

```shell
npm init -y
```

注意：

- 此命令只能在英文目录下成功运行，所以在创建项目时要将文件夹的名称命名为英文，不要使用中文不要出现空格
- 运行此命令时，npm 包管理工具会自动把包的名称和版本号记录到  package.json 中

3. dependencies 节点

package.json 文件中，有一个 dependencies 节点，专门用来记录使用 npm install 命令安装了哪些包

4. 一次性安装所以包

由于第三方包体积很大，在多人协作时不方便成员之间共享代码，所以在共享时一般会将 node_modules 剔除

当拿到一个剔除了 node_modules 的项目后，先需要把所有用到的包下载到项目中才能顺利运行起来，否则会报错

可以运行以下命令一次性安装所有依赖包：

```shell
npm install
```

5. 卸载包

可以运行以下命令来卸载指定的包：

```shell
npm uninstall 包的完整名称
```

命令执行成功后，会把卸载的包自动从 package.json 的 dependencies 中移除掉

6. devDependencies 节点

某些包只在项目开发阶段会用到，项目上线后不再使用，则一般把这些包记录到 devDependencies 节点中

可以使用以下命令将包记录到 devDependencies 节点中：

```shell
npm install 包的完整名称 --save-dev
```

可以简写为：

```shell
npm install 包的完整名称 -D
```

#### 2.3.4解决包下载速度慢的问题

在使用 npm 下包时，默认是从国外的 https://registry.npmjs.org/ 服务器进行下载，网络数据传输需要经过漫长的海底光缆，所有下包速度很慢

而淘宝在国内搭建了一个服务器，专门把国外官方服务器上的包同步到国内服务器，从国内提供下包服务，从而提高下包速度

可以使用以下命令：

```shell
# 查看当前的下包镜像源
npm config get registry
# 将下包的镜像源切换为淘宝镜像源
npm config set registry=https://registry.npm.taobao.org/
# 再次检查当前的下包镜像源
npm config get registry
```

为了更方便的切换下包镜像源，可以安装 nrm 这个小工具，利用 nrm 提供的终端命令可以快速查看和切换下包镜像源

```shell
# 通过 npm 包管理器，将 nrm 安装为全局可以的工具
npm i nrm -g
# 查看所有可用的镜像源
nrm ls
# 将下包镜像源切换为 taobao 镜像
nrm use taobao
```

#### 2.3.5包的分类

使用 npm 包管理工具下载的包可以分为两大类

- 项目包
- 全局包

1. 项目包

被安装到项目的 node_modules 目录中的包都是项目包

项目包又分两类：

- 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
- 核心依赖包（被记录到 dependencies 节点中的包，在开发期间和上线之后都会用到）

2. 全局包

在执行 npm install 命令时如果提供了 -g 参数，则会把包安装为全局包

全局包会被安装到 C:\users\用户目录\AppDate\Roaming\npm\node_modules 目录下

注意：

- 只有工具性质的包，才有全局安装的必要性，因为它们提供了好用的终端命令
- 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明

#### 2.3.6规范的包结构

一个规范的包，它的组成结构必须符合以下要求：

- 包必须以单独的目录而存在
- 包的顶级目录下要必须包含 package.json 这个包配置文件
- package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口

### 2.4模块的加载机制

#### 2.4.1优先从缓存中加载

模块在第一次加载后会被缓存，这也就意味着多次调用 require() 不会导致模块的代码被执行多次

不论是内置模块、用户自定义模块、还是第三方模块，它们都会有限从缓存中加载，从而提高模块的加载效率

#### 2.4.2内置模块的加载机制

内置模块是由 Node.js 官方提供的模块，内置模块的加载优先级最高

例如，require('fs') 始终返回内置的 fs 模块，即使在 node_modules 目录下有名字也叫 fs 的包

#### 2.4.3自定义模块的加载机制

使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载

同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：

- 按照确切的文件名进行加载
- 补全 .js 扩展名进行加载
- 补全 .json 扩展名进行加载
- 补全 .node 扩展名进行加载
- 加载失败，终端报错

#### 2.4.4第三方模块的加载机制

如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块

如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录

#### 2.4.5目录作为模块

当把目录作为模块标识符传递给 require() 加载的时候，有三种加载方式：

- 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口
- 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件
- 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'

## 3Express

### 3.1初识Express

#### 3.1.1Express简介

Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架

通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的

Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法

Express 的中文官网： http://www.expressjs.com.cn/

不使用 Express 的话可以使用 Node.js 原生的 http 模块来创建 Web 服务器，但是 http 内置模块用起来很复杂，开发效率低，Express 是基于内置的 http 模块进一步封装出来的，能够极大的提高开发效率

http 内置模块与 Express 就类似于浏览器中 Web API 和 jQuery 的关系，后者是基于前者进一步封装出来的

对于前端程序员来说，最常见的两种服务器，分别是：

- Web 网站服务器：专门对外提供 Web 网页资源的服务器
- API 接口服务器：专门对外提供 API 接口的服务器

使用 Express，可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器

#### 3.1.2Express的基本使用

1. 安装

在项目所处的目录中，运行如下的终端命令，即可将 express 安装到项目中使用：

```shell
npm i express@4.17.1
```

2. 创建基本的 Web 服务器

```js
//导入 express
const express = require('express');
//创建 Web 服务器
const app = express();

//调用 app.listen(端口号，回调函数) 启动服务器
app.listen(80, () =>{
    console.log('express server running at http://127.0.0.1');
})
```

3. 监听 GET 请求

通过 app.get() 方法，可以监听客户端的 GET 请求，具体的语法格式如下：

```js
//参数1：客户端请求的 URL 地址
//参数2：请求对应的处理函数
//		req：请求对象
//		res：响应对象
app.get('请求url', function(req, res) {/*处理函数*/})
```

4. 监听 POST 请求

通过 app.post() 方法，可以监听客户端的 POST 请求，具体的语法格式如下：

```js
//参数1：客户端请求的 URL 地址
//参数2：请求对应的处理函数
//		req：请求对象
//		res：响应对象
app.post('请求url', function(req, res) {/*处理函数*/})
```

5. 把内容响应给客户端

通过 res.send() 方法，可以把处理好的内容，发送给客户端：

```js
app.get('/user', (req, res) => {
    //向客户端发送 JSON 对象
    res.send({ name: 'zs', age: 20, gender: '男' });
})
app.post('/user',(req, res) => {
    //向客户端发送文本内容
    res.send('请求成功');
})
```

6. 获取 URL 中携带的查询参数

通过 req.query 对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

```js
app.get('/', (req, res) => {
    //req.query 默认是一个空对象
    //客户端使用 ?name=zs&age=20 这种查询字符串形式，发送到服务器的参数，可以通过 req.query 访问到
    //例如：req.query.name   req.query.age
    console.log(req.query);
})
```

7. 获取 URL 中的动态参数

通过 req.params 对象，可以访问到 URL 中通过 : 匹配到的动态参数：

```js
app.get('/user/:id', (req, res) => {
    //req.params 默认是一个空对象
    //里面存放着通过 : 动态匹配到的参数值
    console.log(req.params);
})
```

#### 3.1.3托管静态资源

1. express.static()

express 提供了一个非常好用的函数，叫做 express.static()，通过它，我们可以非常方便地创建一个静态资源服务器

例如：

```js
app.use(express.static('public'));
```

通过上述代码，就可以将 public 目录下的图片、CSS文件、JS文件等对外开放访问了

注意：Express 在指定的静态目录中查找文件，并对外提供资源的访问路径，因此存放静态文件的目录名不会出现在 URL 中

2. 托管多个静态资源目录

如果要托管多个静态资源目录，多次调用 express.static() 函数即可：

```js
app.use(express.static('public'));
app.use(express.static('files'));
```

访问静态资源文件时，express.static() 函数会根据目录的添加顺序查找所需的文件

3. 挂载路径前缀

如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：

```js
app.use('/public', express.static('public'));
```

现在就可以通过带有 /public 前缀地址来访问 public 目录中的文件了

#### 3.1.4nodemon

在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐

可以使用 nodemon 这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试

nodemon 官方地址：https://www.npmjs.com/package/nodemon

安装 nodemon：

```shell
node install -g nodemon
```

### 3.2Express路由

#### 3.2.1路由的概念

广义上来讲，路由就是映射关系

举一个例子，在现实生活中，我们有时会拨打10086客服查询手机话费等信息，这时会让我们选择按键，比如按1是业务查询，按2是手机充值，按6是花费流量等等，在这里按键与服务之间的映射关系就可以称为路由

在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系

Express 中的路由分 3 部分组成，格式如下：

```js
app.METHOD(PATH, HANDLER);
//METHOD 是请求的类型，PATH 是请求的 URL 地址，HANDLER 是处理函数
```

路由的匹配过程：

每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数

在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理

注意：匹配时会按照定义的先后顺序进行匹配，而且请求类型和请求的 URL 同时匹配成功才会调用对应的处理函数

#### 3.2.2路由的使用

在 Express 中使用路由最简单的方式，就是把路由挂载到 app 上：

```js
const express = require('express');
const app = express();
//挂载路由
app.get('/', (req, res) => {
    res.send('Hello World');
})
app.get('/', (req, res) => {
    res.send('Post Request');
})
//启动 Web 服务器
app.listen(80, () =>{
    console.log('express server running at http://127.0.0.1');
})
```

在实际开发中，为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块

步骤如下：

- 创建路由模块对应的 .js 文件
- 调用 express.Router() 函数创建路由对象
- 向路由对象上挂载具体的路由
- 使用 module.exports 向外共享路由对象
- 使用 app.use() 函数注册路由模块

### 3.3Express中间件

#### 3.3.1中间件的概念

中间件（Middleware），特指业务流程的中间处理环节

举一个例子，在现实生活中有污水处理厂，在处理污水的时候，一般都要经过三个处理环节，从而保证处理过后的废水，达到排放标准

一级处理，去除污水中呈悬浮状态的固体污染物质；二级处理，去除污水中呈胶体和溶解状态的有机污染物质；三级处理，处理难降解的有机物、氮和磷等能够导致水体富营养化的可溶性无机物等

处理污水的这三个中间处理环节，就可以叫做中间件

在 Express 中，当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理

Express 的中间件，本质上就是一个 function 处理函数，Express 中间件的格式如下：

```js
const express = require('express');
const app = express();
app.get('/', function(req, res, next) {
    next();
})
app.listen(80);
```

注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res

next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由

#### 3.3.2Express中间件使用

1. 定义中间件函数

```js
const mw = function(req, res, next) {
    console.log('这是一个最简单的中间件函数');
    //在当前中间件的业务处理完毕后，必须调用 next() 函数，表示把流转关系转到下一个中间件或路由
    next();
}
```

2. 全局生效的中间件

客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件

通过调用 app.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下：

```js
const mw = function(req, res, next) {
    console.log('这是一个最简单的中间件函数');
    next();
}
//全局生效的中间件
app.use(mw);
```

简化：

```js
app.use(function(req, res, next) {
    console.log('这是一个最简单的中间件函数');
    next();
})
```

可以使用 app.use() 连续定义多个全局中间件，客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用

3. 中间件的作用

多个中间件之间，共享同一份 req 和 res，基于这样的特性，我们可以在上游的中间件中，统一为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用

4. 局部生效的中间件

不使用 app.use() 定义的中间件，叫做局部生效的中间件，示例代码如下：

```js
const mw = function(req, res, next) {
    console.log('这是中间件函数');
    next();
}
//局部生效的中间件，只在当前路由中生效
app.get('/', mw, function(req, res) {
    res.send('Home Page');
})
//mv 不会影响下面的路由
app.get('/user', function(req, res) {
    res.send('User Page');
})
```

5. 定义多个局部中间件

可以在路由中，通过如下两种等价的方式，使用多个局部中间件：

```js
app.get('/', mw1, mw2, (req, res) => {
    res.send('Home Page');
})
app.get('/', [mw1, mw2], (req, res) => {
    res.send('Home Page');
})
```

6. 中间件注意事项

- 定要在路由之前注册中间件
- 客户端发送过来的请求，可以连续调用多个中间件进行处理
- 执行完中间件的业务代码之后，不要忘记调用 next() 函数
- 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
- 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

#### 3.3.3中间件分类

1. 应用级别的中间件

通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件

2. 路由级别的中间件

绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件

它的用法和应用级别中间件没有任何区别，只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上

```js
var app = express();
var router = express.Router();
//路由级别的中间件
router.use(function(req, res, next) {
    console.log('Time:', Date.now());
    next();
})
app.use('/', router);
```

3. 错误级别的中间件

错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题

错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 (err, req, res, next)

```js
app.get('/', function(req, res) {//路由
    throw new Error('服务器内部发生了错误');//抛出一个定义的错误
    res.send('Home Page');
})
app.use(function(err, req, res, next) {//错误级别的中间件
    console.log('发生了错误：' + err.message);//在服务器打印错误消息
    res.send('Error' + err.message);//向客户端响应相应的错误内容
})
```

注意：错误级别的中间件，必须注册在所有路由之后

4. Express内置的中间件

自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：

- express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
- express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
- express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

5. 第三方的中间件

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件

在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率

#### 3.3.4自定义中间件

1. 需求描述与实现步骤

自己手动模拟一个类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据

实现步骤：

- 定义中间件
- 监听 req 的 data 事件
- 监听 req 的 end 事件
- 使用 querystring 模块解析请求体数据
- 将解析出来的数据对象挂载为 req.body
- 将自定义中间件封装为模块

2. 定义中间件

使用 app.use() 来定义全局生效的中间件，代码如下：

```js
app.use(function(req, res, next) {
    //中间件的业务逻辑
})
```

3. 监听 req 的 data 事件

在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据

如果数据量比较大，无法一次性发送完毕，则客户端会把数据切割后，分批发送到服务器，所以 data 事件可能会触发多次，每一次触发 data 事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接

```js
//定义变量，用来存储客户端发送过来的请求体数据
let str = '';
//监听 req 对象的 data 数据（客户端发送过来新的请求体数据）
req.on('data', (chunk) => {
    //拼接请求体数据，隐式转换为字符串
    str += chunk;
})
```

4. 监听 req 的 end 事件

当请求体数据接收完毕之后，会自动触发 req 的 end 事件

因此，我们可以在 req 的 end 事件中，拿到并处理完整的请求体数据，示例代码如下：

```js
//监听 req 对象的 end 事件（请求体发送完毕后自动触发）
req.on('end', () => {
    //打印完整的请求体数据
    console.log(str);
    //T0D0:把字符串格式的请求体数据解析成对象格式
})
```

5. 使用 querystring 模块解析请求体数据

Node.js 内置了一个 querystring 模块，专门用来处理查询字符串

通过这个模块提供的 parse() 函数，可以轻松把查询字符串，解析成对象的格式，示例代码如下：

```js
//导入处理 querystring 的 Node.js 内置模块
const qs = require('querystring');
//调用 qs.parse() 方法，把查询字符串解析为对象
const body = qs.parse(str);
```

6. 将解析出来的数据对象挂载为 req.body

上游的中间件和下游的中间件及路由之间，共享同一份 req 和 res，因此，我们可以将解析出来的数据，挂载为 req 的自定义属性，命名为 req.body，供下游使用，示例代码如下：

```js
req.on('end', () => {
    const body = qs.parse(str);//调用 qs.parse() 方法，把查询字符串解析为对象
    req.body = body;//将解析出来的请求体对象，挂载为 req.body 的属性
    next();//调用 next() 函数，执行后续业务逻辑
})
```

7. 将自定义中间件封装为模块

为了优化代码的结构，我们可以把自定义的中间件函数，封装为独立的模块，示例代码如下：

```js
const qs = require('querystring');
function bodyParser(req, res, next) {/* 省略其他代码 */}
module.exports = bodyParser;//向外导出解析请求体数据的中间件函数

const myBodyParser = require('custom-body-parser');
app.use(myBodyParser);
```

### 3.4使用Express写接口

#### 3.4.1创建基本服务器

```js
//导入 express 模块
const express = require('express');
//创建 express 服务器实例
const app = express();

//write code here...

//启动 Web 服务器
app.listen(80, () =>{
    console.log('express server running at http://127.0.0.1');
})
```

#### 3.4.2创建API路由模块

```js
//apiRouter.js 路由模块
const express = require('express');
const apiRouter = express.Router();

//bind router here...

module.exports = apiRouter;

//api.js 导入并注册路由模块
const apiRouter = require('./apiRouter.js');
app.use('/api', apiRouter);
```

#### 3.4.3编写GET接口

```js
apiRouter.get('/get', (req, res) => {
    //获取到客户端通过查询字符串发送到服务器的数据
    const query = req.query;
    //通过 res.send() 方法，把数据响应给客户端
    res.send({
        status: 0,          //状态，0成功，1失败
        msg: 'GET请求成功',  //状态描述
        data: query         //需要响应给客户端的具体数据
    })
})
```

#### 3.4.4编写POST接口

```js
apiRouter.post('/post', (req, res) => {
    //获取客户端通过请求体发送到服务器的 URL-encoded 数据
    const body = req.body;
    //通过 res.send() 方法，把数据响应给客户端
    res.send({
        status: 0,           //状态，0成功，1失败
        msg: 'POST请求成功',  //状态描述
        data: body           //需要响应给客户端的具体数据
    })
})
```

#### 3.4.5CORS跨域资源共享

上面编写的 GET 和 POST接口，存在一个很严重的问题：不支持跨域请求

解决接口跨域问题的方案主要有两种：

- CORS（主流的解决方案，推荐使用）
- JSONP（有缺陷的解决方案，只支持 GET 请求）

1. 使用 CORS 中间件解决跨域问题

CORS 是 Express 的一个第三方中间件，通过安装和配置 cors 中间件，可以很方便地解决跨域问题

使用 CORS 中间件的步骤：

- 运行 npm install cors 安装中间件
- 使用 const cors = require('cors') 导入中间件
- 在路由之前调用 app.use(cors()) 配置中间件

2. 什么是 CORS

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源

浏览器的同源安全策略默认会阻止网页“跨域”获取资源，但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制

CORS 注意事项：

- CORS 主要在服务器端进行配置，客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口
- CORS 在浏览器中有兼容性，只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）

3.  CORS 响应头部 Access-Control-Allow-Origin

响应头部中可以携带一个 Access-Control-Allow-Origin 字段，语法如下:

```js
Access-Control-Allow-Origin: <origin> | *
```

其中 origin 参数的值指定了允许访问该资源的外域 URL

例如，下面的字段值将只允许来自 http://itcast.cn 的请求：

```js
res.setHeader('Access-Control-Allow-Origin', 'http://itcast.cn');
```

如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *，表示允许来自任何域的请求

​	4.  CORS 响应头部 Access-Control-Allow-Headers

默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头：

Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）

如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败

```js
//允许客户端额外向服务器发送 Content-Type 请求头和 X-Custom-Header
res.setHeader('Access-Control-Allow-Headers', 'Content-Type, X-Custom-Header');
```

5. CORS 响应头部 Access-Control-Allow-Methods

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求

如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods 来指明实际请求所允许使用的 HTTP 方法

```js
//只允许 GET、POST、HEAD、PUT 请求方法
res.setHeader('Access-Control-Allow-Methods', 'GET, POST, HEAD, PUT');
//允许所有的 HTTP 请求方法
res.setHeader('Access-Control-Allow-Methods', '*');
```

6. CORS请求

客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为简单请求和预检请求

简单请求需同时满足以下两大条件：

- 请求方式：GET、POST、HEAD 三者之一
- HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-formurlencoded、multipart/form-data、text/plain）

预检请求只要符合以下任何一个条件：

- 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
- 请求头中包含自定义头部字段
- 向服务器发送了 application/json 格式的数据

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”，服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据

简单请求和预检请求的区别：

- 简单请求客户端与服务器之间只会发生一次请求
- 预检请求客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求

## 4数据库与身份认证

### 4.1数据库的基本概念

数据库（database）是用来组织、存储和管理数据的仓库

当今世界是一个充满着数据的互联网世界，充斥着大量的数据。数据的来源有很多，比如出行记录、消费记录、浏览的网页、发送的消息等等。除了文本类型的数据，图像、音乐、声音都是数据

为了方便管理互联网世界中的数据，就有了数据库管理系统的概念（简称：数据库）。用户可以对数据库中的数据进行新增、查询、更新、删除等操作

市面上的数据库有很多种，最常见的数据库有如下几个：

- MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise）
- Oracle 数据库（收费）
- SQL Server 数据库（收费）
- Mongodb 数据库（Community + Enterprise）

MySQL、Oracle、SQL Server 属于传统型数据库（又叫做：关系型数据库 或 SQL 数据库），这三者的设计理念相同，用法比较类似

而 Mongodb 属于新型数据库（又叫做：非关系型数据库 或 NoSQL 数据库），它在一定程度上弥补了传统型数据库的缺陷

传统型数据库的数据组织结构，与 Excel 中数据的组织结构比较类似（数据的组织结构指的就是数据以什么样的结构进行存储）

每个 Excel 中，数据的组织结构分别为工作簿、工作表、数据行、列这 4 大部分组成

在传统型数据库中，数据的组织结构分为数据库(database)、数据表(table)、数据行(row)、字段(field)这 4 大部分组成

- 在实际项目开发中，一般情况下，每个项目都对应独立的数据库
- 不同的数据，要存储到数据库的不同表中，例如：用户数据存储到 users 表中，图书数据存储到 books 表中
- 每个表中具体存储哪些信息，由字段来决定，例如：我们可以为 users 表设计 id、username、password 这 3 个字段
- 表中的行，代表每一条具体的数据

### 4.2SQL的基本使用

#### 4.2.1什么是SQL

SQL（Structured Query Language）是结构化查询语言，专门用来访问和处理数据库的编程语言，能够让我们以编程的形式，操作数据库里面的数据

- SQL 是一门数据库编程语言
- 使用 SQL 语言编写出来的代码，叫做 SQL 语句
- SQL 语言只能在关系型数据库中使用（MySQL、Oracle、SQL Server），非关系型数据库（Mongodb）不支持 SQL 语言

#### 4.2.2SQL语句

1. SQL 的 select 语句

select 语句用于从表中查询数据。执行的结果被存储在一个结果表中（称为结果集），语法格式如下：

```sql
-- 从 from 指定的表中查询所有的数据，* 表示所有列
select * from 表名称
-- 从 from 指定的表中查询指定列（字段）的数据
select 列名称 from 表名称
```

注意：SQL 语句中的关键字对大小写不敏感，SELECT 等效于 select，FROM 等效于 from

示例：

```sql
-- 获取名为 username 的列的内容
select username from users
-- 获取名为 username 和 password 的列的内容，多个列之间用英文逗号分隔
select uesrname, password from users
```

2. SQL 的 insert into 语句

insert into 语句用于向数据表中插入新的数据行，语法格式如下：

```sql
-- 向指定的表中插入几列数据，列的值通过 values 指定
-- 列和值要一一对应，多个列和值之间用英文逗号分隔
insert into 表名称 (列1,列2,...) values (值1,值2,...)
```

示例：

```sql
-- 向 users 表中插入一条 username 为 tony，password 为 777888 的用户数据
insert into users (username, password) values ('tony', '777888')
```

3. SQL 的 update 语句

update 语句用于修改表中的数据，语法格式如下：

```sql
-- 用 update 指定要更新哪个表中的数据，用 set 指定列对应的新值，用 where 指定更新的条件
update 表名称 set 列名称 = 新值 where 列名称 = 某值
```

示例：

```sql
-- 把 users 表中 id 为 7 的用户密码更新为 888777
update users set password = '888777' where id = 7
-- 把 users 表中 id 为 2 的用户密码和用户状态分别更新为 777777 和 1
update users set password = '777777', status = 1 where id = 2
```

4. SQL 的 delete 语句

delete 语句用于删除表中的行，语法格式如下：

```sql
-- 从指定表中根据 where 条件删除对应的数据行
delete from 表名称 where 列名称 = 值
```

示例：

```sql
-- 从 users 表中删除id为4的用户
delete from users where id = 4
```

5. SQL 的 where 子句

where 子句用于限定选择的标准，在 select、update、delete 语句中，皆可使用 where 子句来限定选择的标准

可在 where 子句中使用的运算符：

| 操作符  |     描述     |
| :-----: | :----------: |
|    =    |     等于     |
|   <>    |    不等于    |
|    >    |     大于     |
|    <    |     小于     |
|   >=    |   大于等于   |
|   <=    |   小于等于   |
| between | 在某个范围内 |
|  like   | 搜索某种模式 |

在某些版本的 SQL 中，操作符 <> 可以写为 !=

6. SQL 的 and 和 or 运算符

and 和 or 可在 where 子语句中把两个或多个条件结合起来

and 表示必须同时满足多个条件，相当于 && 运算符，or 表示只要满足任意一个条件即可，相当于 || 运算符

and 示例：

```sql
-- 选择所有 status 为 0 且 id 小于 3 的用户
select * from users where status = 0 and id < 3
```

or 示例：

```sql
-- 选择所有 status 为 1 且 username 为 zs 的用户
select * from users where status = 1 or username = 'zs'
```

7. SQL 的 order by 子句

order by 语句用于根据指定的列对结果集进行排序

order by 语句默认按照升序对记录进行排序

如果要按照降序对记录进行排序，可以使用 desc 关键字

asc 关键字代表升序排序，默认可省略

示例：

```sql
-- 对 users 表中的数据按照 status 字段进行升序排序
select * from users order by status asc
-- 对 users 表中的数据按照 id 字段进行降序排序
select * from users order by id desc
-- 对 users 表中的数据先按照 status 字段进行降序排序，再按照 username 的字母顺序进行升序排序
select * from users order by status desc, username asc
```

8. SQL 的 count(*) 函数

count(*) 函数用于返回查询结果的总数据条数，语法格式如下：

```sql
select count(*) from 表名称
```

示例：

```sql
-- 查询 users 表中 status 为 0 的总数据条数
select count(*) from users where status = 0
-- 将列名称从 count(*) 修改为 total
select count(*) as total from users where status = 0
```

### 4.3在项目中操作数据库

#### 4.3.1mysql模块

mysql 模块是托管于 npm 上的第三方模块，它提供了在 Node.js 项目中连接和操作 MySQL 数据库的能力

安装：

```shell
npm install mysql
```

在使用 mysql 模块操作 MySQL 数据库之前，必须先对 mysql 模块进行必要的配置，主要的配置步骤如下：

```js
//导入 mysql 模块
const mysql = require('mysql');
//建立与 MySQL 数据库的链接
const db = mysql.creatPool({
    host: '127.0.0.1',     //数据库的 IP 地址
    user: 'root',          //登录数据库的账号
    password: 'admin123',  //登录数据库的密码
    database: 'my_db_01'   //指定要操作哪个数据库
});
```

测试 mysql 模块能否正常工作，调用 db.query() 函数，指定要执行的 SQL 语句，通过回调函数拿到执行的结果：

```js
db.query('SELECT1', (err, results) => {
    if(err) return console.log(err.message);
    //只要能打印出 [ RowDataPacket { '1': 1 } ] 的结果，就证明数据库连接正常
    consol.log(results);
})
```

#### 4.3.2使用mysql模块操作MySQL

1. 查询数据

```js
//查询 users 表中的所有数据
db.query('select * from users', (err, results) => {
    //查询失败
    if (err) return console.log(err.message);
    //查询成功
    console.log(results);
})
```

2. 插入数据

向 users 表中新增数据，其中 username 为 Spiderman，password 为 pcc321

```js
//要插入到 users 表中的数据对象
const user = {username: 'Spiderman', password: 'pcc321'}
//待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'insert into users (username, password) values (?, ?)';
//使用数组的形式，依次为 ? 占位符指定具体的值
db.query(sqlStr, [user.username, user.password], (err, results) => {
    if (err) return console.log(err.message);//失败
    if (results.affectedRows === 1) {consloe.log('插入数据成功');}//成功
})
```

向表中新增数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速插入数据：

```js
//要插入到 users 表中的数据对象
const user = {username: 'Spiderman', password: 'pcc321'}
//待执行的 SQL 语句，其中英文的 ? 表示占位符
const sqlStr = 'insert into users set ?';
//直接将数据对象当作占位符的值
db.query(sqlStr, user, (err, results) => {
    if (err) return console.log(err.message);//失败
    if (results.affectedRows === 1) {consloe.log('插入数据成功');}//成功
})
```

3. 更新数据

```js
//要更新的数据对象
const user = { id: 7, username = 'aaa', password = '000'}
//要执行的 SQL 语句
const sqlStr = 'update users set username = ?, password = ? where id = ?';
//调用 db.query() 执行 SQL 语句的同时，使用数组依次为占位符指定具体的值
db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
    if (err) return console.log(err.message);//失败
    if (results.affectedRows === 1) {console.log('更新数据成功');}//成功
})
```

更新表中数据时，如果数据对象的每个属性和数据表的字段一一对应，则可以通过如下方式快速更新表数据：

```js
//要更新的数据对象
const user = { id: 7, username = 'aaaa', password = '0000'}
//要执行的 SQL 语句
const sqlStr = 'update users set ? where id = ?';
//调用 db.query() 执行 SQL 语句的同时，使用数组依次为占位符指定具体的值
db.query(sqlStr, [user, user.id], (err, results) => {
    if (err) return console.log(err.message);//失败
    if (results.affectedRows === 1) {console.log('更新数据成功');}//成功
})
```

4. 删除数据

```js
//要执行的 SQL 语句
const sqlStr = 'delete from users where id = ?';
//调用 db.query() 执行 SQL 语句的同时，为占位符指定具体的值
db.query(sqlStr, 7, (err, results) => {
    if (err) return console.log(err.message);//失败
    if (results.affectedRows === 1) {console.log('删除数据成功');}//成功
})
```

使用 delete 语句，会把真正的把数据从表中删除掉，为了保险起见，推荐使用标记删除的形式，来模拟删除的动作

标记删除，就是在表中设置类似于 status 这样的状态字段，来标记当前这条数据是否被删除

当用户执行了删除的动作时，我们并没有执行 delete 语句把数据删除掉，而是执行了 update 语句，将这条数据对应的 status 字段标记为删除即可

```js
db.query('update users set status = 1 where id = ?', 6, (err, results) => {
    if (err) return console.log(err.message);//失败
    if (results.affectedRows === 1) {console.log('删除数据成功');}//成功
})
```

### 4.4前后端身份认证

#### 4.4.1Web开发模式

目前主流的 Web 开发模式有两种，分别是：基于服务端渲染的传统 Web 开发模式，基于前后端分离的新型 Web 开发模式

1. 服务端渲染的 Web 开发模式

服务端渲染的概念：服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的，因此，客户端不需要使用 Ajax 这样的技术额外请求页面的数据，代码示例如下：

```js
app.get('/index.html', (req, res) => {
    //要渲染的数据
    const user = {name:'zs', age: 20}
    //服务器端通过字符串的拼接动态生成 HTML 内容
    const html = `<h1>姓名: ${user.name}, 年龄: ${user.age}<h1>`;
    //把生成好的页面内容响应给客户端
    res.send(html);
})
```

优点：

- 前端耗时少，因为服务器端负责动态生成 HTML 内容，浏览器只需要直接渲染页面即可，尤其是移动端，更省电
- 有利于SEO，因为服务器端响应的是完整的 HTML 页面内容，所以爬虫更容易爬取获得信息，更有利于 SEO

缺点:

- 占用服务器端资源，即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力
- 不利于前后端分离，开发效率低，使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发

2. 前后端分离的 Web 开发模式

前后端分离的概念：前后端分离的开发模式，依赖于 Ajax 技术的广泛应用，简而言之，前后端分离的 Web 开发模式，就是后端只负责提供 API 接口，前端使用 Ajax 调用接口的开发模式

优点：

- 开发体验好，前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性
- 用户体验好，Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新
- 减轻了服务器端的渲染压力，因为页面最终是在每个用户的浏览器中生成的

缺点：

- 不利于 SEO，因为完整的 HTML 页面需要在客户端动态拼接完成，所以爬虫对无法爬取页面的有效信息（解决方案：利用 Vue、React 等前端框架的 SSR （server side render）技术能够很好的解决 SEO 问题）

#### 4.4.2身份认证

身份认证（Authentication）又称“身份验证”、“鉴权”，是指通过一定的手段，完成对用户身份的确认

日常生活中的身份认证随处可见，例如：高铁的验票乘车，手机的密码或指纹解锁，支付宝或微信的支付密码等

在 Web 开发中，也涉及到用户身份的认证，例如：各大网站的手机验证码登录、邮箱密码登录、二维码登录等

身份认证的目的，是为了确认当前所声称为某种身份的用户，确实是所声称的用户

对于服务端渲染和前后端分离这两种开发模式来说，分别有着不同的身份认证方案：

- 服务端渲染推荐使用 Session 认证机制
- 前后端分离推荐使用 JWT 认证机制

1. Session认证机制

了解 HTTP 协议的无状态性是进一步学习 Session 认证机制的必要前提

HTTP 协议的无状态性，指的是客户端的每次 HTTP 请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次 HTTP 请求的状态

在现实生活中，我们在超市结账收银时，超市收银员是记不住当前客户是否为 VIP 用户的，为了方便收银员在进行结算时给 VIP 用户打折，超市可以为每个 VIP 用户发放会员卡

注意：现实生活中的会员卡身份认证方式，在 Web 开发中的专业术语叫做 Cookie

Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串，它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成

不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的 Cookie 一同发送到服务器

Cookie的几大特性：

- 自动发送
- 域名独立
- 过期时限
- 4KB 限制

Cookie 在身份认证中的作用：

- 客户端第一次请求服务器的时候，服务器通过响应头的形式，向客户端发送一个身份认证的 Cookie，客户端会自动将 Cookie 保存在浏览器中
- 随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的 Cookie，通过请求头的形式发送给服务器，服务器即可验明客户端的身份

由于 Cookie 是存储在浏览器中的，而且浏览器也提供了读写 Cookie 的 API，因此 Cookie 很容易被伪造，不具有安全性，因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器

超市收银的例子，为了防止客户伪造会员卡，收银员在拿到客户出示的会员卡之后，可以在收银机上进行刷卡认证，只有收银机确认存在的会员卡，才能被正常使用

这种“会员卡 + 刷卡认证”的设计理念，就是 Session 认证机制的精髓

2. JWT认证机制

Session 认证机制需要配合 Cookie 才能实现，由于 Cookie 默认不支持跨域访问，所以，当涉及到前端跨域请求后端接口的时候，需要做很多额外的配置，才能实现跨域 Session 认证

当前端需要跨域请求后端接口的时候，不推荐使用 Session 身份认证机制，推荐使用 JWT 认证机制

JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案

JWT 通常由三部分组成，分别是 Header（头部）、Payload（有效荷载）、Signature（签名），三者之间使用英文的“.”分隔

- Payload 部分才是真正的用户信息，它是用户信息经过加密之后生成的字符串
- Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性

JWT 的使用方式：

- 客户端收到服务器返回的 JWT 之后，通常会将它储存在 localStorage 或 sessionStorage 中
- 此后，客户端每次与服务器通信，都要带上这个 JWT 的字符串，从而进行身份认证
- 推荐的做法是把 JWT 放在 HTTP 请求头的 Authorization 字段中

#### 4.4.3在Express中使用Session认证

1. 安装 express-session 中间件

在 Express 项目中，只需要安装 express-session 中间件，即可在项目中使用 Session 认证：

```shell
npm install express-session
```

2. 配置 express-session 中间件

express-session 中间件安装成功后，需要通过 app.use() 来注册 session 中间件，示例代码如下：

```js
//导入 session 中间件
var session = require('express-session');
//配置 session 中间件
app.use(session({
    secret: 'keboard cat',   //secret 属性的值可以为任意字符串
    resave: false,           //固定写法
    saveUninitialized: true  //固定写法
}))
```

3. 向 session 中存数据

当 express-session 中间件配置成功后，即可通过 req.session 来访问和使用 session 对象，从而存储用户的关键信息：

```js
app.post('/api/login', (req, res) => {
    //判断用户提交的登录信息是否正确
    if (req.body.username !== 'admin' || req.body.password !== '000000') {
        return res.send({status: 1, msg: '登录失败'});
    }
    req.session.user = req.body;    //将用户的信息存储到 session 中
    req.session.islogin = true;     //将用户的登录状态存储到 session 中
    res.send({status: 0, msg: '登录成功'});
})
```

4. 从 session 中取数据

可以直接从 req.session 对象上获取之前存储的数据，示例代码如下：

```js
//获取用户姓名的接口
app.get('/api/username', (req, res) => {
    //判断用户是否登录
    if (!req.session.islogin) {
        return res.send({status: 1, msg: 'fail'});
    }
    res.send({status: 0, msg: 'success', username: req.session.user.username});
})
```

5. 清空 session

调用 req.session.destroy() 函数，即可清空服务器保存的 session 信息：

```js
//退出登录的接口
app.post('/api/logout', (req, res) => {
    //清空当前客户端对应的 session 信息
    req.session.destroy()
    res.send({
        status: 0,
        msg: '退出登录成功'
    })
})
```

#### 4.4.4在Express中使用JWT

1. 安装 JWT 相关的包

运行如下命令，安装如下两个 JWT 相关的包：

```shell
npm install jsonwebtoken express-jwt
```

- jsonwebtoken 用于生成 JWT 字符串
- express-jwt 用于将 JWT 字符串解析还原成 JSON 对象

2. 导入 JWT 相关的包

使用 require() 函数，分别导入 JWT 相关的两个包：

```js
//导入用于生成 JWT 字符串的包
const jwt = require('jsonwebtoken');
//导入用于将客户端发送过来的 JWT 字符串解析还原成 JSON 对象的包
const expressJWT = require('express-jwt');
```

3. 定义 secret 密钥

为保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于加密和解密的 secret 密钥：

- 当生成 JWT 字符串的时候，需要使用 secret 密钥对用户的信息进行加密，最终得到加密好的 JWT 字符串
- 当把 JWT 字符串解析还原成 JSON 对象的时候，需要使用 secret 密钥进行解密

```js
//secret 密钥的本质就是一个字符串
const secretKey = 'alone777.3vdo.club';
```

4. 在登录成功后生成 JWT 字符串

调用 jsonwebtoken 包提供的 sign() 方法，将用户的信息加密成 JWT 字符串，响应给客户端：

```js
//登录接口
app.post('/api/login', (req, res) => {
    //...
    //登录成功后生成 JWT 字符串，通过 token 属性响应给客户端
    res.send({
        status: 200,
        message: '登录成功',
        //调用 jwt.sign() 生成 JWT 字符串，三个参数分别是：用户信息对象、加密密钥、配置对象
        token: jwt.sign({username: userinfo.username}, secretKey, {expiresIn: '30s'})
    })
})
```

5. 将 JWT 字符串还原为 JSON 对象

客户端每次在访问那些有权限接口的时候，都需要主动通过请求头中的 Authorization 字段，将 Token 字符串发送到服务器进行身份认证

此时，服务器可以通过 express-jwt 这个中间件，自动将客户端发送过来的 Token 解析还原成 JSON 对象：

```js
app.use(expressJWT({secret: secretKey}).unless({path: [/^\/api\//]}));
//expressJWT({secret: secretKey}) 是用来解析 token 的中间件
//.unless({path: [/^\/api\//]}) 是用来指定哪些接口不需要访问权限
```

6. 使用 req.user 获取用户信息

当 express-jwt 这个中间件配置成功之后，即可在那些有权限的接口中，使用 req.user 对象，来访问从 JWT 字符串中解析出来的用户信息了，示例代码如下：

```js
//这是一个有权限的 API 接口
app.get('/admin/getinfo', function(req, res) {
    console.log(req.user);
    res.send({
        status: 200,
        message: '获取用户信息成功',
        data: req.user
    })
})
```

7. 捕获解析 JWT 失败后产生的错误

当使用 express-jwt 解析 Token 字符串时，如果客户端发送过来的 Token 字符串过期或不合法，会产生一个解析失败的错误，影响项目的正常运行，可以通过 Express 的错误中间件，捕获这个错误并进行相关的处理，示例代码如下：

```js
app.use((err, req, res, next) => {
    //token 解析失败导致的错误
    if(err.name === 'UnauthorizedError') {
        return res.send({status: 401, message: '无效的token'})
    }
    //其他原因导致的错误
    res.send({status: 500, message: '未知错误'})
})
```
