# 就业阶段10 day01 vue.js基础

### 一.vue介绍

> Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建**用户界面（User Interface）**的渐进式框架

Vue 的核心库只关注**视图层**，与现代化的工具链（Webpack）以及各种支持类库（Babel、TypeScript）结合使用时，Vue 也完全能够为复杂的单页应用提供驱动
所谓用户界面对于Web开发者来说就是一个网页，也称为视图层。
**学习 Vue 其实是以一种全新的方式编写网页。**
**Vue 其实就是一个封装了大量逻辑的 Javascript 文件**


#### 1.安装

1. [下载](https://cn.vuejs.org/js/vue.js)
2. CDN https://cdn.jsdelivr.net/npm/vue/dist/vue.js
    1. CDN缓存技术
3. npm 仓库

#### 2.体验

```html
<p v-show='false'>这是一段文本</p>
<input type="hidden">
<script src="../vue.js" type=""></script>
<script>
    //当引入vue.js之后,会得到一个全局的构造函数Vue
    //1.需要对这个构造函数进行实例化
    //2.接受一个对象作为参数

    //通过vue自定义的属性可以控制元素,例如将p标签隐藏
    new Vue({
        el: 'p'
    });
</script>
```

写在标签上的属性 ---> 标签属性 

`v-`开头的属性都是Vue提供的

### 二.基础

学习 vue 主要就是掌握 vue 的语法

#### 1.实例化

当在页面中引入 vue 后，便会得到全局的构造函数 `Vue`，**需要对这个构造函数进行实例化** `new Vue({})`



#### 2.视图 --->el

通过 vue 提供的属性，如 `v-if` ，可以丰富页面的逻辑控制，**但是它只能在一定的“范围”才可以生效，我们称这部分为View，即视图层 。** 

**注：将 el 指定的区域称为视图并不严禁，准确一点儿应该叫模板，不过初学者不必细究。**

```html
<!-- el所對應的元素,不可以是html或者body -->
<div id="app">
    <!-- 屬性值為布爾類型時,一般不寫值默認為true -->
    <!-- v-show 如果不添加任何值 默認是false -->
    <p v-show='seen'>div一段文本</p>
    <!-- 'seen'其实就是js里面的表达式 -->
    <p v-text='msg'>div一段文本</p>
    <p>{{msg}}</p>
    <!-- 將數據展示帶標籤內部{{}}和v-text均可 
        {{}}渲染页面会闪烁:先加载html后加载vue.js
    -->
    <p>{{1+1}}</p>
    <!-- 一般在實踐中不建議(不應該)過渡依賴默認值 -->
</div>
<!-- 下面這些v-show都沒有生效 -->
<div>
    <p v-show='false'>div2一段文本</p>
</div>
<p></p>
<ul>
    <p v-show='false'>ul一段文本</p>
</ul>

<input type="hidden">
<script src="../vue.js" type=""></script>
<script>
    //当引入vue.js之后,会得到一个全局的构造函数Vue
    //1.需要对这个构造函数进行实例化
    //2.接受一个对象作为参数

    //通过vue自定义的属性可以控制元素,例如将p标签隐藏
    new Vue({
        //el的值可以是选择器,建议使用id选择器
        //如果選擇器選中的元素有多個,只對第一個生效
        //el的值也可以是dom對象
        // el: 'div'
        // el: document.querySelectorAll('div')[1]
        el: '#app',
        data: {
            seen: false,
            msg: '一段被顯示在視圖中的文本'
        }
    });
</script>
```

vue 可以只针对页面中的某个DOM元素产生效果，所以**Vue 可以与其它前端技术整合。**



#### 3.模型 --->数据 --->data

​		一个**网页的核心是数据**，html 和 css 只是负责将这些数据以较为美观的形式展示，**Vue 可以对页面所承载的数据进行管理，我们称之为 Model，即模型。**

```html
<div id="app">
    <p v-text='msg'>div一段文本</p>
    <p>{{msg}}</p>
    <!-- 將數據展示帶標籤內部{{}}和v-text均可 
        {{}}渲染页面会闪烁:先加载html后加载vue.js
    -->
    <p>{{1+1}}</p>
</div>
<script src="../vue.js" type=""></script>
<script>
    new Vue({
        //el的值可以是选择器,建议使用id选择器
        //如果選擇器選中的元素有多個,只對第一個生效
        //el的值也可以是dom對象
        // el: 'div'
        // el: document.querySelectorAll('div')[1]
        el: '#app',
        data: {
            msg: '一段被顯示在視圖中的文本'
        }
    });
</script>
```

- 实例化 Vue 时，通过 `data` 可以为 `el` 所对应的 DOM 初始数据，其中数据类型可以为任意合法的 Javascript 数据类型。

- `{{}}` 是 Vue 中特殊的语法符号，用于将 `data` 中的数据插入到视图层元素的内容区域（innerHTML）。



#### 4.数据绑定

数据绑定是 vue 中非常高级的特性，它是指将**视图层DOM元素与模型层中的数据建立一一对应的联系**，将这种联系称为数据绑定。

DOM 元素一般包含**属性节点**和**文本节点**,所以 vue 中实现数据绑定主要体验在两个方面:

##### 1.属性节点绑定

1. `v-bind:属性名='值'` 是实现属性节点绑定的语法格式。
2. `class` 和 `style` 是DOM元素中比较重要的两个属性。
    1. class:`v-bind:class`接受一个对象类型数据
        1. 对象的属性为真实存在的类名
        2. 对象的值为布尔类型
            1. 如果为true 则添加属性对应的类名
            2. 如果为false 则不添加
    2. style:`v-bind:style`接受一个对象类型数据
        1. 这个对象的内容是css代码,比如`{color:'red',width:'100px'}`
3. `v-bind:属性名` 可以被简写为 `:属性名`
4. 支持 Javascript 表达式
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>04-数据绑定-属性绑定</title>
    <style>
        .demo {
            color: brown;
        }
        
        .text {
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div id="app">
        <!-- 在vue中對屬性進行數據綁定時使用v-bind:屬性名='值' -->
        <p v-bind:title="title">{{msg}}</p>
        <p :title="title">{{msg}}</p>
        <!-- v-bind:style語法相對特殊一些,接受一個對象類型數據 -->
        <!-- 這個對象的內容都是css的代碼,{color:'red',width:'100px'} -->
        <p :style="{color:'skyblue'}">我是一段帶顏色的文本</p>
        <p :style="styleObject">我是一段帶顏色的文本</p>
        <!-- v-bind:class語法相對特殊一些 接受一個對象類型數據
            對象的屬性為真實存在的類名
            對象的值為布爾類型
         -->
        <p :class="{demo:true,text:true}">一段文本</p>
    </div>

    <script src="../vue.js" type=""></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                title: 'vue的屬性綁定',
                msg: '一段被顯示在視圖中的文本',
                styleObject: {
                    color: 'red',
                    backgroundColor: 'pink'
                }
            }
        });
    </script>
</body>

</html>
```


##### 2.文本节点绑定

1. `{{}}` 是实现文本节点绑定的语法格式
2. `v-text` 一般认为是 `{{}}` 的另一种写法，相当于原生 DOM 中的  `innerText`
3. `v-html` 在渲染时能够解析文本的 `html` 标签，相当于原生 DOM 中的 `innerHTML`
4. 支持 Javascript 表达式
    1. 用中括号来访问数组中的单元
    2. 用.属性来访问对象中的值
    3. 用[属性]访问对象中的值

```html
<body>
    <div id="app">
        <p v-text='msg'></p>
        <p>{{msg}}</p>
        <!-- v-html相當於innerHtml -->
        <p v-html='html'></p>
        <p>{{html}}</p>
        <p>{{a+b}}</p>
        <p>{{list}}</p>
        <!-- 支持中括號來訪問數組的單元 -->
        <p>{{list[0]}}</p>

        <p>{{user}}</p>
        <p>{{user.name}} --- {{user.age}}</p>
        <p>{{user['name']}}</p>
    </div>

    <script src="../vue.js" type=""></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                msg: '一段文本',
                html: '<h3>帶著標籤的文本</h3>',
                a: 10,
                b: 5,
                list: ['pink', 'red', 'blue', 'green'],
                user: {
                    name: '軒銘',
                    age: '24'
                }
            }
        });
    </script>
</body>
```






##### 3.事件绑定

1. 事件可以认定为DOM元素的属性，如 `<a href="javascript" onclick="clicked">点击</a>`，但是由于其特殊含义 vue 中将它与其它属性区别对待。

2. `v-on:事件名="回调函数"` 是为添加事件监听的语法格式

    ```html
    <div id="app">
        <!-- vue中添加事件監聽的語法格式為 v-on:原生事件名稱='回調函數' -->
        <a href="JavaScript:;" v-on:click='clicked'>點擊</a>
    </div>
    ```

3. 回调函数定义在 Vue 实例中的 `methods` 中

    1. 当data中定义了methods中相同的属性
    2. 以data为准,methods不允许重复
    3. methods中定义的方法,不允许使用箭头函数
    
    ```js
    <script>
        new Vue({
            el: '#app',
            //vue提供的專門定義方法的參數
            //也可以定義事件的回調
            methods: {
                //事件回調
                clicked: function() {
                    //事件被觸發,回調就被執行
                    console.log('元素被點擊了');
                }
            }
        });
    </script>
    ```



**`v-on:事件名="回调函数"` 可以被简写为 `@事件名="回调函数"`**

```html
<div id="app">
    <!-- vue中添加事件監聽的語法格式為 v-on:原生事件名稱='回調函數' -->
    <a href="JavaScript:;" v-on:click='clicked'>點擊</a>
    <input type="text" v-on:focus='focus' @blur='blur'>
</div>

<script src="../vue.js" type=""></script>
<script>
    new Vue({
        el: '#app',
        //vue提供的專門定義方法的參數
        //也可以定義事件的回調
        methods: {
            //事件回調
            clicked: function() {
                //事件被觸發,回調就被執行
                console.log('元素被點擊了');
            },
            focus: function() {
                //事件被觸發,回調就被執行
                console.log('獲得焦點了');
            },
            blur: function() {
                //事件被觸發,回調就被執行
                console.log('失去焦點了');
            },
        }
    });
</script>
```



4. `v-on:事件="回调函数($event)"`  $event 做为参数传递时具有特殊含义，用它获得事件对象

    ```HTML
    <div id="app">
        <!-- vue中添加事件監聽的語法格式為 v-on:原生事件名稱='回調函數' -->
        <!-- 
            當事件被觸發時,可以將事件對象以參數形式傳遞
            $event 在 vue 中是具有特殊函數的內容,表示事件對象
         -->
        <a href="JavaScript:;" v-on:click='clicked($event)'>點擊</a>
    
    <script src="../vue.js" type=""></script>
    <script>
        new Vue({
            el: '#app',
            //vue提供的專門定義方法的參數
            //也可以定義事件的回調
            methods: {
                //事件回調
                clicked: function(e) {
                    //事件被觸發,回調就被執行
                    console.log('元素被點擊了');
                    //e是傳過來的事件對象
                    console.log(e);
                    //e.target是原生DOM
                    e.target.style.color = 'red';
                },
            }
        });
    </script>
    ```

    

5. `v-on:事件名.修饰符="回调函数"` 通过添加修饰符来实现事件的特殊处理，如事件冒泡,获取按键信息等

    ```html
    <div id="app">
        <!-- 父子嵌套的盒子 -->
        <div class="parent" @click="parent" :style="{backgroundColor:'pink',width:'300px',height:'300px'}">
            <!-- 
                在vue中,通過修飾符來解決事件執行時的一些特殊邏輯問題
                比如:阻止冒泡/獲取按鍵信息
                語法格式:在事件名稱後添加.符號 即為修飾符
                v-on:事件名.修飾符="函數"
             -->
            <div class="child" @click.stop="child" :style="{backgroundColor:'skyblue',width:'200px',height:'200px'}"></div>
        </div>
    
        <!-- 點擊回車才會觸發 -->
        <input type="text" @keyup.13="send">
        <!-- 點擊回車+shift觸發 -->
        <input type="text" @keyup.13.shift="send">
    </div>
    
    <script src="../vue.js" type=""></script>
    <script>
        new Vue({
            el: '#app',
            methods: {
                parent: function() {
                    console.log('parent');
    
                },
                child: function() {
                    console.log('child');
    
                },
                send: function() {
                    console.log('發送了');
    
                }
            }
        });
    </script>
    ```

    

##### 4.响应式数据绑定

关于响应式可以理解成一种**自动机制**，即一方发生改变后，另一方也相应做出改变。具体在 vue 中，是指当模型 (data) 中的数据被改变后，所对应的视图区域也会相应改变，而这一切又都是自动完成的

1. 实例化对象可以直接访问模型中的数据
2. 还可以直接访问methods中的方法
    1. this指向实例化对象

```html
<div id="app">
    <h1>{{msg}}</h1>
    <button @click="changeData">更改一個數據,視圖自動變化</button>
</div>

<script src="../vue.js" type=""></script>
<script>
    // 實例化對象可以直接訪問模型(data)中的數據
    // vm.xxx
    //還可以直接訪問methods中的方法
    let vm = new Vue({
        el: '#app',
        data: {
            msg: '初始的文本信息',
        },
        methods: {
            //事件回調
            changeData: function() {
                //this指向vm實例
                this.msg = '我是新數據';
                this.demo();
            },
            demo: function() {
                console.log('一個方法');
            }
        }
    });
</script>
```



##### 5.双向数据绑定

数据绑定有单向和双向之分，具体是指数据的流向。

1. 单向，模型 ------> 视图
2. 双向，模型 <------> 视图

表单元素在 html 中具体特殊意义，它的主要作用并不是展示数据，更多的是收集用户填写的数据，因此表单元素也就成为了数据的提供方了，通过修改表单中的内容，实现模型中 data 数据的变化。

为表单元素添加 `v-model` 可以实现数据的双向绑定。

```html
<div id="app">
    <h1>{{txt}}</h1>
    <input type="text" v-model="txt">
    <button @click="checkData">看看數據變了沒</button>
</div>

<script src="../vue.js" type=""></script>
<script>
    // 實例化對象可以直接訪問模型(data)中的數據
    // vm.xxx
    //還可以直接訪問methods中的方法
    let vm = new Vue({
        el: '#app',
        data: {
            txt: ''
        },
        methods: {
            checkData: function() {
                console.log(this.txt);
            }
        }
    });
</script>
```



#### 5.结构

动态网站的页面结构是根据数据展示的需要动态创建的，**vue 具备动态创建页面结构的能力。**

##### 1.条件控制

1. `v-if`

    ```html
    <div id="app">
        <!-- 根据 seen 取值，添加/移除 p 元素 -->
        <p v-if="seen" @click="toggle">你能见我吗？</p>
    </div>
    
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                seen: true
            },
            methods: {
                toggle: function() {
                    // 修改seen的值
                    this.seen = false;
                }
            }
        })
    </script>
    ```

    

2. `v-else`

    ```html
    <div id="app">
        <p>
            大家好，我叫{{name}}，我今年{{age}}岁了，我是
            <span v-if="age >= 18">成年</span>
            <!-- 条件判断 -->
            <span v-else>未成年</span> 人。
        </p>
    </div>
    
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                name: '小明',
                age: 18,
            }
        })
    </script>
    ```

    

3. `v-else-if`

    ```html
    <div id="app">
        本次考试成绩为{{score}}分，成绩等级为
        <span v-if="score >= 80">优秀</span>
        <!-- 条件判断 -->
        <span v-else-if="score >= 70">良好</span>
        <span v-else>及格</span>。
    </div>
    
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                score: 75
            }
        })
    </script>
    ```

    

4. `v-show`

    ```html
    <div id="app">
        <!-- 根据 seen 取值，添加/移除 p 元素 -->
        <p v-if="seen" @click="toggle">你能见我吗？</p>
    
        <!-- 根据 seen 取值，显示/隐藏 p 元素 -->
        <p v-if="seen" @click="toggle">你能见我吗？</p>
    </div>
    
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                seen: true
            },
            methods: {
                toggle: function() {
                    // 修改seen的值
                    this.seen = false;
                }
            }
        })
    </script>
    ```

5. `v-if`和`v-show`的区别:

    1. `v-if` 和 `v-show` 在视觉效果上是一致的，然而其实现是有差异的
    2. `v-if` 是通过添加/移除 DOM 节点实现
        1. `v-if` 会导致 DOM 树中，节点数量变化，开销方面会更大一些
    3. `v-show` 是通过 css 的 display 属性值（block/none）实现
        1. `v-show` 并不影响DOM中节点数量变化，开销相对低一些
    4. 对于操作较为频繁的显示/隐藏操作，建议使用 `v-show`，相反建议使用 `v-if`
    5. 另外 `v-if` 是惰性的，如果其值为假，则内部所有元素都不会被渲染

##### 2.列表控制

1. `v-for` 实现数组/对象类型数据的遍历

    ```html
    <div id="app">
        <table>
            <tr>
                <th>序号</th>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
            <!-- student 和 index 分别可以获取被遍历数据的单元值和索引值 -->
            <!-- <tr v-for="(student, index) in students"> -->
            <!-- 也可以使用 of 实现遍历操作 -->
            <tr v-for="(student, index) of students">
                <td>{{index+1}}</td>
                <td>{{student.name}}</td>
                <td>{{student.gender}}</td>
                <td>{{student.age}}</td>
            </tr>
        </table>
        <div class="box">
            <!-- 对象数据遍历，u 为对象的 属性值，i 为 对象的 属性 -->
            <span v-for="(u, i) of user">{{i}} => {{u}}</span>
        </div>
    </div>
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                user: {
                    name: '小明',
                    age: 18
                },
                students: [{
                        name: '小明',
                        gender: '男',
                        age: 18
                    }, {
                        name: '小红',
                        gender: '女',
                        age: 17
                    }
                ]
            }
        })
    </script>
    ```
    

    
2. `key` 管理可复用的元素

    Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染