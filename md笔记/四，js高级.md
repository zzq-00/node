# js高级-01

## 1.面向对象

### 1.1 面向过程

- 分析问题需要的步骤
- 适用于小项目
- 优点：性能高，步骤紧密
- 缺点：不好维护，不易多次使用及扩展

### 1.2 面向对象

- 把事务看成一个对象（对象有方法和属性）
- 适用于大项目
- 优点：易维护，可复用，可扩展，灵活性高
- 缺点：性能没有面向过程高
- 特性
  - 封装性
  - 继承性
  - 多态性

## ES6的类和对象

- ECMAscript
- ES5：没有类  （构造函数）
- 类：泛指一类  汽车 人  树（放公共的方法属性）
- 对象：具体的某个实例  奔驰  姚明  柳树
  - 方法：(行为)做什么【执行】(动词) 打篮球【语法：对象.属性】
  - 属性：(特征)有什么【访问】(名词) 身高体重...【语法:对象.方法（）】

### 类 class

### 1.创建类

- 语法： class 类名 {放共有的属性和方法}
- 类名首字母必须大写

```js
    //定义：创建类
    class Dog {}
    //实例化 对象
    var obj = new Dog();
    //判断 obj 是不是对象类型
    console.log(obj instanceof Object);
```

### 2.类constructor构造函数

- 构造函数里放属性
- 构造函数 de this 是当前实例对象(new的对象)
- 每当new一个类，就会自动执行constructor构造函数
- class 类名 { constructor (形参){ this.属性名=属性值 } }

```js
class Dog {
    //属性：放到构造函数
constructor (name,age,sex){
    // 对象.属性
    //this：当前实例对象
    //this.属性名 =  属性值;
    this.name = name;  
    this.age = age; 
    this.sex = sex;             
    }
}
//每当new一个类，就会自动执行constructor构造函数
//实例化 对象
var obj = new Dog('毛豆',3,'男');
console.log(obj);
```

### 3.类--添加方法

```js
class Dog {
    //属性：构造函数
    constructor (name,age){
        this.name = name;  
        this.age = age;             
    }
    //方法：普通函数
    //sing:方法名
    sing(){
        console.log(this.name+'唱歌');                   
    }
    dance(){
        console.log(this.name+'跳舞');                    
    }
}
var obj = new Dog('毛豆',3);
console.log(obj);
// 调用方法(普通函数)
obj.sing();
obj.dance();
```

### 4.类的继承

- **extends**
- class Son `extends` Father {}

> **super()**
>
> 1. 调用构造函数 ，普通函数(方法)
> 2. 如果子类不写自己的属性和方法(只有与父类相同的属性和方法)，可以直接继承
> 3. 如果子类有自己的属性和方法，用super 调用父类

​	

```js
// 继承
class Father{
    constructor (name,sex){
        this.name = name;
        this.sex = sex;
    }
    hobby(){
        console.log(喜欢打篮球);      
    }
}
1.继承Father的属性（有相同的属性方法）
//class Son extends Father{}
2.里面不能直接写自己son的属性(this指向不同)
//用super调用相同的属性 ， 再写自己的属性
class Son  extends Father{ 
    constructor(name,sex,age){
        super(name,sex);
        this.age = age;
    }
    hobby(){
        super.hobby(); //继承父的方法
        console.log('踢足球'); //自己的方法     
    }
}
var  son = new Son('李','男','18');
```

### 5.注意点

1. 必须先定义类 --- 再实例化对象 (ES6中不用提升预解析)
2. 在类里面调用属性或方法： 【对象.属性 | 对象.方法】
3. 给元素添加处理程序时，调用方法不能带括号
4. this 构造函数：的this指向 当前实例化对象
       方法(普通函数)：的this 指向 是当前调用者

### 6.创建元素

- insertAdjacentHTML(position , text)
- position
  - 添加兄弟元素  beforebegin  afterbegin
  - 添加子元素 beforeend  afterend

# js-高级-02

## ES5

- **构造函数 必须与 `new`  一起使用**
  **构造函数`名` ====> 首字母大写**

## 构造函数与函数的区分

function fn () {} ------ fn();  -----函数
function Fn () {} ------ new Fn();   ------构造函数

## new 执行时

- 在内存中创建一个空对象
- 让this指向这个新的对象
- 执行函数代码，就有了属性和方法
- 返回这个新对象(所以构造函数里面不需要return)
- **new时 就执行constructor 构造函数**

## 静态成员,实例成员

- 静态成员：构造函数`身上`(外面)的成员，静态成员只能由构造函数访问
- 实例成员：构造函数`内部`(里面)的成员，静态成员只能由实例对象访问

```js
    function Fn (name,age){
        //实例成员
        this.name = name;
        this.age = age;
    }
    var  obj = new Fn('张三丰','22');
    //实例访问
    console.log(obj.name); 

    //静态成员
    Fn.sex =  '男';
    //静态访问
    console.log(Fn.sex);
```

## 1.创建对象的方法

- a. 字面量形式
- b. 构造函数
- c. 自定义构造函数
- 工厂模式

1. 字面量

```js
//1.字面量
    var obj = {
        name:'张三非',
        age:'22',
        hobby:function(){
            console.log(1);           
        }
    }
    //obj.name
    //obj['name']
    console.log(obj.hobby()); //1
    console.log( obj.hobby ); //方法
```

2. 构造函数创建对象   

```js
//2.构造函数创建对象
    var obj = new Object();
    obj.name = '李四';//点方式
    obj['age'] = 23;//
    obj.hobby = function () {
        console.log(2);       
    }
    console.log(obj);

//给元素添加事件 ====> 给元素添加方法
    btn.onclick = function () {
        console.log(3);       
    }
```

3. 自定义构造函数 --函数名首字母大写

```js
//3.自定义构造函数 --函数名首字母大写
    function Fn (name,age){
        this.name = name;
        this.age = age;
    }
    var  obj = new Fn('张三丰','22');
    var  obj1 = new Fn('李四','22')
    console.log(obj); //返回对象
    console.log(obj1);
```

## 2. 构造函数原型--prototype对象

- 多次实例化对象 浪费空间内存
- **所有的`属性`写在构造函数里放, `方法`放在 `原型对象prototype`上**
- prototype:原型对象 --- 是构造函数的一个属性
- 每个构造函数都有原型对象

```js
1.多个方法，(会覆盖-需指回构造函数)
 Fn.prototype = {
        constructor:Fn,
        hobby:function(){},
        sing:function(){},
        dance:function(){}
    }
```

![构造函数，原型对象，对象实例关系](E:\笔记\md笔记\构造函数，原型对象，对象实例关系.jpg)

> Star.prototype  相当于  ldh.__proto__
>
> Star.prototype.constructor   相当于   ldh.__proto__ .constructor   指回构造函数本身

## 3.对象原型 _proto_

- 作用 ： 指向prototype
- 只读属性（不设置,赋值）

```js
function Fn (name,age){
    this.name = name;
    this.age = age;
    this.hobby =function () {
        console.log(1);            
    }
}
//原型对象
Fn.prototype.hobby = function () {
        console.log(1);            
}
var  obj = new Fn('张三丰','22');


//prototype:原型对象 --- 是构造函数的一个属性
console.log(Fn.prototype); //对象
console.log(obj.__proto__);
```

> 构造函数Fn         ====>属性  ----->实例化对象new Fn
> 原型对象prototype  ====>方法
> 对象原型_proto_    ====>指向prototype

## 4. constructor

- constructor : **指回构造函数本身**
- constructor ：是原型对象上的一个属性

```js
console.log(obj.constructor);//构造函数
```

![原型链](E:\笔记\md笔记\原型链.jpg)

## 5. 原型链

- 作用：查找属性和方法的机制  直到找到为null

## 6.继承

- 组合继承：构造函数 + 原型对象

### a. 属性继承 call()

- call() : 改变this的指向
- 让子类里 -----  调用父类函数 . call(指向谁,参数)
- father.call(this,name,age)

### b. 方法继承

- 1.把父类的`实例对象` 赋值给  子类的 `原型对象`
  - Son.prototype  = new. Father()
- 2.会覆盖原来的
- 3.让子类的原型对象再指回原构造函数 Son.prototype.cunstructor = Son

### 内置对象扩展

Date()  Math()  Array()  String()

# ES5

- function Person () {}
- var person = new Person()

```js
var that ;
//1. 自定义构造函数
function Person(name,age) {
    that = this;
    this.name = name;
    this.age = age;
    // this.hobby = function () {
    //     console.log(this.name+'喜欢唱歌');            
    // }
    // this.insert = function () {
    //     console.log(this.name+'兴趣做饭');                
    // }
}
// Person.prototype.hobby = function () {
//     console.log(that.name+'喜欢唱歌');
// }
// Person.prototype.insert = function () {
//     console.log(that.name+'兴趣做饭'); 
// }
Person.prototype = {
    constructor:Person,//找到构造函数本身
    hobby:function(){ console.log(that.name+'喜欢唱歌');},
    insert : function(){ console.log(that.name+'兴趣做饭'); ; }
}

var person = new Person('何炅',33);
console.log(person);
// person.hobby();
Person.prototype.hobby();
console.log(Person.prototype);//构造函数都有原型对象
console.log(person.__proto__);//实例对象都有对象原型
console.log(person.__proto__.__proto__.__proto__);//null


//2. 继承 组合继承：属性继承 + 方法继承
function Star(name,age,sex) {
    //继承属性
  	//调用父 把父的this 指向当前this
    Person.call(this,name,age)
    this.sex = sex;
}
//继承方法
//将父的实例化对象 赋值==>  子的原型对象
Star.prototype = new Person();
Star.prototype.constructor = Star;

var star = new Star('谢娜',30,'女');
console.log(star);
Star.prototype.hobby();
console.log(Star.prototype);
```

# ES6

- class Person   { constructor (形参) {} }
- var person = new Person(实参)

```js
//创建类
class Person {
    constructor (name,age){
        this.name = name;
        this.age = age;
        this.hobby = function () {
            console.log(this.name+'喜欢唱歌');                    
        }
    }
}
Person.prototype.inster = function () {
    console.log(this.name+'喜欢主持');
}
// 实例化对象
var person = new Person('何炅',33);
console.log(person);
person.hobby();
// console.log(Person.prototype);        
person.inster();

// 继承
//1.直接继承
class Zhuchiren extends Person {};
var zcr = new Zhuchiren('杜海涛',28);
console.log(zcr);

//2.有自己的属性
class Star extends Person{
    constructor(name,age,sex){
        super(name,age);
        this.sex = sex;
    }
}
var star = new Star('谢娜',30,'女');
console.log(star);
```



# js高级-03

## 类的本质

- class 的本质还是function
- 类的方法都定义在prototype上

## ES5 中新增的方法

### 1. 数组方法

- js中 遍历--  for(){}
- jQ中遍历 -- each()
- ES5中遍历 -- forEach()   filter()  some()  map()  every()

1. 元素.forEach()
   作用：遍历
   **arr.forEach(function(item,i,arr) {} )**

- 第一个参数：当前项
- 第二个参数：当前 索引值
- 第三个参数：数组本身

2. 元素.filter()
   作用: 筛选满足条件的项 ----> 返回新数组(记得接收)
   **arr.filter(function(item,i,arr) { return item %2 == 0 } )**
3. 元素.some()
   作用：查找 某个值 是否在数组里 ---> 返回布尔值
   找到 就停止执行 (因为return 为true 停止 )
   **arr.some(function(item,i,arr) {return item == 10} )**

### 2. 字符串方法trim()

str.trim();
trim() : 删除字符串两边 的空白格

## 函数进阶

> 函数 先定义 在调用

### 1. 命名函数

- function fn (){} -------  fn()

### 2. 匿名函数

加括号--执行(调用)函数
不加括号--打印函数

- 2.1 定义变量
  - var fn = function(){}  ------  fn()//调用执行;
- 2.2 自调用函数
  - (function(形参){})(实参);

### 3. 实例化对象写法(忽略)

- var obj = function('a','b','consolie.log(a+b)')  -----  obj(10,20);

### 4. 函数调用方法

**this的指向:当前调用者**

- 1. 普通函数 -- fn(); 【】this指向-window
- 2. 对象的方法 --- 对象.方法名();【obj.faming = function(){}】this指向-调用者
- 3. 构造函数 --- new Fn();  【function Fn(){}】this指向-实例对象
- 4. 绑定事件函数 -- btn.onclick = function(){}; 【】this指向-事件源
- 5. 定时器函数 -- window.setInterval(function(){} ); 【】this指向-window
- 6. 立即执行函数 ( function(){} )(); 【】this指向-window

### 5. 改变函数内部this指向方法

**bind() call()  apply() 必须是函数调用.call() **

- 1. call()  **必须是函数调用.call()**

  - 1. fn.call(this指向,参数,参数)
  - 2. 一般用在继承

- 2. apply()

  - 1. fn.apply(this指向,数组)
  - 2. 第二个只能放数组 
  - 3. 一般用在与数组有关的地方

- 3. bind()

  - 1. fn.bind(this指向,参数)
  - 2. 不执行原函数(fn)  返回一个新函数(接收)

- 4. 区别

  - call()  apply() 会执行函数，并且改变this指向
  - bind()  不会调用函数 

### 6. JS的严格模式

之前写的都是正常模式

- 开启严格模式  "use strict";
  - 为脚本开启
  - 为函数开启
- 开启JS严格模式变化
  6.1 变量声明必须加var，不准删除变量
  6.2  在严格模式下，普通函数this指向 undefined(正常是window)
  6.3  在严格模式下，构造函数 new
  6.4 在严格模式下，函数 定义到顶层 
  6.5 在严格模式下，函数名不能重名

### 7. 高阶函数

- 把函数当做`参数传递`或当做`返回值` 返回的函数，叫做高阶函数
- 若函数没有return，则返回undefined
- return ：若函数return后没有值，则返回undefined
           若函数return后有值，这个值返回到调用的位置

```js
function fn (n){
    // n = m;
    console.log(n);//打印的是函数 function(){console.log(123)}
    n();//123
}
var m = function(){console.log(123);};
fn(m);
```

```js
若函数没有return，则返回undefined
return ：若函数return后没有值，则返回undefined
         若函数return后有值，这个值返回到调用的位置
function fn() {
    return 10;
}
var res =  fn(); //10
console.log(res);
```

```js

```

### 8. 闭包

- 作用：延长变量的作用范围
- 定义：指有权访问另一个作用域的局部变量
- 针对于-- 变量来说，有变量才有闭包
- 8.1 变量作用域
  - a. 当函数执行完毕后，作用域内的局部变量会销毁
- 8.2 闭包
  - 一个作用域去访问另一个函数内部的局部变量(作用域)

# js高级-04

## 1. 递归

- 找数据--用递归方法
- 函数自己调用自己,叫递归（无限调用执行，要设置停止）

```js
function fn(){ fn() }; fn();
```

- 递归函数必须要停(return)

```js
function fn(n){
    if(n == 0){
        return//3.结束，返回打印n
    }
    fn(n-1);//2.再调用函数，到结束，打印n
    document.write(n);
    }
    fn(3);//1.先调用函数
```

./递归图.jpg

### 2.递归案例

- 1-n的阶乘
- 1,1,2,3,5,8,13,21，....
- 杀羊

### 3. 递归遍历数据

- 案例：查找数组中数据

## 2. 拷贝

- 拷贝一般都是对象之间的拷贝（拷贝之后两对象修改互不影响）
- 拷贝不能赋值，对象是复杂类型，复杂类型赋值的是地址,
- 对象遍历用 for(var key in obj){}
- key是变量，代表对象的键(属性)

**   2.1 深拷贝**

```js
var obj = {name:'zzq',age:22,color:['red','blue','yellow']message:{sex:'女',score:100}}
var newobj = {};
function kaobei(newobj,obj){
    for(var key in obj){
        //判断呢我newobj里的属性是否是数组类型
        if( newobj[key] instanceof Array){
            newobj = [];
            kaoebi(newobj[key],obj[key])
        }else if (newobj[key] instanceof Object{
             newobj = {};
            kaoebi(newobj[key],obj[key])
        }else{
            newobj[key] = obj[key]; 
        }
    }
}
kaobei(newobj,obj)
```

**   2.2 浅拷贝**
    *   Object.assign(newobj,obj) ----ES6的方法
    *   只能拷贝外边一层的复杂对象类型

```js
将obj的每一项赋值给新的newobj对象，一个变，另一个不影响
var obj = {name:'zzq',age:22}
var newobj = {};
//newobj = obj;//不可以 这叫赋值，一个属性变另一个也变
for(var key in obj){
    newobj[key] = obj[key]; 
}
```

## 3. 正则表达式 / /

### 3.1 创建正则表达式

- 方式1

```js
var reg = new RegExp(/abc/);
console.log(reg); //  /abc/
```

- 方式2

```js
字面量方式
var reg =/abc/;
含义：只要有abc就行
console.log(reg); //  /abc/
```

### 3.2 测试正则表达式

- reg.test(用户输入的字符串)

```js
var reg =/abc/; //包含abc
reg.test("aaaaaa");  //false
reg.test('abababbc');  //false
reg.test("abcabcabc");  //true
console.log(reg); //  /abc/
```

### 3.3 正则表达式组成

简单字符 和 特殊字符【元字符】

- 特殊字符【元字符】：*^&$
- 查看正则表达式的地址：developer.

### 3. 4 边界符

- 正则表达式边界符

  - ^ 表示匹配行首的文本
  - $ 表示匹配行尾的文本

  ```js
  var reg = /abc/;  表示包含abc就行
  
  var reg = /^abc/; 表示以abc开头
  
  var reg = /abc$/; 表示以abc结尾
  
  var reg= /^abc$/; 表示只能是输入abc，精准
  
  var reg = /[abc]/; 表示包含 a 或 b 或 c 即可
  ```

### 3.5. 字符类

```
.1 方括号 [] : 表示括号里面的多选一，包含就行
.2 ^[abc]$  : 表只能是 a 或 b 或 c 中的一个
.3 [a-z] : 表示a到z的字母任选一个,包含就行a123
.4 [a-zA-Z] : 表示a到z，A到Z 的字母任选一个,包含就行
.5 [a-zA-Z0-9] : 表示a到z，A到Z  0到9 的字母或数字任选一个
.6 [a-zA-Z0-9_-] : 表示a到z，A到Z  0到9 下划线 连接线的字母或数字任选一个
.7 [^abc] ：取反，表示不能是他们之中的任意一个

```

### 3.6. 量词符

用来匹配次数的
    .1 * 表示重复0次或更多次 
    .2 + 表示重复1次或多次 
    .3 ? 表示0次或1次
    .4 {n} 表示重复n次
    .5 {n,} 表示重复n次或更多次
    .6 {n,m} 表示重复n到m次

```js
    var reg = /^[abc]*$/;

    var reg = /^[abc]+$/;

    var reg = /^[abc]?$/;

    var reg = /^[abc]{3}$/;
    var reg = /^[abc]{3,}$/;
    var reg = /^[abc]{3,6}$/;

```

### 3.7 案例

- 案例-用户表单验证

## 4. 总结括号

```
*   大括号{}  表示重复次数
*   中括号[]  表示量词符
*   小括号()  表示优先级
```

## 5. 预定义类

```
*   \d   [0-9]
*   \D   [^0-9]
*   \w   [a-zA-Z0-9_]
```

```js
var reg = /^[0-9]$/;
console.log(reg.test())
```

## 6. replace替换

作用：字符串替换 返回新字符串
先遇到谁，就替换谁
str.replace('被替换的','新的替换')

```js
var str = "aaaaaaa"
var newstr = str.replace('a','******');
console.log(newstr);

str.replace(/a|b/g,'******');//替换全局a b

```

- g : 全局
- i : 忽略大小写
- gi ：全局忽略大小写

### 案例

- 屏蔽敏感字符
      

​    

