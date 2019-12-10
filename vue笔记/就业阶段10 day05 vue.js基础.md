# 就业阶段10 day05 vue.js基础

## 一.反馈问题

### 1.label和表单元素

- `label`的`for=""`属性里面绑定`input`表单元素中的`id=""`属性,当点击label中的内容的时候,也会选中input

- checkbox

    - 当元素改变的时候,对于checkbox来讲,那就是当选中状态改变的时候
    - 无论通过什么方式来获取checkbox改变之后的状态,都建议使用change事件,不要使用click点击事件,因为点击事件触发的时候,checkbox的状态可能还没有改变
    - 双向绑定:
        - 如果只是单纯的需要获取元素的绑定状态,那么通过DOM获取就足够了
        - 如果你期望checkbox受vue动态影响,那么就应该使用数据绑定

    ```html
    <div id="app">
        <label for="agree" @click="onClick">是否同意协议</label>
        <!-- @click="onChange" -->
        <input type="checkbox" id="agree" v-model="checked" @change="onChange">
    </div>
    
    <script src="../vue.js"></script>
    <script>
        new Vue({
            el: '#app',
            data: {
                checked: false,
            },
            methods: {
                onClick() {
                    //先触发点击事件再进行选中,所以拿到的是相反的值
                    console.log(this.checked);
                },
                //解决:给input本身注册改变事件
                onChange(e) {
                    console.log(this.checked); //通过v-model获取的选中状态
                    console.log(e.target.checked); //通过DOM获取的选中状态
                }
            }
        })
    </script>
    ```

    

### 2.计算属性和方法用什么

- 所有事件绑定都必须使用methods
- 当遇到需要在模板中绑定一个数据，而这个数据需要通过一段逻辑执行产生，这个时候可以使用方法或者计算属性
    - 建议优先考虑计算属性
    - 计算属性具有缓存功能，当多次使用的时候效率更高
- 计算属性必须要有返回值，方法可以没有返回值
- 计算属性在使用角度和data中的数据是一样的

### 3.数组方法

1. forEach遍历(大多数情况下可以代替for循环)
2. some判断数组中是否包含指定条件的元素
    1. 遍历数组，对每一项都进行条件判定，只要有一个满足条件，停止遍历，返回true
    2. 如果直到遍历结束都没有满足条件的元素，返回false
3. every判断数据中的元素是否全部满足某个条件
    1. 遍历数组，只要有一个元素不满足条件，停止遍历，返回false
    2. 如果遍历结束，所有元素都满足条件，返回true
4. filter从数组中根据某个条件过滤数据
    1. 返回一个新的数组
5. find根据条件查找单个元素
    1. 找到满足条件的第一个元素，停止遍历，立即返回
    2. 返回的是元素
6. findIndex根据条件查找元素的索引
    1. 返回的是索引
7. includes判断数组中是否包含指定元素
    1. 一般用于数组中都是普通数组类型
    2. `includes('值');`
    3. 返回值是布尔值：true或false



## 二.和服务器通信

Vue 不像 jQuery 内置了 ajax 请求函数，在 Vue 中没有提供这样的功能。所以当我们需要在 Vue 中和服务端进行通信的时候可选择的方式会更灵活一些。

> 注意：Vue 不提供的原因是为了让 Vue 本身更专注于视图部分，保持其渐进灵活的特性。

所以 Vue 给了我们更多的选择空间，例如我们可以使用下面的可选方案：

- 原生的 [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)
- 原生的 [Fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)
- 也可以结合使用 jQuery 自带的 [Ajax](http://api.jquery.com/category/ajax/) 请求函数
- 早期大家开发 Vue 应用喜欢使用一个第三方插件：[Vue Resource](https://github.com/pagekit/vue-resource)
- 目前主流的方案是使用社区中知名的第三方库 [axios]

### 1.学习准备

#### JSON Server

- JSON Server是一个提供测试环境接口的工具,它可以帮我们快速生成一套接口服务,专门用于学习测试
- 免费开源的命令行工具

##### 1.使用

1. 安装:`npm install -g json-server`

2. 测试是否安装成功,如果返回一个版本号就证明安装成功`json-server --version`

3. 创建一个目录`json-server-demo`,然后在该目录中创建一个文件`db.json`并写入以下内容:

    ```json
    {
      "posts": [
        { "id": 1, "title": "json-server", "author": "typicode" }
      ],
      "comments": [
        { "id": 1, "body": "some comment", "postId": 1 }
      ],
      "profile": { "name": "typicode" }
    }
    ```

4. 最后,在命令行中进入`db.json`所属目录,执行`json-server --watch db.json`

##### 2.接口说明

接口服务默认占用3000端口

JSON Server会根据`db.json`文件中的内容生成一些借口

1. 获取用户列表
    1. 请求方法:`GET`
    2. 请求路径:`/users`
    3. 请求参数:无
    4. 响应数据:用户列表,数组
2. 添加用户
    1. 请求方法：`POST`
    2. 请求路径:`/users`
    3. 请求参数:`{"name": 姓名,"age": 年龄, "gender": 性别}`
    4. 响应数据:新增的用户信息
    5. 注意：请求体数据必须是 JSON 格式字符串
3. 删除用户
    1. 请求方法:`DELETE`
    2. 请求路径: `/users/用户id`
        1. 例如删除id为3的用户：`http://localhost:3000/users/3`
    3. 请求参数
    4. 响应数据
4. 修改用户
    1. 请求方法:`PATCH`
    2. 请求路径: `/users/用户id`
        1. 例如修改id为3的用户:`http://localhost:3000/users/3`
    3. 请求参数
        1. Body 请求体数据:`{ "name": 名称, "age": 年龄,"gender": 性别}`
    4. 注意:name、age、gender 都是可选的，修改谁就传谁
    5. 响应数据:修改之后的用户的完整信息

##### 3.获取指定条件的数据

- 请求方法：`GET`
- 请求路径 `/users`
- 请求参数

Query （查询字符串）参数：

- name 姓名
- age 年龄
- gender 性别

示例：

```
http://localhost:3000/users?name=张三丰
http://localhost:3000/users?age=18
http://localhost:3000/users?age=18&name=李四二
```







### 2.axios

[axios](https://github.com/axios/axios) 是一个基于 Promise 的第三方 HTTP 客户端请求库，可以用于浏览器或者 Node.js。
axios 本身和 Vue 没有一毛钱关系，只是简单纯粹的封装了 HTTP 请求功能。可以运行在任何支持 JavaScript 环境的平台。

- 在浏览器端使用的是 [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)
- 在 Node 中使用的是 [http](http://nodejs.org/api/http.html)
- 支持 Promise
- 支持请求拦截和响应拦截
- 支持转换请求和响应数据
- 支持取消请求
- 自动转换 JSON 数据
- 客户端支持防止 XSRF

> axios 依赖原生的 ECMAScript 6 Promise 支持。
>
> 如果浏览器不支持 ECMAScript 6 Promise，可以使用 [es6-promise](https://github.com/stefanpenner/es6-promise) 进行兼容处理。

#### 1.基本使用:

1. 安装:`npm install axios`

##### 1.执行一个 `GET` 请求

```js
axios({ // 配置请求相关数据信息
  method: 'GET', // 请求方法
  url: 'http://localhost:3000/users', // 请求路径
  // params: {}, // Query 参数
  // data: {} // Body 参数
}).then(function (res) {
  // res 是响应对象
  // 接口返回的数据再 res.data 中
  //    config: {url: "http://localhost:3000/users", method: "get", headers: {…}, transformRequest: Array(1), transformResponse: Array(1), …}
  //      本次请求配置信息对象，很少使用
  //    data: [{…}]
  //      真正的响应结果数据
  //    headers: {cache-control: "no-cache", content-length: "84", content-type: "application/json; charset=utf-8", expires: "-1", pragma: "no-cache"}
  //      响应头数据，很少使用
  //    request: XMLHttpRequest {readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, onreadystatechange: ƒ, …}
  //      请求对象，几乎不适用
  //    status: 200
  //      响应状态码
  //    statusText: "OK"
  //      响应状态短语
  console.log(res.data)
})
```



##### 2.带有 Query 参数的 GET 请求

```js
const user = {
  name: '张三',
  age: 18
}

axios({
  method: 'GET',
  // url: 'http://localhost:3000/users?name=' + name + '&age=' + age,
  // url: `http://localhost:3000/users?name=${name}&age=${age}`,
  url: 'http://localhost:3000/users',
  // 配置 Query 查询参数
  // axios 在内部把 params 对象转换为 key=value&key=value 的数据格式
  // 然后放到 url 后面，把请求发出去
  params: {
    // name: user.name,
    age: user.age
  }
}).then(res => {
  console.log(res)
})
```



##### 3.执行一个 `POST` 请求

```js
axios({
  method: 'POST',
  url: 'http://localhost:3000/users',
  data: { // POST 请求体放到 data 中
    name: '张三风',
    age: 50,
    gender: '男'
  }
}).then(res => {
  if (res.status === 201) {
    console.log('添加成功')
  }
})
```



##### 4.执行一个 `DELETE` 请求

```js
axios({
  method: 'DELETE',
  url: 'http://localhost:3000/users/3'
}).then(res => {
  console.log(res)
})
```



##### 5.执行一个 `PATCH` 请求

```js
axios({
  method: 'PATCH',
  url: 'http://localhost:3000/users/4',
  data: { // Body 请求体
    name: '张三丰'
  }
}).then(res => {
  console.log(res)
})
```



#### 2.axios API

##### 1.axios(config)

我们可以像使用 `$.ajax()` 一样来使用 `axios`。

```javascript
// Send a POST request
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
})
```

```javascript
// GET request for remote image
axios({
  method: 'get',
  url: 'http://bit.ly/2mTM3nY',
  responseType: 'stream'
}).then(function(response) {
  response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
})
```



##### 2.请求方法别名(了解即可)

为了方便，axios 为所有的请求方法都提供了别名支持。

- axios.request(config)
- axios.get(url[, config])
- axios.delete(url[, config])
- axios.head(url[, config])
- axios.options(url[, config])
- axios.post(url[, data[, config]])
- axios.put(url[, data[, config]])
- axios.patch(url[, data[, config]])

> 注意：当使用了这些别名方法时，`url`, `method` 和 `data` 属性不需要声明在配置对象中。



##### 3.响应体结构

请求的响应包含以下信息。

```json
{
  // `data` is the response that was provided by the server
  "data": {},

  // `status` is the HTTP status code from the server response
  "status": 200,

  // `statusText` is the HTTP status message from the server response
  "statusText": "OK",

  // `headers` the headers that the server responded with
  // All header names are lower cased
  "headers": {},

  // `config` is the config that was provided to `axios` for the request
  "config": {},

  // `request` is the request that generated this response
  // It is the last ClientRequest instance in node.js (in redirects)
  // and an XMLHttpRequest instance the browser
  "request": {}
}
```

当使用 `then` 方法时，将收到如下结果

```js
axios.get('/user/12345').then(function(response) {
  console.log(response.data)
  console.log(response.status)
  console.log(response.statusText)
  console.log(response.headers)
  console.log(response.config)
})
```

#### 3.配置baseUrl

```js
// 配置请求的基础路径
axios.defaults.baseURL = 'https://api.example.com'
```



#### 4.处理错误

```js
axios({
  method: 'PATCH',
  url: '/users/2',
  data: {
    name: 'abc'
  }
}).then((res) => { // 成功执行 then
  // 在 axios 中，默认只有 >=200 和 <400 的状态码都认为是成功的
  // axios 在请求失败以后就不执行 then 里面的代码了
  console.log('请求结果 => ', res)
}).catch(err => { // 失败执行 catch
  console.log('请求失败了', err)
  window.alert('更新失败，请稍后重试！')
})
```



## 三. 在 Vue 中配合使用 axios

### 1.准备页面模板

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <form>
      <div>
        <label for="">姓名</label>
        <input type="text">
      </div>
      <div>
        <label for="">年龄</label>
        <input type="text">
      </div>
      <div>
        <label for="">性别</label>
        <input type="radio" value="男" name="gender"> 男
        <input type="radio" value="女" name="gender"> 女
      </div>
      <div>
        <button>添加</button>
      </div>
    </form>

    <table>
      <thead>
        <tr>
          <th>id</th>
          <th>姓名</th>
          <th>年龄</th>
          <th>性别</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>1</td>
          <td>张三</td>
          <td>18</td>
          <td>男</td>
          <td>
            <button>删除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</body>
</html>

```

### 2.安装依赖

```bash
# 安装 Vue
npm i vue
# 安装 axios
npm i axios
```

### 3.导入 Vue 和 Axios

```html
<script src="../vue.js"></script>
<script src="./node_modules/axios/dist/axios.js"></script>
```

### 4.配置基地址和声明Vue对象

```vue
<script>
    axios.defaults.baseURL = 'http://localhost:3000/';
   
    const vm = new Vue({
        el: '#app',
        data: {
            user: {
                name: '',
                age: '',
                gender: ''
            },
            users: [], //存储用户数据列表
        },
        methods: {}
    })
</script>
```

### 5.添加对象

#### 1.获取表单数据

1. 根据接口和视图抽象出数据初始化到 data 中

    ```js
    data: {
      user: {
        name: '',
        age: '',
        gender: ''
      }
    },
    ```

    

2. 将数据绑定到对应的表单元素

    ```html
    <div>
        <label for="name">姓名:</label>
        <input type="text" id="name" v-model="user.name">
    </div>
    <div>
        <label for="age">年龄:</label>
        <!-- 
            v-model支持一个修饰符 .number 可以把绑定的数据自动转为数字类型
         -->
        <input type="text" id="age" v-model.number="user.age">
    </div>
    <div>
        <label for="">性别:</label>
        <input type="radio" value="男" v-model="user.gender">男
        <input type="radio" value="女" v-model="user.gender">女
    </div>
    <div>
        <input type="submit" value="添加">
    </div>
    ```

    

3. 使用 VueDevTools 调试工具测试数据绑定是否正确。

#### 2.注册表单提交事件

1. 监听表单的 `submit` 事件，并绑定 `onAdd` 处理函数

    ```html
     <form action="" @submit.prevent="onAdd">
        <div>
            <label for="name">姓名:</label>
            <input type="text" id="name" v-model="user.name">
        </div>
        <div>
            <label for="age">年龄:</label>
            <!-- 
                v-model支持一个修饰符 .number 可以把绑定的数据自动转为数字类型
             -->
            <input type="text" id="age" v-model.number="user.age">
        </div>
        <div>
            <label for="">性别:</label>
            <input type="radio" value="男" v-model="user.gender">男
            <input type="radio" value="女" v-model="user.gender">女
        </div>
        <div>
            <input type="submit" value="添加">
        </div>
    </form>
    ```

    

2. 在 `methods` 中添加 `onAdd` 处理函数，请求提交表单

    ```js
    methods: {
        onAdd() {
            axios({
                method: 'POST',
                url: '/users',
                data: this.user
            }).then(res => {
                // console.log("添加成功", res);
                alert("添加成功");
            }).catch(err => { //失败执行catch
                console.log("请求错误了");
            });
        }
    }
    ```

    

### 6.列表加载

1. 在 `mthods` 中封装一个方法 `loadUsers` 用于请求获取数据并更新数据

    ```js
    loadUsers() {
        axios({
            method: 'GET',
            url: '/users',
        }).then(res => { //注意:then方法中的函数务必使用箭头函数,否则箭头函数会有问题
            // console.log(res.data);
            this.users = res.data;
        }).catch(err => { //失败执行catch
            console.log("请求错误了");
        });
    },
    ```

    

2. 在实例选项 `created` 方法中调用 `loadUsers` 方法

    ```js
    //实例选项:created
    //它是一个函数,它会在Vue初始化完成以后自动调用
    //我们可以在它里面访问this获取Vue实例
    //最常见的场景就是:在页面加载好以后请求获取数据列表
    created() {
        // axios({
        //     method: 'GET',
        //     url: '/users',
        // }).then(res => { //注意:then方法中的函数务必使用箭头函数,否则箭头函数会有问题
        //     console.log(res.data);
        //     this.users = res.data;
        // }).catch(err => { //失败执行catch
        //     console.log("请求错误了");
        // });
        //不建议在created中写大量的业务逻辑代码
        //推荐把这些功能毒封装在一个一个函数中 放入methods中
        this.loadUsers();
    }
    ```

    

3. 在模板中使用 `v-for` 遍历展示用户列表

    ```html
    <tr v-for="user in users" :key="user.id">
        <td v-cloak>{{user.id}}</td>
        <td v-cloak>{{user.name}}</td>
        <td v-cloak>{{user.age}}</td>
        <td v-cloak>{{user.gender}}</td>
        <td><button>删除</button></td>
    </tr>
    ```

    

4. 在 `onAdd` 中添加用户完成的 then 回调中调用 `loadUsers` 更新用户列表

    ```js
    onAdd() {
        axios({
            method: 'POST',
            url: '/users',
            data: this.user
        }).then(res => {
            // console.log("添加成功", res);
            alert("添加成功");
            this.loadUsers();
        }).catch(err => { //失败执行catch
            console.log("请求错误了");
        });
    }
    ```

    

### 7.删除对象

1. 给用户列表中的删除按钮绑定点击处理函数

    ```html
    <td><button @click="onDelete(user.id)">删除</button></td>
    ```

    

2. 在 `methods` 中定义 `onDelete` 处理函数

    ```js
    onDelete(id) {
        if (!confirm("确定删除吗?")) {
            return;
        }
        axios({
            method: 'DELETE',
            url: `/users/${id}`, //建议所有字符串拼接都使用es6模板字符串方式
        }).then(res => {
            alert("删除成功");
            this.loadUsers();
        }).catch(err => { //失败执行catch
            console.log("删除失败");
        });
    }
    ```

    