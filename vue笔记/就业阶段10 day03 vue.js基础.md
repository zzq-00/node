# 就业阶段10 day03 vue.js基础

### 一.介绍

>Vue.js (读音 /vjuː/，类似于 view) 是一套构建用户界面的渐进式框架。
>与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。
>Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。
>另一方面，当与单文件组件和 Vue 生态系统支持的库结合使用时，Vue 也完全能够为复杂的单页应用程序提供驱动。

- Vue本身只是一个用于数据驱动视图更新的库
- 操作视图的方式
    - 直接操作DOM
    - jquery(封装了DOM操作),提高了操作DOM的效率
    - Vue.js
        - MVVM(数据驱动视图的方式)
        - 面向数据式编程
- 可以轻松构建**SPA应用程序**(单页面应用程序)
- 核心特点:
    - 通过**数据操作视图更新**,解放了DOM操作
    - **组件化开发**提高了开发的效率和可维护性
- 建议:把官方的学习教程看至少两遍

### 二.像使用模板引擎一样使用vue

1. 怎么更新视图:
    1. 原生js操作DOM(麻烦)
    2. jquery(稍微好点)
    3. 模板引擎(更好一些)
    4. Vue ---> 更高级的模板引擎
2. 步骤:
    1. 安装
        1. 不兼容IE8以下的版本
    2. 创建Vue
    3. 根据视图抽象data数据
    4. 能用Vue的语法把数据绑定到视图中
3. 使用Vue
    1. 初始化data数据
    2. 把数据根据vue的特定语法绑定到视图中
    3. 然后通过修改data的数据从而影响视图更新

### 三.vue实例

每个Vue应用都是通过vue函数创建一个新的vue实例开始的

```js
var vm = new Vue({
  // 选项
})
```

当创建一个Vue实例时,你看也能传入一个`选项对象`,使用这些选项来进行你想要的行为

例如：

- el
- data
- methods
- watch
- computed
- ....

不同的选项具有不同的作用

#### 1.实例选项-el

1. 不能是html,body节点
2. el只能作用在单一节点上

#### 2..实例选项-data

data不是普通的数据,这种数据称之为**响应式数据**,**用来驱动视图层里面更新的数据**

1. 模板中访问的数据必须初始化到data中
2. 模板无法访问Vue实例之外的数据

```js
const app = new Vue({
  /**
   * 告诉 Vue 管理视图的入口
   */
  el: '#app',
  /**
   * 这个 data 就好比之前使用 art-template 模板引擎的数据一样的
   * 我们可以直接在被 Vue 管理的视图中使用 data 中的数据绑定
   */
  data: {
    message: 'Hello Vue.js!',
    user: {
      name: '张三',
      age: 18,
      gender: 0 // 0 男，1 女
    },
    todos: ['吃饭', '睡觉', '打豆豆'],
    count: '',
    num: 0, // 数字
    str: '', // 字符串
    isSeen: false, // 布尔值
    arr: [], // 空数组
    /**
     * 对于对象的修改
     * 1. 没有初始化的对象成员如果修改不会更新视图
     * 2. 也有方式可以动态添加未初始化的数据成员并且能更新视图（后面说）
     * 3. 直接对对象进行重新赋值可以实现视图更新
     *   xxx = 新的数据对象，例如 app.obj = { a: 123 }
     * 建议：最好把所有需要的数据都初始化到 data 中来
     */
    obj: {
      // a: 0
    } // 对象，没有初始化的对象成员如果修改不会更新视图
  }
})
```



### 四.模板语法-插值

#### 1.文本

数据绑定最常见的形式就是使用"Mustache"语法(双大括号)的文本插值

```html
<h1>{{message}}</h1>
<p>姓名:{{user.name}}</p>
<p>年龄:{{user.age}}</p>
```

#### 2.JavaScript表达式

> `{{}}`可以有一些简单的JavaScript逻辑运算

````html
<p>{{ number + 1 }}</p>
<p>性别:{{ user.gender === 0?'男':'女' }}</p>
<p>性别:{{ massage.split('').reverse().join('') }}</p>
````

#### 3.属性:

```html
<p v-bind:title:"message">花括号不能直接使用在属性中</p>
<a v-bind:href="url">去百度</a>
```

简写:

```html
<p :title:"message">花括号不能直接使用在属性中</p>
<a :href="url">去百度</a>
```

属性值中的写法和{{}}中的写法一样,也可以写简单的JavaScript运算表达式

```html
<p :title:"massage.split('').reverse().join('')">hello world</p>
<p :title:"1 + 1">属性中的表达式</p>
<p :title:"number + 1 > 10 ? 'number大于10' : 'number小于10'">属性中的表达式</p>
```

> `{{}}`怎么写,`v-bind`属性绑定也怎么写

#### 4.对于对象的修改:

1. 没有初始化的对象成员如果修改不会更新视图
2. 也有方式可以动态添加未初始化的数据成员并且能更新视图
3. 直接对对象进行重新赋值可以实现视图更新
    1. xxx.新的数据对象, 例如 app.obj = { a:123 }

#### 5.原始html字符串

```html
<div>{{htmlStr}}</div>
<!-- 使用v-html指令渲染html标签内容字符串 -->
<div v-html="htmlStr"></div>
```

> v-html中绑定的html内容数据不能使用数据绑定



### 五.列表渲染

#### 1.遍历数组

html:

```html
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

js:

```js
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
})
```

#### 2.数组的更新

常见的数组操作方法都会正常的进行视图的更新
$$ {数组的操作方法}
posh()
pop()
shift()
unshift()
splice()
sort()
reverse()
$$
或者直接对数组进行重新赋值:

```js
实例.数组=新的数组
```

注意:以下两种情况不会更新视图

1. 利用索引直接设置一个数组项时:`vm.items[indexOfItem] = newValue`
2. 修改数组的长度时:`vm.items.length = newLength`

解决方法:

1. 问题1:使用Vue中提供的==Vue.set==方法解决

    ```js
    //Vue.set
    //参数1:实例的数组
    //参数2:索引
    //参数3:你要修改的数组新值
    Vue.set(vm.items,indexOfItem,newValue)
    ```

2. 官网了解

#### 3.遍历对象

遍历值：

```html
<p v-for="value in user">{{ value }}</p>
```

带有值+属性名：

```html
<p v-for="(value, key) in user">{{ key }} -- {{ value }}</p>
```

遍历值+属性名+索引：

```html
<p v-for="(value, key, index) in user">{{ index }} -- {{ key }} -- {{ value }}</p>
```

#### 4.对象的更新

已知实例中data的数据

```js
const app = new Vue({
    el: '#app',
    data: {
        message: 'hello vue.js',
        user: {
            //初始化了的都可以正常的更新
            name: '张三',
            age: 18,
            //没有初始化的不能直接修改数据更新视图,例如 app.user.gender = '男'
        },
    }
})
```

常规方式修改对象数据更新视图

```js
app.user.name = '小红'  //可以更新
app.user.gender = '女'  //不会更新,因为gender没有初始化
app.user = { name:"小红", age:18, gender:"女" }  //可以更新
```

如果想要动态添加一个可以更新视图的对象成员数据

```js
//Vue.set
//参数1:实例的数据对象
//参数2:属性名
//参数3:属性值
Vue.set(vm.user,'age',27)
```

> 一个建议就是最好都把数据提前初始化好

#### 5.v-for和key

当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。这个类似 Vue 1.x 的 `track-by="$index"`。

这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 `key` 属性：

```html
<div v-for="item in items" v-bind:key="item.id">
  <!-- 内容 -->
</div>
```

建议尽可能在使用 `v-for` 时提供 `key` attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

因为它是 Vue 识别节点的一个通用机制，`key` 并不仅与 `v-for` 特别关联。后面我们将在指南中看到，它还具有其它用途。



注意:

1. **key必须是数字或者字符串,表示唯一,不能是数组或者对象**
2. 不要使用遍历索引 index 作为唯一的 key 值，会有问题
3. 一般使用数据中能表示唯一的那个字段，例如id

#### 6.值范围遍历

> `v-for`也可以接受整数,在这种情况下,它会把模板重复对应次数

```html
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
```



#### 7.在template上使用v-for

> 当需要遍历多个元素而不又不想增加额外的元素节点的时候,可以结合Vue中提供的==template==遍历渲染

```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```





### 六.条件渲染

####  1.v-if

> 根据绑定数据的真假来决定是否渲染这个数据

```html
<h1 v-if="awesome">Vue is awesome!</h1>
```



#### 2.v-else,v-else-if

> 结合v-else进行判定
>
>  `v-else-if`，顾名思义，充当 `v-if` 的“else-if 块”，可以连续使用 

```html
<p v-if="1 === 1">哈哈哈</p>
<p v-else>world</p>
```

**`v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别**

**类似于 `v-else`，`v-else-if` 也必须紧跟在带 `v-if` 或者 `v-else-if` 的元素之后**

#### 3.v-show

> 另一个用于根据条件展示元素的选项是 `v-show` 指令,用法和`v-if`大致一样 

```html
<h1 v-show="ok">Hello!</h1>
```



#### 4.v-if和v-show的区别

1. v-if 条件渲染，如果条件为  false，则不渲染元素
    1. true 渲染 DOM
    2. false 不渲染 DOM
2. v-show 条件显示，无论条件的真假始终都渲染元素
    1. true 渲染 DOM
    2. false 渲染 DOM，不显示（display: none）
    3. 不能和 v-else、v-else-if 结合使用

> 一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好

#### 5.v-if和template

> 当你想要控制多个同级元素的渲染又不想增加额外的节点的时候,可以结合template,最终渲染结果中不会包含template元素

```html
<template v-if="seen">
  <p>hello1</p>
  <p>hello2</p>
</template>
```



注意:**在template元素上使用`v-show`无效**

### 七.事件处理

#### 1.基本语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <!-- 
      v-on:事件名称="处理函数"
      onclick
      事件名称就使用原生的那个事件名称。
     -->
    <button v-on:click="onClick">测试</button>

    <!-- 技巧：原生的怎么写，只需要把 on 替换为 v-on: -->
    <!-- <input type="text" v-on:keydown=""> -->
    <!-- <input type="text" v-on:keyup=""> -->

    <!-- 
      v-on 可以简写
      提示：在 Vue 中，有且之后 v-bind 和 v-on 有简写，其它都没有
        v-bind :
        v-on   @
     -->
    <!-- <input type="text" @keydown=""> -->
    <!-- <input type="text" @keyup=""> -->
  </div>
  <script src="node_modules/vue/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue.js!'
      },
      /**
       * 实例选项 methods，存储模板中使用的方法
       */
      methods: {
        // ECMAScript 6 简写方式
        // 等价于 onClick: function () {}
        // 注意：仅仅是简写而已，和箭头函数没关系
        onClick () {
          window.alert('hello')
        }
      }
    })
  </script>
</body>
</html>
```



#### 2.函数简写

v-on:事件名称 ---> @事件名称

#### 3.指令简写

v-bind:属性  ---> :属性

#### 4.处理函数中的this

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <button @click="onClick">测试</button>
    <button @click="onClick2">测试2</button>
  </div>
  <script src="node_modules/vue/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue.js!'
      },
      methods: {
        onClick () {
          // 事件处理函数中的 this 指向的是 Vue 实例对象，也就是 app
          // 注意：事件处理函数不能使用箭头函数定义
          console.log(this === app)

          this.message = 'hello'
        },

        // 注意：箭头函数定义的 methods 其中的 this 指向的是 window
        // 除非你不需要在函数中访问 Vue 实例 this，你可以定义箭头函数
        // 何必呢？
        onClick2: () => {
          console.log(this)
        }
      }
    })
  </script>
</body>
</html>
```

注意:

1. 事件处理函数中的 this 指向的是 Vue 实例对象
2. 事件处理函数不能使用箭头函数定义
    1. 箭头函数定义的 methods 其中的 this 指向的是 window



#### 5.模板中简写

当处理函数**只有一句代码**的时候，我们可以直接写到模板中

**注意：这里不需要加 this**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <button @click="onClick">测试</button>

    <!-- 
      当处理函数只有一句代码的时候，我们可以直接写到模板中
      注意：这里不需要加 this
     -->
    <button @click="message = 'hello'">测试</button>
  </div>
  <script src="node_modules/vue/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue.js!'
      },
      methods: {
        onClick () {
          this.message = 'hello'
        }
      }
    })
  </script>
</body>
</html>
```



#### 6.自定义传参

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <ul>
      <!-- 
        没有参数，就直接  @click="onShow"
        有参数，就调用传参 @click="onShow(item.title)"
       -->
      <li
        v-for="item in todos"
        :key="item.id"
        @click="onShow(item.title)"
      >
        {{ item.title }}
      </li>
    </ul>
  </div>
  <script src="node_modules/vue/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue.js!',
        todos: [
          { id: 1, shenfenzheng: 'dnsjadl', title: '吃饭1' },
          { id: 2, shenfenzheng: '123', title: '吃饭2' },
          { id: 3, shenfenzheng: 'dnsandlksa', title: '吃饭3' },
          { id: 4, shenfenzheng: 'dsnaklndlksa', title: '吃饭4' }
        ]
      },

      methods: {
        onShow (title) {
          window.alert(title)
        }
      }
    })
  </script>
</body>
</html>
```



#### 7.函数的默认参数event

> 事件处理函数默认接收一个参数:事件对象

和之前接触的事件对象是一样的

```html
<div id="app">
    <h1>{{message}}</h1>
    <button @click="onclick">测试</button>

    <!-- 如果你给事件自定义传参了,那么默认参数event就没了 -->
    <button @click="onclick2(123)">测试</button>
    <!-- 如果事件绑定时候使用了自定义传参,还想使用默认的event事件对象 -->
    <button @click="onclick3(456,$event)">测试</button>
</div>


<script src="../vue.js"></script>
<script>
    const vm = new Vue({
        el: '#app',
        data: {
            message: '学习Vue'
        },
        methods: {
            //事件处理函数默认接受一个参数:事件对象
            //这个事件对象和我们以前接触的那个事件对象是一样的
            onclick(e) {
                console.log(e);
            },
            onclick2(e) {
                console.log(e);
            },
            onclick3(num, e) {
                console.log(num, e);
            },
        }
    })
</script>
```



#### 8.事件修饰符

> 在事件处理程序中调用 `event.preventDefault()` 或 `event.stopPropagation()` 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节 

 为了解决这个问题，Vue.js 为 `v-on` 提供了**事件修饰符**。之前提过，修饰符是由点开头的指令后缀来表示的 

```js
.stop
.prevent
.capture
.self
.once
.passive
```

```vue
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

注意:

> 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 `v-on:click.prevent.self` 会阻止**所有的点击**，而 `v-on:click.self.prevent`只会阻止对元素自身的点击。 

#### 9.按键修饰符

在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符 

```html
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```



### 八.表单输入绑定

> 你用 `v-model` 指令在表单`<input>`,`<textarea>`及`<select>`元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素 

> `v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` 特性的初始值而总是将 Vue 实例的数据作为数据来源 

 `v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件 

1. text 和 textarea 元素使用 `value` 属性和 `input` 事件
2. checkbox 和 radio 使用 `checked` 属性和 `change` 事件
3. select 字段将 `value` 作为 prop 并将 `change` 作为事件



#### 1.文本框

```html
<input v-model="message" placeholder="edit me">
<p>{{ message }}</p>
```



#### 2.多行文本框

> 在文本区域插值 (`{{text}}`) 并不会生效，应用 `v-model` 来代替 

```html
<body>
    <div id="app">
        <h2>多行文本框</h2>
        <textarea cols="30" rows="10" v-model="message"></textarea>

        <h2>复选框</h2>
        <!-- 
            复选框会根据绑定数据的真假来决定是否选中
            true 选中
            false 取消选中
        -->
        <input type="checkbox" v-model="isChecked">

        <h2>单选按钮</h2>
        <!-- 
            单选按钮，它会把 value === 数据 的 radio 设置为被选中状态
            视图改变的时候，它会把用户选中的 radio 的 value 同步到数据中
        -->
        <input type="radio" name="gender" value="男" v-model="gender"> 男
        <input type="radio" name="gender" value="女" v-model="gender"> 女

        <h2>下拉框</h2>
        <!-- 
            1、数据更新视图：它会找到 option 中的 value === city 元素项，设置选中状态
            2、视图更新数据：它会把你选中的那个 option 的 value 同步到数据中
        -->
        <select v-model="city">
      <option value="0">北京</option>
      <option value="1">上海</option>
      <option value="2">广州</option>
      <option value="3">深圳</option>
    </select>
    </div>
    <script src="node_modules/vue/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: 'Hello Vue.js!',
                isChecked: true,
                gender: '女',
                city: '2'
            }
        })
    </script>
</body>
```

##### 1.复选框

 单个复选框，绑定到布尔值 

```html
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```

 多个复选框，绑定到同一个数组 

```html
<div id='example-3'>
    <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
    <label for="jack">Jack</label>
    <input type="checkbox" id="john" value="John" v-model="checkedNames">
    <label for="john">John</label>
    <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
    <label for="mike">Mike</label>
    <br>
    <span>Checked names: {{ checkedNames }}</span>
</div>
```

```js
new Vue({
    el: '#example-3',
    data: {
        checkedNames: []
    }
})
```

##### 2.单选按钮

```html
<div id="example-4">
    <input type="radio" id="one" value="One" v-model="picked">
    <label for="one">One</label>
    <br>
    <input type="radio" id="two" value="Two" v-model="picked">
    <label for="two">Two</label>
    <br>
    <span>Picked: {{ picked }}</span>
</div>
```

```js
new Vue({
    el: '#example-4',
    data: {
        picked: ''
    }
})
```



##### 3.选择框

 如果 `v-model` 表达式的初始值未能匹配任何选项，`` 元素将被渲染为“未选中”状态 

```html
<div id="example-5">
  <select v-model="selected">
    <option disabled value="">请选择</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>
</div>

```

```js
new Vue({
  el: '...',
  data: {
    selected: ''
  }
})
```

##### 4.用 `v-for` 渲染的动态选项 

```html
<select v-model="selected">
  <option v-for="option in options" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
```

```js
new Vue({
  el: '...',
  data: {
    selected: 'A',
    options: [
      { text: 'One', value: 'A' },
      { text: 'Two', value: 'B' },
      { text: 'Three', value: 'C' }
    ]
  }
})
```

