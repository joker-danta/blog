###### 前端面试中，经常提起的面试题（一）

- use strict; 的作用
> use strict;顾名思义也就是 JavaScript 会在所谓严格模式下执行，其一个主要的优势在于能够强制开发者避免使用未声明的变量。对于老版本的浏览器或者执行引擎则会自动忽略该指令。

```
// Example
"use strict";
catchThemAll();
function catchThemAll() {
  x = 3.14; // Error will be thrown
  return x * x;
}
```

- 变量提升机制

> 这也是面试中经常问到的问题，顾名思义即是 JavaScript 会将所有的声明提升到当前作用域的顶部。这也就意味着我们可以在某个变量声明前就使用该变量，不过虽然 JavaScript 会将声明提升到顶部，但是并不会执行真的初始化过程。

```
// Example  

console.log(a); // 输出 function a(){}
var a = 'aaaaa';
function a(){

}
//为什么会这样？这就是js的变量提升机制,上面的代码其实就被转化为了如下代码

var a; //此时变量a的值是undefined
function a (){

}
console.log(a);
a = 'aaaaa'

```

- == 与 === 的区别是什么?

> 其实就是等于和全等的概念 0可以等于（==）false，就是这样，但是呢，当你变为三个等号的时候就不一样了，==只比较值，===不管比较值，还比较类型

- null 与 undefined 的区别

> JavaScript 中，null 是一个可以被分配的值，设置为 null 的变量意味着其无值。而 undefined 则代表着某个变量虽然声明了但是尚未进行过任何赋值。

- javascript原型和原型链

```
//每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。
function person(){
    this.name = '张三';
    this.age = '20';
    person.prototype.color = 'red';
}
var obj = new person();
console.log(obj.name);
console.log(obj.color) //对象的属性上并没有color属性，所以此时它就会向prototype上去查找

//这就是原型链，这是笔者用最简单的形式，告诉大家。如果想要了解更深的知识点，请自行google js原型链接方面的资料
```

- JavaScript 有几种类型的值?

1. 栈：原始数据类型（Undefined，Null，Boolean，Number，String）
2. 堆：引用数据类型（对象、数组、函数）
3. 两种类型的区别：(存储的位置不同)
> 原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
  引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。
  
- new 操作符具体干了什么呢？
```
(1)创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
(2)属性和方法被加入到 this 引用的对象中。
(3)新创建的对象由 this 所引用，并且最后隐式的返回 this 。
var obj = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```    

- 同步和异步的区别？

> 同步的概念应该是来自于操作系统中关于同步的概念:不同进程为协同完成某项工作而在先后次序上调整(通过阻塞,唤醒等方式)。
  同步强调的是顺序性，谁先谁后；异步则不存在这种顺序性。
  
1. 同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作。
2. 异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。  

- document.write 和 innerHTML 有何区别？

> document.write 只能重绘整个页面innerHTML 可以重绘页面的一部分

- 如何判断当前脚本运行在浏览器还是 node 环境中？（阿里）

> 通过判断 Global 对象是否为 window ，如果不为 window ，当前脚本没有运行在浏览器中

- 怎样用js实现千位分隔符？
```
正则 + replace
function commafy(num) { 
   num = num + ''; 
   var reg = /(-?d+)(d{3})/; 
   if (reg.test(num)) { 
       num = num.replace(reg, '$1,$2');
   } 
  return num;
}
```

- HTTP协议的状态消息都有哪些?(如200、302对应的描述)国内外的JS牛人都知道哪些?(此处不一定全部要记住，主要是给大家总结一下)

```
协议是指计算机通信网络中两台计算机之间进行通信所必须共同遵守的规定或规则，超文本传输协议(HTTP)是一种通信协议，它允许将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器，
• “100″ : Continue（继续） 初始的请求已经接受，客户应当继续发送请求的其余部分。（HTTP 1.1新）
•  “101″ : Switching Protocols（切换协议） 请求者已要求服务器切换协议，服务器已确认并准备进行切换。（HTTP 1.1新）
•  “200″ : OK（成功） 一切正常，对GET和POST请求的应答文档跟在后面。
•  “201″ : Created（已创建）服务器已经创建了文档，Location头给出了它的URL。
•  “202″ : Accepted（已接受）服务器已接受了请求，但尚未对其进行处理。
•  “203″ : Non-Authoritative Information（非授权信息） 文档已经正常地返回，但一些应答头可能不正确，可能来自另一来源 。（HTTP 1.1新）。
•  “204″ : No Content（无内容）未返回任何内容，浏览器应该继续显示原来的文档。
•  “205″ : Reset Content（重置内容）没有新的内容，但浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容（HTTP 1.1新）。
•  “206″ : Partial Content（部分内容）服务器成功处理了部分 GET 请求。（HTTP 1.1新）
•  “300″ : Multiple Choices（多种选择）客户请求的文档可以在多个位置找到，这些位置已经在返回的文档内列出。如果服务器要提出优先选择，则应该在Location应答头指明。
•  “301″ : Moved Permanently（永久移动）请求的网页已被永久移动到新位置。服务器返回此响应（作为对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。
•  “302″ : Found（临时移动）类似于301，但新的URL应该被视为临时性的替代，而不是永久性的。注意，在HTTP1.0中对应的状态信息是“Moved Temporatily”，出现该状态代码时，浏览器能够自动访问新的URL，因此它是一个很有用的状态代码。注意这个状态代码有时候可以和301替换使用。例如，如果浏览器错误地请求http://host/~user（缺少了后面的斜杠），有的服务器返回301，有的则返回302。严格地说，我们只能假定只有当原来的请求是GET时浏览器才会自动重定向。请参见307。
•  “303″ : See Other（查看其他位置）类似于301/302，不同之处在于，如果原来的请求是POST，Location头指定的重定向目标文档应该通过GET提取（HTTP 1.1新）。
•  “304″ : Not Modified（未修改）自从上次请求后，请求的网页未被修改过。原来缓冲的文档还可以继续使用，不会返回网页内容。
•  “305″ : Use Proxy（使用代理）只能使用代理访问请求的网页。如果服务器返回此响应，那么，服务器还会指明请求者应当使用的代理。（HTTP 1.1新）
•  “307″ : Temporary Redirect（临时重定向）和 302（Found）相同。许多浏览器会错误地响应302应答进行重定向，即使原来的请求是POST，即使它实际上只能在POST请求的应答是303时才能重定向。由于这个原因，HTTP 1.1新增了307，以便更加清除地区分几个状态代码：当出现303应答时，浏览器可以跟随重定向的GET和POST请求；如果是307应答，则浏览器只能跟随对GET请求的重定向。（HTTP 1.1新）
•  “400″ : Bad Request（错误请求）请求出现语法错误。
•  “401″ : Unauthorized（未授权）客户试图未经授权访问受密码保护的页面。应答中会包含一个WWW-Authenticate头，浏览器据此显示用户名字/密码对话框，然后在填写合适的Authorization头后再次发出请求。
•  “403″ : Forbidden（已禁止） 资源不可用。服务器理解客户的请求，但拒绝处理它。通常由于服务器上文件或目录的权限设置导致。
•  “404″ : Not Found（未找到）无法找到指定位置的资源。
•  “405″ : Method Not Allowed（方法禁用）请求方法（GET、POST、HEAD、DELETE、PUT、TRACE等）禁用。（HTTP 1.1新）
•  “406″ : Not Acceptable（不接受）指定的资源已经找到，但它的MIME类型和客户在Accpet头中所指定的不兼容（HTTP 1.1新）。
•  “407″ : Proxy Authentication Required（需要代理授权）类似于401，表示客户必须先经过代理服务器的授权。（HTTP 1.1新）
•  “408″ : Request Time-out（请求超时）服务器等候请求时超时。（HTTP 1.1新）
•  “409″ : Conflict（冲突）通常和PUT请求有关。由于请求和资源的当前状态相冲突，因此请求不能成功。（HTTP 1.1新）
•  “410″ : Gone（已删除）如果请求的资源已被永久删除，那么，服务器会返回此响应。该代码与 404（未找到）代码类似，但在资源以前有但现在已经不复存在的情况下，有时会替代 404 代码出现。如果资源已被永久删除，那么，您应当使用 301 代码指定该资源的新位置。（HTTP 1.1新）
•  “411″ : Length Required（需要有效长度）不会接受包含无效内容长度标头字段的请求。（HTTP 1.1新）
•  “412″ : Precondition Failed（未满足前提条件）服务器未满足请求者在请求中设置的其中一个前提条件。（HTTP 1.1新）
•  “413″ : Request Entity Too Large（请求实体过大）请求实体过大，已超出服务器的处理能力。如果服务器认为自己能够稍后再处理该请求，则应该提供一个Retry-After头。（HTTP 1.1新）
•  “414″ : Request-URI Too Large（请求的 URI 过长）请求的 URI（通常为网址）过长，服务器无法进行处理。
•  “415″ : Unsupported Media Type（不支持的媒体类型）请求的格式不受请求页面的支持。
•  “416″ : Requested range not satisfiable（请求范围不符合要求）服务器不能满足客户在请求中指定的Range头。（HTTP 1.1新）
•  “417″ : Expectation Failed（未满足期望值）服务器未满足”期望”请求标头字段的要求。
•  “500″ : Internal Server Error（服务器内部错误）服务器遇到错误，无法完成请求。
•  “501″ : Not Implemented（尚未实施） 服务器不具备完成请求的功能。例如，当服务器无法识别请求方法时，服务器可能会返回此代码。
•  “502″ : Bad Gateway（错误网关）服务器作为网关或者代理时，为了完成请求访问下一个服务器，但该服务器返回了非法的应答。
•  “503″ : Service Unavailable（服务不可用）服务器由于维护或者负载过重未能应答。通常，这只是一种暂时的状态。
•  “504″ : Gateway Time-out（网关超时） 由作为代理或网关的服务器使用，表示不能及时地从远程服务器获得应答。（HTTP 1.1新）
•  “505″ : HTTP Version not supported（HTTP 版本不受支持）不支持请求中所使用的 HTTP 协议版本。
国内的比较牛的人：淘宝网UED官方博客。灵玉，大成小胖，承玉，拔赤
```
                