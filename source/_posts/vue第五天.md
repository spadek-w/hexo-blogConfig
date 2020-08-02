---
title: vue第五天
date: 2018-07-05 23:48:16
tags: vue
---
#### 复习
* babel 是个工具
    - 语法 env
    - 函数 transform-runtime
* 单文件（ 形态1:引包var  形态2:模块  形态3:单文件方式 xxx.vue）
    - 形态1: 引包，作为库来使用
    - 形态3:单文件方式(企业开发主流方式)
* App.vue (vue-loader 默认是按ES6导出的  )
    - `<template><script><style>`
    - template写html,保证只有一个根节点
    - script 模块导出除了template之外的options
        + `require('./App.vue').default`
    - style: 默认设置是全局的css,  scoped属性会让其只对当前template有效


#### 今日重点
* 插件补充
* 项目起步

#### webpack-dev-server
* dist已经解决
* src下的资源无法运行，和测试
    - 是一个全局命令行工具 可以在命令行 通过webpack-dev-server运行
    - `webpack-dev-server --inline --open --hot --port 9999`
    - inline 自动刷新
    - open 自动打开浏览器
    - hot 热替换（在不刷新的时候，完成更新内容的显示）

#### mint-ui
* element-ui  饿了么出的ui组件库 针对PC端
* 移动端mint-ui（web应用）组件库
* https://mint-ui.github.io/docs/#/zh-cn2
* DEMO: mint-ui-master\example\pages
* 使用步骤(安装后)
    - 1:引入对象
    - 2:安装插件（注册全局组件|| 挂载属性）
    - 3:引入css
    - 4:直接使用组件



#### vue-rerource(了解)
* 作者明确表示不维护了,推荐使用axios
* vue作者团队开发的ajax请求插件
    - 基于promise
    - .then  .catch
    - 1:引入对象
    - 2:安装插件 (挂载属性)
    - 3:直接使用this.$http
* emulateJSON   boolean 将request body以application/x-www-form-urlencoded content type发送

#### axios
* https://segmentfault.com/a/1190000008470355?utm_source=tuicool&utm_medium=referral

* 1:引入对象
* 2:安装插件(Vue.use) 
    - 没有实现install函数，注册全局组件、挂载对象
    - 挂载属性给所有组件继承使用 Vue.prototype.$ajax = 引入的对象
* 3: 在组件内通过this.$ajax来使用

#### options(对象)
* defaults属性，先配置，后续请求都按配置来
* defaults.headers是一个对象
* 默认配置范围大于个性配置，优先级小于个性配置
* 总结
    - 1:$ajax.defaults  是一个配置对象(options)
    - options:
        + baseURL:基本url
        + headers是一个对象，设置请求头
        + params是一个对象，设置查询字符串参数
    - 2:post请求第二个参数是请求体数据
    - get(url,options) 
    - post(url,data,options)

#### 拦截器
* 对于请求与响应的两种行为：
    - 1:阻止
    - 2:添油加醋

* axios代码执行顺序
    - 1:默认设置 $ajax.defaults
        + 范围最大
    - 2:个性化设置 $ajax.get()中的options
        + 针对单次请求
    - 3:拦截器 $ajax.interceptors.request.use(fn)
        + 范围最大

#### 拦截器应用场景
* loadding图标的显示与隐藏

#### 合并请求
* 多个一起冲，保证都回来，否则就失败
* 不保证请求顺序

#### 顺序执行代码
* 1-> 2->3 一个个的控制
* 顺序执行与合并请求的相同:全成功算成功、一个失败算失败
* 不同点:顺序执行保证顺序，合并请求，不保证顺序的
