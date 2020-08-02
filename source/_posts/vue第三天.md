---
title: vue第三天
date: 2018-06-16 23:37:06
tags: vue
---
#### 复习
* router基本步骤
    - 1: 引入对象 `var VueRouter = require('vue-router.js');`
    - 2: 安装插件 `Vue.use(VueRouter);`
        + 所有的this(VueComponent).$route/$router
    - 3: 创建路由对象 `new VueRouter(options路由配置);`
    - 4: ` { path:'/xxx' ,component:Xxx组件option}  `
    - 5: 将路由对象交给Vue实例 `new Vue({ router:router })`
    - 6: 给component属性留坑 `<router-view></router-view>`
* 生命周期
    - 1: beforeCreate 和 created
        + beforeCreate 还未完成初始化
        + created 已经完成初始化（数据观察||响应式），可以获取数据
            * this.xxx = xxx;  ->  页面也显示不同的结果
            * 基于Object.defineProperty(data,'xxx',{set:fn})
    - 2: created和mounted
        +  created 操作数据
        +  mounted 操作DOM
    - 3: destroyed和active
        + 销毁和停用，是一个类型，v-if="false"触发
        + 激活和创建，是一个类型，v-if="true"触发
        + 激活和停用结合内置组件keep-alive使用,频繁创建和销毁组件的时候
            * v-show
            * 插入和移除，在框架中还可以多一些过渡效果的行为
    - 4:更改组件数据之后也会触发事件，但是这个知道就好，不常用

#### 今日重点
* 路由
    - 后端 : 请求 + URL 来去做判断
    - 前端 : 锚点值 来去做判断
    
#### router-link
* 可以让我们不必担心锚点值的特殊标识
    - 有的是 #/xxx做标识
    - 有的是 #!/xxx做标识
    - 而使用了router-link 只用保证 to属性内的值与路由规则的path一致即可
* 使用方式 `<router-link to="/music">电影</router-link>`

#### 命名路由
* 使用router-link
    - 常规方式 `<router-link to="/music">电影</router-link>`
    - 命名方式 `<router-link :to="{name:'music'}" >音乐</router-link>  `
    - 注意: __需要配置路由规则中有一个name叫做music的规则__
    - ` { name:'music',path:'/xxxx'}  `
* 1:路由规则中 有name属性，:to指向这个对象，从而按规则的path生成href


#### 参数router-link
* 查询字符串
    - 1:操作(去哪里？)
        + `<router-link :to="{ name:'bj' ,query:{city:'顺义'}   }">北京</router-link>`
    - 2: 路由规则(怎么去)
        + `{ name:'bj', path:'/beijing' ,component:BeiJing}`
    - 3: 生成的效果
        + `href="#/beijing?city=顺义" `
* path的方式
    - 1:操作(去哪里？)
        + `<router-link :to="{ name:'bj' ,params:{city:'顺义'}   }">北京</router-link>`
    - 2: 路由规则(怎么去)
        + `{ name:'bj', path:'/beijing/:city' ,component:BeiJing}`
    - 3: 生成的效果
        + `href="#/beijing/顺义" `


#### vue-router中的对象
* 路由信息对象 $route -> 获取信息
    - $route, Vue.use(VueRouter) 来完成给this（组件对象挂载属性的）
    - 在所有的组件中就可以使用 this.$route获取这个对象
* 路由功能对象 $router -> 操作（行为）


#### 总结通过url传递参数
* query的方式
    - 1:操作(去哪里？)
        + `<router-link :to="{ name:'bj' ,params:{city:'顺义'}   }">北京</router-link>`
    - 2: 路由规则(怎么去,导航)
        + `{ name:'bj', path:'/beijing/:city' ,component:BeiJing}`
    - 3: 去了干嘛
        + created钩子函数：获取路由参数，发起ajax请求，把数据放到页面上
        + 查询字符串 `this.$route.query`
        + path方式 `this.$route.params`

#### 插件安装
* 所有Vue相关的插件必须要实现install函数，在Vue.use的时候，会把Vue对象传递到install函数中，从而可以给Vue的原型挂载属性，让继承于Vue的各个组件对象都有该属性

#### 多视图(命名视图)
* 更为灵活的维护，灵活的配置修改显示的效果
* 多个router-view 更灵活
* components属性是一个对象 key(坑名),value(组件)

#### 嵌套路由
* router-view 包含router-view
* 路由中包含子路由
* 每个路由都映射组件
    - 子路由path:  绝对路径/xxx，那访问就是这个路径 /xxx
    - 相对路径 xxx  ,访问则是父路由路径 /home/xxx
* 路由对象中加入children:[路由规则]

#### 重定向及404
* 重定向在路由规则中 `{ path:'/',redirect:{name:'xxxx'}  }`
* 404 在规则的最后`path:'*',component:Xxxx`

#### 编程式导航
* js代码 -> 导航的能力 -> 页面数据变更
* router-link 用户来点击，页面数据变更
* 跳转:`this.$router.push(路由对象{name:'xx'})`
* 根据历史记录前进后退 `this.$router.go(-1||1);`