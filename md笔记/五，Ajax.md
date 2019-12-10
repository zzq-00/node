## 课程介绍

- 目标

- 了解现阶段，我们即将要学习什么

- 案例对比

  - 之前做的案例都是 `单机程序`。
  - 现阶段及之后的案例都类似真正的网站

  > 两个案例为什么有非常大的区别，是因为现阶段的案例使用了ajax、服务器、http等等新的技术。

## 了解上网的过程

你知道当我们在网页浏览器（browser）的地址栏中输入 URL时，页面是如何呈现的吗？

<img src="E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1568256300963.png" alt="1568256300963" style="zoom:70%;" />

页面当然不能凭空显示出来。我们看到的页面也是像我们一样的前端人员写出来的页面，那么这些页面在哪里呢？其实先不用想的很复杂，这些页面不是我们写的，肯定不在自己的电脑上，肯定是谁写的页面就在谁的电脑上呗。

比如，老师演示的留言板页面就在老师的电脑上，百度、新浪、腾讯等公司的页面肯定也在人家的电脑上。

问题是，别人写的页面，为什么通过自己的浏览器也能看到呢？

原因是这样的，根据 浏览器地址栏中指定的URL（形如 `http://www.baidu.com/index.html`），浏览器首先根据指定的 域名^①^ (`www.baidu.com`）找到存放百度页面的计算机，向百度的计算机“索要”指定的文件（`index.html`），百度的计算机就会把index.html 中的代码返回给我们的浏览器，注意，只是把index.html中的代码返回给我们的浏览器，并不是把这个文件下载下来。浏览器刚好是一个可以显示页面的工具，所以浏览器将得到的代码解析^②^后，我们最终就看到了百度的页面了。

![1570856033204](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570856033204.png)

下面对上述内容中几个新知识点做一个解释：

- 域名
  - 域名的作用和IP地址一样，可以找到网络中的一台计算机
  - IP地址是标识网络设备的唯一标识，同一个网络中的计算机，IP地址绝对不会重复
- 解析
  - 这里解释的意思是，浏览器把代码（HTML、css等等代码）呈现到页面上

## 细化上网的过程

前面简单阐述了上网的过程，使用的语言大多都是大白话，接下来我们说一下上网的过程中涉及到的一些转义术语。

- 客户端
  - 在上网的过程中，浏览器还有另外一个名字，叫做客户端。
- 服务器
  - 存储百度网页的那台计算机，叫做服务器，或者叫做Web服务器。
- 请求
  - 请求，或者叫做发送请求，指的是客户端向服务器“索要”页面的过程
- 响应
  - 即回应，当客户端向服务器发送请求之后，服务器会根据客户端的请求，将客户端请求文件的源代码返回给浏览器，这一过程称之为响应。
- 资源
  - 服务器上存储的东西都可以叫做资源，比如html文件、css文件、图片文件、js文件、音频视频文件、字体文件等等。

![1570856713597](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570856713597.png)

网络请求时（上网时），必定是一端担任客户端角色，另一端担任服务器端角色

通过浏览器工具，能够查看每一次网络请求：

![1570860202272](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570860202272.png)

下面，我们来看一个具体的示例。

![c](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/c.gif)

可能你每天都在使用客户端，最常见的客户端就是浏览器。浏览器一个页面时（比如http://192.168.115.56:4000/index.html），浏览器会向服务器（服务器IP地址为`192.168.115.56`）发送一个请求，服务器会去寻找客户端所期望的`index.html`，如果成功，就将`index.html`的内容及一些其他信息放在响应中发送给浏览器。最后浏览器将服务器响应的结果呈现在我们眼前。

## 了解服务器

Web资源（html文件、css文件、js文件、json文件等等...）都是存储在Web服务器上的。

Web服务器会对客户端的请求进行处理并提供响应，术语“Web服务器”可以用来表示Web服务器的软件，也可以用来表示提供Web页面的特定设备或计算机，下文都指后者。

Web服务器有着不同的风格、形状和尺寸。

服务器可以从网络运营商（阿里云、腾讯云、百度云...）租，也可以自己购买。下图是淘宝上搜索“服务器”的截图

<img src="E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1568257353683.png" alt="1568257353683" style="zoom:80%;" />

但不管功能有何差异，所有的Web服务器都能够接收客户端的请求，将服务器端的内容回送给客户端。

总体来说，Web服务器的作用：

- 存储Web资源，资源的概念很广，这里先理解为服务器上的html文件、css文件、js文件、图片文件等等。
- 提供Web服务，理解为能够接收并处理客户端的请求，并做出回应

Web服务器和普通计算机的区别

- 除了硬件设施的区别之外，`Web服务器 === 普通计算机 + 服务器软件`

### 服务器软件

服务器和个人计算机的本质区别是，服务器上安装了服务软件。常见的服务软件非常多，比如：

- Apache
- Nginx
- IIS
- ......

凡是叫做服务器的，肯定都安装了服务软件。

我们上课使用的服务软件是使用Node编写的一个小软件，没有名字（<img src="E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/481A69F1.png" alt="img" style="zoom:50%;" />）

> 服务器 = 计算机 + 服务软件



## 搭建Web服务环境

### 如何拥有服务器

学习阶段，无需购买服务器或租赁服务器，可以像老师一样，把自己的计算机用作服务器即可。

前面介绍到，`服务器 = 计算机 + 服务软件`

- 使用的服务器就是我们自己的计算机
- 使用的服务软件是使用Node编写的一套程序。

开机，运行服务软件，将资料中的ajax文件夹，用编辑器打开，在`app.js`上右键，选择在终端中打开，最后在出现的终端面板中，输入`node app.js`，按回车即表示服务启动了，见下图。

![b](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/b-1568615934932.gif)

要点说明：

- 开启服务后，终端面板可以关闭。关闭终端面板并不表示关闭服务。
- 服务不能重复启动，否则报错。
- 我们自己创建的文件必须放到 `public` 文件夹中。
- ==访问 `public` 里面的文件，必须用访问服务器的方式去访问，即必须使用IP地址或域名访问，不能以文件方式打开==

试着访问服务器上的资源：

- 在 `public` 文件夹创建一个 html 文件，然后使用浏览器访问它

## 初识Ajax

前面我们通过浏览器输入 IP或域名，按下回车的方式，可以向服务器发送请求，并能接收到服务器响应的结果，浏览器的这项可以发送请求并接收结果的功能，可以认为是浏览器本能的行为。

![1570856713597](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570856713597.png)

Ajax是一种技术，通过这种技术，也可以实现客户端和服务器的请求响应过程。这一技术的实现，只需要浏览器执行一小段JS代码即可。

![1570858627610](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570858627610.png)

> 使用Ajax技术，无需浏览器地址栏回车、刷新等，只需要让浏览器执行一段JS代码就可以实现请求响应过程了，言外之意是使用Ajax技术，页面是不会刷新的

## 小试牛刀

接下来，我们先快速实现一次Ajax请求。

具体做法是，在 `public` 文件夹中，随便创建一个 html文件，比如叫做 `01-ajax.html` ，我们就在这个文件中写一段能够实现Ajax请求的JS代码，为了快速体验，我们可以借助于jQuery。

在 `01-ajax.html` 中，加入如下代码

```html
<script src="./assets/jquery.js"></script>
<script>
    $.ajax({
        // 属性: 值
        // url: 'http://localhost:4000/test.txt', // 请求的服务器上的资源的地址
        url: '/test.txt', // 简化的地址
        // success属性，可以接收服务器响应的结果
        success: function (result) {
            console.log(result);
        }
    });
</script>
```

浏览器，请求 01-ajax.html 即可看到Ajax请求了。

![1570859891793](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570859891793.png)

## 认识数据接口

其实，在通过Ajax向服务器发送请求的时候，不但可以请求服务器上的文件资源，也可以请求接口，url也可以这样写：

```html
<script src="./assets/jquery.js"></script>
<script>
    $.ajax({
        url: '/common/abc', // 这里这样写
        success: function (result) {
            console.log(result);
        }
    });
</script>
```

通过代码，发现，`public` 文件夹中并没有 `/common/abc` 这个文件，但是运行之后也不会报错。这种非文件的地址，我们把它叫做接口或接口地址。

- 接口，是后端同学提供的，至于如何实现，我们无需关心，那是后端同学的事。
- 接口，也是一个`网址`，通过客户端向这个网址发送请求，可以获取到接口返回的结果。

实际开发中，有很多这样的接口，也有很多提供接口的网站，下图是一个QQ号码测吉凶的接口，通过改变QQ号，接口返回对应的结果。

接口地址：http://japi.juhe.cn/qqevaluate/qq?key=55b50bf0d8b67d6659b535d138df659d&qq=295424589

![a](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/a.gif)

除此之外，还有很多接口，比如天气信息接口：

[https://www.tianqiapi.com/api/?appid=22449382&appsecret=Vudt9mVQ&version=v1&city=北京](https://www.tianqiapi.com/api/?appid=22449382&appsecret=Vudt9mVQ&version=v1&city=北京)

> 我们把接口看做一个带有返回值的函数即可，通过客户端访问接口，就相当于调用该函数，并可以得到它的返回值。
>
> 有些函数调用需要参数，接口也是如此。

> 对于接口的功能，一般会有一个专门的文档来介绍

## 接口文档

接口文档中记载了后端同学提供的接口的详细信息，大致包括，接口地址、作用、请求方式、请求参数、响应结果等等。

我们使用的服务器软件中也内置了很多接口，具体可以查看 `接口文档`。

向接口发送请求非常之简单，你只需要会套 `$.ajax()` 这个方法即可。

```js
$.ajax({
    type: '请求方式',
    data: '请求参数',
    url: '接口地址',
    dataType: '响应数据类型',
    success: function (res) {
        // res 就是响应结果
    }
});
```

接口参数可以按下面两种方式来填写，哪一种写法都可以：

- 方式一：`参数=值&参数=值...`
- 方式二：`{参数: 值, 参数: 值, ...}`

> 小知识点，请求参数是客户端额外发送到服务器的数据，告知服务器此次请求的具体信息
>
> 无论使用哪种写法编写请求参数，实际发送到服务器的总是方式一那样的字符串

## 接口应用，完成验证用户名案例

在上网注册的时候，经常会遇到验证用户名是否存在的情况。比如下面图示的是[博客园的注册页面](https://account.cnblogs.com/signup)验证用户名的场景。

![d](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/d.gif)

我们也可以使用自己的 `/common/checkUser` 接口，完成这样的验证。

> 注意，接口文档告诉我们了，zhangsan、lisi、wangwu 三个用户名已经注册过了

实现过程分析：

- 不再是刷新页面就发送Ajax请求了，应该在input失去焦点时，发送验证用户名的Ajax请求
- 需要验证的用户名不能写死，应该是用户在文本框中输入的值
- 服务器返回的结果，不应该直接console.log了，应该判断后，在页面中给出提示

具体代码：

```html
<input type="text" id="username">
<span></span>

<script src="./assets/jquery.js"></script>
<script>
    // 1. 注册 input的失去焦点事件
    $('input').blur(function () {
        var uname = $(this).val(); // 获取输入框中的值
        // 2. 发送ajax请求，验证用户名
        $.ajax({
            type: 'GET',
            url: '/common/checkUser',
            data: {username: uname},
            // data: 'username=' + uname, // username=xxx
            dataType: 'json',
            success: function (result) {
                console.log(result);
                // 3. 在span标签中给出提示
                $('span').text(result.msg);
            }
        });
    });
</script>
```



## 案例--留言板

### 发送Ajax请求，获取所有的留言

1. 准备工作
   1. 将 `Ajax阶段资料/03-发布微博网页模板（Ajax案例使用）` 中的 `weibo.html`及`css`、`images`文件夹拷贝到`public`文件夹中。
   2. 浏览器访问 localhost:4000/weibo.html，能够看到初始页面。
2. 按照接口文档，套 $.ajax() 方法

### 将数据渲染到页面中

1. 渲染
   1. 就是把从服务器获取的数据，放到页面上显示
2. 具体做法
   1. 将从服务器获取的数据（变量result）循环
   2. 循环过程中，拼接 `li` 标签
   3. 循环之后，把拼接好的所有 `li` 放到 `ul` 中即可

### 单击按钮，实现发布留言

1. 为按钮注册单击事件
2. 事件处理函数中，获取输入框的值（留言人的名字和内容）
3. 按照接口文档，套 $.ajax() 方法
4. 添加留言成功后，让页面显示新的留言
   1. 将前面获取留言的代码封装成函数。
   2. 添加成功之后，调用函数，从新获取数据。
5. 清空输入框的值

## $.ajax() 方法的详解

### type

1. 意义
   - 表示请求的方式或方法（method）
2. 最常见的两种请求方式
   - GET
   - POST
3. GET和POST的异同
   - 不同点：
     - get  ：获取，得到。这种方式请求用于向服务器请求资源（图片，文件，数据....）。它是最常见的请求方式。它的重点在于，它只是请求，而`不会改变`服务器上的资源。
     - post：派送，投递。这种方式的请求用于向服务器上提交数据，它的重点在于，它`可能会修改`服务器上的资源。
   - 相同点
     - get和post请求都可以在发请求时附带一些数据。例如：根据用户名去检查这个用户是否被占用；在论坛中注册一个账号。
     - get和post请求都能够从服务器上获取返回的数据。

> 实际开发中，接口都是后端同学提供的，所以接口支持哪种请求方式，还得以文档为准。

### data

1. 意义
   - 向接口发送请求的时候，携带的数据，也就是接口文档中的请求参数
2. 写法
   - 对象形式，形如： `{name: 'xxx', content: 'xxx'}`
   - 字符串形式，形如： `name=xxx&content=xxx`

> 无论写法如何，实际上发送给服务器的数据都是 字符串形式。多个请求参数之间，使用 & 符号隔开。GET请求的时候，这个字符串和接口之间使用 ? 隔开

### dataType

1. 意义
   - 服务器响应数据的格式。
   - 指定该项，jQuery会自动将服务器响应的数据处理成JS数据（数组、对象、字符串、布尔等等）
2. 可选的值
   - `json`，它是==最最常见==的数据传输格式。能够以简单的语法表示复杂的数据
   - `text`，表示服务器返回的是文本类型的数据
   - `xml`，表示服务器返回的是xml格式的数据，目前项目中很少使用它了，这里作为了解
   - `jsonp`、`script`、`html`等其他值

> 当我们已经知道了服务器返回数据的格式，则最好指定 `dataType`

### beforeSend

1. 意义

   - 在发送Ajax请求之前，允许我们做一些事情

2. 语法

   ```js
   $.ajax({
       beforeSend: function () {
           // 发送请求之前，你需要做什么？可以写到这里
       }
   });
   ```

### complete

1. 意义

   - 在Ajax请求结束之后，允许我们做一些事情

2. 语法

   ```js
   $.ajax({
       complete: function () {
           // Ajax请求结束了，你想做什么？可以写到这里
       }
   });
   ```

## 原生的Ajax请求

在实际的开发中，我们会直接使用如jquery这样的第三方工具库来调用ajax，而不会自己去手写一个原生的。但对于学习者来说，深入学习原生ajax能帮助我们更好的理解和掌握 。

原生的Ajax实现，是基于浏览器内置对象 `XMLHttpRequest` 提供的API实现的。

### 基本语法

1. GET方式写法

   ```js
   // 1. 实例化 XMLHttpRequest对象
   var xhr = new XMLHttpRequest();
   // 2. 通过 open(请求方式, url) 方法，设置请求方式和url
   xhr.open('GET', '/common/time');
   // 3. 调用 send() 方法，发送请求。 ---> 此步骤，表示开始发送请求
   xhr.send();
   // 4. 准备一个事件，当请求响应过程结束后，会触发该事件；在事件处理函数中，接收服务器响应的结果
   xhr.onload = function () {
       // 使用 xhr.response; 来接收结果
       console.log(xhr.response);
   }
   ```

   如果有请求参数

   ```js
   xhr.open('GET', '接口地址?参数=值&参数=值....');
   ```

   

2. POST方式写法

   和GET请求相比，多了一行代码，并且请求参数的位置变化了。

   ```js
   var xhr = new XMLHttpRequest();
   xhr.open('POST', '/message/addMsg');
   // 相比GET方式，POST方式多下面一行代码
   xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
   xhr.send('name=李白&content=举杯邀明月');
   xhr.onload = function () {
       console.log(xhr.response);
   }
   
   ```

### 用原生的Ajax实现验证用户名案例

实现代码：

```js
document.getElementById('username').onblur = function () {
    // 0. 获取输入框的值
    var uname = this.value;
    // 1. 实例化 XMLHttpRequest对象
    var xhr = new XMLHttpRequest();
    // 2. 通过 open(请求方式, url) 方法，设置请求方式和url
    xhr.open('GET', '/common/checkUser?username=' + uname);
    // 3. 调用 send() 方法，发送请求。 ---> 此步骤，表示开始发送请求
    xhr.send();
    // 4. 准备一个事件，当请求响应过程结束后，会触发该事件；在事件处理函数中，接收服务器响应的结果
    xhr.onload = function () {
        // 使用 xhr.response; 来接收结果
        console.log(xhr.response);
    }
}

```

> 课后，大家可以把留言板案例也用原生的ajax写一写。



### 异步操作

这是ajax这部分的一个难点。

异步指的是一段耗时的JS代码在执行时不会阻塞后续代码的执行。

看一个例子：

```js
// 执行一个输出
console.log(111);

// 一个耗时的定时器
setTimeout(function () {
    console.log(333);
}, 2000);

// 再执行一个输出
console.log(222);

```

执行上面的代码，输出结果是怎样的呢？答案很简单，先输出111、然后输出222、最后输出333。

为什么呢？因为定时器是一个耗时操作，而且定时器之后的代码==不需要==等待定时器执行完毕才执行。==这就是一个异步操作==。

我们来画一个时间轴，来深层次的看一下异步操作。

![1570871012295](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570871012295.png)

从图中不难发现，`定时器` 和 `输出222` 在某个时间点同时运行了。

==所以异步操作的本质是同一个时间点，有多个操作并行执行了；耗时操作（定时器）并不会阻塞后面代码的执行。==

- 同一个时间点，执行了多个操作
- 耗时操作不会阻塞后续代码的执行

我们所说的Ajax也是一个耗时操作，因为从发送请求开始（调用send方法），该请求就去服务器请求资源去了，直到完全接收到服务器响应的结果，这一过程肯定需要一定的时间。

那么如果把定时器的代码换成Ajax的代码，输出结果是怎样的呢？

```js
// 执行一个输出
console.log(111);

// 中间是一个耗时的ajax请求
var xhr = new XMLHttpRequest();
xhr.open('GET', '/common/time');
xhr.send();
xhr.onload = function () {
    console.log(333);
}

// 再执行一个输出
console.log(222);

```

答案和前面一样，也是先输出111、然后输出222、最后输出333。==这说明上面的ajax请求也是一个异步的操作==。

![1570872090640](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-01/%E7%AC%94%E8%AE%B0/%E6%96%B0%E7%89%88Ajax.assets/1570872090640.png)



## 反馈建议与意见

- 会使用$.ajax() 方法

```js
$.ajax({
    type: '请求方式', // 可选的值有GET和POST，默认是GET
    url: '接口地址', // 必填
    data: '请求参数', // 两种写法， 'aa=xxxx&bb=yyyy'    {aa: 'xxxx', bb: 'yyyy'}
    dataType: '响应数据格式', // 绝大多数都是json、默认是text，如果指定这项，jQuery内部会自动处理响应结果
    success: function (res) {
        // 当请求响应成功了，会执行这个函数，并且形参res就是服务器返回的结果
    },
    beforeSend: function () {
        // 请求开始之前，需要做什么，写到这里
    },
    complete: function () {
        // 请求结束（无论请求成功还是失败），需要做什么，写到这里
    }
});
```

- 转变思想
  - 不能直接以文件的方式打开服务器上的资源了，比如使用客户端向服务器发送请求，从而得到服务器响应的结果
  - 必须使用服务器

![1571013161984](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax--02%E5%8E%9F%E5%A3%B0js/%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0.assets/1571013161984.png)



## 原生的Ajax请求

### 基本语法

- GET

  ```js
  // 原生的Ajax请求，使用的是 XMLHttpRequest 对象提供的API（属性和方法）
  
  // 1. 实例化 XMLHttpRequest 对象，request单词的意思是请求
  var xhr = new XMLHttpRequest();
  // 2. 调用open方法，设置请求的方式和url
  xhr.open('GET', '/common/time');
  // 3. 调用send方法，发送请求   ---> 到这一步，才表示发送ajax请求
  xhr.send();
  // 4. 当请求响应过程结束，然后接收服务器响应的结果
  xhr.onload = function () {
      console.log(xhr.response);
  }
  ```

  - 如果有请求参数

    - 请求参数要拼接到url后面即可

      ```js
      xhr.open('GET', '/common/checkUser?username=lisi');
      ```

      

- POST

  ```js
  // 1. 创建xhr对象
  var xhr = new XMLHttpRequest();
  // 2. 调用open方法，设置请求方式和url
  xhr.open('POST', '/message/addMsg');
  // 3. 设置一个请求头，固定的一行代码
  xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');   
  // 4. 调用send，发送请求
  xhr.send('name=xxx&content=xxx');
  // 5. 设置onload事件，接收服务器相应的结果
  xhr.onload = function () {
      console.log(this.response);
  }
  ```

  

### GET和POST的区别

- 意义
  - GET：请求一般用于获取服务器上的资源，这种请求不会改变服务器上的资源
  - POST：一般用于提交数据给服务器，这种请求有可能会改变服务器上的资源
- 写法
  - 请求参数位置不同
  - POST请求多了一行代码

### 小案例

接口中的请求参数id，和下图中的文件名是一个意思。

- id = 0 ,表示获取所有的省
- id = 105 ，表示获取河北省下属的市
- id = 105001， 表示获取石家庄市下属的县

![1571020189620](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax--02%E5%8E%9F%E5%A3%B0js/%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0.assets/1571020189620.png)





### 浏览器的问题

#### readyState和onreadystatechange

xhr.onload 事件，属于XHR对象新增的一个属性，IE6、IE7、IE8不支持onload。低版本的浏览器可以使用onreadystatechange事件来代替。

- onreadystatechange事件
  - 会触发多次
  - 触发时机
    - 当readyState属性值（ajax的状态）改变的时候（0-->1、 1-->2 ....），会触发
    - 接收的数据量发生变化了，也会触发
- readyState属性
  - 表示ajax的执行状态，值分别是0/1/2/3/4 ，共计5个值

![1571022320588](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax--02%E5%8E%9F%E5%A3%B0js/%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0.assets/1571022320588.png)

#### IE缓存问题

- 产生原因
  - 两次或多次ajax的GET请求，url地址完全一致
- 解决办法
  - 让每次请求的url不一致

### 其他API

#### 创建xhr对象的兼容写法

- var xhr = new XMLHttpRequest();
- var xhr = new ActiveXObject('Microsoft.XMLHTTP');   // IE6 IE7 的写法

#### responseType属性

类似于 $.ajax() 中的 dataType。

指定该属性，会把JSON等格式的数据转成JS数据（对象、数组等）



### 原生Ajax小结

至此，我们学习了很多 XHR 对象的 属性和方法 （统称API）。其实这些API分属不同的XHR版本。

- XHR 1 版 API -- 最初的XHR对象提供的API，基本上兼容所有的浏览器
  - open -- 设置请求方式、请求url、同步或异步
  - send -- 发送请求
  - readyState -- ajax的状态，值（0，1，2，3，4）
  - onreadystatechange -- 当readyState的值改变的时候，或当接收的数据发生改变的时候都会触发
  - responseText：-- 用于接收服务器返回的 `文本类型` 的结果
- XHR 2.0 新增API，基本上不再支持IE6、IE7、IE8
  - onload（2014年新增） -- 当请求响应成功了，会触发
  - onprogress -- 当响应的数据，正在接收中，会触发。数据量比较大的话，可能会触发多次，可以使用它做一个进度条
  - onloadstart -- 当请求开始的时候，会触发
  - onloadend -- 当请求结束的时候，会触发
  - response ：可以接收任何的响应结果
  - responseType（2012年新增）：配合response使用的一个属性

> 实际开发中，原生的Ajax使用的概率非常少。一般都使用封装好的库，比如 jQuery中的 $.ajax()

## 同步和异步

### 异步

==所以异步操作的**本质**是同一个时间点，有多个操作同时执行了；耗时操作（定时器）并不会阻塞后面代码的执行。==

- 同一个时间点，执行了多个操作
- 耗时操作不会阻塞后续代码的执行

### 同步

同一个时间点，只能执行一个操作。前面的代码没有执行完毕，后续代码都不能执行。

## 封装

```js
/*
type: 请求方式
url: 请求接口地址
data: 请求参数
cb: 用于处理服务器响应结果的回调函数。cb取自单词 callback
*/
function ajax (type, url, data, cb) {
    var xhr = new XMLHttpRequest();

    var params = null;
    // 判断是否是GET方式
    if (type === 'GET') {
        // 把url和data拼接到一起，形成 /common/checkUser?username=xxx
        url = url + '?' + data;
    }
    xhr.open(type, url);

    // 判断是GET还是POST请求
    if (type === 'POST') {
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        // 重置 aaaaa = data
        params = data;
    }

    xhr.send(params);

    xhr.onload = function () {
        // console.log(this.response)
        cb(this.response);
    }
}

/* function chuli (res) {
            console.log(res);
        } */

ajax(
    'POST', 
    '/message/addMsg', 
    'name=xxx&content=yyy', 
    function (res) {
        console.log(res);
    }
);
```



回调函数是处理异步请求结果的最佳方案。

## 小结

- 原生的Ajax写法
  - GET （4个步骤）
  - POST（5个步骤）
  - GET和POST写法上的区别
    - POST多了一行代码
    - 请求参数的位置不一样
- 浏览器问题
  - onreadystatechange事件配合readyState，完成获取响应结果的任务，代替onload事件
  - IE缓存问题（产生原因、解决办法）
- API小结
  - XHR1.0 版本
    - open
    - send
    - onreadystatechange
    - readyState
    - responseText
  - XHR2.0新增
    - onload
    - responseType
    - response
    - onprogress/onloadstart/onloadend ....
- 同步和异步
  - 异步：同一个时间点，可以执行多个操作。耗时操作不会阻塞后续代码的执行。
  - 同步：同一个时间点，只能执行一个操作。耗时操作肯定会阻塞后续代码的执行。
- 封装
  - 把需要变化的位置，设置为形参即可
  - 处理异步请求的结果，必须使用回调函数。



FormData

模板引擎

综合案例

## 回顾

- readystate change事件的不同触发时机
  - 当readyState的值变化的时候（0-->1  1-->2  2-->3  3-->4）
  - readyState的值没有变化，但是接收到的数据发生变化的时候，也会触发
- 同步和异步
  - 同步：代码从上到下依次执行，前面的代码没有执行完，后面的代码不能执行。
  - 异步：代码从上到下依次执行，前面的代码没有执行完，不会阻塞后续代码的执行。

## FormData

- 有form表单

  ```js
  // 使用FormData步骤1： 找到form表单，找表单的dom对象
  var fm = document.getElementById('fm');
  // 使用FormData步骤2： 实例化FormData，并传递表单即可，得到的对象里面包含了所有的值
  var formdata = new FormData(fm);
  
  ....
  ....
  xhr.send(formdata);
  ....
  ```

- 请求头的设置

  - 如果提交的数据是纯文件，没有文件上传。需要设置请求头
  - ==使用FormData的时候，不需要自己设置请求头==

- 注意事项

  - 不能让表单提交
    - 设置按钮为button类型
    - JS代码中，通过事件对象阻止表单提交的这种默认行为
  - 表单中各项必须有name属性，因为FormData收集表单数据的时候，就是根据name属性获取的

- 关于文件域的补充

  - 标签的属性
    - multiple  --  设置后，表示允许选择多个文件
    - accept -- 可以上传文件的类型，写法有 `.jpg,.png,.gif` 或 `image/png` 或 `image/*`
  - JS代码中，如果找到文件对象
    - `document.getElementById(文件域的id).files[0]`

- FormData 中的 append方法

  - 作用是，向FormData对象中追加一些值
  - 用法： 
    - `formdata.append('pwd', 'hello');`
    - `formdata.append('pic', document.getElementById('pic').files[0]);`

## 模板引擎



## 综合案例

### 删除

==接口代码有误：将 `ajax/router/members.js` 中的第85的`query`改成`body`。保存之后，重启服务即可。==

关键点：

- 删除的接口，需要会员的id。
  - 在渲染页面的时候，就应该把id渲染到页面中
  - id不应该直接显示出来，所以把id当做 Delete 标签的属性值
- 注册事件的时候，必须使用==事件委托==的方案
- confirm() 是一个提示框。用户点击确定，返回true；用户点击取消，返回false
- 移除元素的时候，注意this指向问题

### 查看详情

- 超链接跳转属于GET请求，如果传递参数，需要在url后面拼接  `detail.html?id=23`
- 获取地址栏的参数：`location.search`

### 预览图片

1. 找到文件对象，==必须通过DOM对象找文件对象==；  
2. 通过 `URL.createObjectURL(文件对象)` 可以得到一个用于访问图片的临时的url
3. 设置预览图片的src属性即可。

### 添加会员

- 注意：一定要按接口写代码
- 表单各项（每个input）的name属性必须设置，因为FormData收集表单数据的时候，是根据name属性获取的
- 表单各项的name属性，必须和接口要求的请求参数一致
- jQuery+FormData的使用
  - 必须加入 `contentType: false` ，目的是不需要设置Content-Type，浏览器会自行处理
  - 必须加入 `processData: false`， 目的是不需要处理formdata数据。

### 懒加载

- 思路

  - 找到何时该去加载下一页的数据

    ![1571126953761](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-03-%E6%A1%88%E4%BE%8B/%E7%AC%94%E8%AE%B0/%E7%AC%94%E8%AE%B0.assets/1571126953761.png)

  - 如何加载下一页的数据

    - 调用 `/member/list-page` 接口，只不过让请求参数 `page` 的值加 `1` 

- 解决重复加载的BUG

  - 重复加载数据，是因为滚动条不好控制，不小心就滚动多了，会多次调用loadData() 函数
  - 解决办法
    - 进入到loadData中，马上设置flag为false。（flag=false表示不允许调用loadData了）
    - 当前页的数据处理完毕，重置flag为true。

## Ajax的补充

### 是什么

- 字面意思
  - Ajax 即“Asynchronous  Javascript  And  XML”（异步的 JavaScript 和 XML）
- 深层意思
  - 是一种通过JS代码完成客户端和服务器端交互的技术

### 典型应用场景

在`不更新页面`的情况下（页面有没有更新就检查后退按钮），浏览器要从web服务器获取数据，此时就可以使用ajax技术。

先来对比更新和不更新页面，以分页为例

- 大学的公告页，没有使用AJAX：http://www.whut.edu.cn/tzgg/
- 博客园的主页,   使用了AJAX：<https://www.cnblogs.com/>

经典应用

- 博客页的注册页：<https://account.cnblogs.com/signup>
- 购物网站：http://www.smzdm.com

### AJAX技术的好处

总结如下两点好处：

1. 局部更新，提升用户体验，提升性能。
2. 分离开发，提高开发效率。
   1. 前端 调用接口
   2. 后端 开发接口

## jQuery中的ajax补充

- $.ajax();

  ```js
  $.ajax({
      type: '请求方式',
      url: '接口地址',
      data: '请求参数',
      dataType: '响应数据格式',
      success: function (res) {
          // res就是服务器返回的结果
      },
      beforeSend: function () {},
      complete: function () {},
      contentType: '设置请求头中的content-type的值',
      processData: '是否处理请求参数'
  });
  ```

  

- $.get()

  ```js
  $.get('url', [请求参数], [请求成功后的回调函数], [服务器返回数据的类型]);
  ```

  

- $.post()

  ```js
  $.post('url', [请求参数], [请求成功后的回调函数], [服务器返回数据的类型]);
  ```

  

## 其他封装库 axios （了解）

### axios库

jquery中封装了ajax功能，但是它的体积比较大。如果我们只希望使用ajax功能，而不需要dom操作的话，我们可以选择使用axios库。(fetch)

应用：

```
- 它只专注于处理http请求，比jquery的体积小的多，适用于只需要ajax请求的业务场景；
- 后期学习三大前端框架时也会用到；
```

#### 使用示例

通过官网查看其使用方法。

与jquery一样，要使用它，必须先引入这个文件。然后就可以按如下的格式去使用了。

中文网站：<http://www.axios-js.com/zh-cn/docs/

```javascript
// 获取服务器的返回值
axios.get('/common/get?id=123').then(function(res) {
    // res 就是本次请求的信息
    console.info(res);
    // 获取 从服务器返回的数据
    console.info(res.data);
});

axios.get('/common/get', { params: { id: 123, name: 'jake' } }).then(function(res) {
    // res 就是本次请求的信息
    console.info(res);
    // 获取 从服务器返回的数据
    console.info(res.data);
});

// post请求，不带参数
axios.post('/common/post').then(function(res) {
    console.info(res.data);
});
// post请求，带参数
axios.post('/common/post', { id: 123, name: 'jake' }).then(function(res) {
    console.info(res.data);
});
```



## 模板引擎

### 模板引擎介绍

客户端中拿到请求的数据过后最常见的就是把这些数据呈现到界面上。

如果数据结构简单，可以直接通过字符串操作（拼接）的方式处理，但是如果数据过于复杂，字符串拼接维护成本太大，就不推荐了。

> 模板引擎：
>
> - artTemplate：https://aui.github.io/art-template/

模板引擎实际上就是一个 API，模板引擎有很多种，使用方式大同小异，目的为了可以更容易更高效的将数据渲染到HTML字符串中。==通俗的说，模板引擎的目的就是将服务器返回的数据显示到HTML页面中==。

### 使用模板引擎步骤

1. 准备一个存放数据的盒子（不是必须的，使用body也可以）

2. 引入template-web.js文件

3. 定义模板（具体语法可以去官网查看），一定要指定script的id和type属性

4. 调用template函数，为模板分配数据，template函数有两个参数一个返回值

   1. 参数1：模板的id
   2. 参数2：分配的数据，必须是一个JS对象的形式
   3. 一个返回值：是数据和模板标签组合好的结果

5. 将 “拼接” 好的结果放到准备好的盒子中（不是必须的，console出来也可以看结果）

   ![1566443384929](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/Ajax-03-%E6%A1%88%E4%BE%8B/Ajax%E8%A1%A5%E5%85%85.assets/1566443384929.png)

```html
<script src="./assets/template-web.js"></script>

<script type="text/html" id="test">
        <h2>{{title}}</h2>
        <p>{{age}}</p>
        <ul>
            <li>{{heroes[0]}}</li>
            <li>{{heroes[1]}}</li>
            <li>{{heroes[2]}}</li>
    </ul>
</script>

<script>
    // 下面的数据是模拟的，相当于ajax请求之后，服务器返回的数据
    var data = {
        title: '模板引擎练习',
        age: 20,
        heroes: ['曹操', '刘备', '李逵', '张飞']
    };
    // 调用template函数
    /*
        var str = template(模板的id, 数据); // 数据必须是JS对象格式
        */
    var str = template('test', data);
    console.log(str);
</script>
```

> 定义模板时的script标签一定好指定id和type
>
> tempalte函数语法：var html = template(模板id,  Object);

### 模板语法

- 输出普通数据（字符串、数值等）

  ```
  // 模板写法
  {{var}}
  
  // template函数写法
  var html = template('id', {
      var: 'hello world'
  });
  ```

- 条件

  ```
  // 模板写法
  {{if age > 18}}
  	大于18
  {{else}}
  	小于18
  {{/if}}
  
  // template函数写法
  var html = template('id', {
      age: 20
  });
  ```

- 循环

  ```
  // 模板写法
  {{each arr}}
  	{{$index}} -- 数组的下标
  	{{$value}} -- 数组的值
  {{/each}}
  
  // template函数写法
  var html = template('id', {
      arr: ['apple', 'banana', 'orange']
  });
  
  ```

完整的代码：

```html
<script src="./assets/template-web.js"></script>

    <!-- 1. 定义模板 -->
    <script id="abc" type="text/html">
        <h1>{{name}}</h1>
        <p>我是{{nickname}}，我有一辆{{car}}，我今年{{age}}岁了</p>
        {{if age >= 18}}
            <p>欢迎来玩~</p>
        {{else}}
            <p>未成年人禁止进入</p>
        {{/if}}
        <p>我有好几个女朋友，分别是：</p>
        <ul>
            {{each girls}}
            <li>{{$index}} -- {{$value}}</li>
            {{/each}}
        </ul>
    </script>


    <script>
        // 2. 调用template函数
        var str = template('abc', {
            name: '狗哥',
            nickname: '北狗最光阴',
            car: '宝马',
            age: 31,
            girls: ['王婆', '金莲', '西门大官人', '李师师', '赛金花']
        });

        console.log(str);
        document.body.innerHTML = str;
    </script>

```



### 案例中使用模板引擎处理响应数据

下面以留言板案例为例。

```html
<!-- 引入template-web.js -->
<script src="./assets/template-web.js"></script>

<!-- 定义模板 -->
<script id="moban" type="text/html">
    {{each girls}}
    <li class="media">
      <img class="mr-3" src="avatar.png" alt="">
      <div class="media-body">
        <h4>{{$value.name}}</h4>
        <p>{{$value.content}}</p>
    </div>
    </li>
    {{/each}}
</script>

```

```js
xhr.onload = function () {
    // console.log(this.response);
    var data = JSON.parse(this.response);
    console.log(data);
    // 拼接字符串
    var str = template('moban', {
        girls: data
    });
    // 把变量后，拼接好的str放到 id为 messages 的ul中
    document.getElementById('messages').innerHTML = str;
}

```

