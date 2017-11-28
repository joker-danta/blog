##### if else 简写
> 在代码中根据不同情况执行不同方法/逻辑是非常常见的需求，在js中我们大多使用if/switch语句尽进行判断(大部分情况还是使用if)，就拿if语句来说我们每次都需要写if(条件){}else{}这样的语句,不嫌麻烦吗？ok,let's go
```
//例如:
    var status = true;
    var res = 2;
    if(status) {
        res = 1
    }
    else {
        res = 0
    }
    console.log(res); // 0
    //首先使用三元运算符（有的也叫三目运算符）
    (status) ? res = 1 : res = 0;
    /**
     * 三元运算符适用于很多场景，是一个比较常用的if/else简写形式
     */
     
     
     //下面介绍js逻辑运算符号（也叫短路操作）
     
     var str1 = 0;
     var resultl1;
     str1 && ( resultl1 = 1);
     console.log('resultl1的值是',resultl1);  // undefined
     
     var str2 = 1;
     var resultl2;
     str2 && ( resultl2 = 1 );
     console.log('resultl2的值是',resultl2);  // 1
     
     var str3 = 0;
     var resultl3;
     str3 || (resultl3 = 1);
     console.log('resultl3的值是',resultl3)  //1
     
     /**
      * 其实这里的 && || 符是可以当作if来使用的
      * str1中的例子其实就是当str1为真 的时候，才会去执行后面的代码也就是括号里面的内容
      * str2中和str1是同样的道理，所以str2的console的值是1
      * str3中，只有当str3的值为假 的时候，才回去执行后面的代码段
      */
``` 
> 请大家注意，虽然介绍了这两种if的简写，但并不是代表if就没有作用了。虽然使用三元运算符和短路操作是很简单，但并不是很直观。尤其是当团队中有新手的话就可能造成一些不必要困扰，所以在此，笔者给出自己的意见，大家可以参考。

- 如果是只是单一条件的话，例如if(条件){...逻辑}的话建议使用逻辑运算，最好可以写上注释 
- 如果是if(){...逻辑}else{...逻辑}的形式的话建议是用三元运算
- 如果是多条件例如：if(){...逻辑}else if(){...逻辑}这样的条件，建议老老实实的使用if/或者switch

[MDN文档地址](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_Operators)