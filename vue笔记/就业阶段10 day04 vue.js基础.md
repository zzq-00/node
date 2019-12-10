# 就业阶段10 day04 vue.js基础

### 一.样式处理

#### 1.class

我们可以传给`v-bind:class`一个对象,以动态的切换class:

```vue
<div :class="{active:isActive}"></div>
```

上面的语法表示active这个类名存在与否取决于isActive这个属性值的真假

- 属性名:class样式类名

- 值:布尔值
    - true:作用类名
    - false:去除类名

#### 2.style

style也可以动态绑定

- 属性名:样式规则,例如color,width,fontSize
- 属性值:动态数据

**注意:小写短横杠连接的规则名称都使用驼峰命名**

```html
<div id="app">
    <h1>样式处理</h1>
    <div class="box" :class={dark:isDark,light:isLight} @click="dark" @dblclick="light">样式处理</div>

    <div :style="{color:activeColor,fontSize:fontSize+'px'}">内联样式</div>
</div>

<script src="../vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            isDark: false,
            isLight: false,
            activeColor: 'skyblue',
            fontSize: 24
        },
        methods: {
            dark() {
                this.isDark = !this.isDark;
            },
            light() {
                this.isLight = !this.isLight;
            }
        }

    })
</script>
```



### 二.计算属性

虽然模板内的表达式十分便利,但是它们的设计初衷是为了用于简单运算,在模板中放入太多的逻辑会让模板过重而且难以维护

```html
<p>{{massage.split('').reverse().join('')}}</p>
```

这里模板并不是简单的声明式逻辑,必须看一段时间才能意识到这里是想要显示变量`message`的翻转字符串,如果想要在模板中多次引用时候将会更难处理



#### 1.方法:

- 可以用methods方法来解决,把逻辑封装起来

    - 但是数据改变,方法也会重新调用,而且是每个绑定的地方都会调用,绑几次就调用几次
    - 绑定多次就调用多次,效率低

    ```html
    <p>{{getReverse()}}</p>
    ```

    ```js
    methods: {
        getReverse() {
            return this.massage.split('').reverse().join('');
        }
    }
    ```



#### 2.计算属性:

-  vue提供了一种方式:==计算属性==,也能实现类似methods方法的功能

    -  实例选项:computed,它和el,data,methods等同级
    - 作用:
        - 类似于方法,但是只能当做属性来使用
        - 可以把需要通过一段逻辑执行获取的结果代码封装为一个计算属性(方法),然后在模板中直接使用

    ```html
    <p>{{msg}}</p>
    ```

    ```js
    computed: {
        msg() {
            return this.massage.split('').reverse().join('');
        }
    }
    ```

- 注意:

    - 计算属性本质是方法,但是只能当做属性访问
    - 计算属性更不能当做事件处理函数使用
        - 事件处理函数肯定是methods
    - **计算属性一定要有==返回值==,返回值就是属性的值,它的值可以在模板中使用**

建议:只要是需要通过一段逻辑获取一个新的数据的需求,那就优先使用计算属性

计算属性会把执行之后的结果缓存起来,其它的多次使用就直接从缓存中获取了



#### 3.计算属性和方法的区别

1. **计算属性是基于它们的响应式依赖进行缓存的**,只在相关响应式依赖发生改变时它们才会重新求值
2. 而每当触发重新渲染时,调用方法总会再次执行函数

### 三.侦听器

> 当你需要根据变化执行一些逻辑的时候,可以利用watch监视来处理

Vue 提供了可以自定义监视数据变化的功能：watch 监视，当监视到数据变化之后执行一些需要的业务逻辑

watch也是一个实现选项,和el,data等同级

- 属性名:要监视的数据成员
- 属性值:处理函数
- 作用：
    - 当被监视的数据发生变化的时候,它会自动调用处理函数
    - vue会把改变的新值和旧值作为参数传递给处理函数
        - 第一个参数：新值
        - 第二个参数：旧值
- 注意:它不需要返回值,更不需要在模板中绑定
- **watch中的成员不是数据,不是用于模版绑定的,它是一个功能特点**

```html
<div id="app">
    <h2>{{count}}</h2>
    <button @click="count++">点击+1</button>
</div>

<script src="../vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            count: 0
        },
        watch: {
            count(newValue, oldValue) {
                console.log('count改变了', newValue, oldValue);
            }
        }
    })
</script>
```



### 四.案例中的知识点

#### 1.数组的splice方法

```js
const arr = [1,2,3,4,5];
arr.splice(index);  //从指定索引开始(包括索引本身)一直删到最后
arr.splice(index,n);  //从指定索引开始(包括索引本身),删除指定的个数
arr.splice(index,n,a);  //从指定索引开始,删除n个,替换为a
arr.splice(index,n,a,b,m);  //从指定索引开始,删除n个,替换为a,b,m
//说白了就是从第三个参数开始都是要替换的参数
```

#### 2.遍历数组的some方法

- 常用于判断数组中是否包含符合指定条件的元素
- 每遍历一次就执行一次函数
    - 如果函数调用返回**true**就会**停止遍历** 返回true
    - 如果返回false就继续遍历
    - 如果直到遍历结束都没有符合条件的元素就返回false

```js
数组.some((item,index)=>{
	函数体
})
```

#### 3.遍历数组的every方法

- 遍历数组,对每一个元素执行条件判定
    - 如果条件判定为**false**,则**停止遍历**,返回false
    - 如果直到遍历结束,所有元素都符合条件,返回true
    - 说白了就是所有元素都满足条件,才返回true,只要有一个不满足就返回false
    - 与some方法刚好相反

```js
数组.every((item,index)=>{
	函数体
})
```

