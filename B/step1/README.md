# css编码规范
1. 文件命名建议小写字母加中横线的方式,例如:
> https://stackoverflow.com/questions/25704650/disable-blue-highlight-when-touch-press-object-with-cursorpointer
2. 引入CSS文件的link可以不用带type="text/css"，如下代码：
```
<link rel="stylesheet" href="test.css">
//因为link里面最重要的是rel这个属性，可以不要type，但是不能没有rel。
//JS也是同样道理，可以不用type，如下代码：
<script src="test.js"></script>
//同样没有兼容问题,但是对于css依然建议大家协商type，这样会更加严谨。
```
3. 建议属性书写顺序
> 属性的书写顺序对于浏览器来说没有区别，除了优先级覆盖之外。但是如果顺序保持一致的话，扫一眼可以很快地知道这个选择器有什么类型的属性影响了它，所以一般要把比较重要的属性放前面。比较建议的顺序是这样的：

![image](https://user-gold-cdn.xitu.io/2017/8/24/40dd68c5f860f12f01bfc9a0670506fd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

**我平时就这样写，再次强调，写的顺序对于浏览器没有任何区别。这样写无非就是让人看着舒服，让别人可以一眼看出你想要干什么。**

4. 不建议使用样式的特点命名，例如：
```
// css类名不建议使用驼峰形式，因为css不区分大小写，所以建议大家使用中划线，这一点大家看bootstrap的类名就知道了
.blue-font{
    color:blue
}
.p1{
    font-size:18px;
}
.p2{
    font-size:14px;
} 
// class的命名应当可以表示它当前的逻辑意义，例如：
.company-logo{
    width:100px;
    height:100px;
}
left-bar{
    
}
```
[相关资源推荐](http://codeguide.bootcss.com/)

5. 滥用子选择器

> 这种情况在写css的时候还相对来说比较少见，尤其当大家在写less或者scss的时候最容易发生,嵌套了过多层级的子选择器,例如：
```
//以下代码使用sass语法
.nav{
    .content-left{
        h1{
            span{
            
            }
        }
    }
}
//这样，这段sass代码编译之后就是如下代码
.nav .content-left .h1 span{

}
```
**大家很清楚的看见了，这段代码嵌套了四层，当让嵌套的越多性能肯定越低，但是有不能所有的都写成全局的，那么这个度应该如何来控制呢？通常来说一般都不要超过4层，大家可以去参看以一下bootstrap是样式，它们都没有超过四层嵌套的。如果你是直接写css的话，通常来说这种情况会比较容易的避免。写less,sass的同学一定要注意了,因为在less或者sass的语法中很容易嵌套多层，而自己却毫无感觉。我曾今见过有人能写到七八层的那种。这个问题大家一定要注意，性能是源自一点点小细节的提升和积累**

6. 禁止使用'*'通配符
> 这个就不过多叙述了，通配符可以代表全部，所以不管在哪里，都不要使用通配符，降低不必要的麻烦.

7. 谨慎覆盖元素样式

> 如果我在这里说一个中大型网站没有任何一处的的样式覆盖，大家肯定会喷我。目前市面上貌似也没有任何一个中大型网站没有存在一处掩饰覆盖的地方，但这样毕竟是一种很不优雅的方式，所以大家应该尽可能减少覆盖，例如代码：
```
.house{
    margin-top: 20px;
}
.house:first-child{
    margin-top: 0;
}
//修改为如下代码
.house + .house{
    margin-top: 20px;
}
```

8. css3有很多的高级选择器，用这写选择器也可以完成一些高级功能

> [w3c](http://www.w3school.com.cn/cssref/css_selectors.asp)大家可以去w3c查看这些高级选择器，自己分情况组合使用

9. 尽可能的少用!import
 >在css中用来覆盖样式，并且优先级最高，当你现在使用了import覆盖了某一个样式，后面在想覆盖这样样式的时候就很困难.
 
10. 注释的规范（css写注释是一个好习惯，因为当你过上十天半个月回来调试css的时候就会很舒服，在即将发布上线的时候压缩，去掉注释即可）
**文件顶部的注释**
```
  /*
   * @description通用基础层样式表
   * @author xx
   */
```
**块级注释**
```
/*菜单栏*/
```
**TODO的注释**
```
/* TODO(littledan): Computed properties don't work yet in nosnap.
   Rephrase when they do.
*/
//表示这些代码还有待完善，或者有些缺陷需要以后修复。而这种TODO的注释一般编辑器会把TODO高亮
```
**注释不要写一些无用的内容，例如：这边字体要大一些等**

11. 属性的书写规范
- 如果值为0，通常是不带单位的
```
.container{
    margin:0px;
}
//应该写为
.container{
    margin:0;
}
```
- 色值可以使用十六进值的时候就不要使用rgb
```
.container{
    color: rgb(80, 80, 80);
}
//可以写为
.container{
    color: #505050;
}
//如果色值的6个数组是相同的，就写3个就好了
.container{
    color:#000000;
}
//可以写为
.container{
    color:#000;
}
```
- border none和0的区别
```
.list{
    border:0px solid #000;
}
.list{
    border:none;
}
//这种情况下更建议写为border:none,可能在代码打包的时候工具会帮我们处理，但是对于自己来说，养成一个良好的习惯也未尝不是好事。
```
- 不要使用过大的z-index
```
.list{
    z-index:99999999;
}
// 通常在写自己的业务逻辑的时候，最好控制在两位数。
```
- 清除浮动
```
.clearfix:after{
    content: "";
    display: table;
    clear: both;
}
/*
*虽然清除浮动的方法有很多，但用的最多的还是clearfix大法，大家可以参考一下bootstrap是如何清除浮动的
*/
```
12. 常见样式的css reset

> 推荐可以参考一下normalize.css这个项目，看看css reset应该怎么做会比较的好 [知乎](https://www.zhihu.com/question/20094066),[下载](https://necolas.github.io/normalize.css/)

13. 关于图片压缩
> 通常来说，一般情况产品在交付设计稿的时候也会包含图标的切图，这时图标都是通过插件压缩过的。但是也不排除其他情况，下面给大家推荐一个在线图片压缩网站，很不错，还有ps的插件 [地址](https://tinypng.com/)

14. 适当使用:before/:after
> :before和:after可以用来画页面的一些视觉上的辅助性元素，如三角形、短的分隔线、短竖线等，可以减少页面上没有用的标签。但是页面上正常的文本等元素还是不要用before/after画了。

15. 不要设置input的line-height
```
.request-demo input{
    height: 40px;
    line-height: 40px;
}
```
> 设置了line-height为一个很高的值，这样会导致Safari浏览器的输入光标|变得巨大，所以如果你要居中的话，使用padding吧。

16. 行内元素可以直接设置margin-left/margin-right

```
span.phone-numer{
    display: inline-block;
    margin-left: 10px;
}
// 其实可以直接写为
span.phone-numer{
    margin-left: 10px;
}
```
> 其实行内元素可直接margin的左右，能够把它撑开，不需要设置inline-block,另外需要注意的是img/input/textarea/button默认就是inline-block，也不用再设置。





    

