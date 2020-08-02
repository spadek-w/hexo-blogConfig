---
title: vue第一天
date: 2018-06-16 23:24:38
tags: vue
---
### vue介绍
---
#### 介绍
* 作者: 尤雨溪 14年2月开源

#### vue产品介绍
* weex 能够转换vue代码，成为移动端原生应用 ios Android PC
* vuex 凡是大型项目必用，公共数据管理
* 2014年开源的  
    - 核心特点:
        + 组件化，组件化比模块化更细
            * 组成部件
            * 组件: 模板template+ 动态效果script + 样式style
        + 双向数据流(双向数据绑定的现象)
            * 1向:内存(js对象的属性)发生改变影响页面
            * 1向:页面发生改变影响内存(js对象的属性)
        + 数据驱动
            * 内存的属性发生改变，驱动页面显示做调整
        + 双向数据绑定实现原理（js到页面）
            * 数据劫持(Object.defineProperty(obj,'name',{set:function(v){ //这里就能知道obj.name被改变,操作DOM改变dom元素的值  }}) )
        + 页面需要能知道被改变了，基于什么（事件，页面到js)
            * 基于的是很多的事件，比如onchange -> 改变js属性的值
        + MVVM框架
            * M:从js到页面 利用defineProperty M -> model数据模型obj
            * V:读取模板，获取模板中哪些元素使用了指令，给其添加事件，后期改变元素值
            * VM（view:model）: vue组件
        + IE9以下不支持(Object.defineProperty)
        + 善于开发单页应用SPA

#### vue起步
* 构建vue实例的options
* render

#### vue起步总结
* 流程 
    - 1:引包
    - 2:构建viewmodel(new Vue) 启动vue程序
    - 3:一般项目不使用viewmodel的template，而是通过render属性来渲染指定的组件
        + 组件包含组件，组件又包含组件
    - 3:使用render属性
        + render是一个函数， return createElement(options)
* options:
    - el:指定渲染目的地
    - template:模板
    - data (new Vue的时候其是一个对象,组件上使用 是一个函数，返回一个对象)

####  vue中常用的v-指令演示
* 常用指令 
* v-text 指定data中的属性名, 设置元素的innerText(双标签)
* v-html 指定data中的属性名, 设置元素的innerHTML(双标签)
* v-if 元素是否存在的问题
* v-show 元素是否显示的问题
* v-else 结合v-if使用,两者存在其一
* v-model 双向数据绑定

#### class结合v-bind使用
* v-bind 是绑定属性，其属性值会经过计算，得到最终结果再复制给属性
    - 表达式中，使用的变量都是vue中的属性
    - v-bind:属性名="表达式"

#### methods和v-on的使用
* options:{  methods:{ 函数名:函数体} }
    - methods是一个对象
    - el:是一个字符串或者DOM对象
    - render: 是一个函数
    - data
        + new Vue 是一个对象
        + 组件内 是一个函数，return一个对象

#### v-bind和v-on的简写形式
* v-bind:属性名="表达式"
* :属性名="表达式"
* v-on:原生事件="表达式||函数名"
* @原生事件="函数名||表达式"
    - 函数的调用，如果没有参数，可以省略小括号

#### v-for的使用
* 数组`v-for="(ele,index) in dataArr :key="index" "   `
* 对象`v-for="(value,key,index) in dataObj :key="index" "   `

#### 总结
* 代码步骤
    - 1:留坑 `div id="app"`
    - 2:引包
    - 3:创建主体组件,在全局中声明一个App,设置其options
        + options:  data/el/render/template/methods
        + data 是一个函数,return一个对象
        + render是一个函数,return一个DOM
        + template是字符串或DOM对象
        + methods是一个对象,key是函数名，value是函数体
* 一句心经
    - 在template中使用vue的变量，不需要this.
    - 在methods或者别的行为中使用vue的变量，需要this.
* 指令
    - innerText v-text
    - innerHTML v-html
    - 双向数据绑定 v-model
    - 元素是否存在 v-if  v-else(上一个兄弟节点有v-if 或者 v-else-if)
    - 元素是否显示 v-show
    - 绑定属性 v-bind:属性名="表达式" 简写 :属性名="表达式"
    - 绑定事件 v-on:属性名="函数" 简写   @事件名="表达式"
* template中保证一个根节点（并不一定是div）


#### 看文档的对象分类
* 全局  Vue.
* 选项 options ，可以存在与 单个组件和new Vue()中
* 实例  vm:就是`var vm = new Vue()` ,   this:组件实例
* 指令 v-开头
* 特殊属性 比如 v-for 中的key

#### 漂亮的列表
* 先设置一个对象列表
    - key:最终变量的值，value:样式名
    - {A:'a'}[变量的值(A)]

#### 父子组件使用(父传子)
* options 选项
    - components 是一个对象，key是子组件名，值是子组件对象

* 父组件向子组件传递值
    - 父，指定某个属性值，给赋值就可以了 `xxx="父的值"`
    - 子,需要声明接受参数，props:['xxx']

#### 创建全局组件
* 但凡父用子，父要声明子 components
* 全局注册全局组件，不用声明直接使用
* `Vue.component(组件名,组件对象(options))`

#### 子向父组件通信（获取组件对象）(扩展)
* 事件
    - 1:先on
    - 2:再emit
    - 3:第一个参数名一致，保证是同一个频率
    - 4:要实现其功能需要同一个对象
