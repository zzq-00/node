# WebApi-01

ECAMAScript(es)

DOM:document object model 文档对象模型 , 相对于页面

* DOM节点 ,在js中把标签 ,标签属性 , 标签内文本叫做DOM节点

BOM: 相对于浏览器 

##  1.获取元素对象 

DOM节点,也叫元素对象  (例:如下)

```js
<div id="btn">获取dom节点 </div>

<script>
 //参数:id的名称 ,必须是是字符串形式
var btn = document.getElementById("btn");
console.log(txt); //返回的是dom节点(标签)
</script>
```

**获取属性**

**div .style   //返回的是对象**

btn.style.width="300px"

获取body:   document.body.style.background Color= "red";

因为body唯一,

****

##  2.注册事件 click

注册事件:和用户形成交流,点击行为

onclick  :  响应用户

匿名函数:响应用户点击后的效果

```js
<div id="btn" value="开灯">获取dom节点 </div>

<script>
 //参数:id的名称 ,必须是是字符串形式
var btn = document.getElementById("btn");
console.log(txt); //返回的是dom节点(标签)

btn.onclick  =  function(){    
    document.body.style.backgroundColor = "red";
    btn.style.width =  "200px
    btn.value = "开灯";
}
</script>
```

##  onfocus   onblur 事件

```js
光标焦点 onfocus.onclick = function () {};
光标模糊 onblur.onclick =function () {};

```



##  获取类名

```js
<div id="box" class="top"></div>
```

* 获取类名 .console.log( div.className) ;   //输出类名 top  **返会的是字符串**
* 覆盖原类名  div.clssName  = "bottom";
* 在原类名上 再加一个新类名
  * div.className = div.className  +   "  bottom";   //不智能

##  classList属性

**返回的是对象**

* 添加类名(一个或多个类名)
  * box.classList . add("bottom" , "left");
* 移除类名
  - box . classList . remove("bottom");
* 切换类名
  - box . classList . toggle ("bottom");

##  获取元素对象

###  TagName

根据标签名 获取元素对象(DOM节点),返回的是伪数组,可以用for循环遍历

###  ClassName

根据类名 获取元素对象(DOM节点) , 返回的是伪数组,可以用for循环遍历

```js
var input = document.getElementsByTagName("input");

var btn = document.getElementsByClassName("btn")
```

##  自定义属性

* 使用场景:  数据与数据 一一对应关系,要写入自定义属性里
* 自定义属性命名规则   data-src = ""; data -自定义 = " " ;
* 获取自定义属性  console.log(div . dataset)  //是一个对象
  * console.log("div . dataset . src")

##  this

* 原则 :当前事件 (当前你点击是哪个DOM节点,this就是谁)
* 函数内部的关键字 this

##  checked属性

```js
//开关属性
```

获取元素对象

* document.getElementById();   //返回的是一个DOM节点
* document.getElementsByClassName() ;//返回一组DOM节点
* document . getElementsByTagName (); //返回一组DOM节点

# WebApi - 02

## css选择器

css选择器 : 类名 id名  标签名 

- querySelector()  //返回元素对象,DOM节点(标签)
- querySelectAll()  //返回伪数组

```js
<div id="box"  class="box" ></div>
var box = document.querySelector("#box");
coconsole.log(box);//返回一个元素对象,DOM节点(标签)
var box = document.querySelector(".box")
```

```js
var li =document.querySelectorAll("li");
console.log(li) //返回(伪)数组  可以用forEach方法遍历
```

## 属性:Attribute()

**一般用于自定义属性**(标准属性也可以用)

```js
<div id ="box"  class="box"  abc="123"  data-name = "zz"> </div>
var abc = document.getAttribute("abc");
console.log(abc); //返回属性值 123
```

- 设置(添加)自定义属性

  - 设置 :属性名   属性值

  ```js
  box.setAttribute("abc" ,456) //
  ```

- 删除自定义属性

  - 设置 :属性名

  ```js
  box.removeAttribute("abc" );
  ```

## 注册事件 

### addEventLietener

- 多次注册事件,不会被覆盖(之前的on ,注册事件,会被覆盖)

```js
//元素 . addEventLietener(事件类型 , 事件执行处理程序(事件对象){ });
//获取谁 元素就是谁  获取页面的 就是 document
btn.addEventLietener("click",function(){
  console.log(1);
})

```

### 事件三个阶段

**事件发生的时候 ,存在的三个阶段  捕获 到达目标  冒泡 **

#### 捕获和冒泡

- 捕获 : 从根部节点往目标节点上,一层一层的找,,捕获到用户点击的dom节点
- 冒泡 false:  从用户点击目标的Dom节点,到根节点,都会触发
  - 事件默认在冒泡阶段执行,若父元素也注册了和目标节点同样的事件,.也会执行

```js
box_1 .addElementLisener("click",function() {},false) //冒泡默认false 从自己 到 根元素

box_1 .addElementLisener("click",function() {},true)  //捕获  从根部 到 自己
```

#### 阻止冒泡

```js
box_1 .addElementLisener("click",function(e) {
  //e :event 事件对象
  //写在函数内部,不分先后顺讯
  e.shopPropagation();
},false)
```

## 事件对象e-属性

- 语法:事件对象 .描述一些事物的属性和方法,描述位置的一些属性

```js
var box_1 = document.querySelector("#box_1");
box_1 .addElementLisener("click",function(e) {
  //e(event):事件对象
  //1.client:可视区域
  e.clientX;
  e.clientY;
  
  //2.page页面
  e.pageX;
  e.pageY;
  console.log(e.pageX, e.pageY);//X,Y坐标
  
  //3.事件的目标对象，用户点击到谁上面；就是谁
  e.target; //返回DOM节点(标签) 
  
  //4.事件的绑定对象(事件源)，就是是绑定在哪个DOM节点上 和 this一样
  e.currentTarget;
  console.log( e.currentTarget); //返回DOM节点(标签) 
})
```

```js
//右键弹窗 浏览器的默认行为
// 1 给 页面-document  注册点击事件
// 以后但凡有希望在页面的任何位置都可以触发的事件，给document注册
document.oncontextmenu("click" ,function(e){
  //阻止默认行为
  e.preventDefault();
})
```

## 获取元素位置 

- offparent
- offsetLeft
- offsetTop

```js
var box =document.querySelector("#box");
console.log(box.style.top) //只能获取 行内样式里的 ,style标签里的获取不到

//offsetLeft = margin-left + left;
//只能获取位置 ,不能设置(设置只能通过style.left="")
console.log(box.offsetLeft);//获取位置 数字

//找一个有定位的父元素作参考,如没有则找body 或html
元素.offsetParent
```

### 事件解绑

```js
box.onclick = function (){}
box.onclick = function (){
  box.onclick = null;
}

box.addEventListener("click", function fn(){})
box.removeEventListener("click",fn)
```

## innerHTML

获取console.log(ul.innerHTML); //返回字符串

设置 ul.innerHTML = "可以添加内容,可识别标签"

### 事件委托

不给子元素注册事件,给父元素注册,点击子元素--根据冒泡规则,--父元素触发

## DOM节点属性

nodeName   返回DOM节点的标签名

**e.terget  返回DOM节点 .  **

# webApi day03

##  DOM

### 属性：修改DOM节点内容

- innerHTML ：
  - 可以获取和设置元素的内部的结构；
  - 会把旧的结构覆盖掉；

```js
// 元素.innerHTML = '是满足html语法的标签结构';
ul.innerHTML = '<li>狗蛋</li>';
```

- innerText：获取和设置元素对象（DOM节点）的文本信息；
- 对于页面上已存在的，或者即将新创建的节点都适用；

### 方法：创建DOM节点

- document.write();该方法可解析HTML结构，且多次写多次输出；
- document.createElement：根据指定的标签名，创建一个新的元素；

```js
// 参数：要创建的新的标签的标签名
// 返回值：一个元素对象 DOM节点；
// 注意：该方法创建的元素，是不会自动进入结构里面的，需要自己手动添加
document.createElement('标签名');
```



### 方法：添加DOM节点

- appendChild：指定一个父元素，追加子元素，**作为最后一个子元素**；**从后添加一个子元素**

```js
// 元素.appendChild(子元素);
var li = document.createElement('li');
li.innerText = "我是一个li"
ul.appendChild(li);
```

- insertBefore：在某个子元素之前，插入新的子元素

```js
//父元素.insertBefore(新的子元素,旧的子元素)
var second = document.querySelector('.second');
ul.insertBefore(li,second);
```

- 上面两个方法都是操作DOM节点（对象）在HTML结构中的真实的位置；





## 案例：发布微博-发布

- 需求：发送一条内容，显示在列表的第一条；
- 实现：
  - 获取元素：文本域、按钮、ul
  - 注册事件：按钮click
  - 点击之后：
    - 文本为空时：返回return；
    - 文本非空时：
      - 创建一个DOM节点；创建节点
      - DOM节点里设置我们新的内容：修改内容
      - 插入到列表最前面；追加节点；
      - 清空文本域

```js
  // 2 注册点击事件
  btn.onclick = function() {
    // 3.1 获取内容 - 注意： 表单元素的内容使用value获取
    var content = text.value;
    
    // 3.2 创建一个新的li，设置它的内容是一个p标签和一个span标签
    var li = document.createElement('li');
    li.innerHTML = '<p>' + content + '</p><span>删除</span>';
      
    // 3.3 使用insertBefore 把新建的li放到最前面
    // 3.3.1 先得到ul的第一个子元素
    var first = document.querySelector('ul > li:first-child');
    ul.insertBefore(li, first);
    // 3.4 把文本域的内容清空
      
    text.value = '';
  }
```



### 属性：根据DOM节点 获取 DOM节点

- 获取子元素：可以得到某个元素之下的所有的子元素的集合，一个**伪数组**

```js
父元素.children
```

- 获取父元素：返回一个；

```js
元素.parentNode
```

- 获取兄弟元素

```js
元素.nextElementSibling  -  得到下一个兄弟元素
元素.previousElementSibling - 得到上一个兄弟元素
```

## 案例：发布微博-发布优化

- 实现：插入到列表最前面；追加；
  - 插入：`父元素.insertBefore(新的子元素,旧的子元素)`
  - 旧的子元素：
    - 原来：`document.querySelector('ul > li:first-child')`;
    - 现在：通过节点的获取，`ul.children[0]`;



### 方法：删除节点

```javascript
// 父元素.removeChild(要删除的子元素);
var first = ul.children[0];
// 调用方法，移除
ul.removeChild(first);

```



## 案例：发布微博-删除

- 删除功能：
  - 获取元素：所有的删除按钮；（包括已有的和新增的）
  - 注册事件：click
  - 点击之后：删除按钮的父亲节点，被删除；
    - 找父亲节点：dom.parentNode;

```js
// 1. 获取所有的span
var spans = document.querySelectorAll('.weibo-list span');
// 2 注册点击事件
for(var i = 0; i < spans.length; i++){
    spans[i].onclick = function(){
        // 通过span得到li 通过this
        var li = this.parentNode;
        // 调用removeChild移除li
        ul.removeChild(li);
    }
}

```

- 点击新增微博的删除按钮，无效；因为新发布的信息上，删除按钮没有注册事件；
- 用事件委托：

```js
  // 2 使用事件委托实现点击span的效果
  ul.addEventListener('click', function(e) {

    // 判断点击的对象，是不是span
    if (e.target.nodeName === 'SPAN') {
      // 通过事件对象.target 得到触发事件的元素
      
      // 要通过span得到li
      var li = e.target.parentNode;
      // 通过ul把li移除
      ul.removeChild(li);
    }
  });

```





# BOM

- BOM： browser object model，是把**浏览器看成是一个对象**，就是学习浏览器对象的各种方法和属性；
- 浏览器对象：**window对象**；

### window 对象 

- 特点：
  - 所有window对象的属性和方法，**都可以直接省略  `window.`，而直接使用**
  - 因为window对象在浏览器中被称为顶级对象；
  - **顶级对象**：页面中所有的东西都是依赖于这个对象存在的；
  - 变量与函数：
    - **所有的全局变量和全局函数都是window对象的属性和方法**；
    - 在js代码里面，不使用var声明的变量，都是隐式全局变量，这个方式是不推荐的，因为如果不使用var声明，是不会变量提升的；

```js
// 1.所有window对象的属性和方法，直接省略  `window.`
document.getElementById('xx');


// 2.顶级对象
console.log(window.document == document);


// 3.全局变量和函数 都是window上的挂载
var a = 10;
console.log(window.a);

function fn() {
    console.log(1);
}
window.fn();


// 4.隐式变量：定义变量，变量赋值；
b = 2;
console.log(window.b);

// 访问变量：无赋值，就是访问变量；报错，无定义；
c;
console.log(window.c);

```



### 方法：onload

- 作用：页面加载完毕的时候执行
- 页面加载完毕：**页面所需的静态资源**全部加载完毕；
- 静态资源： **html文件、css文件、js文件、图片，**
- 这个方法调用一般是用window.onload 不省略window;

```javascript
window.onload = function(){
    // 想要获取图片的宽高，就需要等待图片加载完成后才执行后面的函数；
}

```



### 方法：定时器

#### 语法

- setTimeout：一次性定时器；set - 设置；Timeout - 超时

```javascript
// 作用： 延迟一定的毫秒之后，调用函数一次;
// 返回值： 是该定时器的id，id可以用于停止这个定时器
var timer = setTimeout(函数,延迟的毫秒数);

// 停止一次性的定时器：清除后，就不会执行这个定时器；
clearTimeout(timer);

```

- setInterval：永久性的定时器；interval - 间隔

```js
// 作用：阶段的时间执行函数；
// 返回值：就是该定时器的id
var timer = setInterval(函数,间隔毫秒数);

// 清除永久定时器
clearInterval(timer);

```

- 上面两个方法都是window对象下的方法；执行定时器，都是等待自己的间隔才开始执行；



### 案例：获取验证码-倒计时

- 获取元素：按钮
- 注册事件：click
- 点击之后：
  - 按钮表现为**禁用状态；**
  - 倒计时设置：
    - 开始计时，初始化
    - setInterval 1秒间隔，设置：
      - time--：
      - 改变按钮的值；
      - 清除倒计时：time==0时清除定时器；按钮恢复文字和可点击的样式；

```js
// 获取按钮
var btn = document.getElementById('getCode');
// 注册点击事件
btn.onclick = function(){
  // 禁用按钮，禁用不能点击了；
  btn.disabled = true;
    
    
  // 开始倒计时
  var time = 5;
  // 在点击的时候，先改变一次
  btn.value = '获取验证码('+ time +')';
    
  
  // 设置倒计时
  var timer = setInterval(function(){  
    // 每隔1秒钟，数字要减少1
    time--;  
    // 修改按钮的内容
    btn.value = '获取验证码('+ time +')';   
      
      
    // 当倒计时到达0的时候，停止定时器
    if(time === 0){
      // 停止的定时器
      clearInterval(timer);
      // 把按钮还原
      // 文字还原
      btn.value = '获取验证码';
      // 可以点击
      btn.disabled = false;
    }
      
  },1000);
}

```





### 属性：location

- location：负责管理浏览器地址栏相关的行为和信息的对象；
- 属性：  location.href 属性；该属性就是浏览器的地址栏里面的内容，
  - 获取：当前浏览器的地址；
  - 重新设置，页面就会发生跳转；

```javascript
// 如果想要使用js进行跳转，只需要 location.href = 新的地址;
location.href = 'https://www.jd.com';

```



### localStorage和JSON

#### localStorage

- 以前：我们在页面上操作一些，一刷新没有了。
- 把数据进行**本地储存**，刷新还是操作后的样子;
- 本地储存：本地指浏览器，储存指浏览器可以储存数据；

```js
// 存储： 后面的值 前面可以放入任何数据类型，保存后为字符串；
// 特别： 如果存储的是对象之类的复杂类型，需要先把复杂类型转换为的字符串，再存进去；
// 多次对一个键进行赋值，会把前面的值覆盖；
localStorage.setItem(键,值);

// 读取 数据
// 返回：我们存入的的数据的值，返回的是字符串；
localStorage.getItem(键);

// 删除键的值
localStorage.removeItem(键);　　

// 全部清空
localStorage.clear();　

```

### JSON

- 是个字符串，有一定格式的字符串；
- 格式：模拟JS对象和数组的格式；

```js
// [] JS 数组  {} 对象
// JSON: []模拟表示数组   {} 模拟对象  在字符串
// var str = '[{"name":"李狗蛋","age":12,"sex":"男"},{"name":"翠花","age":13,"sex":"女"}]';

```

- JSON方法：我们自己转json格式比较麻烦；js提供了JSON方法，里面封装好了很多跟json操作相关的方法

```js
// 将对象转换为json格式的字符串
// 返回值：一个满足json格式的 字符串
JSON.stringify(对象);

// 将json格式的字符串 转换为 对象
// 返回值：依赖于你的json格式字符串，可能返回数组，或者是对象....
JSON.parse(json格式字符串);

```





### 案例：发布微博v3.0

- 数据本地化、无删除功能

#### 已有数据本地化：（抽象数据）

- 页面上看到的列表，不是直接写在HTML结构上的，是从某个地方拿到到；
- 从哪里拿？
  - **真实的情况从服务器获取，服务器（大硬盘）里存的数据；**
  - 我们现在只能从本地（U盘）获取；
- 本地（U盘）：存的是什么数据格式？JSON数据格式；
- 拿到数据：把拿到的数据，展示在页面上；
- **需要我们把当前页面的数据，抽象为一个对象；工作经验：全部数据列为数组，一条数据列为对象；**
- 将数组变成json格式的字符串，使用localStorage.setItem() 进行存储

#### 初始化列表

- 获取元素：ul
- 注册事件：无
- 初始化：
  - **本地数据初始化：声明个变量，用于接收本地数据**  
    - 读取变量：
      - 有数据，转化为数组，JSON.parse();
      - 把数据渲染为列表
        - 新建DOM节点
        - 修改内容
        - 把每个DOM节点，从后插入父级的DOM节点里；
    - 没有数据：直接给变量赋值为空数组，**承接上面新增功能的全局声明一个数组**

```js
  var arr;
  // 正面本地化有这个数据，存在，已存储；
  if (localStorage.getItem('wbshuju') != null) {
    arr = localStorage.getItem('wbshuju');
    arr = JSON.parse(arr);
  }
  // 没有存在
  else {
    arr = []
  }

  // 列表显示
  var li = null;
  arr.forEach(function(ele, index) {
    li = document.createElement('li');
    li.innerHTML = '<p class="content">' + ele.content + '</p>' +
      '<span data-id="" class="del">删除</span>' +
      '<em class="time">' + ele.time + '</em>';

    // 插入到ul里面
    ul.appendChild(li);
  });

```

- 时间格式的函数化；

```js
  function patchZero(v) {
    return v < 10 ? '0' + v : v;
  }

  function formatDate() {
    var now = new Date();
    var y = now.getFullYear();
    var m = now.getMonth() + 1;
    var d = now.getDate();
    var h = now.getHours();
    var mm = now.getMinutes();
    var s = now.getSeconds();
    return y + '-' + patchZero(m) + '-' + patchZero(d) + ' ' + patchZero(h) + ":" + patchZero(mm) + ':' + patchZero(s);
  }

```

- 思考：如何把删除进行数据本地化

#### 发布

- 获取元素：文本域、按钮、UL；
- 注册事件：click
- 点击之后：
  - **新增DOM节点：**
    - 创建一个新的li
    - 获取文本域的内容，
    - 修改新的LI标签的内容
    - 从前插入插入到ul里面
  - **数据本地化：（抽象数据）**
    - 已经存在的数据，
    - **工作经验：全部数据列为数组，一条数据列为对象；**
    - 从后插入，为了保证数据的顺序和列表显示顺序一样；
    - 将数组变成json格式的字符串，使用localStorage.setItem() 进行存储
  - **清空文本域；**

```js
 btn.onclick = function() {
    // 2.3 获取文本域的内容
    var content = text.value;
    
     // 2.3.2 准备一个发布时间
    var time = formatDate();
    // 2.4 创建新的li
    var li = document.createElement('li');
    // 2.4.2 把ul里面也生成
    li.innerHTML = '<p class="content">' + content + '</p><span data-id="1557655950236" class="del">删除</span><em class="time">' + time + '</em>';
    
    // 2.5 插入到ul里面
    ul.insertBefore(li, ul.children[0]);

    // 2.6 把数据，存储到localStorage里面
    var obj = {
      content: content,
      time: time
    };
    arr.unshift(obj);

    // 2.7 把数据转换为json格式的字符串
    var arr_str = JSON.stringify(arr);
    localStorage.setItem('wbshuju', arr_str);

    // 把文本域清空
    text.value = '';
  }

```

# webApi day04

# DOM

## 事件：onkeydown、onkeyup

- 键盘事件：
  - 事件类型
    - 按键按下：keydown
    - 按键弹起：keyup
  - 按下哪个键？
    - 事件对象.keyCode，这个属性被称为  键盘码 ，每个按键对应的数字是不一样 ，只需要判断数字，就知道按下的按键是哪一个； keyCode==13 回车键
    - 按下了ctrl：事件对象里面有一个属性 ctrlKey ；如果是true，按下了ctrl键
- 实现：
  - 获取元素：文本域；
  - 注册事件：keydown；（组合键）
  - 按下键盘：判断e.ctrlKey && e.keyCode === 13全部成立

```js
text.onkeydown = function(e) {
    console.log(e.keyCode, e.ctrlKey);
    // 判断是否同时按下ctrl和回车
    if (e.ctrlKey && e.keyCode === 13) {
    }
}
```

## 案例：微博案例v4.0-组合键发布

- 实现：

```js
text.onkeydown = function(e) {
    console.log(e.keyCode, e.ctrlKey);
    // 判断是否同时按下ctrl和回车
    if (e.ctrlKey && e.keyCode === 13) {
        // 在代码中执行；
        btn.onclick();
    }
}
```

- btn.onclick()： 为什么可以这样写？.onclick只是元素对象上的属性，赋值为方法，调用执行；

## 案例：微博案例v4.0-删除

- 思路：
  - DOM节点操作：**在点击删除的时候，把对应li从ul里面移除**；背后实现事件委托：给父级注册点击事件，响应节点是子元素li;
  - 本地化数据更新：**删除对应的那个数据，那我怎么知道我要删除哪个？**
    - 唯一的ID：
      - ID：identification身份证，保证该数据绝对的唯一，我们就能找到它；
      - 构成：采用 时间戳+随机数，基本可以保证不会重复；
    - 生成ID，在发布阶段生成：
      - 新增DOM节点，修改DOM节点内容同时，把新增的ID通过赋值为自定义属性的方式加进去；
      - 本地数据，把ID存进去；
    - 删除：有了发布时新增的ID，点击删除时，获取点击对象的自定义属性ID，
      - DOM去除：删除DOM，
      - 数据去除：根据唯一的ID去找当前的数组内的数据，剔除掉；完成更新本地数据；

```javascript
// ------------------------------------------------------发布
// 生成一个唯一的id
var id = Date.now() + '' + Math.floor(Math.random() * 10000);

// 更变发布时的ID插入，自定义属性
li.innerHTML = '<p class="content">' + content + '</p>' +
  '<span class="del" data-id="'+ id +'">删除</span>' +
  '<em class="time">' + time + '</em>';
ul.insertBefore(li, ul.children[0]);

// 保证你的存的数据顺序和展示的顺序一样；
wbData.unshift({
  id : id,
  content: content,
  time: time
});


// ----------------------------------------------------删除
// 获取ID
var delId = e.target.dataset.id;

// 删除DOM
var li = e.target.parentNode;
ul.removeChild(li);


// 删除本地数据
wbData.forEach(function(e,i){
  if(e.id === delId){
    wbData.splice(i,1);
  }
});

// 更新本地数据
var result = JSON.stringify(wbData);
localStorage.setItem('wbshuju',result);
```



## 事件：onmouseover、onmouseout

- 鼠标移入某个元素的时候，触发事件；

```js
<div class="box" index=0></div>

// 鼠标移入时触发
var box = document.querySelector('.box');

// 对象属性，
box.a = 0;

box.onmouseover = function() {
    // 获取自定义属性
    this.getAttribute("index");
    
    // 添加节点属性，随便添加；
    console.log(this.a);
}

// 鼠标移除时触发
dom.onmouseout = function(){ 
}
```

## 案例：tab栏

- 案例：鼠标移入一个选项（选项变为当前选择状态），下面图就会跟着发生变化；
- 实现：
  - 获取元素：选项、图片；
  - 注册事件：选项，鼠标移入；
  - 移入后的变化：
    - 按钮的状态变化：**排他思想**
      - 先把所有的清除为初始化状态；
      - 给当前DOM节点加当前选择状态；
    - 图片的变化：**排他思想**
      - 先把所有图片清除样式；
      - 给当前选项一样的下标的图片，当前样式；

```js
  // 给所有的tab注册鼠标移入事件
  for (var i = 0; i < tabs.length; i++) {
	
    tabs[i].onmouseover = function() {
      // 排他思想： 就是遇上一部分不一样，其他都一样，就使用排他思想
      // 排他的第一步： 先把所有的都变成普通
      for (var j = 0; j < tabs.length; j++) {
        tabs[j].classList.remove('active');
      }
      // 然后把特殊的变特殊
      // 给自己添加一个class
      this.classList.add('active');

      // 3.3 根据索引获取对应的商品
      // console.log(this.index);
      // 排他的设置商品的显示和隐藏
      for (var k = 0; k < goods.length; k++) {
        goods[k].classList.remove('selected');
      }

      var index = this.getAttribute("index");
      // 把对应的商品显示
      goods[index].classList.add('selected');
    }
  }
```

- **上面是通过获取自定义属性的方式拿到对应的下标，也可以把index的值，作为每个DOM节点的对象属性存起来；**这个在工作上非常常用，可以把一一对应的数据初始化在你的DOM节点上，也可以后期在JS内把相关属性设置在对象上；

```js
  // 给所有的tab注册鼠标移入事件
  for (var i = 0; i < tabs.length; i++) {
	tabs[i].index = i;
    tabs[i].onmouseover = function() {
      // 排他思想： 就是遇上一部分不一样，其他都一样，就使用排他思想
      // 排他的第一步： 先把所有的都变成普通
      for (var j = 0; j < tabs.length; j++) {
        tabs[j].classList.remove('active');
      }
      // 然后把特殊的变特殊
      // 给自己添加一个class
      this.classList.add('active');

      // 3.3 根据索引获取对应的商品
      // console.log(this.index);
      // 排他的设置商品的显示和隐藏
      for (var k = 0; k < goods.length; k++) {
        goods[k].classList.remove('selected');
      }
	
      // 获取当前DOM节点 对应的下标；  
      var index = this.index;
      // 把对应的商品显示
      goods[index].classList.add('selected');
    }
  }
```



## BOM方法：获取DOM节点样式

```js
// Computed：计算后的样式
// 返回值： 当前作用在这个元素身上的所有样式的集合对象  BOM的方法；
// 属性：具体的属性 无论是行内的还是样式设置的，都可以获取到；字符串
var res = window.getComputedStyle(元素对象)；
res.width 

// 只能操作行内属性；
var dom = document.getElementById('xx');
dom.style.color；
```

## 属性：获取元素的实际宽度和高度

- 元素的实际宽高 = border+padding+content（width和height）

```js
// 返回值：数值；

// 只能进行获取；
// 元素的实际宽度
元素.offsetWidth 
// 元素的实际高度
元素.offsetHeight

// 获取和设置
dom.style.width；
```

## 案例：轮播图需求

- 布局：ul下有很多li标签；浮动在一行；
- 原理：切换图片的时候，把ul位置修改一下，给ul的父容器，设置一个 overflow:hidden；
- 功能需求：
  - 序号轮播
  - 左右按钮的轮播
  - 自动轮播
  - 鼠标在轮播图里面的时候，停止自动轮播，离开后继续自动轮播

## 需求：序号轮播

- **其实就是tab栏；**
- 获取元素：所有的小圆点序号
- 注册事件：鼠标移入mouseover小圆点的事件
- 移入之后：
  - 小圆点：排他思想实现当前样式出现；
  - 图片切换：计算ul应该向左移动多少，`ul的位置 = 图片宽度 * 索引 * -1`;

```js
    // 1.1 获取元素 (小圆点，ul)
    var circles = document.querySelectorAll('.list>i');

    var ul = document.getElementById('imglist');

    // 定义一个变量，保存图片的宽度 // li和图片的宽度是一样的
    var imgWidth = ul.children[0].offsetWidth;

    // 1.2 给序号注册鼠标移入事件
    for (var i = 0; i < circles.length; i++) {
	  // 先把数据存起来；
      circles[i].index = i;
      circles[i].onmouseover = function() {
        var target = imgWidth * this.index * -1;


        ul.style.left = target + 'px';
        ul.style.transition = "left 300ms linear";

		// 当前样式设置；排他思想；
        circles.forEach(function(c) {
          c.classList.remove('current');
        });
        this.classList.add('current');
      }

    }

```



## 需求：左右轮播

- 获取元素：左右按钮
- 注册事件：click
- 点击之后：整体向左滑动一格；
  - 变量控制下标增1；
  - 我要一直向右滑动动么？
    - 不能滑动到无限，
    - 点击下标为5，显示为第6张；
    - 点击下标为6，显示为第1张；回归下标为0；
- 实现：**点击右侧**
  - 设置变量，为初始化图片的下标为0；
  - 点击右侧，变量加+；
    - 下标0：显示第一张；
    - 下标为5：显示第六张；
    - 下标为6，当前显示第1张，回到下标为0;

```js
    //注册点击事件
    // 下标为0；当前显示第1张
    // 下标为1；当前显示第2张
    // 下标为5，当前显示第6张
    // 下标为6，当前显示第1张，回到下标为0;
    rightBtn.onclick = function() {
      currentIndex++;

      // 下标等于长度的时候，应该恢复到第1张，下标为0；
      if (currentIndex == ul.children.length) {
        currentIndex = 0;
      }

      // 算出ul的位置
      var target = currentIndex * imgWidth * -1;
      // 设置ul的位置
      ul.style.left = target + 'px';

    };

```

- 实现：**点击左侧**
  - 设置变量，为初始化图片的下标为0；（0：已经显示为第一张图片）
  - 点击左侧，变量加-；
  - 当 变量==0 时，让它归到ul.children.length - 1；
    - 0下标：显示第一张；
    - 5下标：显示第六张；
    - 所以：点击的一瞬间：变量==0，应该显示第六站图片，归于ul.children.length - 1；

```js
leftBtn.onclick = function() {
    // 如果已经第一张，切换到最后一张
    if (currentIndex === 0) {
        currentIndex = ul.children.length - 1;
    } else {
        // 让表示第几张图片的变量--
        currentIndex--;
    }
    // 算出ul的位置
    var target = currentIndex * imgWidth * -1;
    // 设置ul的位置
    ul.style.left = target + 'px';
}

```



## 需求：左右联动序号

- 点击左右按钮切换图片后，小圆点也应该跟着切换当前样式；
- 让当前下标的小圆点的样式变化：排他思想；

```js
    rightBtn.onclick = function() {
	  ...

      // 联动序号
      // 归根到底，左右切换控制的就是index，序号也是控制的index。
      // 左右切换时，应该把左右切换控制的index,影响到序号的样式上；

      // 样式联动：排他思想
      circles.forEach(function(c) {
        c.classList.remove('current');
      });
      circles[currentIndex].classList.add('current');

    };


```



## 需求：序号联动左右

- 完成上面左右切换联动序号样式；
- 当鼠标通过序号切换后，在用左右切换，会出现问题，原因：
  - 左右按钮控制一个**全局变量**，也把全局变量的值联动给**小圆点的样式**了；（左右切换联动序号）
  - **小圆点自己切换的时候，没有影响到全局变量，所以会出现乱转的情况；**
- 如何设置：把小圆点切换时控制的当前的下标，赋值给全局的变量（左右按钮控制的那个变量）即可；

```js
    // 1.2 给序号注册鼠标移入事件
    for (var i = 0; i < circles.length; i++) {
      // const element = array[index];
      circles[i].index = i;
      circles[i].onmouseover = function() {
        // 计算
        var target = imgWidth * this.index * -1;
        // 移动
        ul.style.left = target + 'px';

        // 样式设置
        circles.forEach(function(c) {
          c.classList.remove('current');
        });
        this.classList.add('current');

        // 联动
        // 要把序号切换的值，影响到全局的变量形成统一；
        currentIndex = this.index;
      }

    }

```



## 需求：自动轮播及鼠标控制轮播

- 初始化页面，页面自动向右轮播；
- 实现：
  - 需要把向右的函数提炼为一个函数
  - 定时器：执行向右点击的函数

```js
// 自动轮播
var timer = setInterval(function() {
    moveRight();
}, 2000);

```

- 鼠标不在整个盒子上操作时，图片自动向右轮播；
- 现实：
  - 获取元素：整个盒子；
  - 注册事件：鼠标移出；
  - 移出之后：定时器执行向右的函数；（需要把向右的函数提炼为一个函数）

```js
// 鼠标移出，恢复自动轮播
box.onmouseout = function() {
    timer = setInterval(function() {
        moveRight();
    }, 2000);
}

```

- 鼠标在盒子上，停止自动轮播
- 实现：
  - 获取元素：整个盒子；
  - 注册事件：鼠标移入；
  - 移入之后：清除定时器；

```js
var box = document.getElementById('box');
box.onmouseover = function() {
    clearInterval(timer);
};

```

# day-05



# 案例：手风琴特效

## 需求

- 鼠标移入，鼠标当前的图片变宽，其他变小（排他思想）
- 鼠标移出，所有图片大小恢复原状

## 移入

- 获取元素：所有的li元素
- 注册事件：鼠标移入
- 移入之后：排他
  - 所有的li变为一个值100；
  - 当前单独变为一个值800；

```js
var lis = document.querySelectorAll('#box li');

  for (var i = 0; i < lis.length; i++) {


    // 注册鼠标移入事件
    lis[i].onmouseover = function() {
      // 排他的设置每个li的宽度
      lis.forEach(function(element) {
        element.style.width = 100 + 'px';
      })
      this.style.width = 800 + 'px';
    };

  }
```

## 移除

- 获取元素：所有的li元素
- 注册事件：鼠标移出
- 移出之后：所有的元素回复原来的宽度240

```js
  for (var i = 0; i < lis.length; i++) {

    // 注册鼠标的移出事件
    lis[i].onmouseout = function() {
      // 把所有的li恢复原状
      lis.forEach(function(element) {
        element.style.width = 240 + 'px';
      });
    };

  }
```





# 案例：点击按钮切换位置

- 需求：点击按钮切换盒子的位置；
- 需知：**控制盒子的位置和大小的类名为数组；**
- 实现：
  - 初始化：把数组按照盒子的循环，改变类名；
  - 点击按钮，改变类名数组的位置，重新给盒子循环赋值类名；

```js
  var pos_arr = ["pos_1", "pos_2"];
  var boxs = document.querySelectorAll("p");
  // 初始化
  setTimeout(function() {
    for (var i = 0; i < boxs.length; i++) {
      boxs[i].className = pos_arr[i];
    }
  }, 1000);
  
  // 点击切换；
  var btn = document.querySelector("#btn");
  // 点击后，位置发生改变；
  // 实质上为 控制位置类名的数组发生改变；
  btn.onclick = function() {
    // 
    var last = pos_arr.pop();
    pos_arr.unshift(last);

    // console.log(pos_arr);

    for (var i = 0; i < boxs.length; i++) {
      boxs[i].className = pos_arr[i];
    }

  }
```

- 函数优化：

```js
  var pos_arr = ["pos_1", "pos_2"];
  var boxs = document.querySelectorAll("p");

    function change(){
        for (var i = 0; i < boxs.length; i++) {
          boxs[i].className = pos_arr[i];
        }
    }
  // 初始化
  setTimeout(function() {
    change();
  }, 1000);
  
  // 点击切换；
  var btn = document.querySelector("#btn");
  // 点击后，位置发生改变；
  // 实质上为 控制位置类名的数组发生改变；
  btn.onclick = function() {
    // 
    var last = pos_arr.pop();
    pos_arr.unshift(last);

    change();
  }
```

- 特点：HTML结构不变，变的是类名数组；



# 案例：旋转木马

## 需求

- 让所有的图片从中间展开
- 点击右边按钮，让图片可以逆时针旋转
- 点击左边按钮，让图片可以顺时针旋转

## 初始化

- 初始化布局：给每个li分别设置一个可以控制位置、大小、层级的类名，给类名使用一个数组的方式管理起来，直接按照索引对应的方是设置位置即可；
- 获取元素：获取所有的li
- 注册事件：无
- 初始化：使用循环设置所有的li的大小、位置、层级->只是设置一个已经准备好的类名

```js
var lis = document.querySelectorAll('.slide li');
var pos = ['left1', 'left2', 'middle', 'right2', 'right1'];
// 遍历所有的li，设置类名，就可以发送位置的变化
for (var i = 0; i < lis.length; i++) {
    lis[i].className = pos[i];
}
```

## 左右按钮

- 右按钮分析：第一张图
  - HTML结构：没变；
  - 变化的是：类名在数组中的位置；
- 如何变化：

```js
// 初始化：
// HTML : 1        2         3         4          5
// 位置：'left1', 'left2', 'middle', 'right2', 'right1'


// 右侧点击下：
// HTML :    1        2         3         4          5
// 位置类名：'left2', 'middle', 'right2', 'right1'  'left1',
```

- 实现：
  - 获取元素：左右按钮
  - 注册事件：click
  - 点击之后：
    - **右侧：把第一个类名拿出来，从后添加；**
    - **左侧：把最后一个类名拿出来，从前添加；**

```js
// 初始化再次设置每个li的位置
lis.forEach(function (e, i) {
  e.className = pos[i];
});
// 封装为函数
function rotate() {
  lis.forEach(function (e, i) {
    e.className = pos[i];
  });
}


// 点击右边按钮
var rightBtn = document.querySelector('.next');
// 注册点击事件
rightBtn.onclick = function () {
  // 把位置数组的第一个取出，放到最末尾
  pos.push(pos.shift());
  // 再次把每个li移动
  rotate();
}


// 左侧
leftBtn.onclick = function () {
  // 把位置数组从最后面抽取一个，放到最前面
  pos.unshift(pos.pop());
  rotate();
}
```



# 案例：360开机动画

## 知识

- 动画结束事件：专门是指c3里面的动画结束会触发的事件，c3动画有两种，结束动画事件也有两个；
- **不能使用on的方式注册，只能使用addEventListener的方式注册**
- transitionend：元素的过渡动画结束的时候触发；

```js
var box = document.querySelector('.box');
box.addEventListener('transitionend',function(){
  console.log(123);
});
```

- animationend：会在帧动画结束的时候触发

```js
var box = document.querySelector('.box');
box.addEventListener('animation end',function(){
  console.log(123);
})

```

- 注意：如果帧动画是无限次的，不会触发该事件animationend

## 需求

- 分两段**过渡动画**，先让底部的高度逐渐为0，再让整个盒子的宽度为0；

## 实现

- 获取元素：盒子底部，整体盒子
- 注册事件：盒子底部 transitionend
- 过度完成：设置整体盒子width

```js
closeButton.onclick = function() {
    // 把下半部分的高度设置为0
    bottomPart.style.height = 0;
}


var box = document.querySelector("#box");
bottomPart.addEventListener('transitionend',function(){
  // 把box盒子的宽度修改为0
  box.style.width = 0;
});

```







# 案例：放大镜效果

## 需求分析

- 鼠标移入，出现黄色的遮罩，和用来放大的盒子
- 鼠标移出，遮罩和放大的盒子消失
- 鼠标在小图片上面进行移动的时候
  - 黄色遮罩层会随着鼠标一起移动
  - 用来放大显示的图片，也跟着一起移动

## 移入移出

- 获取元素(box,遮罩，放大用的盒子)
- 注册事件：移入移出
- 之后：遮罩和放大盒子显示和隐藏

```js
//2 注册鼠标的移入和移出事件
box.onmouseover = function(){
  // 3 控制遮罩和放大的盒子显示
  mask.style.display = 'block';
  big.style.display = 'block';
}
box.onmouseout = function(){
  // 3 控制遮罩和放大的盒子隐藏
  mask.style.display = 'none';
  big.style.display = 'none';
}

```

## 遮照随鼠标移动

- 获取元素：small图
- 注册事件：mousemove
- 移动之后：鼠标的位置计算出遮罩应该在位置，设置给遮罩；
  - 应该在的位置：遮罩的位置 = 鼠标的位置 - box的位置 - mask的宽高的一半

![1557907954256](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/01-%E8%B5%84%E6%96%99/assets/1557907954256.png)

```js
small.onmousemove = function(e){
  // 根据鼠标的位置，计算出遮罩应该在哪个位置
  var mx = e.pageX;
  var my = e.pageY;
  
  // 5 遮罩在盒子内的位置 = 鼠标位置 - box的位置 - 遮罩宽高的一半
  var x = mx - box.offsetLeft - mask.offsetWidth / 2;
  var y = my - box.offsetTop - mask.offsetHeight / 2;

  // 7 设置给mask
  mask.style.top = y + 'px';
  mask.style.left = x + 'px';
}

```

- 范围问题：遮罩只能在small里面移动；最小值和最大值
  - 最小值：0；如果遮罩的位置小于0了，强行设置为0；
  - 最大值： small的宽高 - mask的宽高；遮罩的位置大于最大值了，强行设置为最大值；

```js
small.onmousemove = function(e){
  // 4 根据鼠标的位置，计算出遮罩应该在哪个位置
  var mx = e.pageX;
  var my = e.pageY;
  
  // 5 遮罩的位置 = 鼠标位置 - box的位置 - 遮罩宽高的一半
  var x = mx - box.offsetLeft - mask.offsetWidth / 2;
  var y = my - box.offsetTop - mask.offsetHeight / 2;
  
  // 6 不让遮罩超出边界,最小值0
  x = x < 0 ? 0 : x;
  y = y < 0 ? 0 : y;
    
   
  // 算出mask移动的最大距离
  var maxX = small.offsetWidth - mask.offsetWidth;
  var maxY = small.offsetHeight - mask.offsetHeight;
  x = x > maxX ? maxX : x;
  y = y > maxY ? maxY : y;
    
  // 7 设置给mask
  mask.style.top = y + 'px';
  mask.style.left = x + 'px';
}

```

- offset属性总结：

```js
  元素.offsetTop - 得到元素距离它的offsetParent的垂直距离
  元素.offsetLeft - 得到元素距离它的offsetParent的水平距离
  元素.offsetParent - 得到一个距离我最近的定位的前代元素，如果我的前代元素都没有定位，得到body或者html
  元素.offsetWidth - 元素的实际宽度 = border+padding+width
  元素.offsetHeight - 元素的实际高度 = border+padding+height

```

## 放大效果

- 获取元素：大图片

- 注册事件：小图片移动

- 移动之后：鼠标的位置计算出大图应该在的位置，设置给大图

  - 移动比例：
    - 我在小图上移动从左到右，移动了`small.offsetWidth - mask.offsetWidth`，
    - 按照道理大图应该移动 `bigImg.offsetWidth - big.offsetWidth`；

  ```js
  (small.offsetWidth - mask.offsetWidth)/(bigImg.offsetWidth - big.offsetWidth) 
  = 
  y/big_y
  
  ```

  - 计算大图应该移动的位置：

  ```js
  var bigImgX = x * bigImgMaxX / maxX;
  var bigImgY = y * bigImgMaxY / maxY;
  
  ```

  - 设置：

  ```js
  // 10 设置给大图,注意方向是相反的
  bigImg.style.top = -bigImgY + 'px';
  bigImg.style.left = -bigImgX + 'px';
  
  ```

  - `bigImg.offsetWidth - big.offsetWidth`：
    - offsetWidth包括：content+padding+border；border不应该计算在内；原因：小遮照覆盖的范围是自己的offsetWidth(border+padding+width)
    - 大遮照显示的范围应该是盒子的视图宽度，不包括border值；获取盒子的视图宽高： 包括padding + content 

  ```js
  元素.clientWidth - 可视区域的宽度  content+padding
  元素.clientHeight - 可视区域的高度
  
  (small.offsetWidth - mask.offsetWidth)/(bigImg.offsetWidth - big.clientWidth) 
  = 
  y/big_y
  
  ```

# webAPI day_06 



# DOM

## 触摸事件

- **pc端click**：经常使用的一个事件是点击事件，这个事件一般在移动端是不用的；
- **移动端不使用click的原因**：
  - 在移动端可以双击，当我们点一下的时候，移动端不会立刻执行点击事件的，而是会稍微等待一下，
  - 因为移动端会在**点下的瞬间需要知道到底是单击还是双击**，
  - 有一个短暂的延迟才会执行click事件，**但是这个对于用户来说不是太友好。**
- 移动端事件：触摸事件

```js
touchstart - 会在手指触摸到屏幕的时候触发
touchmove - 会在手指触摸到屏幕，移动的过程中触发
touchend - 会在手指离开屏幕的瞬间触发
```

- 注点意：
  - 触摸事件在pc端是不会触发的，**必须是在移动端才可以**
  - 推荐使用addEventListener的方式注册：有很多移动端的事件，都是后面h5或者c3才出现的，on的方式没有对应的属性
- **事件对象属性：触摸点**

```js
事件对象.touches - 屏上面的触摸点
事件对象.targetouches - 元素上面的触摸点
事件对象.changedTouches - 变化的触摸点
```

![1557973130914](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/1557973130914.png)

- 用一个手指触摸屏幕内的元素：
  - 刚触摸时touchstart：touches、targetTouches、changedTouches，有一个值；都是同一个值；
  - 在元素上触摸移动时touchmove：touches、targetTouches、changedTouches，有一个值；都是同一个值；
  - 离开屏幕：touches、targetTouches没有值；changedTouches有最后离开屏幕的值；

```js
  box.addEventListener('touchstart', function(e) {
    // console.log(123);
    console.log(e.touches);
    console.log(e.targetTouches);
    console.log(e.changedTouches);

  })

  var key = true;
  box.addEventListener('touchmove', function(e) {
    if (key) {
      key = false;
      console.log(456);
      console.log(e.touches);
      console.log(e.targetTouches);
      console.log(e.changedTouches);
    }
  });
  box.addEventListener('touchend', function(e) {
    console.log(789);
    console.log(e.touches);
    console.log(e.targetTouches);
    console.log(e.changedTouches);
  })
```



## 封装tap手势

- **手势：**单击、双击、三击、放大、旋转、滑动....（相当于类型PC端的各种事件类型，PC端相对简单）
- 以上这些手势，**都没有原生的事件对应的**；
- 比如类似PC的点击click，在移动叫tap事件，我们只能自己利用js里面提供的touch事件自己封装。（封装的难度较大）
- **tap要求：模拟PC端的点击**
  - 点下和松开的**位置要接近**
  - 点下和松开的**时间不能太长**
- 封装思路：
  - 在touchstart的时候，**记录开始位置**，在touchend的时候**记录结束位置**，相减，判断这个差不能大于某个值；
  - 在touchstart的时候，**记录开始时间**，在touchend的时候**记录结束时间**，相减，判断这个差不能大于某个值；
- 实现：
  - 获取元素：随便获取个元素对象；
  - 注册事件：touchstart、touchend
  - touch之后：
    - touchstart：
      - 判断点击touches的对象数量，若为2，则不是一个手指在点击；返回false;
      - 若为1个对象：**记录开始位置和开始时间；**
    - touchend：
      - 判断点击changedTouches的对象数量，若为2，则不是一个手指在点击；返回false;
      - 若为1个对象：
        - 记录结束位置和结束时间
        - 把位置和时间相减，再判断是否小于我们规定的值；
        - 从而判断是否为单个手指的“点击”效果；
        - 最后执行回调函数；

```js
// 封装：现阶段，封装对于我们来说，函数比较容易实现
// 函数，就需要参数，所以需要明确函数的参数的作用；
/**
 * 自己封装的tap事件
 * @param {object} element 事件源
 * @param {function} callback 事件处理程序
 * @param {number} offset 手指抖动的最大偏移量,默认是50
 * @param {number} timeSpan 点下的最大毫秒数，默认是300
 */
function tap(element, callback, offset, timeSpan) {
    offset = offset || 50;
    timeSpan = timeSpan || 300;
    var startX, startY, startTime;

    element.addEventListener('touchstart', function (e) {
      // 判断是否是一个手指按下
      if (e.touches.length != 1) {
        console.log('已经不是一个手指的操作了');
        return;
      }
      // 记录开始位置
      startX = e.touches[0].pageX;
      startY = e.touches[0].pageY;
        
      // 记录开始的时间
      startTime = Date.now();
    })

    element.addEventListener('touchend', function (e) {
      // 判断是否只有一个手指
      if (e.changedTouches.length != 1) {
        console.log('不是单击操作');
        return;
      }
        
      // 记录结束位置
      var endX = e.changedTouches[0].pageX;
      var endY = e.changedTouches[0].pageY;
      // 记录结束时间
      var endTime = Date.now();
        
        
      // 计算，判断
      if (endTime - startTime > 300) {
        // 不是单击，是长按
        console.log('是长按了');
        return;
      }
      
      // 希望开始和结束之间的距离不要超过50 - 要计算一下绝对值，因为我们滑动的方向可能不确定
      if (Math.abs(endX - startX) >= 50 || Math.abs(endY - startY) >= 50) {
        console.log('滑动了太多的位置');
        return;
      }

      // 如果是一个单击tap事件，就应该调用一个函数
      callback && callback();
    })
  }
```

- 自己封装一个是比较麻烦，一般在开发里面，会使用别人**封装好的类库；**



# zepto 类库

## 介绍

- 一个比较流行的，**移动端专用的类库**(尽量不要在pc端使用)；
- **Zepto**是一个轻量级的**针对现代高级浏览器的JavaScript库，** 
  - 它与jquery**有着类似的api**。 如果你会用**jquery**，那么你也会用zepto。
  - jquery：很早的类库，PC端使用的类库，我们下个阶段会学；
- zepto类库能做什么？**封装好的功能，更简单的使用；**
  - **操作DOM节点**：增删
  - **注册事件**
  - 操作属性（标准、自定义）
- 引入：
  - 中文API：https://www.html.cn/doc/zeptojs_api/
  - 下载：选择版本；
  - 使用script:src的形式引入JS文件；

![1557979012914](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/1557979012914.png)

## API

- 中文API：https://www.html.cn/doc/zeptojs_api/
- 获取元素对象

```js
// 返回值是一个伪数组 称为 zepto对象，
var box = $(选择器); 
```

- 注册事件、修改样式

```js
// zepto的事件源.on(事件类型,处理程序);
box.on('click', function() {
    // 修改样式 zepto对象.css(属性名,属性值);
    $(this).css('backgroundColor', 'red');
});
```

- 操作DOM节点

```js
box.append('<a href="#">百度</a>');
```

- 其他：

```
// 获取宽度
box.width()；
box.css("width","200px")；
```



- 其他如果感兴趣，自己看看文档，可以提前参考**jquery**进行学习；



## 手势 touch.js

- zepto这个类库特点：把**多个功能分割为了多个独立的模块**，每个模块负责不同的功能，当我们需要哪个功能，就引入哪个模块。
- 分模块的原因：以前移动端的网络速度比较慢，希望把每次加载页面所需的资源尽量减少。提高页面的加载速度。
- 手势模块：zepto里面有一个专门负责封装手势的模块，touch.js
- 引入：
  - 找到文档里面的模块部分，点击跳转到模块描述区域，点击touch.js的模块跳转过去，把该页面的js代码自己复制到自己的项目里面
  - 引入，但是必须是在引入了zepto.js之后引入，因为touch.js仅仅是zepto.js的功能的拓展

![](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/001.png)

- API文档：touch模块的使用
  - 可以直接使用on的方式注册
  - 可以使用事件名称作为方法使用

![](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/002.png)

## tap

- 手势：点击

```javascript
// zepto.js提供了下面的方式注册tap事件
// 1 使用on的方式注册
$('.box').on('tap',function(){
  console.log(1);
});

// 2 调用tap方法
$(".box").tap(function(){
  console.log(3);
});

```

## swipe

- 手势：滑动

```js
// 注意：这不是原生的事件，这是类库人家封装后的方案；
// 封装后：我们只需要关注如何使用，能给我们提供什么就可以了，想研究可以集中研究；
$(".box").on('swipeLeft', function() {
    console.log(2);
});

```

### 案例：简单轮播图

- 需求：
  - 左划效果：图片从第n张到第n+1张
  - 右划效果：图片从第n张到第n-1张
- 左划实现：
  - 获取元素：box、ul
  - 注册事件：box注册swipeLeft 
  - 左划之后：
    - 设置全局索引，代表当前的图片的下标及显示的位置；
    - 左划，索引从当前+1，计算出ul应该出现的位移，设置给ul;
    - 同时划到最后一张时，当前下标是图片数组长度-1，再次左划，归于0；

```js
// 这个伪数组我们称为 zepto对象，
var box = $(".box"); 
var ul = $(".box > ul");
// 获取图片的宽度
var imgWidth = box.width();


// 下标：0 显示HTML：第1张
var currentIndex = 0;

// 往左划
box.on('swipeLeft', function() {
    // 让当前索引++
    currentIndex++;

    // 下标0:1；
    // 下标6:7
    // 设置6张
    if (currentIndex == li_arr.length) {
        currentIndex = 0;
    }

    // 计算出ul应该在的位置 = 索引 * 图片宽度 * -1
    var target = currentIndex * imgWidth * -1;
    ul.css('transform', 'translate(' + target + 'px)');
});


// 右划
box.on('swipeRight', function() {
    currentIndex--;
	
    // 下标-1：应该是第六张，就是5；
    if (currentIndex == -1) {
        currentIndex = 5;
    }

    var target = currentIndex * imgWidth * -1;
    ul.css('transform', 'translate(' + target + 'px)');
});

```



### 案例：无缝轮播

- 上个案例：从第6张到第1张的时候，我们想也要一个滑动过渡的效果；
- **解决：我们使用一个小手段，骗下用户的眼睛。给首尾各添加一张图片；**

```html
<ul>
      <li><a href="#"><img src="./images/6.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/1.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/2.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/3.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/4.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/5.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/6.jpg" alt=""></a></li>
      <li><a href="#"><img src="./images/1.jpg" alt=""></a></li>
    </ul>

```

- 左划思路：
  - 当我们划到6.jpg时（实际上在HTML顺序上是倒数第二张），让用户觉得已经到最后一张了。
  - 再往左划时，会划出来1.jpg（实际上在HTML顺序上是最后一张），让用户觉得到无缝到了第一张了。
  - **这个时候，我们通过一个事件（当过渡结束时），我们一瞬间把整个管理图片的父亲的位置归到1.jpg（实际上在HTML顺序上是第二张）的位置；这样就无缝完成！**
- 第一步：修改HTML结构上增加了两个子元素，css样式要改变

```css
ul {
  /* 把li变成8张之后，需要，把ul的宽度变宽 */
  width: 800%;
  display: flex;
}
li {
  float: left;
  width: 12.5%;
}

```

- 实现：
  - 获取元素：box，ul等
  - 注册事件：左右划、过渡结束
  - **划动过渡结束后：**
- 第二步：**判断当前的下标在划动过渡结束后进行判断，那么就不需要左划右划里进行判断了**；
- 第三步：默认显示HTML结构第2张，下标初始化为1；

```js
  var currentIndex = 1;

  // 一开始执行下；
  var target = currentIndex * imgWidth * -1;
  ul.css('transform', 'translate(' + target + 'px)');

  // 需要把CSS的过渡效果注释掉；
  // 若一开始加上，会有过渡的效果发生；
  setTimeout(() => {
    ul.css('transition', 'transform 300ms');
  }, 1);

```

- 第三步：**划动过渡结束后的全局的下标的值进行判断**
  - 往左划时：
    - 下标为7时，显示的为HTML结构上的第8张；
    - 在过渡结束后，下标立马回到1；（下标为1，HTML显示为2）
    - 是返回去了，但是过渡效果还在；所以应该先去除过渡效果，在移动，再加上过渡效果；

```javascript
ul.on('transitionend', function() {
    // 往左滑动的时候；
    // 当下标变为7的时候，显示的是HTML结构上的第8张；
    // 滑动的过程中，过渡没有结束
    // 过渡结束后（过渡效果已经完成了），如果为7时，应该立即让你回到HTML结构上的第2张，下标为1；
    if (currentIndex == li_arr.length - 1) {
      // 立马回到HTML结构上的第2张，设置下标1；
      currentIndex = 1;
		
          
      // 回到正确的位置
      var target = currentIndex * imgWidth * -1;
      ul.css('transform', 'translate(' + target + 'px)');
        
        
      // 但是过渡效果还在啊；去掉过渡
      ul.css('transition', 'transform 0ms');

      // 回到正确的位置后，后面还应该加上过渡
      setTimeout(function() {
        ul.css('transition', 'transform 300ms');
      }, 1);
    }


    // 往右滑动
    // 当我们滑到1.jpg,实际上HTML结构顺序是2，下标是1；
    // 当我们滑到6.jpg,实际上HTML结构顺序是1，下标是0；
    // 过渡结束后（过渡效果已经完成了），如果为0时，应该立即让你回到HTML结构上的第7张，下标为6；
    if (currentIndex == 0) {
      currentIndex = li_arr.length - 2;

      // 回到正确的位置
      var target = currentIndex * imgWidth * -1;
      ul.css('transform', 'translate(' + target + 'px)');

      // 但是过渡效果还在啊；去掉过渡
      ul.css('transition', 'transform 0ms');

      // 回到正确的位置后，还应该加上过渡
      setTimeout(function() {
        ul.css('transition', 'transform 300ms');
      }, 1);
    }

  });

```





# swiper 插件

## 介绍

- 插件：部分小功能的实现，比如轮播图；
- 中文官网 ：https://www.swiper.com.cn/
- 以后如果找一个插件，去到人家提供下载和demo的地方，先看看demo，是不是你想要的效果；如果确定了这就是你想要的效果，看**教程开始**学习

## 使用

- 下载

![](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/003.png)

![](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/004.png)

- 引入

```HTML
<link rel="stylesheet" href="./swiper/css/swiper.css">
<script src="./swiper/js/swiper.js"></script>

```

- 教程：按照官方教程一步一步来；根据自己的需求稍微修修改

![](E:/%E5%B0%B1%E4%B8%9A%E7%8F%AD/%E8%80%81%E5%B8%88%E8%B5%84%E6%96%99/webapi_day_005/05-%E9%A2%84%E4%B9%A0/01-%E8%B5%84%E6%96%99/assets/005.png)

```html
<!-- swiper插件需要的一个固定结构 -->
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <div class="swiper-slide">
        <a href="#">
          <img src="./images/1.jpg" alt="">
        </a>
      </div>
      <div class="swiper-slide">
        <a href="#">
          <img src="./images/2.jpg" alt="">
        </a>
      </div>
      <div class="swiper-slide">
        <a href="#">
          <img src="./images/3.jpg" alt="">
        </a>
      </div>
      <div class="swiper-slide">
        <a href="#">
          <img src="./images/4.jpg" alt="">
        </a>
      </div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
  </div>

```

- 根据文档的指示，调用一个方法

```javascript
var swiper = new Swiper('.swiper-container');

```

- 根据文档学习更多的功能：分页器、左右按钮、无缝滚动、自动播放；

```javascript
var swiper = new Swiper('.swiper-container',{
  // 动画持续时间，过渡的持续时间
  speed : 毫秒数,
  
  
  // 是否形成闭环，无缝滚动；
  loop:true,
    
  // 分页
  pagination : {
    // 分页器的选择器
    el : '.swiper-pagination'
  },
    
  // 左右按钮
  navigation: {
    // 按钮的选择器
    nextEl: '.swiper-button-next',
    prevEl: '.swiper-button-prev',
  },
  
  // 自动轮播
  //autoplay : true,// 按照默认的时间切换 , 默认是3000毫秒
  // 自定义自动轮播的时间
  autopaly : {
    delay : 毫秒
  }
});

```











