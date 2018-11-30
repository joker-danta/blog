### call,apply,bind的使用

> call()、apply()、bind()都是函数对象的一个方法，它们的作用都是改变函数的调用对象。它的使用极大的简化了代码的调用

#### call方法

> 语法：call([thisObj[,arg1[, arg2[, [,.argN]]]]])
定义：调用一个对象的一个方法，以另一个对象替换当前对象。
说明： call 方法可以用来代替另一个对象调用一个方法。
call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。

thisObj的取值有以下4种情况：
1. 不传，或者传null,undefined， 函数中的this指向window对象
2. 传递另一个函数的函数名，函数中的this指向这个函数的引用
3. 传递字符串、数值或布尔类型等基础类型，函数中的this指向其对应的包装对象，如 String、Number、Boolean
4. 传递一个对象，函数中的this指向这个对象

#### apply方法

> 语法：apply([thisObj,[argArray]]) 定义：应用某一对象的一个方法，用另一个对象替换当前对象。 说明：apply的第一个参数thisObj和call方法的一样，第二个参数argArray为一个传参数组。thisObj如果未传，那么 Global 对象被用作 thisObj。

> call 和 apply的区别,对于 apply、call 二者而言，作用完全一样，只是接受参数的方式不太一样。

```
function class1(args1,args2){
  this.name=function(){
   console.log(args,args);
  }
}
function class2(){
  var args1="1";
  var args2="2";
  class1.call(this,args1,args2);  
  /*或*/
  class1.apply(this,[args1,args2]);
}
var c=new class2();
c.name();

输出：1 2

/*
在JavaScript 中，某个函数的参数数量是不固定的，因此要说适用条件的话，当你的参数是明确知道数量时用 call ；而不确定的时候用 apply，然后把参数 push 进数组传递进去。当参数数量不确定时，函数内部也可以通过 arguments 这个类数组对象来遍历所有的参数。
*/
```
> apply call 方法的应用场景
[链接](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
```
// 可以合并两个数组(注意当第二个数组(如示例中的moreVegs)太大时不要使用这个方法来合并数组，因为事实上一个函数能够接受的参数个数是有限制的)
var vegetables = ['parsnip', 'potato'];
var moreVegs = ['celery', 'beetroot'];

// 将第二个数组融合进第一个数组
// 相当于 vegetables.push('celery', 'beetroot');
Array.prototype.push.apply(vegetables, moreVegs);

console.log(vegetables); 
// ['parsnip', 'potato', 'celery', 'beetroot']


// 实现继承
function Animal(name) {
  this.name = name;
  this.showName = function () {
    console.log(this.name);
  }
  }
function Cat(name) {
  Animal.call(this, name); 
  }
var cat = new Cat('Black Cat');
cat.showName(); // Black Cat

// 获取数组中的最大值和最小值
var num = [1,3,5,7,2,-10,11];
var maxNum = Math.max.apply(Math, num);
var minNum = Math.min.apply(Math, num);
console.log(maxNum); // 11
console.log(minNum); // -10


//将伪数组转化为数组
var fakeArr = {0:'a',1:'b',length:2};
var arr1 = Array.prototype.slice.call(fakeArr);
console.log(arr1[0]); 
var arr2 = [].slice.call(fakeArr);
console.log(arr2[0]); 
arr1.push("c");
console.log(arr1)

```

#### bind方法

> 在ECMAScript5中扩展了叫bind的方法（IE6,7,8不支持） 语法：bind([thisObj[,arg1[, arg2[, [,.argN]]]]]) 定义：应用某一对象的一个方法，用另一个对象替换当前对象。 说明：bind的thisObj参数也和call方法一样，thisObj如果未传，那么 Global 对象被用作 thisObj。arg1 … argN可传可不传。如果不传，可以在调用的时候再传。如果传了，调用的时候则可以不传，调用的时候如果你还是传了，则不生效。例如：

```
var person = {
    name:"tsrot",
    age:24,
    sayHello:function(age){
        console.log(this.name);
        console.log(age);
    }
    };
var son = {
 name:"xieliqun"
 };
var boundFunc = person.sayHello.bind(son);
boundFunc(25);

var boundFunc = person.sayHello.bind(son,25);
boundFunc();

var boundFunc = person.sayHello.bind(son,25);
boundFunc(30);
```