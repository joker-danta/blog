###### 这一节给大家整理一些关于js对象/数组遍历的方法

- indexOf方法
```
let numArr1 = [10, 1, 8, 21, 16, 25, 9, 5, 29, 3];
/**
 * indexOf
 * indexOf()方法返回在该数组中第一个找到的元素位置，如果它不存在则返回-1。
 */
console.log('这是indexOf的结果' + numArr1.indexOf(8)) //2
console.log('这是indexOf的结果' + numArr1.indexOf(100)) // -1
```

- lastindexOf方法
```
/**
* lastindexOf
* lastIndexOf() 方法返回在该数组中最后一个找到的元素位置，和 indexof相反。
*/
let numArr2 = [10, 1, 8, 21, 16, 1, 25, 9, 5, 29, 3];
console.log('这是lastIndexOf的结果' + numArr2.lastIndexOf(1)) //5
```

- every方法
```
/**
* every
* every()可是检测数组中的每一项是否符合条件，注意是每一项，如果有一项不符合条件即为false
* 返回 true 或者 false
*/
let numArr3 = [10, 1, 8, 21, 16, 1, 25, 9, 5, 29, 3];
let result3 = numArr3.every(function(item, index) {
    return item >= 1
});
console.log('这是every的结果' + result3)
```

- some方法
```
/**
* some
* some()可以检测数组中是否有某一项符合条件
* 返回 true 或者false
* some和every相反，一个是只有一个满足条件即可，一个是所有的都要满足条件
*/
let numArr4 = [10, 1, 8, 21, 16, 1, 25, 9, 5, 29, 3];
let result4 = numArr4.some(function(item, index) {
    return item >= 10
});
console.log('这是some的结果' + result4)
```

- forEach
```
/**
* forEach()
* forEach为每个元素执行对应的方法
*
*/
let numArr5 = [10, 1, 8];
numArr5.forEach(function(item, index, array) {
    console.log('这是forEach的结果' + item);
});
```

- map
```
/**
 * map()
 * map()对数组的每个元素进行一定操作（映射）后，会返回一个新的数组
 * map()是处理服务器返回数据时是一个非常实用的函数
 */
let numArr6 = [{
    first_name: "Colin",
    last_name: "Toh"
}, {
    first_name: "Addy",
    last_name: "Osmani"
}, {
    first_name: "Yehuda",
    last_name: "Katz"
}];
numArr6.map(function(item, index) {
    console.log('这是map的结果' + [item.first_name, item.last_name].join(" "))
})
console.log('aaaa', numArr6)
/**
* forEach 与map的区别：
*
* 语法：forEach和map都支持2个参数：一个是回调函数（item,index,list）和上下文
* forEach：用来遍历数组中的每一项；这个方法执行是没有返回值的，对原来数组也没有影响；数组中有几项，那么传递进去的匿名回调函数就需要执行几次；每一次执行匿名函数的时候**还给其传递了三个参数值：数组中的当前项item,当前项的索引index,原始数组list；理论上这个方法是没有返回值的，仅仅是遍历数组中的每一项，不对原来数组进行修改；但是我们可以自己通过数组的索引来修改原来的数组
*
* forEach方法中的this是ary,匿名回调函数中的this默认是window
*
* map： 和forEach非常相似，都是用来遍历数组中的每一项值的，用来遍历数组中的每一项
* 区别：map的回调函数中支持return返回值；return的是啥，相当于把数组中的这一项变为啥（并不影响原来的数组，只是相当于把原数组克隆一份，把克隆的这一份的数组中的对应项改变了）
* 不管是forEach还是map 都支持第二个参数值，第二个参数的意思是把匿名回调函数中的this进行修改
*/
```

- for循环

```
var numArr7 = [1,2,3,4];
for(let i = 0;i<numArr7.length;i++) {
    console.log('for 循环',numArr7[i])
}
/**
 * for循环，太常见用，就不赘述了。
 */
```

- for in 循环

```
var numArr8 = {
    name:'zhangsan',
    age:18
};
for (let obj1 in numArr8) {
    console.log('for in 循环',obj1)
}
/**
 * for in 循环，也是经常遍历对象额方法，也就不多赘述了
 */
```

- for of 循环

```
var  numArr9 = [1,2,3,4];
for(let y of numArr9) {
    console.log('for of 循环',y)
}
/**
 * for of 循环是es6中新增的一种循环，用法于for for in 循环基本类似
 * 推荐在循环对象属性的时候，使用for...in,在遍历数组的时候的时候使用for...of
 * for...in循环出的是key，for...of循环出的是value
 * 注意，for...of是ES6新引入的特性。修复了ES5引入的for...in的不足
 * for...of不能循环普通的对象，需要通过和Object.keys()搭配使用
 */
```

- filter遍历

```
//filter()方法创建一个新的匹配过滤条件的数组。（ES6新增）
var numArr10 = [1,2,3,4,5,6];
var newnumArr10 =  numArr10.filter((item) => {
    return item > 3
});
console.log('filter',newnumArr10);
/**
 * filter是一个很好用的方法
 * 主要就是应用在从一个数组或者对象中返回出满足条件的项
 */
```


