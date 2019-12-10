# 就业阶段10 day07 vue.js基础

### 一.回顾

#### 1.组件嵌套

1. 在组建中使用了`其他组件`的标签就是组件嵌套
2. 全局组件在任何实例都可以使用
3. 局部组件只能在当前实例上使用
4. 组件嵌套 ---> 传值 ---> 父传子

#### 2.路由

1. 动态路由
    1. 定义参数path
        1. user/:参数名 
    2. 传递参数
        1. user/123
        2. $route.params.参数名
2. 编程式导航
    1. push/replace/go
    2. this.$router



### 二.Vue-cli

#### 1.工具介绍

vue-cli:脚手架

1. 介绍:`vue-cli`是一个`辅助开发工具`
    1. 代码编译
    2. 样式
    3. 语法校验
    4. 输出设置
    5. 其他...
2. 作用:可以为开发者提供一个`标准的项目开发结构`和配置
3. vue.cli:一个`命令行`工具,最新版本也支持`图形化`操作,可以快速搭建大型网络应用



#### 2.vue-cli安装和2-3版本解释

1. 安装
    1. vue-cli本质上是一个npm包,需要通过npm去安装下载
    2. `npm i -g @vue/cli`
        1. 全局安装脚手架,默认安装最新版本4.0+
    3. 查看版本
        1. `vue -V`查看脚手架版本号
        2. `vue --version`和上面等价
2. vue-cli命令行关键字是**vue**
3. 执行以下命令可以2.0和3.0兼得
    1. 2.0和3.0/4.0创建项目的命令是不一样的
    2. `npm install -g @vue/cli-init`    安装桥接工具 将2.0的功能补齐到目前的脚手架上
4. 注意:vue生成的模板有难有易
    1. 简单业务 ---> 简易模板
    2. 复杂任务 ---> 内容丰富模板

#### 3.vue-cli创建项目

1. 创建项目: 采用 cli 2.0的特性 (生成简易模板)

```bash
#  heroes 创建的项目名称
$ vue  init webpack-simple heroes //  webpack-simple 为模板名称 固定写法
# 切换到当前目录
$ cd  heroes 
# 安装依赖
$ npm install  
# 在开发模式下 启动运行项目
$ npm run dev

```

2. 创建项目: 采用 cli 3.0 特性 (两种 默认 /选填)

```bash 
# 3.0下创建项目
$ vue create heroes // create(创建) 为关键字
# 切换到当前目录
$ cd  heroes 
# 在开发模式下 启动运行项目
$ npm run serve
```

**注意** 3.0 +创建项目时  有两种模式, 一种**`默认模式`**, 一种选择模式,

1. 默认模式:一种标准的模板

2. 选择模式 可以根据自己的需求选择需要的工具和模式

**`任务`**

1. 分别使用vue-cli 2.0 和 3.0特性创建一个叫做heroes的项目 
2. 分别启动运行



#### 4.vue-cli项目目录解释

对2.0项目目录生成的模板文件进行识别认识

1. .bablelrc=>存放 babel编译的配置信息 () => es6 => es5 
2. .editorconfig => 存放编辑器的配置信息
3. .gitignore => git忽略文件
4. index.html => 单页应用的html
5. package.json => 用于存放依赖信息 及 其他项目信息
6. README.md => 项目介绍信息 github上的页面信息
7. webpack.config.js => wepack工具的配置文件 => webpack是一个前端工程化的工具  编译代码 -压缩代码- 处理代码,其他....
8. webpack => 代码编译,打包 压缩
9. build.js =>  不是人写的 => webpack 打包而来 => webpack中可以配置文件的**`入口`** ,可以配置文件的**`出口`**
10. webpack 文件的出口 =>buildjs =>  配置信息  =>  webpack.config.js
11. entry => 整个项目的入口文件=> main.js
12. output => 整个项目的出口文件 => filename => build.js  =>  build.js 启动项目时  并不是物理文件,而是内存中一个文件流



### 三.ES6模块的导入和导出

>**ES6**提供`import 变量 from 路径` 语法 来**`引入组件/模块`** 

1. `import  别名 from  路径`  => 引入 
    1. 如果 引用的包是第三方的包 可以用包名代替路径
        1. 如`import Vue from 'vue'`
    2. 如果 不需要别名 可以 用 **`import`**  "路径"
        1. 自己写的组件
        2. `import App from './App.vue'`
        3. `import router from './router.js';`

2. 导出 =>  export default  对象   

    1. 提供了 export default 变量  **`导出组件`**

    2. 提供 **export**  **default**  **`对象`** 语法来导出组件

        ```js
        export default vue //导出对象   vue.js
        ```

    3. 如果想引入一个文件,并且使用,这个文件必须导出

        ```js
        export default new VueRouter()
        ```

    4. 如果想引用一个组件,就必须先导出该组件 

        ```js
        export default {}
        ```

3. 导入和导出 带来的好处是  **`可以将很多模块拆成一个个的文件`**

4. 拓展

    ```js
    export const function  fn1() {} // 方法1
    export const function  fn2() {} // 方法2
    export const function  fn3() {} // 方法3
    // 一个文件
    ```

    ```js
    import { fn1,fn2, fn3 } from '文件'
    ```

    

### 四.基础-Vue-单文件组件及入口解析

1. `App.vue`
    1. 所有组件的根组件
2. 单文件组件
    1. 一个后缀名为`.vue`的文件就是一个组件
        1. **template** 组件结构 :有且只有一个根元素  ---> html结构
        2. **script** 导出一个对象  ---> 逻辑结构以及数据对象
            1. data
            2. methods
            3. computed
            4. ...
        3. **style** 组件的样式  ---> css



### 五.案例-英雄列表

#### 1.导入素材处理样式

1. 将项目所需样式导入到项目中 

2. 运行时依赖 / 开发时依赖 
    1. 运行时依赖  => 项目在线上运行的时候所需要依赖的文件
    2. 开发依赖 =>  开发调试过程中 辅助开发的依赖 脚手架
    3. npm i  包名 -S或者 --save  => 将包装包运行时依赖包
    4. npm i 包名  -D 或者 --save--dev => 将包装到开发时依赖
        1. cnpm  必须写 -S或者-D

3. 安装 bootstrap固定版本
    1. `npm i  bootstrap@3.3.7 `
    2. 安装完成之后 ,在main.js入口处引入css文件

```js
import "./../node_modules/bootstrap/dist/css/bootstrap.css"; // 引入 bootstarp的样式文件
import "./assets/index.css"; // 引入index.css

```

4. 重启运行,发现bootstrap.css文件 运行报错 

5. 根据错误 需要在webpack.config.js增加对不识别文件的处理

```js	
{
test: /.(ttf|woff2|woff|eot)$/,
loader: "file-loader",
options: {
name: "[name].[ext]?[hash]"
}
}
```



#### 2.提取公共组件-头部-侧边栏-列表

将静态内容的 头部 侧边栏 , 列表分别封装成Vue组件 ,并在视图中显示

步骤

1. 新建vue文件
2. 拷贝html静态内容到 template中
3. 在app.vue中引入注册组件
4. 注册在app.vue的组件中 
5. 在app.vue的模板中使用注册组件



#### 3.提取路由模块

提取路由模块,并应用视图

步骤:

1. 安装路由

    1. `npm i vue-router`

2. 创建`router.vue`专门负责路由配置

3. 在`router.vue`中引入路由模块

    1. `import Vue from 'vue'`
    2. `import VueRouter from 'vue-router'` ---> 第三方包可以用包名代替路径

4. 使用router 

    1. `Vue.use(VueRouter)` 注册路由

5. 实例化router 并暴露出去

    ```js
    export default new VueRouter({
    routes:[] //实例化routes
    })
    ```

6. 配置路由表

7. 提取组件完善路由表

    1. ```js
        routes: [{
            path: '/',
            redirect: '/heroes'
        }, {
            path: '/heroes',
            component: heroContainer,
            children: [{
                //什么都不写代表二级路由的默认组件
                path: '',
                component: heroList,
            }, {
                path: '/heroes/add',
                component: addHero,
            }, {
                path: '/heroes/edit/:heroid',
                component: editHero,
            }]
        }, {
            path: '/weapon',
            component: weapon
        }, {
            path: '/gear',
            component: gear
        }]
        ```

8. 在`main.js`中引入`router.vue`路由模块

    1. `import router from './router.js';`

9. 在`main.js`中挂载路由

    1. ```js
        new Vue({
            el: '#app',
            router,
            render: h => h(App)
        })
        ```

10. router-link 组件**`默认生成`**的a标签

    1. 通过一个属性`tag`(标签)来改变其最终生成的标签

11. router-link **`默认`**激活样式 是  router-link-active

    1. 通过`linkActiveClass`属性将默认的激活样式换掉  
    2. `linkActiveClass: "active"`

12. 在`App.vue`中加入路由承载视图

    ```html
    <div id="app">
        <app-header></app-header>
        <div class="container-fluid">
          <div class="row">
            <!-- 左侧导航 -->
            <app-slidebar></app-slidebar>
            <!-- 一级路由容器 -->
            <div class="col-sm-9 col-sm-offset-3 col-md-10 col-md-offset-2 main">
              <router-view></router-view>
            </div>
          </div>
        </div>
      </div>
    ```

    

#### 4.json-server-启动接口服务器

准备json-server服务器.启动实现 数据接口 增删改查的联通

步骤

1. 安装json-server

    1. json-server 是一个命令行工具,和vue以及vue-cli没有任何关系 安装在任何位置都可以
    2. `npm i -g json-server`

2. 新建json文件

    ```json
    {
      "hero": [
        {
          "id": 1,
          "name": "张三疯",
          "company": "阿里巴巴"
        },
        {
          "id": 2,
          "name": "李四少",
          "company": "京东"
        },
        {
          "id": 3,
          "name": "王五",
          "company": "拼多多"
        }
      ]
    }
    ```

3. 启动json-server

    1. `json-server --watch 文件名.json`



#### 5.列表渲染

步骤:

1.  安装axios 插件 

    1. `npm i axios`

2.  英雄列表组件中引入 axios

    1. `import axiod from 'axios'`

3. 定义数据list

    ```js
    data(){
        return {
            list:[]
        }
    }
    ```

4. 请求英雄列表的方法封装 

    ```js
    loadData(){
        this.$axios.get('/hero').then(res=>{
            this.list=res.data;
        });
    }
    ```

5. 实例创建完成之后执行created

    ```js
    created(){
        this.loadData();  
    }
    ```

    

#### 6.删除功能

步骤

1. 注册删除事件 

    1. `<a @click.prevent="delItem(item.id)">删除</a>`

2. 方法函数

    ```js
    delItem(id) {
        if(confirm("你确定要删除吗?")){
          this.$axios.delete(`/hero/${id}`).then(res=>{
            this.loadData();
          })
        }
    },
    ```

3. 请求过后重新加载页面

    1. `this.loadData();`



#### 7.添加英雄功能

1. 添加页面的视图

    1. 创建`add-hero.vue`组件

    2. 写入静态内容

        ```html
        <div>
            <h2 class="sub-header">添加英雄</h2>
            <form>
              <div class="form-group">
                <label for="exampleInputEmail1">姓名</label>
                <input 
                  v-model="formData.name" 
                  type="text" 
                  class="form-control" 
                  id="exampleInputEmail1" 
                  placeholder="请输入你的姓名">
              </div>
              <div class="form-group">
                <label for="exampleInputPassword1">公司</label>
                <input 
                  v-model="formData.company" 
                  type="text" 
                  class="form-control" 
                  id="exampleInputPassword1" 
                  placeholder="请输入你的公司">
              </div>
              <button class="btn btn-success" @click.prevent="addHero">添加英雄</button>
            </form>
        </div>
        ```

    3. 在路由表中配置添加功能的路由

    4. 给列表组件的添加按钮设置导航

        1. `<router-link class="btn btn-success" to="/heroes/add">添加英雄</router-link>`

2. 功能实现

    1. 定义表单数据  和  表单进行绑定 

        ```js
        data() {
            return {
                formData: {
                    name:'',
                    company:''
                }
            }
        }
        ```

    2. 给添加按钮注册事件

        ```html
        <button class="btn btn-success" @click.prevent="addHero">添加英雄</button>
        ```

    3. 实现函数功能

        ```js
        addHero() {
          if(this.formData.name && this.formData.company){
            this.$axios.post("/hero",this.formData).then(()=>{
              //回到列表页
              //编程式导航
              this.$router.push('/heroes');
            })
          }
        }
        ```

    4. 添加完成后回到列表页

        1. `this.$router.push('/heroes');`

    

#### 8.编辑功能 ---> 和添加功能基本一致

1. 添加视图

    1. 创建`edit-hero.vue`组件
    2. 写入静态内容
    3. 在路由表中配置编辑功能的路由
        1. 路由中传递参数表示修改的数据
    4. 给列表组件的编辑按钮设置导航
        1. `<router-link :to="`/heroes/edit/${item.id}`">编辑</router-link>`
        2. 这里要写入数据id

2. 实现功能

    1. 定义表单数据  和  表单进行绑定 

    2. 静态数据加载完成后传入要修改的内容

        ```js
        created() { this.$axios.get(`/hero/${this.$route.params.heroid}`).then(res=>{
                this.formData=res.data;
            })
        }
        ```

    3. 给编辑按钮注册事件

    4. 实现函数功能

        ```js
        editHero() {
          if(this.formData.name && this.formData.company){
            this.$axios.put(`/hero/${this.$route.params.heroid}`,this.formData).then(()=>{
              //回到列表页
              //编程式导航
              this.$router.push('/heroes');
            })
          }
        }
        ```

    5. 修改完成后回到列表页

        1. `this.$router.push('/heroes');`



#### 9.优化-axios统一导入

1. 在入口main.js文件中引入axios,并给全局Vue对象的原型链赋值

    ```js
    Vue.prototype.$axios = axios; //所有的实例都直接共享拥有了 这个方法
    ```

2. 调用接口时  采用 实例.属性的方式即可调用 

    1. `this.$axios`后面跟.get/.delete等请求方法



#### 10.优化-设置baseUrl

1. 给axios中的baseUrl设置常态值

    ```js
    Axios.defaults.baseURL = "http://localhost:3000"; // 设置共享的方法
    ```

2. 将所有请求中的基地址去掉



#### 11.优化-目录划分

将组件的目录进行整理划分,并统一当前路由的激活样式

1. 路由级组件 =>直接挂载到路由上的文件 => 不用注册 => views目录名
2. 普通级组件 => 在组件中用标签来使用的组件 叫做普通组件 =>需要注册 => components目录名
3. 划分完目录修改文件中的组件/模块引入地址