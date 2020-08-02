---
title: vue第四天
date: 2018-07-05 22:30:07
tags: vue
---
#### 复习
* 基本使用步骤
    - 1：引入对象
    - 2: 安装插件（挂载属性、注册全局组件）
    - 3: 创建路由对象配置路由规则
    - 4: 把路由对象交给vue的实例
    - 5: 留坑`<router-view></router-view>`
* a 标签来传递参数
    - 组件router-link 
    - to 让我们不必关心锚点值标记,给一个url
* 命名路由
    - 查询字符串
        + 1: 去哪里
            * `<router-link :to="{ name:'bj',query:{id:'1'} }" `
        + 2: 导航
            * ` { name:'bj',path:'/beijing',component:Beijing  } `
        + 3: 去了干嘛
            * 获取路由参数 `this.$route.query.id`
            * 生成a标签的href="#/beijing"
    - path的方式
        + 1: 去哪里
            * `<router-link :to="{ name:'bj',params:{mid:'1'} }" `
        + 2: 导航
            * ` { name:'bj',path:'/beijing/:mid',component:Beijing  } `
        + 3: 去了干嘛
            * 获取路由参数 `this.$route.params.mid`
            * 生成a标签的href="#/beijing/1"


* 对于参数传递是否带引号的问题
    - 常量字符串 加上单引号
    - 数字、变量不加单引号


* 多视图
    - 一次填入多个坑，灵活，并且将控制从业务逻辑代码，转移到了配置区
    - 1: 路由匹配有一个属性 components:{ 坑名:组件  }
    - 2: 当前匹配锚点值后，先有的组件 App主体部分，存在这些坑
    - 总结: router-view的数量要和组件所对应
    - 当锚点值一匹配，触发三个组件，填入三个坑
    - 坑名 `<router-view name="xxx"></router-view>`

* 嵌套路由
    - 嵌套路由可以用来完成多页应用
    - 父路由 
        + path匹配 组件显示（包含视图）
    - 子路由 1对1  path匹配，显示组件
    - Home组件中 <router-view>  用来显示子路由的视图
    - { path:'/home',component:Home ,children:[{ path:'music',conponent:Music }]    }
    - 名称个不相关,建议子路由 叫父路由.xxx

* 404 和重定向
* 重定向写在上面 404 写在最后
    - `{  path:'/',redirect:{name:'home'}   }`
    - `{  path:'*', component:NotFound }`
* 编程导航
    - 锚点值改变页面改变
        + `this.$router.push( { name:'list' }  );`
    - 根据浏览器历史记录前进和后退
        + `this.$router.go(-1||1)`


#### 今日重点

#### 历史介绍
* 2009年初，commonjs规范还未出来，此时前端开发人员编写的代码都是非模块化的，
    - 那个时候开发人员经常需要十分留意文件加载顺序所带来的依赖问题
* 与此同时 nodejs开启了js全栈大门，而requirejs在国外也带动着前端逐步实现模块化
    - 同时国内seajs也进行了大力推广
    - AMD 规范 ，具体实现是requirejs define('模块id',[模块依赖1,模块依赖2],function(){  return ;}) , ajax请求文件并加载
    - Commonjs || CMD 规范 seajs 淘宝玉伯
        + commonjs和cmd非常相似的
            * cmd  require/module.exports
        + commonjs是js在后端语言的规范: 模块、文件操作、操作系统底层
        + CMD 仅仅是模块定义
    - UMD 通用模块定义，一种既能兼容amd也能兼容commonjs 也能兼容浏览器环境运行的万能代码
* npm/bower集中包管理的方式备受青睐，12年browserify/webpack诞生
    - npm 是可以下载前后端的js代码475000个包
    - bower 只能下载前端的js代码,bower 在下载bootstrap的时候会自动的下载jquery
    - browserify 解决让require可以运行在浏览器，分析require的关系，组装代码
    - webpack 打包工具，占市场主流

```javascript
(function (root, factory) {  
    if (typeof exports === 'object') { 
        module.exports = factory();  //commonjs环境下能拿到返回值
    } else if (typeof define === 'function' ) {  
        define(factory);   //define(function(){return 'a'})  AMD
    } else {  
        window.eventUtil = factory();  
    }  
})(this, function() {  
    // module  
    return {  
        //具体模块代码
        addEvent: function(el, type, handle) {  
            //...  
        },  
        removeEvent: function(el, type, handle) {  
              
        },  
    };  
});  
```
#### webpack打包模块的源码
* 1:把所有模块的代码放入到函数中，用一个数组保存起来
* 2:根据require时传入的数组索引，能知道需要哪一段代码
* 3:从数组中，根据索引取出包含我们代码的函数
* 4:执行该函数，传入一个对象 module.exports
* 5:我们的代码，按照约定，正好是用module.exports = 'xxxx' 进行赋值
* 6:调用函数结束后，module.exports从原来的空对象，就有值了
* 7:最终return module.exports; 作为require函数的返回值

#### webpack配置文件
* 在当前命令行的目录中，创建一个webpack.config.js文件
* 由于webpack是基于node,配置文件中的写法参照commonjs的模块导出


#### webpack.config.js文件配置（认识）
* entry 是一个对象，程序的入口
    - key:随意写
    - value: 入口文件
* output 是一个对象,产出的资源
    - key: filename
    - value : 生成的build.js
* module 模块（对象）
    - loaders:[]
        + 存在一些loader   `{ test:正则,loader:'style-loader!css-loader'    }`


#### npm2.5以前
* 各个包内包含node_modules,会导致目录层级很深，有些包下载的时候就会报错
* npm2.5以后，安装的依赖包，就全部都是在平级根目录

#### 处理css
* require('./xxx.css');

#### 处理less
* `loader:'style-loader!css-loader!less-loader'`

#### 处理ES6
* babel是一个语法转换器,可以单独使用，也可以给打包工具结合起来使用
* webpack  -> babel-loader
* browserify -> babelify
* 可以转换es6/es7/react -> es5
* 设置当前语法: preset(预设)  es2015
* 下载预设
    - babel-loader + babel-preset-env(es2015/2016/2017)
* babel默认只转换语法部分 关键字 
* 函数部分需要插件支持

#### 处理文件 + base64
* url-loader 可以将文件生成为base64编码，到build.js中
* 文件在base64加密后会比原来大三分之一
* 应用场景是比较小的图片 4kb以内的图片

#### 特殊符号
* ! 分隔多个loader
* 字符串后跟上? 参数   key=value&key=value
* 对象: options:{ key:value,key:value  }

#### 字符串内使用的内置变量
* name: `[name].[ext]`
* name是获取原文件名,ext是获取原文件名的后缀
* output:{   path:'绝对路径', //设置产出的资源目录 ,filename:'build.js'}

#### 处理html
* html-webpack-plugin
* 1:下载
* 2:在webpack.config.js文件中引入
* 3:plugins属性中，配置该对象
* 4:给其options设置template（参照物）

#### 单文件方式
* 依赖 vue-loader
* vue-template-compiler


#### webpack-dev-server


#### mint-ui
* 移动端组件库
* https://mint-ui.github.io/docs/#/zh-cn2
* DEMO: mint-ui-master\example\pages

#### vue-rerource(了解)

#### axios
* https://segmentfault.com/a/1190000008470355?utm_source=tuicool&utm_medium=referral

#### options
#### 拦截器

#### 拦截器应用场景

#### 合并请求



