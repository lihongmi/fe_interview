
## JavaScript部分
### 1.引起内存泄漏的操作有哪些
1.全局变量引起

2.闭包引起

3.dom清空，事件未清除

4.子元素存在引用

5.被遗忘的计时器

### 2.简要介绍ES6
ES6在变量的声明和定义方面增加了let、const声明变量，有局部变量的概念，赋值中有比较吸引人的结构赋值，同时ES6对字符串、
数组、正则、对象、函数等拓展了一些方法，如字符串方面的模板字符串、函数方面的默认参数、对象方面属性的简洁表达方式，ES6也
引入了新的数据类型symbol，新的数据结构set和map,symbol可以通过typeof检测出来，为解决异步回调问题，引入了promise和
generator，还有最为吸引人了实现Class和模块，通过Class可以更好的面向对象编程，使用模块加载方便模块化编程，当然考虑到
浏览器兼容性，我们在实际开发中需要使用babel进行编译。

### 4.对js原型的理解
我们知道在es6之前，js没有类和继承的概念，js是通过原型来实现继承的。在js中一个构造函数默认自带有一个prototype属性，
这个的属性值是一个对象，同时这个prototype对象自带有一个constructor属性，这个属性指向这个构造函数，同时每一个实例
都有一个__proto__属性指向这个prototype对象，我们可以将这个叫做隐式原型，我们在使用一个实例的方法的时候，会先检查
这个实例中是否有这个方法，没有则会继续向上查找这个prototype对象是否有这个方法，刚刚我们说到prototype是一个对象，
那么也即是说这个是一个对象的实例，那么这个对象同样也会有一个__proto__属性指向对象的prototype对象。

### 5.对js模块化的理解
在ES6出现之前，js没有标准的模块化概念，这也就造成了js多人写作开发容易造成全局污染的情况，以前我们可能会采用立即执行
函数、对象等方式来尽量减少变量这种情况，后面社区为了解决这个问题陆续提出了AMD规范和CMD规范，这里不同于Node.js的
CommonJS的原因在于服务端所有的模块都是存在于硬盘中的，加载和读取几乎是不需要时间的，而浏览器端因为加载速度取决于网速，
因此需要采用异步加载，AMD规范中使用define来定义一个模块，使用require方法来加载一个模块，现在ES6也推出了标准的模块
加载方案，通过export和import来导出和导入模块。

### 7.简要介绍事件代理，以及什么时候使用，事件代理发生在事件处理流程的哪个阶段，有什么好处？
事件代理就是说我们将事件添加到本来要添加事件的父节点，将事件委托给父节点来触发处理函数，这通常会在
这通常会使用在大量的同级元素需要添加同一类事件的时候，比如一个动态的非常多的列表，需要为每个列表项都添加
点击事件，这时可以使用事件代理，通过判断e.target.nodeName来判断发生的具体元素，从而判断是否是在
列表项中触发，这样的好处是可以减少事件绑定，同时动态的DOM结构仍然可以监听。事件代理发生在冒泡阶段。

### 13.原生JS操作DOM的方法有哪些？
获取节点的方法getElementById、getElementsByClassName、getElementsByTagName、
getElementsByName、querySelector、querySelectorAll,对元素属性进行操作的 getAttribute、
setAttribute、removeAttribute方法，对节点进行增删改的appendChild、insertBefore、replaceChild、removeChild、
createElement等

### 14.typeof操作符返回值有哪些，对undefined、null、NaN使用这个操作符分别返回什么
typeof的返回值有undefined、boolean、string、number、object、function、symbol。对undefined
使用返回undefined、null使用返回object，NaN使用返回number


### 16.javascript做类型判断的方法有哪些？
typeof、instanceof 、 Object.prototype.toString()

### 20.ES6之前JavaScript如何实现继承？
ES6之前的继承是通过原型来实现的，也就是每一个构造函数都会有一个prototype属性，然后如果我们调用一个实例的方法或者属性，首先会在自身寻找，然后在
构造函数的prototype上寻找，而prototype本质上就是一个实例，因此如果prototype上还没有则会往prototype上的构造函数的prototype寻找，因此实现继承
可以让构造函数的prototype是父级的一个实例就是以实现继承。


### 21.如何阻止事件冒泡和默认事件？
标准的DOM对象中可以使用事件对象的stopPropagation()方法来阻止事件冒泡，但在IE8以下中IE的事件对象通过设置事件对象的cancelBubble属性为true来阻止冒泡；
默认事件的话通过事件对象的preventDefault()方法来阻止，而IE通过设置事件对象的returnValue属性为false来阻止默认事件。

### 22.addEventListener有哪些参数？
有三个参数，第一个是事件的类型，第二个是事件的回调函数，第三个是一个表示事件是冒泡阶段还是捕获阶段捕获的布尔值，true表示捕获，false表示冒泡

### 25.函数节流是什么？
函数节流就是让一个函数无法在很短的时间间隔内连续调用，而是间隔一段时间执行，这在我们为元素绑定一些事件的时候经常会用到，比如我们
为window绑定了一个resize事件，如果用户一直改变窗口大小，就会一直触发这个事件处理函数，这对性能有很大影响。

### 27.什么是深拷贝，什么是浅拷贝？
浅拷贝是指仅仅复制对象的引用，而不是复制对象本身；深拷贝则是把复制对象所引用的全部对象都复制一遍。


### 34.请说一下实现jsonp的实现思路？
jsonp的原理是使用script标签来实现跨域，因为script标签的的src属性是不受同源策略的影响的，因此可以使用其来跨域。一个最简单的jsonp就是创建一个script标签，设置src为相应的url，在url之后添加相应的callback，格式类似于
url?callback=xxx，服务端根据我们的callback来返回相应的数据，类似于res.send(req.query.callback + '('+ data + ')')，这样就实现了一个最简单的jsonp


### 40.let和const的异同有哪些？
let和const都是对变量的声明，都有块级作用域的概念，不同的是const是对常量的声明，因此声明同时必须赋值，且之后不能更改，而let则可以。
