> 此文章适合vue小白，对于有一定vue开发经验的人来说，帮助不太大。主要会汇总一些新手们经常碰到的问题，分享给大家。(这里，代码均采用ES6语法，如果你还不会ES6的话请参考[阮大神的ES6教程](http://es6.ruanyifeng.com/))

- Node环境相关错误
    
    1.npm 包安装超时（install timeout）
    
    **一般情况下都是npm 被墙掉的原因（大天朝这局域网，大家懂的）,在这种情况下，大家可以使用ss进行翻墙（ss如何使用在此就不多叙述了，大家自行谷歌）。还有是就是使用淘宝的cnpm，cnpm就是npm的镜像。但是cnpm个人感觉并不是很好，所以建议大家还是使用npm，但是npm上的包并不是所有的包都被墙掉了，根据笔者的使用经验，在不翻墙的情况下大部分包还是可以使用的，就是稍微慢一点。但是有些包，例如：node-sass包就会被墙，得需要翻了墙才能使用。做技术的人嘛，怎么能不会科学上网呢？**
    
    2.安装一些需要编译的包:提示没有安装python、build失败等
    
    **因为有些npm包的安装需要编译的环境，这样的环境在mac,linux一般都还好，但是在window平台下却表现的不是很好,建议window的小伙伴都装上[windows-build-tools](https://github.com/felixrieseberg/windows-build-tools)和[python 2.x](https://www.python.org/downloads/)**
    
    3.找不到某些依赖或者模块（can't not find 'xxModule'）
    
    **这种情况一般报错信息可以看到是哪个包抛出的信息.一般卸载这个模块,安装重新安装下即可.**
    
- vue使用相关错误
    
    1.data functions should return an object
    > 这句话是说，vue的实例内组件的data必须返回一个对象
    ```
    export default {
        name:'demo',
        data(){
            return {
                status:false,
                title:'张三'
            }
        }
    }
    ```
    [请参考官网，data-必须是函数](https://cn.vuejs.org/v2/guide/components.html#data-必须是函数)
    
    2.给组件添加内的原生空间控件添加事件失效
    
    ```
    //例如使用了第三方框架封装好的组件，然后绑定事件失效
    <el-input placeholder="请输入" @mouseover="test()"></el-input>
    /*
    *这样使用肯定是失效的，是没有办法触发到事件的
    */
    ```
    > 其实要解决其实很简单，添加一个native就好了[官网文档解释](https://cn.vuejs.org/v2/guide/components.html#给组件绑定原生事件)
    
    3.使用了axios，却在ie下无法正常运行(ie9+)
    
    > 因为ie系列都不支持promise的回调,解决办法如下
    ```
    npm install es6-promise
    // 在 main.js 引入即可
    // ES6的polyfill
    require("es6-promise").polyfill();
    ```
    
    4.报错,this.xxx,Cannot set property 'xxx' of undefined;等和this相关的
    
    > 说来说去都是一个经常谈论的问题，this的是指向，建议大家去看看es6的箭头函数是怎么回事。要不就使用let _this = this;这样的形式将this保存起来，虽然箭头函数转化为es5的语法之后也是这样的形式，但在开发阶段街头函数还是快捷了不少，而且更加清楚明了.
    
    5.为什么引用小图片最终出来的却是data:image/png;base64xxxxxxxx这样的形式
    
    > 首先你要知道这是图片被打成了base64的编码形式，图片可以照常显示，而且不需用请求。在vue-cli中webpack.base.conf.js文件里可以设置。
    
    6.Component template shold contain exactly one root element.If you are useing v-if on multiple elements , xxxxx 
    
    > 大体就是说,单组件渲染 DOM 区域必须要有一个根元素,不能出现同级元素.可以用v-if和v-else-if指令来控制其他元素达到并存的状态换个直白的解释,就是有一个唯一的父类,包裹者;比如一个 div(父包含块) 内部多少个同级或者嵌套都行,但是最外层元素不能出现同级元素!!!!
    ```
    <template>
    <div>
        <!-- 一定在外部要有一个容器 -->
    </div>
    </template>
    ```
    
    7.No 'Access-Control-Allow-Origin' header is present on the requested resource.
    
    > 首选，这是跨域的错误。虽说解决跨域的办法很多，但是却没有最好的，只有最合适的，大家应该根据当前的业务场景，选择最经济实惠的解决方案。我在此就简单给大家分享几中办法吧
    
    ```
    /*
    * 1.vue-cli本身自带了一个反向代理的工具，大家只需要配置一下地址即可
    * 2.服务端ng反向代理
    * 3.还有就是万古长青的jsonp（切记,jsonp并不能使用post请求）
    * 当然方法肯定不止这些，就不给大家一个个写了，后面会单独给大家分享一章来说说跨域
    */
    ```
    
    8.在spa应用中，为何相同的class样式不能复用以及覆盖
    
    > 首先需要看看你是否开启了路由懒加载，如果开启了懒加载的话，只有当进入这个组件的时候css样式才会动态通过style的形式添加到head里，其次就是要看看是否开启了css模块化功能。
    ```
    <template>
        <p class="title">模块化</p>
    </template>
    <script>
        export default {
            name:'demo',
            data(){
                return {
                    
                }
            }
        }
    </script>
    <style scoped>
    
    </style>
    /*
    * 就是这个scoped，如果在style上添加了scoped的话
    * 那么最终生成的样式就类似于这样.title[data-v-1ec35ffc]{}
    * 有添加了一段hash所以会导致相同的class并不会匹配样式
    * 笔者建议大家scoped不要经常使用，因为这样生成的选择器会携带上属性选择器
    * 而属性选择器的性能并不是很好，而且在最终打包的时候也会增加文件体积。
    * 所以笔者建议大家在通用型组件，插件样式的时候使用，页面的样式最好不要使用scoped
    */
    ```
    
    9.路由模式改为history后,除了首次启动首页没报错,刷新访问路由都报错
   
    > 为什么会这样呢？是因为使用history模式之后最终生成的链接类似于这样www.baidu.com/home/page,并没有携带#号，所以会跳转页面，但是服务器上却没有这样的页面，在这样的情况下需要后端配合拦截一下
    [官方说明](https://router.vuejs.org/zh-cn/essentials/history-mode.html)
    
    10.拦截页面，或者在页面进来之前想做一些操作，比如权限验证应该怎么做？
    
    > 在使用vue-router的时候,官方是有配置路由守卫的，就是可以在路由的不同状态执行某某方法[官方说明](https://router.vuejs.org/zh-cn/advanced/navigation-guards.html)
    
    11.Error in render function:"Type Error: Cannot read property 'xxx' of undefined"类似于这样的错误
    
    > 碰到这样的问题，大多都是对生命周期不了解，使用的姿势错误。这种情况也存在于props传递数据的时候。去将vue的生命周期好好看看
    [官方说明](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)，要清楚created,mounted等周期分分别能访问什么数据.
    
    12.npm run build之后不能直接访问
    
    > 打包之后的静态资源是不能直接访问，需要跑在服务器上才行.
    
    13.CSS background引入图片打包后,访问路径错误
    
    > 可能是路径出错，需要查看一下配置文件中static
    
    14.安装模块时命令窗口输出unsupported platform xxx
    
    > 一般两种情况,node版本不兼容,系统不兼容;解决方案: 要么不装,要么满足安装要求;
    
    15.Unexpected tab charater等类似错误
    
    > 检查一下eslint,一般情况笔者不建议新手一上来就是用eslint,解决办法也很简单，要不修改eslint的检验规则，要不就遵守eslint的规则。eslint是什么我就不解释了，代码遵守一些规则还是可以降低后期项目维护的成本的。
    
    16.Failed to mount component: template or render function not defined
    
    > 组件挂载失败，检查是否正确引入，顺序是否出错等。
    
    17.Unknown custom element: <xxx> - did you register the component correctly?
    
    > 组件是否正确引入，引入之后是否正确注册？
    
    18.axios的 post 请求后台接受不到
    
    > 引入qs模块（无需安装，直接require即可）
    ```
    import qs from 'qs' //导入
    data:qs.stringify(data) //传递数据的时候用qs.stringify()方法格式化一下即可
    ```
    19.Invalid prop: type check failed for prop "xxx". Expected Boolean, got String.
    
    > 这种问题一般就是组件内的 props 类型已经设置了接受的范围类型,而你传递的值却又不是它需要的类型。注意js的隐式类型转换
    
    20.组件的通讯有哪几种?
    
    - 父传子: props
    - 子传父: emit
    - event bus: 就是找一个中间组件来作为信息传递中介
    - vuex:中央管理仓库
    
    21.vuex的用户信息为什么还要存一遍在浏览器里
    
    > 因为vuex里面存储的值，在页面一刷新之后就会消失，回归到初始化状态
    
    22.npm run dev 报端口错误!Error: listen EADDRINUSE :::8080
    
    > 找到config/index.js文件，配置一下port: 8080,即可。
    
    23.v-if  v-show有什么不同，分别应该在什么情况下使用
    
    > 好好去看看官方的说明吧，很详细. [官方地址](https://cn.vuejs.org/v2/guide/conditional.html#v-if-vs-v-show)
    
    24.单组件中里面的 import xxx from '@/components/layout/xxx'中的@是什么?
    
    > 打开webpack的配置文件，可以看到，其实就是这个@相当于一个别名，然后从这个别名下去找到对应的文件
    
    25.为什么我的 npm 或者 yarn 安装依赖会生成 lock文件,有什么用?
    
    > lock 文件的作用是统一版本号,这对团队协作有很大的作用;
      若是没有 lock 锁定,根据package.json里面的^,~这些..
      不同人,不同时间安装出来的版本号不一定一致;
      有些包甚至有一些breaking change(破坏性的更新),造成开发很难顺利进行!!!
      
    26.如何缓存组件?
   
    > 可以使用keep-alive，但不是无脑缓存所有的组件。[官方说明](https://cn.vuejs.org/v2/api/#keep-alive)
    
    27.文件打包体积过大，首屏加载太慢
    
    > 首先应该尽可能的减少第三方库的依赖，比如JQ等，而且在使用vue的时候基本可以放弃JQ了，可以使用路由懒加载。官方已经提供好了相关功能，大家前去查阅即可.
    
    28.spa应用没法seo？
    
    > 目前谷歌是可以爬取js的，但是百度就不行，这种情况下就只能使用服务端渲染。
    [参考链接](https://zh.nuxtjs.org/)
    
    29.vue可以写 hybird App 吗!
    
    - [codorva](https://cordova.apache.org/) + [nativescript](https://github.com/rigor789/nativescript-vue)
    - [weex](https://weex.apache.org/cn/) 阿里巴巴出品，据说阿里的钉钉就是使用这个做的
    
    
        

    
    