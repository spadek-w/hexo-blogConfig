---
title: vue第二天
date: 2018-06-16 23:30:19
tags: vue
---
#### 复习
* vue的 启动步骤
    - 1: index.html  在之中留坑 div id="app"
        + 在vue1中可以在body，html中声明id="app"
        + 在vue2.x中不可以将原生声明为body或者html标签
    - 2: 引包，启动vue(new Vue的实例)
    - 3: 将options作为vue构造的参数
    - 4: 声明组件组件对象(options)
* options
    - el DOM的目的地
    - template: 组件模板
    - data: 组件的数据
    - methods: 是一个对象 
    - render： c=>c(App)     c是形参，代表着vue提供的根据options创建组件的DOM方式
    - components: 声明子组件
    - props:是一个数组

* data 是一个函数，return 一个对象
* methods 是一个对象，key是函数名,value是函数体
    - 内部使用data的变量，需要加上this......vue处理了this的指向
    - 在js中使用到this.xxx  在template中就可以直接使用
* components 组件内声明，是一个对象，key 是组件名，value是组件的options对象
    - 全局组件 Vue.component(组件名,组件的options)

#### 今日重点
* 路由插件


#### 问题
* 全局API，Vue.
* Vue.component/Vue.filter

#### 监视watch
* 更改内存中js变量的值，影响着别的地方，做一些行为
    - options: watch是一个对象
        + key 是要监视的变量,value 是一个function(newV,oldV){ 做一些行为}

* 在vue中也存在对于对象的深度监视
    - watch:对象,变量名,valueFn  
        + 参数是newV,oldV
    - 深度监视
        + watch:{  变量名:{deep:true,handler:valueFn}      }

#### 计算属性(options->computed)
* 需求: 做一个计算器，num1 + num2 * rate = 结果
    - input num1,num2,rate, result
        + 情况1: 通过某些按钮，而不是直接更改num1的输入框的值，来改变num1的值
* __计算属性中使用到this.的变量更改后会触发函数的执行，从而重新计算，return作为显示的值，注意:如果原值未发生改变，则不触发该函数__

#### 总结
* 计算属性和watch的区别
    - 多个监视和一个监视的区别
* 和普通输出是一样`{{计算属性名}}`
* options
    - 模板数据的目的地: el
    - 根据options-> App 渲染到目的地 : render函数
    - 数据 data,是一个函数，return一个对象
    - 组件的方法 methods ，是一个对象 ，key是函数名，value是函数体
    - 接收父组件的参数 props, 是一个数组。元素是字符串
    - 组件内声明组件 components 是一个对象 key是组件名,value就是options(组件的)
    - 过滤器 filters 是一个对象 key是过滤器名，value是过滤器方式fn
    - 监视单个 watch 是一个对象 key是监视的变量名，value方式fn
    - 计算属性 computed 是一个对象 key计算名,value是方式fn return 是返回的内容


#### 获取元素
* 在元素上声明ref="xxx"
* 获取这个DOM元素 `this.$refs.xxx`

#### 事件回调函数(钩子函数) 总结
* beforeCreated和created的注意事项  
    - beforeCreated 还未完成数据的初始化，不能操作数据
* created 和mounted的注意事项
    - created 还未生成DOM （应用场景，在真正生成DOM 前，去获取数据，等待mounted装载到DOM中）（操作数据）
    - mounted 已经根据data和template生成了DOM，可以获取或者修改DOM
* created操作和获取数据，mounted操作和获取DOM

* actived和deactivated是结合keep-alive（vue内部的组件）使用的，
    - 频繁的插入和移除组件，vue将其缓存起来，不频繁创建和移除
    - 有停用(相当于以前的destroyed)和激活(相当于created)的两种状态


#### 复习
* 钩子： 事件回调函数
* Vue中给你在执行流程(vue生命周期)开放了一些方式，来完成你的代码
* created 操作数据
* mounted 装载数据之后，操作DOM
* 关于更新前后的钩子，建议使用computed来完成
* watch 监视单个data的属性 ，遇到对象的属性或者元素需要监视，就需要深度监视
    - deep:true ,handler:fn
* computed 监视在函数内使用到的this相关的属性


#### 利用webpack 完成模块化打包
* 1:全局安装webpack `npm i -g webpack`
* 2:打开当前命令行 

#### 总结结合webpack打包
* 1:从main.js中 启动vue
* 2:通过require引入相关依赖 vue,App
* 3:编写App.js  以module.exports方式向外导出
* 4:检查App.js中有没有依赖，require, 结合module.exports
* 5:执行命令 `webpack ./main.js ./build.js`
* 6:在index.html中引入build.js

#### 基本使用
* vue中核心插件之一  vue-router
* 1:下载vue-router
* 2:引入vue-router(require)
* 3:创建路由对象 new VueRouter();
* 4:配置路由规则,在路由对象的构造中完成 routes:[ path:锚点值路径,component:显示的组件]
* 5:安装插件
* 6:将其加入到new Vue中
* 7:留坑
