# 就业阶段10 day02 vue.js基础

### 一.结构-列表控制-`key`管理可复用的元素

Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染

```html
<div id="app">
    <p v-if='true'>{{msg}}</p>
    <!-- key是vue提供的一个特殊属性 -->
    <div class="login ">
        <div v-if="loginType === 'username'">
            <label for="">username:</label>
            <input type="text" key="username" placeholder="用户名">

        </div>
        <div v-if="loginType === 'email'">
            <label for="">email:</label>
            <input type="text" key="email" placeholder="email">
        </div>
    </div>
    <button @click="changeType">切换</button>
</div>

<script src="../vue.js "></script>
<script>
    //vue中在进行模板渲染的时候,为了提升性能,并不是每次都创建生成新的节点,它会选择复用(如果有)
    //通过key属性可以强制告诉vue DOM节点重新创建生成
    var vm = new Vue({
        el: '#app',
        data: {
            msg: '学习',
            loginType: 'username'
        },
        methods: {
            changeType: function() {
                // if (this.loginType === 'username') {
                //     this.loginType = 'email';
                // } else {
                //     this.loginType = 'username'
                // }
                if (this.loginType === 'username') return this.loginType = 'email';
                this.loginType = 'username';
            }
        }
    })
</script>
```

```html
<div id="app">
    <button @click="addStudent">添加</button>
    <table>
        <tr>
            <th>id</th>
            <th>姓名</th>
            <th>性别</th>
            <th>年龄</th>
        </tr>
        <!-- 添加key才能保证DOM的更新 -->
        <tr class="item" v-for="(student, index) of students" :key="student.id">
            <td>{{student.id}}</td>
            <td>{{student.name}}</td>
            <td>{{student.gender}}</td>
            <td>{{student.age}}</td>
        </tr>
    </table>
</div>
<script src="../vue.js "></script>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            user: {
                id: Math.floor(Math.random() * Date.now()),
                name: '小明',
                age: 18
            },
            students: [{
                id: Math.floor(Math.random() * Date.now()),
                name: '小明',
                gender: '男',
                age: 18
            }, {
                id: Math.floor(Math.random() * Date.now()),
                name: '小红',
                gender: '女',
                age: 17
            }, ]
        },
        methods: {
            addStudent: function() {
                // 向数组头部添加一条记录
                this.students.unshift({
                    id: Math.floor(Math.random() * Date.now()),
                    name: '小李',
                    gender: '男',
                    age: 17
                });
            }
        },
        mounted: function() {
            document.querySelectorAll('.item')[1].style.color = 'red';
        }
    })
</script>
```

当 Vue 正在更新使用 v-for 渲染的元素列表时，它**默认使用“就地更新”的策略**。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。

​		这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

​		**建议尽可能在使用 v-for 时提供 key 属性**，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升

### 二.指令

> 指令 (Directives) 是带有 `v-` 前缀的特殊特性（属性）。

到目前为止我们已经学习了很多指令了，那个时候我把它叫做属性是为了方便大家理解，其实在 vue 中它有一个专门的名称，指令。

还有几个指令需要了解：

1. `v-once`只渲染元素一次

    ```html
    <div id="app">
        <p v-once='true'>{{msg}}</p>
        <p>{{msg}}</p>
        <button @click='click'>切换</button>
    </div>
    
    <script src="../vue.js "></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                msg: '学习',
            },
            methods: {
                click: function() {
                    this.msg = '个p'
                }
            }
        })
    </script>
    ```

    

2. `v-cloak` 优化用户体验，**避免闪烁现象**

    1. 由于代码自上向下解析执行，Vue 来不及渲染而导致 {{msg}} 被浏览器显示出来 ---> 当 Vue 被执行后，才会将 {{msg}} 解析并渲染
    2. 通过 v-text 是可以避免这个问题的，原因是 v-text 是一个属性，即使被浏览器解析也不会显示到页面  ---> `v-text本来就不会闪烁`
    3. 还可以通过 v-cloak 配合 [v-cloak] {display: none;} 来解决 ---> `v-cloak专门用来解决闪烁`

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>03.v-cloak</title>
        <style>
            [v-cloak] {
                display: none;
            }
        </style>
    </head>
    <body>
        <div id="app">
            <p v-once='true' v-cloak>{{msg}}</p>
            <p v-cloak>{{msg}}</p>
            <button @click='click'>切换</button>
        </div>
    
        <script src="../vue.js "></script>
        <script>
            var vm = new Vue({
                el: '#app',
                data: {
                    msg: '学习',
                },
                methods: {
                    click: function() {
                        this.msg = '个p'
                    }
                }
            })
        </script>
    </body>
    </html>
    ```

    

    

3. `v-pre` 所在元素不会被编译处理，可以理解为忽略

    ```html
    <div id="app">
      <!-- 添加了 v-pre 后 {{}} 就不会被 vue 识别了 -->
      <p v-pre>{{text}}</p>
    </div>
    
    <script>
    	var vm = new Vue({
        el: '#app',
        data: {
          text: '一段文本'
        }
      });
    </script>
    ```

    

4. `v-model` 获取表单元素中的值，支持**修饰符**

    1. `.lazy` 取代 `input` 监听 `change` 事件
        1. `.lazy`可以将`v-model`默认的input事件更改成change事件
        2. 某种程度上可以提升性能
    2. .number 字符串转为有效的数字
        1. 能转的情况下转为数字类型
    3. .trim 首尾空格过滤
    4. `v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件
        1. text 和 textarea 元素使用 `value` 属性和 `input` 事件
        2. checkbox 和 radio 使用 `checked` 属性和 `change` 事件
            1. 不需要在标签里写checked做默认选中了
            2. 多选框对应数组类型
        3. select 字段将 `value` 作为 prop 并将 `change` 作为事件
            1. 如果指定了value值,v-model以value做参照
            2. 如果不指定value值,v-model以option文本作为参照

    ```html
    <body>
        <div id="app">
            <h2>{{username}}</h2>
            <form>
                <ul>
                    <!-- .lazy可以将v-model默认的input事件更改成change事件 -->
                    <li>姓名: <input type="text" v-model.lazy="username" /></li>
                    <!-- .trim 为修饰符，其作用是清空两端空白符 -->
                    <li>密码: <input type="password" v-model.trim="password" /></li>
                    <!-- .number 为修饰符，其作用是只允许数字 -->
                    <li>年龄: <input type="text" v-model.number="age" /></li>
                    <li>
                        性别:
                        <!-- value 属性不可以省略 -->
                        <!-- 不需要checked做默认选中了 -->
                        <input type="radio" value="男" v-model="gender" /> 男
                        <input type="radio" value="女" v-model="gender" /> 女
                    </li>
                    <li>
                        爱好:
                        <!-- value 属性不可以省略 -->
                        <input type="checkbox" value="睡大觉" v-model="hobby" /> 睡大觉
                        <input type="checkbox" value="写代码" v-model="hobby" /> 写代码
                    </li>
                    <li>
                        籍贯:
                        <!-- value 属性不建议省略 -->
                        <select v-model="hometown">
                            <option>请选择</option>
                            <option>北京市</option>
                            <option>河北省</option>
                            <option>河南省</option>
                          </select>
                    </li>
                    <li>
                        个人介绍:
                        <textarea v-model="bio"></textarea>
                    </li>
                    <li><button>提交</button></li>
                </ul>
            </form>
        </div>
    
        <script src="../vue.js"></script>
        <script>
            var vm = new Vue({
                el: '#app',
                data: {
                    username: '',
                    password: '',
                    age: 18,
                    // 单选框
                    gender: '男',
                    // 多选框对应数组类型
                    hobby: ['睡大觉'],
                    // 下拉框
                    hometown: '请选择',
                    bio: ''
                }
            })
        </script>
    </body>
    ```

    

5. 动态参数，`v-on`、`v-bind` 支持动态参数绑定

    ```html
    <div id="app">
        <img :[aaa]="msg">
        <button @click="toggle">图片显示</button>
        <!-- <p :[aaa]="'一段文字'">一段文字</p> -->
        <!-- 更改 myevent 变量的值 -->
        <button @click="changeEvent('input')">input 事件</button>
        <button @click="changeEvent('change')">change 事件</button>
        <!-- myevent 变量的值决定了 input 监听的事件名称 -->
        <input @[myevent]="handler" />
    </div>
    
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                // 将事件名称定义成一个变量
                myevent: 'input',
                aaa: 'title',
                msg: '一张图片.png'
            },
            methods: {
                toggle: function() {
                    this.aaa = 'src'
                },
                // 点击事件切换事件
                changeEvent: function(arg) {
                    this.myevent = arg;
                },
                // 监听表单事件
                handler: function(ev) {
                    console.log(ev.type + '事件被触发了...');
                },
    
            }
        })
    </script>
    ```

    

### 三.计算属性

实例化 Vue 时通过 `data` 初始的数据都是确定的，开发中经常遇到不确定的数据

1. 计算属性是要经过计算(一些逻辑)才能得到的值
2. 通过**计算属性**非常方便的解决了"不确定数据"的获取，而且计算属性也是响应式的通过**计算属性**非常方便的解决了"不确定数据"的获取，而且计算属性也是响应式的
3. 该函数的返回值即为计算属性的值

```html
<div id="app">
    <input type="text" v-model="val" />
    <div class="item" v-cloak v-if="student[0]">
        <span>{{student[0].name}}</span>
        <span>{{student[0].gender}}</span>
        <span>{{student[0].age}}</span>
    </div>
    <div v-else v-cloak>没有找到相关学生信息</div>
</div>

<script src="../vue.js"></script>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            // student: null,
            dataname: '',
            val: '',
            // 学生信息
            students: [{
                name: '小明',
                gender: '男',
                age: 18
            }, {
                name: '小红',
                gender: '女',
                age: 16
            }, {
                name: '小花',
                gender: '女',
                age: 17
            }, {
                name: '小刚',
                gender: '男',
                age: 19
            }]
        },
        // 声明/定义数据（计算属性）
        computed: {
            // 计算数据（通过逻辑获取的数据称为计算属性）
            student: function() {
                //该函数的返回值就是计算属性的值
                return this.students.filter(item => {
                    return item.name == this.val;
                });
            }
        }
    })
</script>
```

```html
<div id="app">
    当前时间为: {{now}}
    <br>
    当前时间为: {{now}}
</div>

<script>
    var vm = new Vue({
        el: '#app',
        computed: {
            now: function () {
                return (new Date()).getTime();
            }
        }
    });
</script>
```

**如果使用计算属性时，数据是会有缓存的，某种程度上是有利于提升性能。**

### 四.侦听器

在 Vue 中数据的变化是响应式的，这一切都由 Vue 内部自动处理，给开发者带来了极大的方便，然而某些复杂的场景（数据校验、异步请求等）**需要开发者能够监听到数据的变化并执行特定的逻辑。**

1. 校验数据

    ```html
    <div id="app">
        <h2>{{msg1}}</h2>
        <input type="text" v-model="msg"> 年龄:
        <input type="text" v-model="age">
    </div>
    
    <script src="../vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                msg: '',
                text: '',
                msg1: '',
                age: 18
            },
            watch: {
                //对data中的msg进行侦听
                msg: function(newValue, oldValue) {
                    // console.log('msg的内容正在改变');
                    // console.log(newValue, oldValue);
                    this.msg1 = newValue.split('').reverse().join('')
    
                },
                age: function(newValue, oldValue) {
                    //如果输入的内容不能转为数字类型
                    //值为旧值
                    if (!Number(newValue)) {
                        this.age = oldValue;
                    }
                }
            }
        })
    </script>
    ```

    监听中的函数参数`function(newValue, oldValue)`**第一个参数代表新的值,第二个参数代表旧的值**

    

2. 网络请求

### 五.过渡&动画



### 六.实例属性



### 七.进阶-指令



### 八.过滤器



### 九.生命周期

