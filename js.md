
## JavaScript部分
### 引起内存泄漏的操作有哪些
1.全局变量引起

2.闭包引起

3.dom清空，事件未清除

4.子元素存在引用

5.被遗忘的计时器

### 简要介绍ES6
ES6在变量的声明和定义方面增加了let、const声明变量，有局部变量的概念，赋值中有比较吸引人的结构赋值，同时ES6对字符串、
数组、正则、对象、函数等拓展了一些方法，如字符串方面的模板字符串、函数方面的默认参数、对象方面属性的简洁表达方式，ES6也
引入了新的数据类型symbol，新的数据结构set和map,symbol可以通过typeof检测出来，为解决异步回调问题，引入了promise和
generator，还有最为吸引人了实现Class和模块，通过Class可以更好的面向对象编程，使用模块加载方便模块化编程，当然考虑到
浏览器兼容性，我们在实际开发中需要使用babel进行编译。

### 对js原型的理解
我们知道在es6之前，js没有类和继承的概念，js是通过原型来实现继承的。在js中一个构造函数默认自带有一个prototype属性，
这个的属性值是一个对象，同时这个prototype对象自带有一个constructor属性，这个属性指向这个构造函数，同时每一个实例
都有一个__proto__属性指向这个prototype对象，我们可以将这个叫做隐式原型，我们在使用一个实例的方法的时候，会先检查
这个实例中是否有这个方法，没有则会继续向上查找这个prototype对象是否有这个方法，刚刚我们说到prototype是一个对象，
那么也即是说这个是一个对象的实例，那么这个对象同样也会有一个__proto__属性指向对象的prototype对象。

### 对js模块化的理解
在ES6出现之前，js没有标准的模块化概念，这也就造成了js多人写作开发容易造成全局污染的情况，以前我们可能会采用立即执行
函数、对象等方式来尽量减少变量这种情况，后面社区为了解决这个问题陆续提出了AMD规范和CMD规范，这里不同于Node.js的
CommonJS的原因在于服务端所有的模块都是存在于硬盘中的，加载和读取几乎是不需要时间的，而浏览器端因为加载速度取决于网速，
因此需要采用异步加载，AMD规范中使用define来定义一个模块，使用require方法来加载一个模块，现在ES6也推出了标准的模块
加载方案，通过export和import来导出和导入模块。

### 简要介绍事件代理，以及什么时候使用，事件代理发生在事件处理流程的哪个阶段，有什么好处？
事件代理就是说我们将事件添加到本来要添加事件的父节点，将事件委托给父节点来触发处理函数，这通常会在
这通常会使用在大量的同级元素需要添加同一类事件的时候，比如一个动态的非常多的列表，需要为每个列表项都添加
点击事件，这时可以使用事件代理，通过判断e.target.nodeName来判断发生的具体元素，从而判断是否是在
列表项中触发，这样的好处是可以减少事件绑定，同时动态的DOM结构仍然可以监听。事件代理发生在冒泡阶段。

### 原生JS操作DOM的方法有哪些？
获取节点的方法getElementById、getElementsByClassName、getElementsByTagName、
getElementsByName、querySelector、querySelectorAll,对元素属性进行操作的 getAttribute、
setAttribute、removeAttribute方法，对节点进行增删改的appendChild、insertBefore、replaceChild、removeChild、
createElement等

### typeof操作符返回值有哪些，对undefined、null、NaN使用这个操作符分别返回什么
typeof的返回值有undefined、boolean、string、number、object、function、symbol。对undefined
使用返回undefined、null使用返回object，NaN使用返回number


### javascript做类型判断的方法有哪些？
typeof、instanceof 、 Object.prototype.toString()

### ES6之前JavaScript如何实现继承？
ES6之前的继承是通过原型来实现的，也就是每一个构造函数都会有一个prototype属性，然后如果我们调用一个实例的方法或者属性，首先会在自身寻找，然后在
构造函数的prototype上寻找，而prototype本质上就是一个实例，因此如果prototype上还没有则会往prototype上的构造函数的prototype寻找，因此实现继承
可以让构造函数的prototype是父级的一个实例就是以实现继承。


### 如何阻止事件冒泡和默认事件？
标准的DOM对象中可以使用事件对象的stopPropagation()方法来阻止事件冒泡，但在IE8以下中IE的事件对象通过设置事件对象的cancelBubble属性为true来阻止冒泡；
默认事件的话通过事件对象的preventDefault()方法来阻止，而IE通过设置事件对象的returnValue属性为false来阻止默认事件。

### addEventListener有哪些参数？
有三个参数，第一个是事件的类型，第二个是事件的回调函数，第三个是一个表示事件是冒泡阶段还是捕获阶段捕获的布尔值，true表示捕获，false表示冒泡

### 函数节流是什么？
函数节流就是让一个函数无法在很短的时间间隔内连续调用，而是间隔一段时间执行，这在我们为元素绑定一些事件的时候经常会用到，比如我们
为window绑定了一个resize事件，如果用户一直改变窗口大小，就会一直触发这个事件处理函数，这对性能有很大影响。

### 什么是深拷贝，什么是浅拷贝？
浅拷贝是指仅仅复制对象的引用，而不是复制对象本身；深拷贝则是把复制对象所引用的全部对象都复制一遍。


### 请说一下实现jsonp的实现思路？
jsonp的原理是使用script标签来实现跨域，因为script标签的的src属性是不受同源策略的影响的，因此可以使用其来跨域。一个最简单的jsonp就是创建一个script标签，设置src为相应的url，在url之后添加相应的callback，格式类似于
url?callback=xxx，服务端根据我们的callback来返回相应的数据，类似于res.send(req.query.callback + '('+ data + ')')，这样就实现了一个最简单的jsonp


### let和const的异同有哪些？
let和const都是对变量的声明，都有块级作用域的概念，不同的是const是对常量的声明，因此声明同时必须赋值，且之后不能更改，而let则可以。

### GET和POST的区别，何时使用POST？
    GET：一般用于信息获取，使用URL传递参数，对所发送信息的数量也有限制，一般在2000个字符

    POST：一般用于修改服务器上的资源，对所发送的信息没有限制。


    GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值，

    也就是说Get是通过地址栏来传值，而Post是通过提交表单来传值。



### 然而，在以下情况中，请使用 POST 请求：

无法使用缓存文件（更新服务器上的文件或数据库）

向服务器发送大量数据（POST 没有数据量限制）

发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠css sprite是什么,有什么优缺点
概念：将多个小图片拼接到一个图片中。通过background-position和元素尺寸调节需要显示的背景图案。

优点：

减少HTTP请求数，极大地提高页面加载速度
增加图片信息重复度，提高压缩比，减少图片大小
更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现
缺点：

图片合并麻烦
维护麻烦，修改一个图片可能需要从新布局整个图片，样式

### display: none;与visibility: hidden;的区别
联系：它们都能让元素不可见

区别：

display:none;会让元素完全从渲染树中消失，渲染的时候不占据任何空间；visibility: hidden;不会让元素从渲染树消失，渲染师元素继续占据空间，只是内容不可见
display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示；visibility: hidden;是继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式
修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。
读屏器不会读取display: none;元素内容；会读取visibility: hidden;元素内容


### 什么闭包,闭包有什么用
闭包是在某个作用域内定义的函数，它可以访问这个作用域内的所有变量。闭包作用域链通常包括三个部分：

函数本身作用域。
闭包定义时的作用域。
全局作用域。
闭包常见用途：

创建特权方法用于访问控制
事件处理程序及回调


### HTTP状态码
    100  Continue  继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息

    200  OK   正常返回信息

    201  Created  请求成功并且服务器创建了新的资源

    202  Accepted  服务器已接受请求，但尚未处理

    301  Moved Permanently  请求的网页已永久移动到新位置。

    302 Found  临时性重定向。

    303 See Other  临时性重定向，且总是使用 GET 请求新的 URI。

    304  Not Modified  自从上次请求后，请求的网页未修改过。


    400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。

    401 Unauthorized  请求未授权。

    403 Forbidden  禁止访问。

    404 Not Found  找不到如何与 URI 相匹配的资源。

    500 Internal Server Error  最常见的服务器端错误。

    503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。


### 说说你对前端架构师的理解
负责前端团队的管理及与其他团队的协调工作，提升团队成员能力和整体效率； 带领团队完成研发工具及平台前端部分的设计、研发和维护； 带领团队进行前端领域前沿技术研究及新技术调研，保证团队的技术领先 负责前端开发规范制定、功能模块化设计、公共组件搭建等工作，并组织培训。

### 请解释什么是事件代理
事件代理（Event Delegation），又称之为事件委托。是 JavaScript 中常用绑定事件的常用技巧。顾名思义，“事件代理”即是把原本需要绑定的事件委托给父元素，让父元素担当事件监听的职务。事件代理的原理是DOM元素的事件冒泡。使用事件代理的好处是可以提高性能

### 什么样的前端代码是好的
高复用低耦合，这样文件小，好维护，而且好扩展。

