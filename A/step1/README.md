> 市面上常见的浏览器如下

- ie系列的，最让人诟病的不外乎ie6,ie7兼容性简直让人抓狂
- Firefox，兼容性不错，就是有点卡，不过最新版的火狐升级了内核，性能提升了不少
- 神器chrome，谷歌出品，功能多性能还好，目前占有的市场份额最大
- Safari,苹果旗下
- opera
- 还有一堆国产浏览器例如360等，其实不外乎就是使用ie系列或者chrome内核，在此不多赘述。

#### 关于内核

- IE（Trident内核），IE 从版本 11 开始，初步支持 WebGL 技术。IE8 的 JavaScript 引擎是 Jscript，IE9 开始用 Chakra，这两个版本区别很大，Chakra 无论是速度和标准化方面都很出色。国内很多的双核浏览器的其中一核便是 Trident，美其名曰 “兼容模式”。Window10 发布后，IE 将其内置浏览器命名为 Edge，Edge 最显著的特点就是新内核 EdgeHTML。关于 Edge 浏览器更多可以参考 [如何评价 Microsoft Edge 浏览器？](https://www.zhihu.com/question/29985708)
- Firefox(Gecko内核)，火狐虽然好用但就是消耗的资源太多，有一个段子就是说当你要打开火狐的时候，点击之后去倒杯咖啡回来就好了。但是最新版的火狐已经重写了内核，也不再使用Gecko内核，称为Firefox Quantum(火狐量子)，火狐对外宣称它的运行速度是一些浏览器的二倍。[火狐chrome性能对比请查看](http://mp.weixin.qq.com/s/IdGNBOl7KINZ6xHwI-MTdg)
- Safari (Webkit内核)，虽然苹果是Webkit的鼻祖，但是将webkit深入人心对的却是chrome，不知道苹果有没有哭。现在Safari依然是使用webkit内核
- Chrome（Blink，Chromium内核），chromium内核源自于webkit，却在webkit的基础上将性能提高了太多，而且谷歌还开发出了自己的javascript v8 引擎，大大得分提升了js的运行速度，然后在2013年谷歌在 Chromium Blog 上发表，称将与苹果的开源浏览器核心 Webkit 分道扬镳，在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。Blink 引擎问世后，国产各种 chrome 系的浏览器也纷纷投入 Blink 的怀抱，可以在浏览器地址栏输入 chrome://version 进行查看。
- Opera（Presto内核），这是Opera公司自己研发的引擎，但是在2013年2月宣布放弃Presto转投向了Chromium。

#### 关于移动端

- 苹果产品系列，webkit内核
- 安卓系列，在安卓4.4版本之前系统浏览器的内核都是webkit，而在4.4之后系统浏览器切换到了Chromium，内核是 Webkit 的分支 Blink
- window phone系列，虽然现在已经基本没人用WP的手机了，但是我曾经用过，感觉还真心不错，就应用太少了，可能这也是它死掉的原因吧。系统浏览器为Trident内核