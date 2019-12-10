# 就业阶段10 day06 vue.js基础

### 一.vue简单回顾

- Vue是一个框架 ---> 单页面  --->自底向上增量
- jquery是一个类库  ---> 工具箱
- MVVM框架  
    - M --> Model数据
    - V --> View VM
        - ViewModel ---> 响应式数据 --->数据变化 ---> 视图变化
- v-model ---> 实现双向绑定
- v-bind ---> 动态绑定属性 ---> 直接通过数据修改视图上的属性
- v-if/v-show ---> 条件渲染
- v-for ---> 遍历循环
    - 循环数组/对象 
        - 数组 (item,index) in items
        - 对象(value,key,index) in objs
- v-on ---> 注册事件
- v-bind:class
- v-bind:style
- v-cloak
- v-once 
- v-pre 跳过
- template
- el/data/methods/computed/created/



### 二.组件

#### 1.组件体验

1. 目标:建立对组件的认识
2. 场景:重复的`页面结构`,`数据`,`逻辑`都可以抽提成一个`组件`
3. 对于复杂的结构来说,都可以通过抽提组件的方式来简化开发过程
    1. vue ---> 全局 ---> Vue.component(给全局Vue对象注册了一个组件)
    2. new Vue() --> 自动拥有了这个注册的组件
    3. 局部注册 ---> 在当前实例上注册 ---> 只有当前实例才可以使用
    4. 简单 高效 不重复

```html
<div id="app">
    <!-- 使用组件,一个标签就是一个组件 -->
    <h2>组件1</h2>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
</div>
<div id="app2">
    <!-- 使用组件,一个标签就是一个组件 -->
    <h2>组件2</h2>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
    <span-btn></span-btn>
</div>

<script src="../vue.js"></script>
<script>
    // 注册全局组件
    Vue.component("span-btn", {
        //页面结构 ---> 有且只有一个根节点
        template: `
            <div>
                <span>{{count}}</span>
                <button @click="changeCount">点击增加</button>
            </div>`,
        // data是一个带返回值的函数 --> 组件和组件之间要保持独立的数据
        // 每个组件都会各自独立维护它的 count。因为你每用一次组件，就会有一个它的新实例被创建
        // 一个组件的 data 选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立的拷贝
        data() {
            //这里相当于返回了一个新的Object对象
            return {
                count: 0
            }
        },
        methods: {
            changeCount() {
                this.count++;
            },
        },
    });
    new Vue({
        el: '#app'
    });
    new Vue({
        el: '#app2'
    })
</script>
```



#### 2.组件特点

1. 组件特点:组件是一个`特殊的Vue实例`
2. 和vue实例相似之处:data/methods/computed/watch 等一应俱全 Vue实例有的组件基本都有
3. 组件没有el,但是有template ---> 组件页面结构
4. 注意:
    1. 组件和Vue实例的区别为,在组建中的data是一个函数,组件没有el选项
    2. 组件的data是一个`带返回值的函数`
        1. 组件的数据是独立的
        2. data:返回一个新数据
    3. template代表其`页面结构`
        1. 有且只有一个根元素
    4. 每个组件都是`独立`的运行作用域,数据逻辑没有任何关联

```html
<div id="app">
    <!-- 使用组件,一个标签就是一个组件 -->
    <!-- 直接写组件的名称就是使用组件了 -->
    <!-- 写了一个标签相当于写了一个标签的实例 -->
    <eight-eight></eight-eight>
</div>

<script src="../vue.js"></script>
<script>
    // 全局组件注册,应该放在Vue实例化之前
    // Vue.component(组件名称,组件对象)
    // 命名:abc 单词 或者 abc-d 双词(建议全小写)
    // 注册全局组件
    Vue.component("eight-eight", {
        //组件对象
        //页面结构 ---> 有且只有一个根节点
        template: `
            <div>
                <p>hello</p>
                <p>{{name}}</p>
                <input type='text' v-model="name" />
            </div>`,
        // data是一个带返回值的函数 --> 组件和组件之间要保持独立的数据
        // 每个组件都会各自独立维护它的 count。因为你每用一次组件，就会有一个它的新实例被创建
        // 一个组件的 data 选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立的拷贝
        data() {
            //这里相当于返回了一个新的Object对象
            return {
                name: "字节跳动"
            }
        },
        methods: {},
        computed: {}
    });
    new Vue({
        el: '#app'
    });
</script>
```



#### 3.全局组件

1. 全局和局部:注册方式不同,应用范围不同
2. 路径:实现一个全局组件

```js
// 全局组件注册,应该放在Vue实例化之前
// Vue.component(组件名称,组件对象)
// 命名:abc 单词 或者 abc-d 双词(建议全小写)
// 注册全局组件
Vue.component("eight-eight", {
    //组件对象
    //页面结构 ---> 有且只有一个根节点
    template: `
        <div>{{count}}</div>`,
    data() {
        //这里相当于返回了一个新的Object对象
        return {
            count: 1
        }
    }
});
```

##### 案例-全局组件,实现一个加减步进器

```html
<div id="app">
    <!-- 使用组件,一个标签就是一个组件 -->
    <h2>加减步进器</h2>
    <span-counter></span-counter>
</div>

<script src="../vue.js"></script>
<script>
    // 注册全局组件
    Vue.component("span-counter", {
        //页面结构 ---> 有且只有一个根节点
        template: `
            <div>
                <button @click="cut">-</button>
                <span>{{count}}</span>
                <button @click="add">+</button>
            </div>`,
        data() {
            //这里相当于返回了一个新的Object对象
            return {
                count: 0
            }
        },
        methods: {
            cut() {
                //如果前面的等于0 返回false 后面不执行
                this.count && this.count--;
            },
            add() {
                this.count++;
            },
        },
    });
    new Vue({
        el: '#app'
    });
</script>
```



#### 4.局部组件

> `局部组件`在谁的实例上注册,就只能在谁的实例上使用

1. 局部组件的实现
    1. 定义一个局部组件
    2. 写入组件选项
    3. 使用组件
2. 局部和全局的区别 
    1. 注册位置不同
    2. 应用范围不同

```js
new Vue({
    el: '#app',
    data:{},
    // 局部组件需要在当前实例上注册
    components: {
        //key(组件名称):value(组件对象)
        "step-counter": {
            template: `<div></div>`,
            data() {},
            methods: {},
            },
        }
    }
});
```

##### 案例-局部组件,实现一个加减步进器

```html
<div id="app">
    <!-- 使用组件,一个标签就是一个组件 -->
    <h2>加减步进器</h2>
    <step-counter></step-counter>
</div>
<!-- 出错 -->
<div id="app1">
    <!-- 使用组件,一个标签就是一个组件 -->
    <h2>加减步进器</h2>
    <step-counter></step-counter>
</div>

<script src="../vue.js"></script>
<script>
    new Vue({
        el: '#app',

        // 局部组件需要在当前实例上注册
        components: {
            //key(组件名称):value(组件对象)
            "step-counter": {
                //页面结构 ---> 有且只有一个根节点
                template: `
                    <div>
                        <button @click="cut">-</button>
                        <span>{{count}}</span>
                        <button @click="add">+</button>
                    </div>`,
                data() {
                    //这里相当于返回了一个新的Object对象
                    return {
                        count: 0
                    }
                },
                methods: {
                    cut() {
                        //如果前面的等于0 返回false 后面不执行
                        this.count && this.count--;
                    },
                    add() {
                        this.count++;
                    },
                },
            }
        }
    });

    new Vue({
        el: "#app1"
    })
</script>
```



#### 5.组件嵌套

> 组件嵌套就是在组件中使用其它组件

```html
<div id="app">
    <!-- 使用组件,一个标签就是一个组件 -->
    <abc-p></abc-p>
    <!-- <child></child> -->
</div>

<script src="../vue.js"></script>
<script>
    Vue.component("abc-p", {
        //页面结构 ---> 有且只有一个根节点
        template: `
            <div>
                我是一个全局组件
                <child></child>
            </div>`,
        components: {
            child: {
                template: `
                    <div style="color:red;">
                        我是一个局部组件
                    </div>`,
            }
        }
    })
    new Vue({
        el: '#app',

    });
</script>
```

**一旦形成组件嵌套,就有了`父子关系`**

##### 案例

1. 实现一个Vue案例
2. 自定义一个组件parent-b,内容为我是父组件parentb
3. 自定义一个组件child-a,内容为我是子组件childa
4. 将在父组件中使用childa,并在页面上显示两个parentb

```html
<div id="app">
    <!-- 使用组件,一个标签就是一个组件 -->
    <parent-b></parent-b>
    <parent-b></parent-b>
    <!-- <child></child> -->
</div>

<script src="../vue.js"></script>
<script>
    Vue.component("parent-b", {
        //页面结构 ---> 有且只有一个根节点
        template: `
            <div>
                我是父组件parent-b
                <child-a></child-a>
            </div>`,
    })
    Vue.component("child-a", {
        //页面结构 ---> 有且只有一个根节点
        template: `
            <div style="color:green;">
                我是一个子组件child-a
            </div>`,
    })
    new Vue({
        el: '#app',

    });
</script>
```

##### 实现组件嵌套

1. 定义多个组件
2. 组件对组件进行引用
3. 使用根组件

注意:**组件嵌套和全局以及局部组件没关系**



#### 6.组件通信的几种情况

1. 父组件 --> 子组件   需要将数据传给子组件 
2. 子组件 --> 父组件  如果父组件需要 子组件也可以传数据给父组件
3. 兄弟组件1 --> 兄弟组件2 

#### 7.父组件给子组件传值Props

1. props作用:接受父组件传递的数据
2. props就是父组件给子组件标签上定义的`属性`
3. **给谁传就在谁的标签上写属性**
4. props
    1. props是组件的选项,定义接受属性
    2. props的值可以是字符串数组`props:["list"]`
    3. props数组里面的元素称之为prop(属性) 属性的=?值
    4. prop的值来源于外部(组件的外部)
    5. prop是组件的属性 ---> 自定义标签的属性
    6. prop的赋值位置 ---> 在使用组件时,通过标签属性去赋值
    7. prop的用法和data中的数据用法一样
5. 注意:父组件传递给子组件的数据是`只读`的,`只可以用,不可以改`
6. 用props完成父组件给子组件传值 传值的属性都是定义在 子组件的标签上,可以采用v-bind的形式传递动态值
7. 定义props属性 在标签上定义属性  v-bind传递动态值
8. 在子组件中声明接收的属性
9. 在子组件中使用 组件 
    1. 注意: **属性只可以用 不可改**

##### 案例

1. 定义子组件
2. 在父组件中将 ["北京", "上海","天津"] 传递给子组件
3. 在子组件中获取该数据 并采用v-for循环显示在页面上

```html
<div id="app">
    <!-- Vue实例就是city组件的父 -->
    <!-- 1.定义属性 给谁传就在谁的标签上写属性,属性名随便写-->
    <city :citylist="list"></city>
</div>

<script src="../vue.js"></script>
<script>
    Vue.component("city", {
        //2.接收属性 props 字符串数组
        template: `
            <div>
            <p>城市</p>
            <ul>
                <li v-for="item in citylist">{{item}}</li>
            </ul>
            </div>`,
        props: ["citylist"],
    })
    new Vue({
        el: '#app',
        data: {
            list: ["北京", "上海", "天津", "重庆"]
        },
    });
</script>
```

 1. 定义父子组件 
    
2. 定义props接受父组件属性

3. 父组件中通过属性给子组件传值

4. 注册使用子组件

    ```js
    const comA = {
    template: `<div>
    <span v-for="(item,index) in list" :key="index">{{item}}</span>
    </div>
    `,
    props: ["list"] // props可以是数组  也可以是对象
    };
    ```

    



### 三.单页应用

#### 1.SPA的特点

1. 传统模式:每个页面及其内容都需要从服务器一次次请求 如果网络差,体验则会感觉很慢
2. spa模式:`第一次`加载会将所有的资源都请求到页面,`模块之间切换`不会再请求服务器

#### 2.SPA优缺点

##### 1.优点:

1. 用户体验好,因为前段操作几乎感受不到网络的延迟
2. 完全组件化开发,由于只有一个页面,所以原来属于一个个页面的工作被归类为一个个`组件`

##### 2.缺点:

1. `首屏`加载慢 ---> `按需加载`不刷新页面,只请求js模块
2. 不利于SEO ---> `服务器渲染`(node-->自己写路由-->express-art-template+res.render())
3. `开发难度高`(框架)相对于传统模式,有一些学习成本和应用成本

vue适合开发SPA --> 什么是SPA+SPA特点

SPA不利于SEO --> 搜索引擎排名靠前 --> 搜索引擎机制 --> 搜索引擎不能去找到局部刷新的网站内容

#### 3.SPA实现原理

1. **`目标`** 掌握前段SPA的实现原理
    1. SPA要实现 能够在前端自由切换模块 
    2. SPA要能记忆当前切换的模块,并且刷新页面模块依然还在当前视图
    3. SPA要实现在前端切换模块时,不能引起页面刷新,否则页面内容会被重置
2. **`结论`**
    1. 可以通过页面地址的锚链接来实现spa
    2. hash(锚链接)位于链接地址 **`#`**之后
    3. hash值的改变**`不会触发`**页面刷新
    4. hash值是url地址的一部分,会存储在页面地址上 我们可以获取到
    5. 可以通过**`事件监听`**hash值得改变 `hashchange`事件
    6. 拿到了hash值,就可以根据不同的hash值进行不同的**`模块切换`**



### 四.路由

#### 1.js实现路由

> 采用**`hash值改变`**的特性来进行前端路由切换

步骤:

1.  实现导航结构 

2.  监听hash改变

3. 根据改变切换视图

    

##### 案例

1. 在页面上实现4个链接,北京,上海,天津,重庆
2. 实现点击4个链接时,页面上显示对应的城市名称
3. 并且刷新页面之后,上次切换的城市还在

```html
<a href="#bj">北京</a>
<a href="#sh">上海</a>
<a href="#tj">天津</a>
<a href="#cq">重庆</a>
<div id="container"></div>

<!-- 
    1.在页面上实现4个城市
    2.实现点击4个链接时,页面上显示对应的城市名称
    3.刷新页面,上次切换的城市还在
 -->
<script>
    //hash值改变事件
    var func = function() {
        var dom = document.querySelector('#container');
        //获取当前hash值
        var path = window.location.hash.substr(1);
        //根据hash值决定哪个hash值显示
        switch (path) {
            case "bj":
                dom.innerText = "北京顺义马坡";
                break;
            case "sh":
                dom.innerText = "上海陆家嘴";
                break;
            case "tj":
                dom.innerText = "天津红桥区";
                break;
            case "cq":
                dom.innerText = "重庆洪崖洞";
                break;
            default:
                break;
        }
    }
    window.onhashchange = func;
    func();
</script>
```



#### 2.vue-router

1. Vue-Router 是 [Vue.js](http://cn.vuejs.org/) 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建**单页面**应用变得易如反掌   它是一个插件
2. Vuejs中不包含vue-router
3. 实现根据不同的请求地址 而**`显示不同的组件`**
4. 如果要使用 vue开发项目,前端路由功能**`必须使用`**vue-router来实现



#### 3.vue-router-体验及使用步骤

步骤:

1. 导入vue和vue-router

2. 定义导航

3. 定义容器

    ```html
    <div id="app">
        <!-- 2.定义导航 -->
        <router-link to="/main">主食</router-link>
        <router-link to="/meat">肉食</router-link>
        <router-link to="/soup">汤</router-link>
        <!-- 3.定义容器 -->
        <router-view></router-view>
    </div>
    ```

4. 实例化一个VueRouter组件

5. 配置路由表

    1. 一个地址对应一个组件(模块)

6. 挂载路由

    ```html
     <script>
        // 4.实例化一个VueRouter
        const router = new VueRouter({
            //5.配置路由表
            //一个地址对应一个组件(模块)
            routes: [{
                path: "/main",
                component: {
                    template: `<div>馒头-米饭-饼</div>`,
                }
            }, {
                path: "/meat",
                component: {
                    template: `<div>红烧肉-糖醋里脊-鱼香肉丝</div>`,
                }
            }, {
                path: "/soup",
                component: {
                    template: `<div>免费汤</div>`,
                }
            }]
        });
        //6.挂载路由
        var vm = new Vue({
            el: '#app',
            data: {},
            methods: {},
            router
        })
    </script>
    ```



##### 案例-实现一个菜品导航 

主食 => 狗不理包子/过桥米线/油泼面

凉菜 => 拉皮/拍黄瓜/凉拌木耳

热菜 => 烤全羊/羊蝎子/烤鸭

```html
<div id="app">
    <!-- 2.定义导航 -->
    <router-link to="/main">主食</router-link>
    <router-link to="/cold">凉菜</router-link>
    <router-link to="/got">热菜</router-link>
    <!-- 3.定义容器 -->
    <router-view></router-view>
</div>


<!-- 1.引入js -->
<script src="../vue.js"></script>
<script src="../vue-router.js"></script>
<!-- 
    主食 => 狗不理包子/过桥米线/油泼面
    凉菜 => 拉皮/拍黄瓜/凉拌木耳
    热菜 => 烤全羊/羊蝎子/烤鸭
 -->
<script>
    // 4.实例化一个VueRouter
    const router = new VueRouter({
        //5.配置路由表
        //一个地址对应一个组件(模块)
        routes: [{
            path: "/main",
            component: {
                template: `<div>狗不理包子/过桥米线/油泼面</div>`,
            }
        }, {
            path: "/cold",
            component: {
                template: `<div>拉皮/拍黄瓜/凉拌木耳</div>`,
            }
        }, {
            path: "/got",
            component: {
                template: `<div>烤全羊/羊蝎子/烤鸭</div>`,
            }
        }]
    });
    //6.挂载路由
    var vm = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router
    })
</script>
```



#### 4.vue-router-动态路由

1. 点击**`列表页`** 跳转到**`详情页`**时,跳转的链接需要携带参数,会导致**`path`**不同
2. 当path不同却需要对应同一个组件时,需要用到动态路由这一概念

##### 路由传参

步骤:

1. 路由规则中增加参数，在path最后增加 **:动态参数**

2. 通过 <router-link> 传参，在路径上传入具体的值

3. 在组件内部可以使用，**this.$route** 获取当前路由对象

 ```html
<div id="app">
    <!-- 2.定义导航 -->
    <!-- 传递动态路由参数 -->
    <router-link to="/company/阿里巴巴/30000">阿里巴巴</router-link>
    <router-link to="/company/腾讯/40000">腾讯</router-link>
    <router-link to="/company/美团/20000">美团</router-link>
    <!-- 3.定义容器 -->
    <router-view></router-view>
</div>


<!-- 1.引入js -->
<script src="../vue.js"></script>
<script src="../vue-router.js"></script>
<script>
    // 4.实例化一个VueRouter
    const router = new VueRouter({
        //5.配置路由表
        //一个地址对应一个组件(模块)
        routes: [
            //动态路由传参
            //定义动态路由参数:companyname
            {
                path: "/company/:companyname/:money",
                //获取参数 组件实例.$route.params ---> 代表所有动态路由参数的集合
                component: {
                    template: `<div>工作想去{{$route.params.companyname}},月薪{{$route.params.money}}</div>`,
                }
            }
        ]
    });
    //6.挂载路由
    var vm = new Vue({
        el: '#app',
        data: {},
        methods: {},
        router
    })
</script>
 ```

#### 5.vue-router-to属性赋值

to 有多种赋值方式 

```html
<!-- 常规跳转 -->
  <!-- <router-link to="/sport">体育</router-link> -->
  <!-- 变量 -->
  <!-- <router-link :to="path">体育</router-link> -->
  <!-- 根据对象name跳转 -->
  <!-- <router-link :to="{name:'abcdefg'}">体育</router-link> -->
  <!-- 根据对象path跳转 -->
  <!-- <router-link :to="{path:'/sport'}">体育</router-link> -->
  <!-- 带参数的跳转 -->
  <router-link :to="{name:'abcdefg',params:{a:1}}">体育</router-link>
```

##### 案例

1. 用vue-router实例化路由 

2. 导航为 北京 上海 

3. 分别采用四种赋值方式 将上海跳转到对应的组件

4. 在北京跳转时 实现 带参数的跳转

    ```html
    <div id="app">
        <!-- 字符串 -->
        <router-link to="/sh">上海</router-link>
        <!-- 变量 -->
        <router-link :to="shStr">上海(变量)</router-link>
        <!-- 对象 -->
        <router-link :to="{path: '/sh'}">上海(对象path)</router-link>
        <!-- 对象 name形式 -->
        <router-link :to="{name: 'abc'}">上海(对象name)</router-link>
        <!-- 带参数的跳转 -->
        <router-link to="/bj/abc">北京(带参数)</router-link>
    
        <router-view></router-view>
    </div>
    
    <script src="../vue.js"></script>
    <script src="../vue-router.js"></script>
    <script>
        const router = new VueRouter({
            routes: [{
                path: "/bj/:cs",
                component: {
                    template: `<div>帝都北京{{$route.params.cs}}</div>`,
                }
            }, {
                name: "abc",
                path: "/sh",
                component: {
                    template: `<div>魔都上海</div>`,
                }
            }]
        });
        //6.挂载路由
        var vm = new Vue({
            el: '#app',
            data: {
                shStr: '/sh'
            },
            router
        })
    </script>
    ```

    

#### 6.vue-router-重定向

> 当希望某个页面被强制中转时  可采用`redirect `进行路由重定向设置

拦截谁 就在谁的路由上写 `redirect`

```js
{
  path: "/sport",
  redirect: "/news", // 强制跳转新闻页
  component: {
    template: `<div>体育</div>`
  }
},
```

案例

```html
<div id="app">
    <router-link to="/bj">北京</router-link>
    <router-link to="/sh">上海</router-link>
    <router-link to="/tj">天津</router-link>
    <router-link to="/cq">重庆</router-link>

    <router-view></router-view>
</div>

<script src="../vue.js"></script>
<script src="../vue-router.js"></script>
<script>
    const router = new VueRouter({
        routes: [{
            path: "/bj",
            component: {
                template: `<div>北京</div>`,
            }
        }, {
            path: "/sh",
            component: {
                template: `<div>上海</div>`,
            }
        }, {
            path: "/tj",
            redirect: "/bj",
            component: {
                template: `<div>天津</div>`,
            }
        }, {
            path: "/cq",
            component: {
                template: `<div>重庆</div>`,
            }
        }]
    });
    //6.挂载路由
    var vm = new Vue({
        el: '#app',
        router
    })
</script>
```



#### 7.vue-router-编程式导航

1. 跳转不同的组件 不仅仅可以用router-link 还可以采用代码行为
2. (Vue实例)this.$router 可以拿到当前路由对象的实例
3. 路由对象的实例方法 有 push  replace, go()  goBack
4. push 方法 相当于往历史记录里推了一条记录 如果点击返回 会回到上一次的地址
5. replace方法 相当于替换了当前的记录  历史记录并没有多 但是地址会变
6. go(数字) 代表希望是前进还是回退,当数字大于0 时 就是前进 n(数字)次,小于0时,就是后退n(数字)次
7. goBack() 代表返回上个页面



##### 案例

1. 实例化一个导航路由
2. 导航为 A, B, C ,D 
3. 实现A => B , B => C, 然后从C返回时,直接回到A
4. 实现A => B ,B => C , C =>D 从D返回时 不能返回
5. 实现A => B ,B => C , C =>D 从D返回直接返回到A 在A中直接前进到D

```html
<div id="app">
    <!-- 导航可以不要,容器必须要 -->
    <router-view></router-view>
</div>
<script src="../vue.js"></script>
<script src="../vue-router.js"></script>
<script>
    const router = new VueRouter({
        routes: [{
            path: "/",
            redirect: '/A'
        }, {
            path: "/A",
            component: {
                template: `<div>
                我是A,我想去B
                <button @click="goB">去吧</button>
                </div>`,
                methods: {
                    goB() {
                        this.$router.push('/B');
                    },
                },
            },
        }, {
            path: "/B",
            component: {
                template: `<div>
                我是B,我想去C
                <button @click="goC">去吧</button></div>`,
                methods: {
                    goC() {
                        this.$router.replace('/C');
                    },
                },
            }
        }, {
            path: "/C",
            component: {
                template: `<div>
                我是C,我想去D
                <button @click="goD">去吧</button></div>`,
                methods: {
                    goD() {
                        this.$router.replace('/D');
                    },
                },
            }
        }, {
            path: "/D",
            component: {
                template: `<div>
                我是D,我想去A
                <button @click="goA">去吧</button></div>`,
                methods: {
                    goA() {
                        this.$router.go(-1);
                    },
                },
            }
        }]
    });
    //6.挂载路由
    var vm = new Vue({
        el: '#app',
        router
    })
</script>
```



#### 8.vue-router-routerlink-tag-激活样式

> 当前路由在导航中是拥有激活class样式的

1. 审查导航元素,可以发现 激活样式

```html
<a href="#/news" class="router-link-exact-active router-link-active">新闻</a>
```

2. 设置激活class样式即可

```css
.router-link-active {
    //css样式
}
```



##### 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>19-vue-router-激活样式</title>
    <style>
        .router-link-active {
            font-size: 48px;
            font-weight: 700;
            color: coral;
        }
    </style>
</head>
<body>
    <div id="app">
        <router-link to="/bj">北京</router-link>
        <router-link to="/sh">上海</router-link>
        <router-link to="/tj">天津</router-link>
        <router-link to="/cq">重庆</router-link>

        <router-view></router-view>
    </div>
    <script src="../vue.js"></script>
    <script src="../vue-router.js"></script>
    <script>
        const router = new VueRouter({
            routes: [{
                path: "/bj",
                component: {
                    template: `<div>北京</div>`,
                }
            }, {
                path: "/sh",
                component: {
                    template: `<div>上海</div>`,
                }
            }, {
                path: "/tj",
                component: {
                    template: `<div>天津</div>`,
                }
            }, {
                path: "/cq",
                component: {
                    template: `<div>重庆</div>`,
                }
            }]
        });
        var vm = new Vue({
            el: '#app',
            router
        })
    </script>
</body>

</html>
```



#### 9.vue-router-嵌套路由

1. 如果存在`嵌套路由`,就需要提供多个视图容器`<router-view></router-view>`
2. 同时`router-link`和`router-view`都可以添加类名、设定样式

##### 案例

1. 实现一个嵌套路由   
2. 第一级路由为 热点 教育 社会 音乐
3. 音乐下 二级路由为 流行.古典.爵士

```html
<div id="app">
    <router-link to="/hot">热点</router-link>
    <router-link to="/edu">教育</router-link>
    <router-link to="/soc">社会</router-link>
    <router-link to="/music">音乐</router-link>
    <router-view></router-view>
</div>

<script src="../vue.js"></script>
<script src="../vue-router.js"></script>
<script>
    const router = new VueRouter({
        routes: [{
            path: "/",
            redirect: "/hot"
        }, {
            path: "/hot",
            component: {
                template: `<div>热点</div>`,
            }
        }, {
            path: "/edu",
            component: {
                template: `<div>教育</div>`,
            }
        }, {
            path: "/soc",
            component: {
                template: `<div>社会</div>`,
            }
        }, {
            path: "/music",
            //二级路由的导航和容器
            component: {
                template: `<div>
                音乐
                <router-link to="/music/lx">流行</router-link>
                <router-link to="/music/gd">古典</router-link>
                <router-link to="/music/js">爵士</router-link>
                <router-link to="/music/gf">古风</router-link>
                <router-view></router-view>
                </div>`,
            },
            children: [{
                path: "", //什么都不写就是二级路由的默认显示组件
                component: {
                    template: `<div>我是默认的二级路由内容</div>`,
                }
            }, {
                path: "/music/lx",
                component: {
                    template: `<div>流行</div>`,
                }
            }, {
                path: "/music/gd",
                component: {
                    template: `<div>古典</div>`,
                }
            }, {
                path: "/music/js",
                component: {
                    template: `<div>爵士</div>`,
                }
            }, {
                path: "/music/gf",
                component: {
                    template: `<div>古风</div>`,
                }
            }]
        }]
    });
    var vm = new Vue({
        el: '#app',
        router
    })
</script>
```

**注意:以/开头的嵌套路径会被当做根路径,这让你充分的使用嵌套组件而无需设置嵌套的路径**



### 五.总结

1. 组件
    1. 重复的页面结构/重复的数据/重复的逻辑
    2. 局部注册/全局注册
        1. 全局注册:`Vue.component(组件名,组件对象)`
            1. 组件名:全小写的abc或者abc-d
            2. 任意的Vue或者组件实例都可以使用
        2. 局部组件
            1. 当前实例(Vue实例/组件实例) `components:{组件名:组件对象}`
    3. 组件特点:
        1. 一个特殊的Vue实例
            1. 没有el选项
            2. 必须有template选项
                1. 指的是页面结构
                2. 有且只有一个根节点
        2. data是带返回值的函数
            1. 组件实例n个,每个实例被创建的时候调用data方法
            2. 返回一个新对象
            3. 组件实例是独立运行作用域
        3. Vue实例有的组件都有 包括`components`
    4. 组件嵌套:
        1. 组件模块中使用了其它组件
        2. Vue实例 div视图使用组件
        3. 只要嵌套就会生成父子关系
            1. 父子组件传值
                1. 父传子
                    1. 定义属性(给谁传值就在谁的标签上写属性)
                        1. Vue实例也是组件的父级
                    2. 接收属性
                        1. 用props接收属性[属性名1,属性名2...]
                    3. 使用属性
                        1. this指向当前组件实例this.属性
                        2. 可以拿到data中所有的数据,methods所有的方法,computed中所有的属性
                        3. 也可以拿到props传过来的所有属性
                            1. 插值表达式{{props属性名称}}
    5. SPA
        1. 优点:速度快,体验好,组件化开发
        2. 缺点:首屏加载慢,SEO不友好,开发成本高
        3. SPA前端路由实现原理
            1. hash值改变,不刷新页面
            2. js实现纯前端路由
    6. 路由
        1. vue-router
            1. 引入js
            2. 定义导航(不是必须)
            3. 定义容器(必须)
            4. 实例化路由
            5. 配置路由表 
                1. 一个地址对应一个组件
            6. 挂载在Vue实例上
                1. router:router ---> es6简写 : router
        2. 动态路由
            1. 多个地址对应同一个组件
                1. 定义参数 `{path:"/user/:参数名"}`
                2. 传递参数`<router-link to="user/123"></router-link>`
                3. `$route.params`:所有动态路由参数的集合
                    1. `$route.params.参数名`
            2. to属性赋值
                1. 字符串
                2. 变量
                3. 对象
                    1. path形式
                    2. name形式
                4. 带参数
        3. 重定向`redirect`
            1. 拦截谁就在谁的路由上写`redirect`
        4. 编程式导航
            1. 导航可以不要,容器必须要
            2. 代码导航
                1. `this.$router(路由实例对象).push/replace/go()`
        5. 嵌套路由
            1. 一级路由
            2. 二级路由
            3. 一级路由的组件里写二级路由的导航和容器
                1. 一级路由的路由表里`children`配置二级路由表