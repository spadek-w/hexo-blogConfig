---
title: vue第六天
date: 2018-07-05 23:50:33
tags: vue
---
### 准备开始    
* nrm -> 是一个全局命令行工具 `npm i -g nrm`
    用来管理npm的镜像源

    - 查看当前镜像源 nrm ls 
    - 切换镜像源  nrm use taobao
#### 复习
* axios
    - options(defaults)
        + baseURL :基本URL
        + params:是一个对象， url上的查询字符串
        + headers:是一个对象，设置头信息
    - 拦截器
        + 视图层面的应用场景
            * 请求发起的时候，开启loadding图标
            * 响应回来的时候,关闭loadding图标
        + 数据层面的应用（移动端原生应用）
            * 在发起请求的时候，自己做一个cookie来标识自己的身份
            * 在请求拦截器中，给请求头添加这个cookie，服务器就能认识你了
    - 合并请求
        + 请求省、市数据，只有都成功才算成功，一个失败，就算失败
        + 不保证顺序
    - 取消请求
        + 核心xhr.abort(); //客户端主动关闭连接
        +  var CancelToken = this.$ajax.CancelToken;
        +  var source = CancelToken.source();
        +  在options中传递参数 cancelToken: source.token
        +  调用取消，就相当于调用reject() ,触发catch -> xhr.abort();
            *  source.cancel(); 

#### 今日重点

#### 模块
* 有时导出的对象是值(commonjs)，有时导出的是{ default:值}(es6)
* es6的导入 优先选择{ default:值} ,如果没有default属性，就作为 整个对象获取
    - 通过es6导入，我们无需关系是否有default属性来导出
        + 有就拿，没有就是整体对象
* commonjs  导入:require  导出:module.exports
*  ES6      导入:import xxx from './xx.js';   
        +  导出: export default 数据

#### ES6模块
* 默认导出(导入名可以随便写)
    - 入 `import Xxx from './xxx.js';`
    - 出 `export default Obj;`
* 声明式(导入名称一定与导出的一致)
    - 先声明，再导出 
        + `let num1 = 1; export { num1 } `
    - 声明并导出
        + `export let num2 = 1;`
    - 导入 `import { num1,num2 } from './xxx.js';`

#### http-server
* 在当前有index.html的命令行输入 hs -o -p 端口号

#### 下载依赖
* npm i vue vue-router axios moment vue-preview mint-ui -S && npm i style-loader css-loader less less-loader url-loader file-loader babel-core babel-loader babel-preset-env babel-plugin-transform-runtime vue-loader vue-template-compiler html-webpack-plugin webpack webpack-dev-server -D
