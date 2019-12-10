# Node.js - day01

1. Ajax

   1. 工作中:页面布局,js效果,调接口
   2. 原生的Ajax
   3. 封装的Ajax(用的最多):
      1. jQuery.Ajax
      2. `axios`
   4. Ajax发生请求必须知道的内容
      1. url地址
      2. 请求的方法
      3. 参数
      4. success:(回调函数)
         1. 根据需求来编写
         2. 提示用户
         3. 结合模板引擎渲染页面
         4. 跳转页面

   ```javascript
   // 特定的时候
   $.ajax({
   	url:'c+v出来',
       type:'c+v出来',
       // 根据文档来生成
       // 对象形式{key:value,key2:value2}
       // data:{}
       // formData 创建formData
       // new FormData(form的dom元素)
       // form中没有的数据`append(key,value)`
       data:formData,
       contentType:false,
       processData:false,
       // 请求成功的处理逻辑
       success:function(backData){
           // 基于backData写逻辑
         	//刷新自己的页面
         	window.location.reload();
       }
   })
   
   ```

   原生Ajax的使用 :偶尔会被问及

   ```javascript
   // 实例化一个Ajax对象(异步对象)
   var xhr = new XMLHttpRequest()
   // 设置请求的地址和请求的方法
   xhr.open(url,type)
   // 设置请求头(post必须,get可选)
   xhr.setRequestHeader('content-type','application/x-www-form-urlencoded')
   // 发生请求
   xhr.send()
   // 注册回调函数(事件)
   xhr.onload = function(){
       // 判断状态
       xhr.responseText
       
   }
   ```

   ![1571792342869](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/node%E5%9F%BA%E7%A1%80-01/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571792342869.png)

   ![1571792581328](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/node%E5%9F%BA%E7%A1%80-01/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571792581328.png)

2. 大事件

   1. Ajax的综合使用
      1. 什么时候需要调用接口?
      2. 操纵数据的时候需要调用接口
         1. 增删改查
   2. 插件的实际应用
      1. 导包
      2. `c+v`示例代码 基本都能跑
      3. `根据需求`设置各种选项
         1. 第三步,会随着你的使用越来越熟练
   3. 业务逻辑
      1. 在特定的时候
         1. 点击事件
         2. 失去焦点
         3. onload事件
         4. ....事件
      2. 干一些事情
         1. dom操纵
            1. 获取元素,操纵他们
         2. 基于Ajax的数据操作
            1. 根据文档调用
            2. 回调函数中干事情











## Node.js课程介绍

1. 安排:
   1. node基本概念
   2. es6新语法
   3. 内置模块,第三方模块(用包)
   4. express框架(web开发的框架,快速写接口,写后台逻辑)
   5. mysql(数据库,增删改查)
   6. 项目(自己写接口,自己调用自己写的接口)
2. 重点:
   1. 了解后台开发干的事情:
   2. 能够写出简单的接口:基本的增删改查
   3. 能够熟练用`npm`的装包,引包,用包
3. 全栈工程师:
   1. 前端+后端

## Node.js基本概念

> 基于chrome v8引擎的 javascript运行环境
>
> 服务端的js

官网: https://nodejs.org/en/ 

中文网: http://nodejs.cn/ 

1. 浏览器中 有一个可以解析 js的 解析器
   1. 解析器:(翻译官)
      1. 把编程语言  翻译为计算机可以识别的 二进制
      2. js---(翻译官v8引擎)->计算机执行
   2. chrome的js解析器(翻译官),v8引擎 目前世界上最快的,js解析器
2. js运行环境:
   1. 通过`node.js`也可以直接运行`js`代码
3. 这个阶段的js代码很大一部分,不需要通过浏览器运行,直接敲命令即可

## Node.js安装

下载地址: https://nodejs.org/en/ 

![1571793573698](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/node%E5%9F%BA%E7%A1%80-01/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571793573698.png)一直下一步:即可

打开黑窗 

```bash
node -v
```

## js组成

1. 浏览器端:
   1. ECMAScript:js语法,for循环,if else,var...
   2. DOM(文档对象模型):
      1. 约定了操纵dom元素的语法
      2. `dom.style.width`样式中的宽度
      3. `dom.onclick`事件绑定
      4. `dom.appendChild`追加后代
      5. ....
   3. BOM(浏览器对象模型):
      1. 操纵浏览器的语法
      2. `window.alert()`
      3. `window.location.href`
      4. `window.setTimeout`
      5. ....
2. 服务器端(没有浏览器):
   1. ECMAScript:js基础语法,for循环,if else,var....
   2. 学习了bom语法中的一些常用api
      1. `定时器,console 等等`
   3. 模块(类似于之前用的jQ,swiper...)
      1. 内置模块:自带的
      2. 第三方模块:别人写的,下载才可以使用

## Node.js 基本使用-REPL(了解)

1. 打开黑窗
2. 输入`node`回车
3. 写`js代码` 回车运行
4. 循环`步骤3`

REPL

read(读取) eval(解析) print(打印) loop(循环)

用的不多,了解即可,跑一些简单的代码

## Node.js 基本使用-执行js文件

1. 写好一个`js文件`
2. 内部有`node.js`支持的代码
3. 打开黑窗输入`node 文件名` 回车
4. 运行



注意

1. 文件名不能写错,写错提示找不到
2. 文件名不需要打全,写个开头 +`tab`自动提示
3. 黑窗打开的位置 和`js`在一个文件夹下
4. 语法不要写错
5. 路径确保和js文件一致
6. 文件名不要叫`node.js`
7. 报错查看
8. ![1571796605214](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/node%E5%9F%BA%E7%A1%80-01/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571796605214.png)



在vscode中打开终端

右键文件->在终端中打开->输入命令运行即可

关闭终端的快捷键

ctrl+`   1左边的那个按钮



## ES6 - 基本概念

 `ES6`等同于`ECMAScript 2015`

1. `2015年推出的新的语法规范`
2. 简称`ES6`
3. `ES6`的改变最大,新功能最多

阮一峰ES6教程: http://es6.ruanyifeng.com/ 

不适合新手入门

## var的缺点

1. 变量提升
2. 没有块级作用域`{}`
3. 可以重复声明

## ES6 - let

> 变量声明

1. 没有变量提升
2. 有块级作用域`{}`
3. 不能重复声明
4. 替代`var`
5. 别再写`var`了,用`let`

```javascript
let 变量名 = 值
```

## ES6 - const

> 常量声明

1. 不会提升
2. 有块级作用域
3. 不能重复声明
4. 必须在声明式就赋值
5. 能用const 不用let 能用let 不用 `var`

   



## ES6 - 对象的属性的简化写法

> 更简单的属性赋值

```javascript
const name ="jack"
const person ={
    // 属性名和 值的名字相同
	name:name,
	// 可以写成
	name,
	jump:function(){},
	// 可以写成
	jump(){}
}
```



## ES6 - 模板字符串

> 轻量级的`模板引擎`,原生支持,不用导包

1. 定义的时候使用  `(1左边的符号)
2. 挖坑的语法`${表达式}`
3. 坑中必须有东西
4. 可以换行,简单的模板生成直接使用`模板字符串`即可
5. 复杂的还是用模板引擎



## 易错点

1. 输入了`node`回车 如何退出? `ctrl+c`两次
2. 对象的属性获取语法,还是`对象.属性`或者`对象.方法()`
3. `模板字符串`使用

## ES6 - 函数默认值

> 为函数设置默认值

1. 调用函数时,不传递参数,参数可以有一个默认值
2. 早期会使用短路运算来实现默认值的设置

```javascript
// es6中的默认值
// 参数=默认值
// 不传递参数直接使用默认值,传递了参数使用传递的值
function sayHi(name='路飞',skill='橡胶果实') {
    console.log(name,skill);
}
// sayHi();
sayHi('索隆','迷路');
```



## ES6 - 对象解构(使用频率挺高)

> 更方便的对象属性取值

```javascript
// 定义对象
const person = {
    name:"食戬(jian)之灵",
    desc:"美食番,教你做饭",
    spec:"食物越好吃,衣服就越少"
}
// const name = person.name;
// const desc = person.desc;
// const spec = person.spec;

// 解构赋值
// skill undefined 上面没有定义
// const {name,desc,spec,skill} = person;
// 也可以只获取某一些
const {name} = person;
```



## ES6 - 对象解构实际应用

> 结合函数用起来挺过瘾的

1. 函数的参数解构
   1. ![1571803973215](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/node%E5%9F%BA%E7%A1%80-01/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571803973215.png)
   2. 实际调用时会有更多的提示
2. 函数的参数解构结合默认值

```javascript
function eatFood({food1="西兰花炒蛋",food2="西红柿炒蛋",food3="韭菜炒蛋",food4="黄瓜炒蛋"}) {
    console.log(food1,food2,food3,food4);
}
```



## ES6 - 数组解构(了解)

> 更快的获取数组中的值

```javascript
// 数组
const cartoonArr = ['喜洋洋','熊出没','铁甲小宝','天线宝宝','海绵宝宝','中华小当家'];

// 取值
// const c1 = cartoonArr[0];
// const c2 = cartoonArr[1];
// console.log(c1,c2);

// 解构
// 获取的顺序 和数组的的元素的对应关系是一致
// 数组大部分时候都是通过下标获取某一个
// 数组的解构用的 不多 了解即可
const [c1,c2,c3,c4,c5,c6] = cartoonArr;

console.log(c1,c2,c3,c4);

```

## 终端补充

1. 多个终端的区别
   1. 终端可以理解为是一个没有界面的    软件
   2. 通过输入内容让他干事情
   3. `cmd`微软早期推出的 功能最少,不太好用
   4. `git bash` 安装了`git`之后自带的,功能强大,支持很多`cmd`没有的命令,`linux`的命令也基本上都支持
   5. `power shell`:微软后续退出的终端,功能牛逼很多,但是还是比`git bash `支持的命令少一些

## ES6 - 对象展开

> ...结合对象使用

```javascript
// 对象
const person = {
    skill:"跳水",
    habbit:"抗冻"
}
const student ={
    sleep:"呼噜呼噜!!",
}

const son ={
    // 写在前面的同名属性会被覆盖
    // skill:"游泳",
    ...person,
    ...student
    //  sleep:"呼噜呼噜!!",
    // skill:"跳水",
    // habbit:"抗冻"
}

```



## ES6 - 数组展开

> ... 结合数组使用

```javascript
// 数组
const vegetables =["西兰花","西红柿","苦瓜","菜花"];
const meats =["牛肉","羊肉","驴肉","鸭肉","鸡肉"]


// 把数组展开
const foods =[...vegetables,...meats];
// const foods =["西兰花","西红柿","苦瓜","菜花","牛肉","羊肉","驴肉","鸭肉","鸡肉"]

console.log(foods);

```

1. 数组不会出现覆盖问题,索引会依次向后

## ES6 - 箭头函数

> 简单的令人发指的函数写法

1. 省略`function` 变为`=>`
2. 如果形参`只有一个`,可以省略小括号
3. 如果函数体`只有一行`,可以省略大括号
4. 如果函数体`只有一行`,并且`有返回值`
   1. `省略大括号`的同时,必须省略`return`

```javascript
// 函数 无参数,无返回值的函数
// const func1 = function() {
//   console.log('函数1');
// };
// 省略 function
// const func1 = ()=>{
//     console.log('函数1');
// };

// 省略大括号
// const func1 = ()=>console.log('函数1');

// func1();

//有一个参数,无返回值的函数
// const func2 = function(name) {
//   console.log(name + '你好吗!');
// };

// 省略 function
// const func2 = (name) => {
//   console.log(name + '你好吗!');
// };

// 省略 小括号
// const func2 = name => {
//   console.log(name + '你好吗!');
// };

// 省略大括号
// const func2 = name => console.log(name + '你好吗!');

// func2('rose');

// 有一个参数,又返回至的函数
// const func3 = function(name) {
//   return name + ' 哦哈哟!';
// };

// 省略function
// const func3 = (name)=>{
//     return name + ' 哦哈哟!';
//   };
// 省略小括号
// const func3 = name => {
//   return name + ' 哦哈哟!';
// };
// 省略大括号,有返回值时,必须一起省略 return
// const func3 = name => name + ' 哦哈哟!';

// const res = func3('菜花');
// console.log(res);

// 参数有多个,函数体有多行的函数
// const func4 = function(name, age) {
//   console.log(name + ' 阿尼阿瑟哟');
//   console.log(`你竟然${age}岁了`);
// };

// function 省略
const func4 = (name, age) =>
 {
    //  如果非要省略大括号,只有第一行会当做函数内部的代码
  console.log(name + ' 阿尼阿瑟哟');
    // 第二行开始就和上面的函数没有关系了
  console.log(`你竟然${age}岁了`);
};
func4('路飞',18);


```

## ES6 - 箭头函数中的`this`

> 不再是调用的时候确认`this`,变成创建的时候确认`this`

1. 箭头函数的this 在创建时就确定了 是上下文(和他平级的环境中)中的this
2. 可以通过 `babel`的工具把高级的js代码翻译成低版本的js,查看内部的实现套路
3. babel传送门: https://www.babeljs.cn/ 

![1571816159485](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/node%E5%9F%BA%E7%A1%80-01/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571816159485.png)

## Node.js - 内置模块

> 脱离了浏览器的限制,通过内置模块可以实现很多在浏览器中干不了的事情哦

官方文档: http://nodejs.cn/ 

## Node.js - fs模块基本使用

文档地址: http://nodejs.cn/api/fs.html 

1. 文件基本读写会用即可
2. `const fs = require('fs')`
3. `fs.readFile`
4. `fs.writeFile`

## Node.js - 第三方模块

1. 官方的网站(包,模块管家的搜索界面): https://www.npmjs.com/ 
2. 找包 官方的包检索网站`npm`
3. 下包:模板的网页中有命令`npm i xxx`
4. 导包:文档中也有
5. 用包
6. 文档中都可以找到



## 补充清屏的命令

小黑窗中输入`cls`

# Node.js -day02

1. Node.js执行代码

   1. 打开`黑窗`(终端):
   2. 输入命令:`node 文件名` 用`node`去执行(解析)某个js文件
   3. 路径:`黑窗和代码的路径是相同`

2. fs模块文件读写

3. 箭头函数的this

   1. 在创建的时候就确定了

   ```javascript
   // 箭头函数 绑定this
   // 箭头函数中的this在创建时就去确定了
   // 是上下文中的this,和他平级的this
   // babel 翻译
   setTimeout(() => {
       console.log('定时器');
       console.log(this);
   });
   
   // 上面的代码 等同于
   // const _this = this;
   // setTimeout(function(){
   //     console.log(_this)
   // })
   ```

## 终端命令:cd

> 在终端中切换路径

可以用来切换路径

```bash
cd 路径
cd ../
cd 文件夹
```



## Node.js中的相对路径

> Node.js中的相对路径相对的是执行环境中(小黑窗)的路径

想要看这个错误,终端中,跳出当前的路径

通过路径去执行代码就可以出现这个错误

![1571965604863](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day02/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571965604863.png)

```javascript
// console.log("我是代码");

// 导入fs
const fs = require('fs');

// 读取文件
// node.js中的相对路径 相对的谁
// 1. 当前这个js文件
// 2. 终端中的路径 小黑窗中所处的路径

fs.readFile('./novel/01.txt','utf-8', (err,data)=>{ 
    if(err==null){
        console.log(data);
    }else{
        console.log('错啦');
        console.log(err);
    }
 })
```



## 两个路径相关的全局变量

> 通过代码的方式来获取绝对路径

1. 4中的问题可以通过绝对路径来解决,保证一定可以读取到文件
2. 结合这两个全局变量就可以动态的生成绝对路径,避免写死
3. 是node.js中推荐的写法
4. `全局变量`不需要定义,直接就可以使用

```javascript
__dirname // js文件所在文件夹的绝对路径
__filename// js文件的绝对路径
```



## Path模块基本使用

> 专门用来处理路径的模块

文档传送门:http://nodejs.cn/api/path.html

```javascript
path.extname('info/novel.txt');// 获取文件的扩展名 .txt
path.dirname('info/novel.txt');// 获取路径中文件夹的部分 info/
path.join(路径1,路径2,路径3...);// 把多个路径拼接到一起,保证格式正确
```

其中重点掌握`path.join`即可

```javascript
// 使用fs模块和path模块完成文件的读取
// 导入模块 fs
const fs = require('fs');
// 导入模块 path
const path = require('path');

// 生成绝对路径 path.join
const fullPath = path.join(__dirname,'./novel/01.txt');

// 读取文件
fs.readFile(fullPath,'utf-8',(err,data)=>{
    if(err==null){
        console.log(data);
    }
})
```

注意

1. `\`转义符 需要注意
2. `path.join(路径1,路径2)`不要写成 字符串拼接`+`
3. 使用绝对路径的目的是`保证一定可以获取到文件`

## http模块-创建服务器

> 通过它几行代码就可以创建服务器了哦

使用步骤

1. 导包(内置模块,模块名叫`http`)
2. 调用`createServer`方法创建服务器对象
3. 开启服务器(监听端口)`listen`



概念解释:

` http://192.168.156.65:8848/ `

```
http://  协议: http模块开启的服务是http服务访问的时候带上 `http://`
192.168.156.65:ip地址,花姐的电脑在当前这个局域网中的ip地址 
打开黑窗 输入 ipconfig 
:8848  端口号
```

端口:

​	电脑和外部通讯的一个通道

1. 物理端口:
   1. usb口
   2. 网线口
   3. 耳机口
   4. hdmi(显示器,投影仪)
   5. ...
2. 虚拟端口:电脑中的软件和外部通讯的通道
   1. 只要和外部通讯的软件,都会使用某一个虚拟端口
   2. 一个号而已`0开始递增`
   3. 虚拟端口很多
   4. 前`10000`很多都被用了 
   5. 靠后的一般都可以使用,一些比较另类的也没有使用
   6. `8848,8888,4399,3000`
   7. 端口一次只能被一个程序使用



## http模块 - 服务器的交互流程

```javascript
// 导入内置http模块
const http = require('http');

// 创建服务器对象
const server = http.createServer(function(request,response){
    // 返回内容
    response.end('nice to meet you!! ^_^');
})

// 开启服务器 开启监听
// 参数1 端口号
// 参数2 监听的地址 省略的话就是本机,
// 参数3 开启之后的回调函数
server.listen(8848,function(err){
    if(err==null){
        console.log('开启成功了哦!^_^');
    }else{
        console.log('哎呀,失败啦!');
    }
})
```

![1571972568596](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day02/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571972568596.png)

## http模块-响应英文

> 服务器如何返回内容给浏览器呢?

```javascript
response.end('abc')

```



## http模块-响应中文

> 对于中文需要额外的设置响应头哦

## http模块-响应网页

> 返回一个写好的网页

在`response.end`之前调用

`response.setHeader`设置编码格式，浏览器就可以正常解析内容了

```javascript
// 创建服务器对象
const server = http.createServer(function(request,response){

    // 解决中文乱码 返回一个格式
    // content-type内容类型
    // text/plain 普通文本
    // charset=utf-8 编码格式
    response.setHeader('content-type','text/plain;charset=utf-8');
    // 返回内容
    // response 返回的英文内容可以被正常解析
    // response.end('nice to meet you!! ^_^');
    response.end('怎么老是你！');
})

```

问题

1. 设置header的代码不能乱写
2. 重开终端中`ctrl+c` 不需要选择内容
3. 访问时，写上端口
4. 记得导包哦`http`

## http模块-获取请求url

> 请求是可以携带信息,如何获取这些呢?

1. 在回调函数中可以通过`request.url`获取在url中的信息
2. `request`请求的意思
   1. 会吧请求的信息都保存在这个对象中
   2. `url`就是请求的地址
3. 如果`url`中有中文，可以通过`decodeURI()`进行转码

```javascript
// 导入http模块
const http = require('http');

// 创建服务器
const server = http.createServer((request,response)=>{
    // 打印内容
    // console.log('有人请求我哦！！');
    // 打印请求的地址
    // console.log(request.url);
    // decodeURI url中文解码
    console.log(decodeURI(request.url));
    response.setHeader("content-type",'text/plain;charset=utf-8');
    response.end("辛苦了");
})

// 开启服务器
server.listen(4399,function(err){
    if(err==null){
        console.log('开启成功了哦');
    }
})

```



## http模块 - 根据url响应不同的内容

> 不要都是固定的内容,根据url响应不同的值吧

实现步骤：

1. 获取请求的url`request.url`
2. 根据不同的`url`返回不同的结果

## http模块 - 读取并返回页面

步骤

1. 导包
2. 用包
   1. 创建服务器的时候
      1. 读取写好的页面 并返回



注意：

```
1. 如果想要修改用户看到的页面，只需要修改页面的代码即可

```

2. 不需要重新开启服务器
3. 目前只能返回`index.html`

## http模块 - 根据url响应不同的文件

步骤

1. 写多一些`if else` 根据不同的值
2. 读取不同的文件并返回

缺点

1. 如果返回的页面有上百个，上百个`if else`

## http模块 - 静态资源服务器

作用

1. 开启服务之后，可以通过浏览器输入`http://地址:端口`访问
2. 如果输入的地址后面还更有网页，可以读取对应的文件并返回
3. 如果请求的是`css`,`js`,`img`也可以正常返回
4. 读取文件是，不要设置编码格式为`utf-8`



## 静态资源服务器 - 访问注意

1. 保证 js文件同级目录下有一个`web`文件夹，内部有网页
2. vscode每次 右键打开终端，会新建一个小黑窗
3. 快速访问自己的服务器
   1. http://localhost    本机
   2. http://127.0.0.1     本地回环地址
4. 让同局域网的人访问必须通过本机`ip`才可以

## http模块 - 获取请求的方法

1. `request.method`获取请求方法
2. 结合请求地址的判断，可以自行不同的逻辑
3. 更为复杂的逻辑，不太适合用原生的编写，比较繁琐

## 第三方模块使用步骤

1. 新建文件夹(不要中文)
2. 初始化  打开终端输入:`npm init -y`或者`npm init` 自行输入
   1. 生成一个`package.json`文件
   2. 文件保存了项目的信息，比如版本，名字，使用的第三方模块名...
   3. `npm init `自行输入每一项（初期用的不多）
3. `npm网站`找包
4. 根据提示 下包 `npm i 包名`
   1. `package.json`中 增加一个`dependencies`把下载的包名，记录进去，和版本信息
   2. 文件夹下多
      1. `node_modules`所有下载的第三方模块都会在里面
      2. `package-lock.json`：模块名，版本号，在线地址等。。
         1. 为了让我们第二次下载的时候速度更快
5. 根据提示 导包
6. 根据提示 用包



第二次下载

1. 保存`package.json`及`package-lock.json`有之前下载的模块名
2. 直接输入`npm i`自动读取用到的模块，并下载

## express 基本使用

1. 新建文件夹非中文输入`npm init -y`
2. 找包
3. 根据提示下包
4. 根据提示用包



## 补充 - 云服务器

1. 个人电脑互联网上无法被访问
2. 除非你有一个公网ip
   1. 互联网可以想象为一个巨大的局域网
3. 不建议用自己的电脑作为服务器放到互联网上
   1. 不安全
4. 买一个专门的服务器
   1. 服务器：电脑，和普通电脑有点区别，配置上，系统上
   2. 系统：
      1. window服务器系统
      2. linux：最为常见
   3. 配置：内存较大，cpu更好一些
   4. 安全性和稳定性会更好
5. 为了让更多人体验互联网应用，有了很多的云供应商
6. 供应商A:有一台超级牛逼的服务器
   1. 装了几百台虚拟机
   2. 卖钱
7. 用户可以根据需求购买云服务器
   1. 本质就是一个供应商 给你的虚拟机
   2. 大部分情况够用
8. 云服务器
   1. 可以在互联网上被访问
   2. 24小时不停机
   3. 如果有人攻击你，云供应商帮你处理
9. 购买推荐：
   1. 找打折的即可
   2. 阿里云：折后90一年，只能买一年，第二年巨贵
   3. 腾讯云：折后10元一个月，可以买3年
      1. https://cloud.tencent.com/act/campus?fromSource=gwzcw.2432747.2432747.2432747&utm_medium=cpc&utm_id=gwzcw.2432747.2432747.2432747 
      2. 10元一个月可以让你购买三次
      3. 每次最多购买一年
   4. 百度云
   5. 京东云
   6. 华为云
   7. 。。。。
10. 买了之后能干嘛
    1. 有了一台24小时运行的电脑
    2. 抢票
    3. 挂网站
    4. 挂接口
11. 花姐写的接口 
    1. https://github.com/AutumnFish/testApi 
12. 域名：
    1. 很便宜
    2. 买服务器的时候一般会送，或者搭配购买打折
    3. 冷门的便宜
    4. 热门的巨贵

## 补充 - vscode配色

![1571991613205](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day02/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571991613205.png)

## 补充 - 电脑卡顿

1. 过热:

   1. 垫高：有一点点用
   2. 买散热器：有多一点点用
   3. 清灰：蛮有用的
   4. 加硅脂：需要一定的动手能力，不太建议自己弄
   5. 新电脑
      1. 超极本，散热本来就不好
      2. 直接找售后

2. 硬盘:

   1. 机械硬盘使用的时候读写速度慢，卡顿的感觉
   2. 买个固态硬盘：
      1. 推荐买256g
      2. 256g:300左右
      3. 主流的牌子基本没问题`三星，金士顿，闪迪，东芝。。。`
   3. 安装：
      1. 找小伙伴帮你，修电脑的
      2. 重新安装系统，把系统装到`固态硬盘`中
   4. 成本：300左右

3. 内存：

   1. 单位时间内允许运行的软件多少
   2. 推荐8g
   3. 上不封顶
   4. 成本:250

   

## 补充 - nodemon(可选)

node 的一个 `全局模块`

当做一个没有图形化界面的软件

安装了之后可以自动检测文件修改，自动重新运行

1. 任意位置执行`npm i nodemon -g`
2. 安装完毕之后
   1. `node xxx`
   2. 换成
   3. `nodemon xxx`

# Node.js - day03

## 反馈

1. server.listen(1999, err => { if (err == null) { console.log('开启成功'); } }) 花姐，如果服务器开启成功，err为null 但是，当我把if注释后，只打印err 为什么出来的是undefined，而且不影响服务器使用

2. 逻辑理解起来有点困难鸭，语法也好难记鸭

3. 花哥今天讲的十分清楚，贼好

4. 花姐，笔记可以再写详细点吗，或者把代码里面的内容也粘贴到md里面，好捋~ 服务器和数据库的区别能帮再回忆一下吗？又记混了

5. 谢谢老师啦

6. <h2>花姐 美美哒！给你一朵小红花！</h2> <span>/xianhua <span> /<br> <h3 style="color:red">we love you in heart</h3>

7. 你永远不懂我伤悲 像白天不懂夜的黑 花姐能唱一下不

8. 老师再讲一下动态读写的方法，还有万人血书求抢票软件！！！！！！！！！！！！！

9. 花姐震惊的读了下一条反馈,并发出了 "斯国一耐 欧尼酱" 的声音

10. __dirname 和 __filename 这里有点没太懂 花姐 优秀的男人都那么帅 要是可以再稍微慢一点就更帅了 就有点还没想起来这个代码是什么用法,花姐就已经写完了

11. 棒棒的，懵中带点懂，可以的话能再带着穿一遍html的动态创建吗

12. 摇落深知宋玉悲，风流儒雅亦吾师。 怅望千秋一洒泪，萧条异代不同时

13. 花花姐，你讲的好好哟！！！但是 就是听不懂呢

14. 花姐，练的时间可以短点，然后最好一个知识点给1-2分钟敲一下，只需要1-2分钟就好

## 回顾

1. 浏览器&服务器&数据库
2. ![1572050794102](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572050794102.png)
3. 静态资源服务器
   1. 模块：
      1. http:开启服务器
      2. fs:读取文件
      3. path:获取路径
   2. 创建服务器
      1. 回调函数中
      2. 获取url地址
      3. 根据url地址生成路径
      4. 根据路径读取文件
      5. 读取成功：返回
      6. 失败：返回404
   3. 开启服务器：端口，错误判断
4. get和post请求判断
5. 第三方模块使用

## express基本使用

> 相比于原生http模块，开发速度更快的web开发框架

传送门1:http://www.expressjs.com.cn/

传送门2:http://expressjs.com/

1. 只要框架流行，基本都会有中文网
2. express是`node.js`中的一个`web开发框架`
3. 很多框架都是基于`express`哦 

使用步骤:

1. 创建文件夹:
   1. 不要叫`express`和模块同名
2. 初始化:`npm init -y`
3. 下载express:`npm i express`
4. 导入`express`
   1. c+v
5. 使用`express`
   1. c+v
   2. http模块的方法都可以用，但是更建议用`express`的

```javascript
// 导包 express
const express = require('express');
// 创建服务器对象 http.createServer类似
const app = express();

// 如果请求的是 / （url为空）
app.get('/', (request, response) => {
  // 原生的方法也支持
//   response.end('很高兴认识你');
  // 返回一个 hello world
  // 更高级的 end方法
  response.send('很高兴认识你');
});

// 开启服务器
app.listen(3000, err => {
  if (!err) {
    // 不打印是没有内容的
    console.log('success');
  }
});

```



特点:

```
1. 静态资源托管
```

2. 路由
3. 中间件
   	1. 第三方中间件
      	2. 自定义中间件

## express - 托管静态资源

> 一行代码让外部可以访问指定的文件夹

传送门: http://www.expressjs.com.cn/starter/static-files.html 

![1572055329726](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572055329726.png)

```javascript
// public文件夹下的文件就可以被访问了
app.use(express.static('public'))
```

1. public 建议和js文件统计
2. 重复打开需要关闭之前的那个
3. 初期花姐强烈建议`c+v`
4. `ip地址`每天是会变的 用`localhost`或者`127.0.0.1`



## express - get路由

> get请求时，url地址  和   后台函数(逻辑)的对应关系

1. 接口调用 

   1. 浏览器`调用` 定义在`服务器的函数`

2. 写接口

   1. 根据接口文档注册路由
   2. 实现逻辑
   3. 返回结果

   ![1572056755260](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572056755260.png)

```javascript
// 导包 express
const express = require('express');

// 创建服务器对象 http.createServer类似
const app = express();

// 什么都不写的url地址
app.get('/',function(request,response){
  // 返回内容
  response.send("/默认");
})

// list
/*
  食物数组接口
  请求地址:http://192.168.156.65:3000/list
  请求方法:get
  请求参数:无
  返回结果:食物数组
*/
app.get('/list',(request,response)=>{
  // 返回一个食物列表
  const foods = ["西兰花炒蛋","花菜炒蛋","菜花炒蛋","肉炒蛋"];
  // 返回内容
  // response.send("/列表");
  response.send(foods);
})

// 开启服务器
app.listen(3000, err => {
  if (!err) {
    // 不打印是没有内容的
    console.log('success');
  }
});

```



## api- 笑话接口

> 写个接口试试，请求之后返回固定的笑话

- 请求地址：/joke
- 请求方法：get（数据的获取用`get`）
- 请求参数：无
- 响应内容：一条笑话

步骤：

```
1. 注册路由
```

2. 根据文档写方法，写地址
3. 根据响应内容写返回的结果即可

注意

1. app.get（/joke）根据文档注册路由，写地址
2. 报错还是从上往下看
3. 今天的服务器名叫做`app`





## api- 随机笑话接口

> 固定的笑话多没意思，返回随机的笑话吧

- 请求地址：/randomJoke
- 请求方法：get(数据获取)
- 请求参数：无
- 响应内容：随机的笑话

实现步骤：

```
1. 准备多条笑话`[笑话1，笑话2，笑话3....]`
```

2. 从多条笑话中获取一条`parseInt(Math.random()*数组长度 ）`
3. 返回获取到的这一条`response.send(笑话数组[随机索引])`

注意

1. 逻辑写在函数内部
2. 只要地址不同，`app.get`可以写多个

## api - 随机笑话接口优化

> 笑话和代码分离可以吗？
>
> 可以

- 请求地址：/randomJokePro
- 请求方法：get
- 请求参数：无
- 响应内容：随机的笑话



步骤

1. 把笑话放到项目文件夹下`data/jokes.json`
2. 从文件中读取笑话
   	1. `fs`模块
      	2. `path`模块
              	3. `path.join(__dirname,路径)`
            	4. 读取完成之后
                     	1. 编码格式`utf-8`
                     	2. 类型是字符串
                     	3. `JSON.parse`把字符串转为数组
3. 从读取的笑话中中获取一条`parseInt(Math.random()*数组长度 ）`
4. 返回获取到的这一条`response.send(笑话数组[随机索引])`



注意

1. fs，path需要额外的导入
2. 文件的路径是灵活的，可以自行更改

## express - get请求参数获取

> express中如何获取get请求的参数呢
>
> 参数有点类似于函数的形参

1. get请求的参数放在那里 `url?key=value&key2=value2`
2. `key`接口文档提供给我们的
3. `value`前端准备好的
4. get请求的数据全部都放在`request`中
5. ![1572063759714](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572063759714.png)

重点

1. url中的数据通过`request.query`来获取

## api - 随机笑话接口带参数

> 让用户来决定笑话的个数吧

- 请求地址：/getSomeJoke
- 请求方法：get
- 请求参数：num(随机个数)
- 响应内容：

```json
{
    num:个数,
    msg:'获取成功',
    jokes:['笑话1','笑话2']
}
```

实现步骤

1. 注册路由`app.get('/getSomeJoke')`

2. 回调函数中

   1. 获取传递过来的参数`request.query.num`
   2. 读取笑话
   3. 定义空数组`[]`
   4. 循环`num`次
   5. 循环完毕之后，返回数据

   

   注意

   1. 当涉及到参数传递时
   2. 后台接口在实现的时候
      1. 接收数据
      2. 处理数据
      3. 返回数据

## express - post路由

> post请求时，url和后台函数的对应关系

```javascript
app.post('/地址',function(request,response){})
```

注意

1. post路由的注册方法 和get类似，名字变为`post`
2. 直接通过浏览器的url访问发送的是`get`
3. 可以通过`postman`发请求
4. 自己写ajax设置请求的`type`为post
5. 默认注册的post路由中无法获取到提交过来的参数(数据)

## express - post数据获取（普通文本）

> 通过express的`中间件` 获取post提交的文本数据

传送门: https://www.npmjs.com/package/body-parser 

1. 中间件是一个特殊的第三方模块
2. 必须结合`express`才可以使用
3. 类比为`jQuery`插件

![1572075812290](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572075812290.png)

使用步骤·

1. 下包
2. 导包
3. 用包

```javascript
// 导入express
const express = require('express');
// 导入body-parser 第三方模块（中间件）
const bodyParser = require('body-parser')

// 创建服务器对象
const app = express();

// parse application/x-www-form-urlencoded
// 解析 application/x-www-form-urlencoded 这种格式的数据
app.use(bodyParser.urlencoded({ extended: false }))

// 注册路由
app.post('/add',(request,response)=>{
    console.log(request);
    response.send("/add  你通过post请求的哦@");
})

// 开启监听
app.listen(4399,(err)=>{
    if(!err){
        console.log('服务器跑起来了哦，这个地址就可以访问了哦 http://192.168.156.65:4399');
    }
})

```

## api - 用户名验证接口

> 用户注册之前，咱们先验证一下这个用户名是否已经被注册了

![1572076135271](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572076135271.png)

- 请求地址：/checkUsername
- 请求方法：post
- 请求参数：username
- 响应内容：

```
{
	msg:可以注册 或 已被注册,
	code:200 或 400
}
```

实现步骤：

1. 下载`body-parser`中间件
2. 导入中间件
3. 使用中间件
4. 注册路由`app.post('/checkUsername')`
5. 回调函数中 
   1. 获取用户名`request.body.username`
   2. 定义一个用来模拟所有用户的数组`userArr=['a','b','c']`
   3. 判断是否存在
      1. indexOf: -1不存在
      2. some:false不存在
   4. 返回信息
      1. 可以注册
      2. 不可以注册

注意

1. 用户主动的数据提交，用`post`
2. 约定好了数据的名字之后，不要胡乱提交
3. 数据比约定的要多，服务器可以不处理，
4. 如果比约定的要少，可能逻辑就会有问题

## express - post文件提交

> express通过第三方中间件来获取上传的文件

传送门: https://www.npmjs.com/package/express-fileupload 

1. 下包
2. 导包
3. 用包
   1. `request.files` 保存了所有文件信息
   2. `request.files.xxx` 获取 key为`xxx`的文件信息
   3. `request.files.xxx.mv（路径，回调函数）`把文件移动到某个地方

```javascript
// 导入express
const express = require('express');
// 导入 express-fileupload
const fileUpload = require('express-fileupload');

// 导入
const path = require('path');

// 创建服务器对象
const app = express();

// 使用中间件 接收文件
app.use(fileUpload());

// 上传
app.post('/upload',(request,response)=>{
    // console.log(request);
    // 使用了 中间件之后 可以通过 request.files获取文件信息
    // console.log(request.files);
    // files中用对象属性的方式 保存了上传的文件信息
    console.log(request.files.icon);
    // 通过 文件属性的.mv方法 移动文件到某个地方
    // 获取文件名
    const fileName = request.files.icon.name;
    // 生成路径
    const fullPath = path.join(__dirname,'./files/',fileName);
    request.files.icon.mv(fullPath,(err)=>{
        if(!err){
            console.log('哎哟，文件上传过来了哦');
        }
    })
    response.send("/upload");
})




// 开启监听
app.listen(4399,(err)=>{
    if(!err){
        console.log('服务器跑起来了哦，这个地址就可以访问了哦 http://192.168.156.65:4399');
    }
})

```



## 中间件

1. 就是一个特殊的第三方模块
2. 依赖于express
3. 起了一个牛逼的名字

## 课外阅读 - 原生http模块 - get参数获取

> 解析在url中参数

- 在http协议中，一个完整的url路径如下图
  - 通过下图我们可以得知，get请求的参数是直接在url路径中显示。
  - get的请求参数在path资源路径的后面添加，以`?`表示参数的开始，以`key=value`表示参数的键值对，多个参数以`&`符号分割
  - hash部分表示的是资源定位符（滚动网页可视区域），由浏览器自动解析处理，它的作用是跳转到对应id的标签的位置

![1571414438199](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day03/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1571414438199.png)



```javascript
//1.导入模块
const http = require('http');
//url模块：解析url路径得到url协议中的每一部分
const url = require('url');

//2.创建服务器
let server = http.createServer((req,res)=>{
    //req.url:获取整个请求url  包含路径和参数
    console.log(req.url);
    //decodeURI():了解即可，默认情况下url中的中文会进行URI编码，使用decodeURI解码可以得到中文
    console.log(decodeURI(req.url));

    /*1.使用url模块解析get请求 
    第一个参数：要解析的url
    第二个参数: 布尔类型  true：推荐使用，得到的参数是一个对象   false：得到参数是字符串
    返回值：对象类型：将url中的每一部分作为对象的属性
     */
    let urlObjc = url.parse(req.url,true);
    console.log(urlObjc);

    //2.获取请求的路径
    let urlPath = urlObjc.pathname;
    console.log(urlPath);
    //3.获取请求的参数
    let query = urlObjc.query;
    console.log(query);

    //响应客户端请求
    //服务端不能直接响应js对象，需要转成json对象（后台具有跨平台性，不是只为前端服务）
    res.end(JSON.stringify({
        code:10000,
        list:[10,20,30]
    }));
   /*
   {
  protocol: null,//协议名
  slashes: null,//表示 //到第一个/之间都是host
  auth: null,//认证
  host: null,//主机名+ 端口号  hosetname+port
  port: null,//端口号
  hostname: null,//主机名  ip地址
  hash: null,//资源定位符
  search: '?name=OldFe&age=18',
  query: { name: 'OldFe', age: '18' },//get请求的参数对象
  pathname: '/getRequest',//路径
  path: '/getRequest?name=OldFe&age=18',//路径+请求参数
  href: '/getRequest?name=OldFe&age=18' }
   */
   //console.log(urlObjc);

});

//3.开启服务器
server.listen(3000,()=>{
    console.log('success');
});

```



## 课外阅读 - 原生http模块 - post参数获取

> 解析通过请求主体发送过来的参数

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <form id="form" action="http://127.0.0.1:3000/register" method="POST" enctype="application/x-www-form-urlencoded">
        <div>
            <input type="text" placeholder="用户名" name = "username">
        </div>
        <div>
            <lable><input type="radio" value="男" name = "gender" checked>男</lable>
            <lable><input type="radio" value="女" name = "gender">女</lable>
        </div>
        <div>
            <input type="password" placeholder="密码" name="password">
        </div>
        <div><input type="submit"></div>
    </form>
</body>
</html>



## 课外阅读 - nodejs实现服务端重定向

- **服务端重定向常见于某些网站引导登陆注册的功能（当我们访问网站首页的时候，会跳转到登陆注册的界面）**
- **服务端的重定向功能主要由响应头的302状态码来实现**



```javascript
//1.导入模块
const http = require('http');

const fs = require('fs');

const path = require('path');

//2.创建服务器
let server = http.createServer((req,res)=>{
    console.log(req.url);
    //请求路径
    let urlPath = req.url;
    //请求方法
    let  method = req.method;

    if(req.url === '/'){
        //302表示重定向
        //(1)设置重定向地址
        res.writeHead(302, {
            'Location': 'login'  //键值对，键表示客户端浏览器将进行重定向  值：表示客户端浏览器重定向的请求
            //add other headers here...
        });
        //(2)响应本次请求
        res.end();
    }
    //登陆页
    if(req.url === '/login'){
        fs.readFile(path.join(__dirname,'login.html'),function(err,data){
            if(err){
                throw err;
            }
            res.end(data);
        });
    };
});


//3.开启服务器
server.listen(3000,  ()=> {
    console.log('服务器启动成功');
});
```

#  Node.js - day04

##  回顾

1. express

   * 下包 nmp init -y    nmp i express
   * 导包 let express = require('express')
   * 创建对象 let  app = express();
   * 用包 app.get('/',function(reuest,response){response.send('hello')})
   * 开启服务器 app.listen(端口号,function(err){})

   > 1. 静态资源托管
   >
   > app.use(express.static('文件夹'))；
   >
   > 2. 获取地址参数
   >
   >    request.query

   * 注册post路由

     app.post('/',function(reuest,response){response.send('hello')})

     > 1. 获取参数
     >
     > requset.body【导入body-parser】
     >
     > 2. 获取文件
     >
     >    request.files
     >
     >    移动文件位置
     >
     >    request.files.icon.name；
     >
     >    request.files.icon.mv('地址')；

     ```javascript
     // 导包express
     const express = require('express')
     // 导包 body-parser
     const bodyParser = require('body-parser')
     // 导包 express-fileupload
     const fileUpload = require('express-fileupload');
     // 导包 path
     const path = require("path");
     // 创建服务器
     const app = express()	
     
     // 静态文件
     // app.use(express.static('public'))
     // 访问的时候 先写上public 再跟上文件名
     app.use('/public',express.static('public'))
     
     // 解析post请求的文本
     // parse application/x-www-form-urlencoded
     app.use(bodyParser.urlencoded({ extended: false }))
     
     // 增加接收文件的功能
     app.use(fileUpload());
     
     // 注册路由 url和后台函数的对应关系
     app.get('/', function (req, res) {
       res.send('Hello World')
     })
     
     // get路由
     app.get('/search',(request,response)=>{
       // 参数获取
       // 打印一次，再去取值
       console.log(request.query);
       console.log(request.query.name);
       console.log(request.query.age);
     
       // 原生的方法 功能不够强大，中文乱码
       // response.end("/search")//http
       // express提供的 更加强大
       response.send("/search")
     })
     
     // post路由
     // ajax设置请求方法为post
     // post去测试
     // 浏览器直接访问是 get请求
     app.post('/update',(request,response)=>{
       console.log(request.body);
       console.log(request.body.name);
       console.log(request.body.skill);
     
       // 提交的数据 - 文本数据
       // 提交的数据 - 文件数据
       response.send("/update");
     })
     
     // post路由 文件
     app.post('/upload',(request,response)=>{
       // 打印文件信息
       // 默认没有files属性
       // files 对象 包含了上传的所有文件
       console.log(request.files);
       // 头像文件保存起来
       const fileName = request.files.icon.name;
       request.files.icon.mv(path.join(__dirname,'./upload',fileName),(err)=>{
         if(!err){
           console.log('success');
         }
       })
       response.send("/upload");
     })
     
     app.listen(3000,(err)=>{
       if(!err){
         console.log('success');
       }
     })
     ```

     

##  1. 跨域

### 1. 同源

 1. 浏览器打开的页面地址
 2. Ajax调用接口的地址
 3. 协议http://，地址127.0.0.1，端口880 全部相同，成为同源
 4. 可以自由访问，不会报错

### 2. 不同源

 1. 协议，地址，端口不相同，成为不同源
 2. 浏览器默认禁止访问
 3. 解决方法：（不同源--叫跨域）
    * cors
    * jsonp

### 3. 跨域方式

### 3.1.  jsonp

* 与ajax没有关系
* 利用的是script的src属性【不受跨域的限制】
* 向不同源的服务器发送一个get
* url中携带了一个callback参数
* 服务器接收到之后返回一个函数的调用xxx({name:'zz'})
* 返回浏览器之后解析成js，调用

```java
//=====后端写法
注册路由--返回方法response.jsonp({name='zz',age=22});
//======前端写法
$.ajax({
  type:'get',
  url:'http://127.0.0.1:3000/',
  dataType:'jsonp',
  success(backData){
    console.log(backData);
  }
})
```

script标签的src也可以发请求，没有同源

jsonp 跟ajax没有关系【在Network中XHR看不到请求，属于js分类:本质是动态创建了一个script标签---src="接口地址+发送的数+callback=xxx据"，请求成功自动移除】

* 优点：兼容性好

* 缺点：
  * 不支持post，只能是get
  * 数据大，搞不定【参数】

### 3.2. CORS
【cross  origin resource sharing】

1. HTML5中推出的新标注，低版本浏览器不支持
2. 前端：不用干
3. 后端：设置允许跨域就可用

```java
中间件，设置跨域
app.use((request,response,next{
  //设置允许跨域
  response.header(Access-Control-Allow-Orgin,'*');
  next();//执行下一个函数
})
```

### 3.4 自己创建模块

* 抽取出模块---导入模块 module.export = ;
* 模块页--导入模块 require('./utils/...')【可省略文件后面的.js】

##  2. 数据库

### 2.1 MySQL

* 免费，开源 ，轻量级，关系型数据
* 建库 建表  建字段

> 1. 新增数据insert
>    1. insert into 表名 (字段1，字段2) values('值1'，'值2')；
> 2. 删除数据delete
>    1. delete from 表名 where 条件
> 3. 修改数据update
>    1. update 表名 set  字段1 = ' 新值 ' , where条件
> 4. 查询数据select
>    1. select * from 表名  where 条件

* 下包：mysql
* 导包:require('mysql');

### 2.2mysql-ithm模块使用

- 下包：mysql ，mysql-ithm
- 导包:require('mysql');

###  3. Mockjs

http://mockjs.com

> 生成随机测试数据

* 下包 npm i mockjs
* 导包

# Node.js - day05

## 回顾

1. 运行代码

   1. `node xxx.js`: 代码如果修改了,需要重新运行`ctrl+c`,运行
   2. `nodemon xxx.js`:代码修改了,自动重新运行

2. 同源

   1. `http://192.168.156.88:3000`
   2. http:// 协议
   3. (192.168.156.88)(www.jd.com) ip地址,域名
   4. :3000 端口
   5. 对比:
      1. `http://192.168.156.88:3000`
      2. `http://192.168.156.88:5500`

3. 跨域:

   1. 地址1:页面的地址,浏览器地址栏中的地址
      1. `http://192.168.156.88:5500/index.html`
   2. 地址2:Ajax发送请求的`url`地址
      1. $.ajax
         1. url:`http://192.168.156.88:3000/search`

4. 跨域方案 - jsonp

   1. 和Ajax木有关系
   2. 利用的是`script`标签的src属性不受跨域限制
   3. 向不同源的服务器,发送了一个`get`
   4. url中携带了一个`callback`的参数
   5. 服务器接收到之后返回了一个 函数的调用`xxx({name:'jack'})`
   6. 返回浏览器之后解析成js,调用

   

   使用方式:

   1. 前端: $.ajax( dataType:'jsonp' ,type:'get')
   2. 后端:response.jsonp({name:'jack'})
      1. 文档中:
      2. 请求方法:get  (jsonp)
      3. 请求参数:
      4. 请求地址:

   缺点:

   1. 只能发get请求,无法进行大量数据的提交

   优点

   1. 兼容性好

5. 跨域方案 - cors

   1. `html5`中推出的,低版本浏览器不支持
   2. 前端什么都不用干
   3. 后端设置一个允许的`header`
   4. 浏览器看到了这个`header`

   优点:

   1. 支持get和post

   缺点:

   1. 兼容性不太好

6. `mysql-ithm`模块使用

   1. 数据库: 保存数据,保证数据的安全性

   2. 数据库管理员:DBA

   3. SQL语句:

      1. 增:insert
      2. 删:delete
      3. 改:update
      4. 查:select

   4. ``mysql-ithm``

      1. 提供了以一堆的`方法`
      2. 调用方法,用操纵对象的方法,
      3. 内部生成对应的`sql`语句
      4. 间接操纵数据库

      ![1572312665126](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572312665126.png)

## 英雄管理 - 项目说明

1. 开发方式:
   1. 后端:
      1. 照着接口文档
      2. 写接口:接收数据,接收文件,增删改查数据库,返回结果
   2. 前端:
      1. 写静态
      2. 照着接口文档
      3. 调接口

## 英雄管理 - 接口文档

> 自己写接口，自己调用自己写的接口
>
> 素材在其他资料中

1. 文档:
   1. 项目开始之前
   2. 架构根据需求,定需要的接口

| 服务器说明            | 作用描述                     |
| --------------------- | ---------------------------- |
| http://127.0.0.1:3000 | 服务器基地址                 |
| 200                   | 请求成功 状态码              |
| 401                   | 用户名已存在 或者 用户名错误 |
| 402                   | 密码 错误  或者  验证码错误  |
| 500                   | 服务器内部错误               |
| 302                   | 服务器重定向                 |

| 接口名称     | URL          | 请求方式 | 请求参数                 | 返回值             |
| ------------ | ------------ | -------- | ------------------------ | ------------------ |
| 查询英雄列表 | /hero/list   | get      | 无                       | {heros:[英雄列表]} |
| 查询英雄详情 | /hero/info   | get      | id : 英雄id              | {data:英雄详情}    |
| 编辑英雄     | /hero/update | post     | name , skill , icon , id | {code : 200)       |
| 删除英雄     | /hero/delete | post     | id                       | {code:200}         |
| 新增英雄     | /hero/add    | post     | name , skill , icon      | {code:200}         |

```javascript
//4.设计路由（接口文档）

//(1)查询英雄列表
app.get('/hero/list', (req, res) => {
});

//(2)查询英雄详情
app.get('/hero/info', (req, res) => {
});

//(3)编辑英雄
app.post('/hero/update', (req, res) => {
});

//(4)删除英雄
app.post('/hero/delete', (req, res) => {
});

//(5)新增英雄
app.post('/hero/add', (req, res) => {
});

```



## 英雄管理 - 项目初始化

步骤

1. 新建文件夹`heroManage`
2. 在文件夹中打开终端:`npm init -y`
3. 创建`index.js`
4. 下包`npm i express`
5. `c+v`express的基本结构
6. `c+v`今天要写的路由

## 英雄管理 - 数据库初始化

![1572313078688](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572313078688.png)

步骤:

1. 装包:

   1. `npm i mysql-ithm `
   2. `npm i mysql`
   3. 一行装多个`npm i mysql mysql-ithm`

2. 导包

3. 用包

   1. ```javascript
      //2.连接数据库
      //如果数据库存在则连接，不存在则会自动创建数据库
      hm.connect({
          host: 'localhost',//数据库地址
          port:'3306',
          user: 'root',//用户名，没有可不填
          password: 'root',//密码，没有可不填
          database: 'herodb'//数据库名称
      });
      
      //3.创建Model(表格模型：负责增删改查)
      //如果table表格存在则连接，不存在则自动创建
      const heroModel = hm.model('hero',{
          // 名字 字符串
          name:String,
          // 技能 字符串
          skill:String,
          // 头像 路径 用字符串存
          icon:String
      });
      ```



注意:

1. `mysql` `mysql-ithm`导入
2. `mysql-ithm`保存的变量值 是`hm`
3. `const app = express()`保留
4. 类型记住是大写
5. 端口
   1. 一个端口一次只能被一个软件使用
   2. 3306已经被数据库使用了
   3. 3000被express使用了

![1572315580719](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572315580719.png)

## 英雄管理 - 查询英雄列表

> 读取并返回所有的英雄

![1572315661666](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572315661666.png)

步骤:

1. 注册路由(搞定)
2. 查询所有数据:`heroModel.find((err,result)=>{})`
3. 查询完毕之后:`回调函数中`
   1. 对
      1. 返回给浏览器`response.send({heros:[英雄列表]})`
   2. 错
      1. 返回服务器内部错误,

注意:

1. 返回的格式按照接口文档的来
2. 读取成功或者失败都会返回值
3. 最下面的测试返回值,注释掉了
4. 花姐加了一条测试数据,大伙没加

## 英雄管理 - 查询英雄详情

> 根据id查询出某一个英雄

![1572317733695](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572317733695.png)

实现:

1. 注册路由
2. 回调函数中
   1. 获取id:`request.query.id`
   2. 查询数据(数据库):`heroModel.find('id='+id,(err,result)=>{})`
   3. 查询的回调函数中
      1. 对
         1. 查询出了数据
            1. 返回
         2. 没有查询出数据
            1. 返回id错误
      2. 错
         1. 500



注意:

1. id的目的是精确的查询出一个
2. 文档,后端的`leader`写,`组长`,`架构`
3. find方法哪怕只有一条数据也是数组,没有数据也是数组
4. 最初的测试返回的结果,一定要注释掉

## 英雄管理 - 新增英雄

> 新增英雄数据,名字和技能是字符串,icon是文件路径,文件需要上传到服务器

![1572321007589](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572321007589.png)

步骤

1. 注册路由
2. 回调函数
   1. 接收post提交的文本`body-parser`
      1. 装包,导包,用包
   2. 接收post提交的文件`express-fileupload`
      1. 装包,导包,用包
   3. 获取数据
      1. 名字:name  `request.body.name`
      2. 技能:skill  `request.body.skill`
      3. icon:`request.files.icon.name`
   4. 移动文件
      1. ``request.files.icon.mv(路径,回调函数)`
   5. 保存数据到数据库:`heroModel.insert(数据,回调函数)`
   6. 回调函数中
      1. 返回结果

注意:

1. 包名,复制,`求你们了`
2. 使用包的代码顺序
   1. 在app的后面才可以
3. es6新语法使用:
   1. 老语法还是兼容的
   2. 用新看起来逼格高,日后工作时,绝大多是都是es6新语法
4. 第三方模块的使用:
   1. 新建项目
   2. c+v示例代码 没问题
   3. 迁移到项目中



## 英雄管理 - 删除英雄

> 删除某一个英雄

![1572322753416](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572322753416.png)

步骤:

1. 注册路由
2. 回调函数中
   1. 接收id`request.body.id`
   2. 删除数据
   3. `heroModel.delete('id=${id}',(err,result)=>{})`
   4. 删除数据的回调函数中
      1. 没错 返回 
      2. 有错 500

## 英雄管理 - 编辑英雄

![1572331098720](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/node/Node.js-Day05/01-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1572331098720.png)

步骤

1. 注册路由
2. 回调函数中
   1. 接收文本
      1. `name,skill,id`  `request.query`
   2. 接收文件名字
      1. `icon` `request.files.icon.name`
   3. 移动到`uploads`中
   4. 修改数据:`heroModel.update('id=${id}',{对象},(err,result))`
      1. 修改数据的回调函数中
         1. 对:`{code:200}`
         2. 错:500



注意:

1. 文件的上传和post文本的获取需要依赖于
   1. `body-parser`post文本
   2. `express-fileupload`post文件
2. postman测试
   1. 参数要和文档一致
3. 数据不改变
   1. 修改id存在的数据
   2. 最初新建表格的时候,和最终的表头不相同
      1. 删除表格,重新执行代码

## 前后端工作分工

1. 后端:------------------------------->写接口
2. 前端:写静态,写js效果--------->调用接口

## 整合静态页面

步骤

1. 把`其他资料/web`文件夹拷贝到`heroManage`项目的根目录
2. `index.js`中 增加`app.use(express.static('web'))`
3. 可以通过和接口同源的地址,访问`web文件夹`下面的页面
4. `http://127.0.0.1:3000/index.html` 访问到页面了
5. 调用接口时
   1. url:`/hero/list`
   2. 自动把左侧的基地址补上去

## 接口调用 - 英雄列表

步骤

1. 调用接口`/hero/list`
2. 调用成功之后渲染到页面上
   1. 定义模板
   2. 挖坑
   3. 起名字
   4. 填坑
   5. `template(模板id,数据)`
   6. 渲染到页面上

注意:

1. 图片默认访问不到
2. 去`index.js`中增加`app.use(express.static('uploads'))`
   1. 把`uploads`暴露出来,外部才可以访问的到

## 接口调用 - 英雄新增

步骤-图片预览:

1. 文本绑定`change`事件
   1. `this.files[0]`
   2. `URL.createdObjectURL()`
   3. 把生成的url设置给`img`的`src`属性

步骤 - 英雄新增

1. 点击新增
2. 创建formData
   1. 表单元素的`name`属性和接口要求的`key`要一致
3. $.ajax
   1. url:`/hero/add`
   2. type:`post`,
   3. data:formData
   4. contentType:false,
   5. processData:false
   6. success(){}

## 接口调用 - 英雄删除

步骤

1. 点击删除
   1. 事件绑定给tbody,用委托的方式指定触发的元素
   2. confirm确认
2. 调用删除接口
   1. url:`/hero/delete`,
   2. type:`post`,
   3. data:{id:id},
      1. id去找父元素获取
   4. success()
      1. 判断
      2. 重新获取数据

## 接口调用 - 英雄编辑01

> 进入编辑状态

步骤

1. `index.html`中用事件绑定的方式为编辑按钮绑定点击事件

2. 获取父元素上的`data-id`

3. 跳转到`add.html?id=具体的值`

4. `add.html`页面中

   1. 获取id

   2. 调用根据id查询数据的接口

      1. url:`/hero/info`,
      2. type:`get`,
      3. data:{id},
      4. success
         1. 把数据渲染到页面上
            1. id保存到隐藏域中`type=hidden`

      

## 接口调用 - 英雄编辑02

> 保存

步骤

1. 点击保存
2. 创建formData
3. 调用接口
   1. url:`/hero/update`,
   2. data:formData
   3. type:post,
   4. processData:false,
   5. contentType:false
   6. success
      1. backData.code==200
      2. 提示用户
      3. 去首页

## Mockjs 模拟数据生成

> Mock模拟数据

1. Mockjs的js库,可以生成随机的测试数据

   http://mockjs.com/

2. Mockjs生成随机测试数据

## 补充 - 快捷键

1. home,end:行头,行位
   1. mac: fn+左右
2. shift+home或end:选中一行
3. ctrl+左右:识别词组跳跃
4. vscode中快捷键:
   1. ctrl+enter:光标换行,文字不换行
   2. ctrl+shift+enter:光标去上一行,文字不动

 https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf 

## 补充 - typora主题

> 如何自定义typora**主题**

#  Node.js - day06

1. express
   1. app.get('地址'，(request,response)=>{})
   2. 获取文本方式
      1. request.query【get】
      2. request.body  【post】
      3. request.files  【文件 files.文件名.mv()】





