# js--01-基本

- JavaScript:运行在浏览器端的脚本编程语言

- 作用:

  - HTNL 骨架 结构
  - CSS 样式 
  - JS  交互:给骨架设计一系列能响应的动作,能和用户交流互动

- 语法

  - 在script标签中写JS的代码

    ```js
    <script>
    	document.write("<div class="box">页面语义化</div>")  
    	documunt.getElementById("box")=function(){
        alter("点击弹出框")
    }  
    </script>
    ```

- 引入方式

  - 内嵌式<script></script>
  - 外链式<link rel="" src="./jx/1.js" />
  - 行内

- 输入框

  - prompt("请输入您的密码");
  - 输入:对于用户要输入括号的里要写的信息.要用单(双)引号

- 弹出框:

  - alert("弹出框");
  - 输出:告诉用户的信息

- 控制台console

  - console.log("控制台输出的信息")

- 变量

```javaScript
/*声明变量 变量名称 赋值*/
var num_1=30;
var num_2=20;
//console.log(num_1+num_2); //50
//console.log(num_1,num_2); //30 20
```

```js
/*接受用户输入的信息*/
var a = Number(prompt("输入基本工资"))
//alter(a);
console.log(a);
```

```js
//声明变量
var a;
//给变量赋值
a = 10;
//修改变量的值
a = 20;
//弹出的a为改变后得值 20;
console.log(a);
```

```js
//运算顺序
[] ()
++ -- !
* / % +  -
> >=  < <=  
==  ===   !=   !==
&&
||
=  += -= *= /= %=
var a = 200 ==== (10+10)*10>1
a = 200 === 20*10>1
a = 200 === 200 >1
a = 200 === true
false
```

```js
//变量的运算
//把左边的 赋值给 右边的变量
var a = 10;
++a;//11
a++;//11
a = a + 1;//11
b=a++ + 1;//11
b=++a + 1;//12

```

```js
//1.可以同时声明多个变量
var a,b,c.d;
//2.可以声明多个变量并赋值
var a=1,b=2,
    c=3,d=4;
//3.将a的值 赋值给 变量b
var a=10;
var b=a;
```

- 变量命名规范
  - 范围:字母,数字 ,下划线 , $符号
  - 不能以数字开头   错误提示...token无效的标识
  - 关键字,保留字不能用
  - 区分大小写
  - 驼峰命名法userName,get_Date

## 基本数据类型

- 数字(Number)类型

  - NaN(not a number):不是某个数,泛指
  - var a = 10;

- 字符串(String)类型

  - 字符串**必须加单(双)引号** [ 否则会被看成变量 ]
  - var a="b";

- 布尔(boolean)类型

  - 语法:表示某个结果,存在(true)或不存在(false)

  ```js
  var a = 5<4; //[先比较,再赋值]
  console.log(a);//false
  ```

- Null值

  - 表示尚未存在的对象,复杂类型

- Undefined

  - 一个没有赋值变量,默认值为undefined

  ```js
  var a;
  console.log{a);
  ```

* 查看数据类型

```js
var a = 10;
console.log(typeof a);  //number

var a="abd";
console.log(a,typeof a); //string

var a = 5>4;
vonsole.log(a,typeof a); //true  

var a = NaN;
console.log(a);  //Number

var a = null
console.log(a,typeof);   //null
            
var a ;
console.log(a,typeof);   //Undefined
```

### 其他   转   数字 类型

**结果:数字或NaN**

- Number()

```js
var jx = prompt("请输入绩效工资"); //1000
var jb = 3000;
//string类型遇到 + , 把其他类型转化为string类型,形成字符串拼接
//console.log( jx +jb); //100030000
console.log( Number(jx) + jb ); //4000
```

- parseInt()
  - 整型
  - boolean类型, Null类型 , undefined类型都转换为NaN
  - 字符串类型特殊,如下

```js
//字符串转整型 只有前面是数字,才能转换出整数
var a = "1000abc"
var result = parseInt(a);
console.log(a,result); //1000abc, 1000

//字符串转整型 .前面不是数字,转成NaN
var a = "abc1000"
var result = parseInt(a);
console.log(a,result); //abc1000, NaN
```

- parseFloat()
  - 浮点数

### 转字符串类型

- String()

- Number类型 , boolean类型 , Null类型 , Undefined类型   都可以转成字符串类型

- .toString();

  - null 和undefined 不能用toString转

  ```js
  var a = 10;
  var res = a.toString();
  console.log(a,res,typeof res); //10 "10" "string"
  
  ```

### 转boolean类型

变量值为 0,NaN , null , undefined .结果为false

## 操作符

算术运算符 比较运算符  逻辑运算符  赋值运算发

- 算数操作符

```js
//1.字符串左右两边遇到+ .会拼接,为字符串类型
var a = 10 + "10";
console.log(a,typeof a)//1010 string

var a = 10 + 10 +"10";
console.log(a,typeof a);//2010

//2.字符串除了遇到 + ,会拼接为字符串,其他 - * / % 都会 隐式 转化为数据类型
var a = 10 - "5";
console.log(a,typeof a);//5 number
var a = 10 - "你我他";
console.log(a);//NaN

//3.其他 true null undefined类型,也都会隐式转换
var a = true + 10;
console.log(a);//11

var a = null + 10;
console.log(a);//10`

```

- 自增++    自减- -

  在自己的基础上

  - ++在变量前, 先算++ ,再算整个式子
  - ++在变量后,先算整个式子,再++

- 比较运算法

  - <  >   >=  <=
  - 非常规操作 : 非number类型 和 number类型比较,非number类型隐式转化为数据类型
  - == 比较数据类型是否相同,不同则因性转化为Number类型,相同比值大小
  - === 比较左右两边类型相同的,如果不同就是falsle
  - !=
  - !==

- 逻辑运算符

  - && 且     ||或      ! 取反  

- 赋值运算法

  - +=    - =   *=  /=

  ```js
  var a = 10;
  a += 2;   (a=a+2)
  
  var a = "abc";
  a += 2; (a = "abc" + 2;)
  
  ```

- 运算优先级

  ```
  [] ()
  ++ -- !
  * / %
  + -
  > >=  < <=  
  ==  ===   !=   !==
  &&
  ||
  =  += -= *= /= %=
  
  ```

# js-02-循环

### 流程控制

- 表达式:有返回结果,布尔值
- 语句:
- 结构 :
  - 顺序结构:默认代码从上到下顺讯执
  - 分支结构:不同情况走不同分支
  - 循环结构 : 有重复的思想

#### 分支结构

- if-else结构

  ```js
  //单分支
  if(判断表达式){
     执行代码
  }
  //2个分支
  if(条件表达式){
     当条件表达式为true时,执行
  }else{
      当条件表达式为tfalse时,执行
  }
  
  //多分支
  if(条件表达式1){
     当条件表达式1为true时,执行此代码
  }
  else if(条件表达式2){
     当条件表达式2为true时,执行此代码     
  }
  else if(条件表达式3){
       当条件表达式3为true时,执行此代码   
  }
  else{
      都不满足条件表达式,执行此代码
  }
  ```

  - 案例:求输入的两个数的最大值

    ```js
    var a = Number(prompt("请输入数字"));
    var b = Number(prompt('请输入数字'));
    if(a < b){
        console.log("最大值是" + b);
    }else{
        console.log("最大值是" + a);
    }
    ```

- switch-case结构

```js
//语法  变量与多个固定值进行
var d = d.getWeek()
switch(d){
case "星期一"
   //d === "星期一"
   break
case  "星期一"
   break
case "星期一"
   break
default "周末"
   break
}
```

- 三元表达式

  表达式1  ?  表达式2  :   表达式3;

> 求最大值

#### 循环结构

```js
while(条件表达式){
    循环体
}
//先执行条件表达式
//表达式为false,循环结束. 
//表达式为true,执行循环体
```

```js
for(初始化表达式;条件表达式;自增表达式){
    循环体
}
执行初始化表达式
执行条件表达式
若条件表达式为false,退出当前for循环
若条件表达式为true,执行循环体,执行自增表达式
```

```js
do{
    循环体
}while(条件表达式)
先执行循环体
执行条件表达式
若条件表达式 为false,结束循环
若条件表达式 为true,执行循环体
```

```js
var i=1;
while(i<=6){
    console.log('现在到'+i+'楼了');
    if(i===3){
    	console.log("3楼到了");
        break;
    }
    i++;
}
```

案例

```js
//打印1-5,再求和
var a=1;
var sum=0;
while(a<=5){
    console.log(a);
    sum=sum + a;  //sum += a;
    a++;
}
console.log(sum);

//1-100之间的所有偶数,打印出来
//将1-100个数一个一个过(循环)
//在判断当前这个数是否为偶数,偶数判断方法(判断 i % 2 === 0;`比较===`)
var a=1;
while(a<=100){
    if( a%2 === 0){
       console.log(a);
  	}
    a++;
}
```

```js
//1-10偶数的和
var sum=0;
for(var a=1;a<=10;a++){
    if(a%2===0){
        sum=sum+a;      
    }
}
consolre.log(sum);

//10行10列的圆

```

### break 和continue

```js
// break 
/* 电梯一共有6层，现在我们要上电梯，我们的教室在3楼，电梯只要到3楼就可以了。*/
for(var i = 1; i <= 6 ; i++ ){
    console.log('现在是'+i+'楼');
    if(i == 3){
        console.log('3楼到了，电梯停了，请下电梯。');
        // 程序 执行到 3，执行了四次就结束了；
        break;
    }
}

// continue
// 电梯一共有6层，除了3楼没人下去，其他楼层都有人下去(3楼不停，其他楼层都要停)
for(var i = 1; i <= 6; i++){
    if(i == 3){
        // 执行到 3 时。当前次的程序后面的全部跳过；继续执行后面的次数；
        continiue;
    }
    console.log(i+'楼到了，电梯停了，请下电梯。');      
}

```

### 注意

总结：这个地方只是用for做终止

- break用于结束整个循环
- continue用于结束整个循环中的一次，**结束当前这次循环**；
- break和continue**后面的代码都不会执行**，执行前面的代码；

if(){}如果表达式为false则返回上一级

break代表结束上一个for循环回到最上层

continue代表跳这次循环

# js-day-03-数组

### 复习

```js
//输出1-100的质数
//只有1和它本身
//1-100的每一个数都过一次
//让每个数去除他以下得数到2就可以了(因为除以1的任何书都是本身,排除)
//如除以所以数的余数不为0,则是质数
for(var i=1;i<=100;<i++){
    for(var j=2;j<i;j++){
        if(i%j==0){
            if(i==j){
                console.log{""}
            }else{
                break;
            }
        }
    }    
}

var is_zhishu;
for(var i=1;i<=100;<i++){
    is_zhishu= true;
    for(var j=2;j<i;j++){
        if(i % j != 0){
        	is_zhishu=false;
            break
        }
    }
    if(is_zhishu) {
        console.log(i+"是素数");
    }
}
```

## 数组

**有顺序,有长度得数据集合**

### **1.声明**

```js
// 字面量的形式 从字面能看出数据的类型 空数组
var arr = [ ];
console.log(arr); //Array[];"Object" 字符串类型 空数组

//2.构造函数
var arr =  new Array();
```

### **2.存值**

- 数组中的数据使用索引管理.索引从0开始
- 索引:下标
- 数据中的元素可以使任意类型

```js
arr[0]='学号";
arr[1]='166715';
arr[2]="成绩";
arr[3]=98;
/// arr["学号","166715","成绩",98]
```

### **3.取值**

- console.log(arr[3]); 3是下标,代表第四个数

### **4.遍历**

把数组的每一项都拿出来(循环)

```js
//1.遍历输出每一个数
//循环:用下标
for(var i=0;i<arr.length;i++){
    console.log(i);//i代表数组的下标
    console.log(arr[i]);
}
//2.数组求和
var sum=0;
for(var i=0;i<arr.length;i++){
    //console.log(arr[i]);
     sum = sum + arr[i]; //sum += arr[i];注意数组元素的数据类型.若有字符串,则是拼接,若都是数字,才相加.
}
console.log(sum);

//arr.length 数组长度
```

arr.length 数组长度

清空数组  arr.length = 0;

### **5 .构造函数**

```js
var arr = arr[10]//代表数组里的项,是90  声明变量
var arr = new Array(10);//长度为10的空数组
```

### **6. 案例----小娜介绍**

> 转义字符  
>
> - \n  换行
>
> prompt(); 输出的一定是字符串形式

### **7.把字符串 转成 数组的方法**

- **str.split(指定的分隔符) 分隔**字符串,括号里是要转的符号

  ```js
  var str = prompt("请输入数字,必须用',"隔开);
  console.log(str,typeof str)//91,92,88  string
  //把接收到的字符串str,转换成数组
  var arr = str.split(",");
  console.log(arr typeof arr);//91,92,88  Array["91","92","88"]  也是字符串形式
  ```

### **8.获取时间**

**var date =new Date();  时间对象**

- 获取年份   date.getFullYear();
- 获取月份    date.getMonth();    
- 获取日期    date.getDate();
- 获取星期    date.getDay();
- 获取时        date.getHours();
-  获取分       date.getMinutes()
- h获取秒      date.getSeconds();

```js
var date = new Date();
var year = date.getFullYear(); 
console.log(year);
var month = date.getMonth();//月份从0-11
if(month<10){
    month = month+1;
    month = "0" + month;
}
console.log(month);
alert(`${year}-${month}-${riqi} ${hour}:${Minute}:${Second}`)
```

### **9.随机获取**

Math.random();

- Math 内置对象
- random  随机返回一个[ 0 , 1)的小数

```js
var a =Math.random();
//获取0-5的数(乘以倍数)
a = a * 5;
```

> 向下取整(给变量a向下取整)
>
> Math.floor(a);
>
> 向上取整
>
> Math.ceil();

```js
var a = Math.random();
a =  a * 5;
//向下取整
a = Math.floor(a);
alert(a);
```

## 案例

```js
while(true){
    var info =prompt("你好,我是小娜 \n 计算数字求和 请输入1 \n 显示系统时间,请输入2 \n 想听笑话,请输入3 \n 退出请输入q")
    
    if(info == "q"){
        alert("确定要退出嘛");
        break;
    }else if(info == "1"){
        //将输入的数据存储到变量str里
         var str = prompt("请输入数字,以引文逗号','隔开")
         //将 数据 转成 数组
         var arr = str.slipt(",");
        //求和,循环遍历数组的每一项,再加到变量sum上(要将字符串转换成数据才能相加)
        var sum =0;
        for(var i=0;i<arr.length; i++){
            sum = sum + paseFloat(arr[i]);
        }
        console.log(sum);
        alert("求得的总和是:"+ sum);
    }else if(info == "2"){
        var date = new Date();
        var year = date.getFullYear();
        var montn = date.getMonth();
        month += 1;
        if(month<10){
            month = "0" + month;
        }
        var day =date.getDate()
        if(day<10){
            day="0" + day
        } 
        var week = date.Day()
       	alert("系统时间" + `${year}-${month}-${day} ${week}`);
    }else if(info == "3"){
         var arr = ["笑话1-----------",
          "笑话2-------------",
          "笑话3-------------",
          "笑话4-------------",
          "笑话5-------------",
          "笑话6--------------"]
         var a = Math.random();//随机取得是[0,1)的小数
        	a = a * arr.length;//要去数组里0-5的数组项,则乘以他的倍数
        	a = Math.floor(a);//因为数组下标是整数,所以取整
        alert(arr[a]);//弹出
    }
}
```

## 总结

1,数组:有顺序,有长度得数据集合

2.声明  

- 字面量 var arr = [ ];
- 构造函数 var arr = new Array();

3.存值: 可存储任意数据类型

4.遍历

- 遍历数组每一项 (通过数组下标 从0开始)
- for(var i=0;i<arr.length;i++){ console.log(arr[ i ]); }

5.转数组的方法

-  分隔字符串  var str = str.split(",");

6.获取时间

- var date = new Date();
- var year =date.getFullYear();
- 显示时间格式方法 : alert( ` ${year}-${month}-${day} `);

7.获取随机小数 [ 0 , 1 )

- var a  = Math.random();
- 倍数  a = a * 5 ;
- 向下取整  a = Math.frool(a);
- 向上取整  a = Math.ceil(a);

**注意:prompt()  中输入的数默认 字符串形式  **

# js-day-04-函数

### 复习

1.数组:

字面量:var arr = [ ];

构造函数:var arr =new Array[ ];

2.arr.length  数组长度

3.遍历循环数组for( var i=0;i<arr.length;i++){ console.log( arr[ i ] ); }

4.求数组最大值,求最大值的下标

5.var str = prompt(" ") 输出的一定是字符串

6.字符串分隔,转数组

​	var arr=str.split(制定分隔的符号)

7.获取时间

​	时间对象 var date = new Date();

​	var month = date.getMonth() + 1; // 0-11

​	if(month<10){ month = "0" +month }//判断月份小于0,前面加个0

8.获取随机小数[ 0, 1)

​	var a = Math.random();

​	a = a * 5 //倍数

​	a = Math.floor(a); //向下取整

​	a = Math.ceil; //向上取整

## 函数

作用:有公共思想的部分,封装起来

function 函数名() {  };

函数名();

### 1.语法-调用

```javascript 
//1.声明函数
//关键字  函数名
function tell_Story(){
    //函数体,封装的代码
}


//2.调用函数,随时随地都可以调用
//直接调用 函数名();
tell_Story();
```

- **注意 函数名不可以重名,会被覆盖**

### 2.参数配置

参数 : 函数内部的变量

function  tell_Story( a , b ) {  };

tell_Story("熊大" , "熊二")

参数:

- 形参 :  函数名括号里的变量  ,函数内部声明的变量
- 实参  :  调用函数时, 给的确切值,实际参与运算的
- 实参与形参之间相互不影响,,但实参必须是简单数据类型

```js
//形参  a b
function tell_Story( a , b){
    //如果调用函数时,没有传入参数,则判断一下
    //三元表达式 a == undefined ? "大和尚" : a
    //三元表达式 b == undefined ? "小和尚" : b
    if(a == undefined) {
        a="大和尚"
    }else{
        a = a
    }
    console.log(a + "对" + b + "说:早上好");
}

//调用
//实参  "熊大" "熊二"
tell_Story("熊大" , "熊二")

//不传入实参(赋值),默认值为Undefined
tell_Story(); // Undefined 对 Undefined 说
```

### 3.函数返回值

return 

- 只能返回一个值
- 终止函数执行
- 求:n-m的和.平均值

```js
//返回值
function qiuhe(a, b) {
    var sum =a + b;
    return sum; //返回值
}
var he = qiuhe (20,35);
conlose.log(he);// 55


//终止函数执行
function zhongzhi(){
    console.log(1);
    console.log(2);
    return;//终止后面的函数执行
    console.log(3);
    consolr.log(4);
}
zhongzhi(); //输出 1 2  后面的不执行

```

### 4. arguments

- 函数内部的隐藏变量 

  - function fn() { console.log(argument); }
  - 调用 fn(12, 63 , "abc" , 76)

- 适合多个参数

  作用:可以输出多个没有明确的参数, 看起来像数组,叫伪数组

- 有顺序, 有长度 ,可以遍历for

- arguments.length  长度,有下标

```js
function fn() {
      console.log(arguments); //打印arguments
    
      var sum = 0;
      for (var i = 0; i < arguments.length; i++) {
        sum = sum + arguments[i];
      }
      return sum; // 返回arguments 的和
    }

    var sum = fn(91, 87, 56);
    console.log(sum);//
```

### 5.函数表达式

一种声明方式

```js
var fn =  function () { 
	函数体
} //function fn ( ) { 函数体 };
```

匿名函数 , 不能单独使用,需配合其它方式使用

### 6.回调函数

- 函数也是数据类型
- 可以把函数作为其他函数的实参传进去

### 7.作用域

变量  函数生效的范围 作用范围

- 全部作用域(变量) :  在外部声明
- 局部作用域  :  函数内部声明的变量,只能在函数内部生效

### 预解析

会把 声明的变量 提升到当前作用域最顶端;

```js
//说出执行结果
var num = 10;
fun();
console.log(num);

function fun() {
    console.log (num);
    var num = 20;
}

//////-------------------------
```

解析:  var num;

function fun() {

​	var num ;

​	console.log (num); 

 	num = 20;

}

num = 10;

//fun ( )

console.log(num);   

/////  undefined   10 

# js-05-对象

### 复习

1.函数

- 语法 function  get_time() {  }
- 调用 get_time()'
- 配置参数:函数内部的变量    形参  实参
  - 实参的变量可以  传给  形参   
  - 实参与形参互不相关
- 函数返回值(可以让外部接受[函数属性局部范围])
  - return   sum
  - return  也可以结束函数
- 作用域
  - 全局作用域
  - 局部作用域(变量)
- argument
  - 函数内部的隐藏变量 , 叫 伪数组
  - 适合于有不确定有多个参数的, 
  - argument.length  长度
  - 可遍历 for( var a =0; a<argument.length; a++){ console.log(argument[a]);}    a表示小标
- 预解析
  - 把声明变量  函数 function (){}   提升到  当前作用域的顶端 
  - 全局变量可以在任何地方访问
  - 局部变量只能在局部访问,外部访问不了(除非在函数里设置函数返回值)

## 函数对象

​	对象:一个有属性有方法的集合

### 1.语法

```js
//声明
//1.字面量
//var arr = [ ]; //数组
var object = { }

//2.构造函数
//var arr = new Array();//数组
var obj =new Objet();
```

### 2.添加

- 1.添加一个属性
- 2.添加一个方法名

```js
//1.声明
var obj = {};
//2.对象.属性  属性值
obj.name= "张三";//点方式
obj["name"]= "张三";//键值对
//2对象.方法名 
obj.sayname = function () {  };
obj["sayname"] = function () {  };

//3.调用方法
obj.name; //调用属性
obj.sayname();//调用方法
obj["sayname"]();

//声明对象时,设置属性和方法,必须用逗号隔开
var obj = {
	name:"张三",
  age : 12,
	sayName : function (){
    	console.log(obj.name);
	}
}
obj.sayName();//调用方法

//键值对  属性名必须是字符串 
var obj_1 = {}
obj_1["name"] = "张三"; 
obj_1["sayName"]=function(){ };
```

### 3.遍历

for( var key  in  obj )  { console.log(obj[key];)  }

key : 是键 不是值

```js
//在遍历内部,点的方式,会把obj当做属性名取获取
//需要通过键值对的方式获取
for( var key  in  obj {
    console.log( obj[key];)
}
```

###  4.  Math获取n-m的随机整数

```js
  //n-m的随机小数
    var get_Random = function(n, m) {
      //   var a = Math.random();
      //   a = a * (m - n + 1);
      //   a = Math.floor(a);
      //   a = a + n;
      var a = Math.floor(Math.random() * (m - n + 1)) + n; //简写
      return a; //返回值
    }
    alert(get_Random(10, 20));//调用 弹出
```

### 5. 数组的拼接(添加新数组)

var arr= [1 , 2 , 3 ,4]

arr  =  arr.concat([5 , 6] ,"abc" ,  [65 ,99])

###  6.简单数据,复杂数据

* 内存上有两个空间 一个栈, 一个堆,存储数据

* 栈 : 存简单数据类型

* 堆 : 存复杂数据类型  , 复制的是地址,将之前的变量也改变了

  ```js
  //简单数据
  var a = 10;  //存在栈上
  var b = a;
  b =b + a;
  console.log(a,b); //10 20 
  //复杂数据类型
  var c = { }; //存在堆上
  
  ```

  

### 案例

```js
<script>
    //声明对象
    var na = {};

    //1.字符串转数组 求和
    na.get_sum = function(num) {
      var arr = num.split(",");
      var sum = 0;
      for (var i = 0; i < arr.length; i++) {
        sum += parseFloat(arr[i]);
      }
      return sum;
    }

    //2.获取系统时间
    na.get_time = function() {
        var date = new Date();
        var year = date.getFullYear();
        var month = date.getMonth() + 1;
        month = na.lt_0(month);
        var day = date.getDate()
        day = na.lt_0(day);
        var week = date.getDay();
        return `${year}-${month}-${day} ${week}`
      }
      //小于10,前面加0
    na.lt_0 = function(a) {
      if (a < 10) {
        a = "0" + a;
      }
      return a;
    }

    //3.笑话数组
    na.joke = [] //空数组 ,可添加
      //随机下标
    na.Random_index = function() {
        var num = Math.random();
        num = num * na.joke.length;
        num = Math.floor(num);
        return num;
      }
      //添加笑话
    na.add_joke = function(user_joke) {
      na.joke = na.joke.concat(user_joke);
    }
//console.log(na); 

 while (true) {
      var info = prompt("你好小娜 \n q退出 \n 1求和 \n 2显示系统时间  \n 3 输入随机笑话")
      if (info == "q") {
        break
      } else if (info == "1") {
        var num = prompt("请输入数字,以英文逗号隔开','");
        alert(na.get_sum(num));
      } else if (info == "2") {
        alert("系统时间" + na.get_time());
      } else if (info == "3") {
        var user_joke = na.add_joke(prompt("输入你的笑话"));
        var index = na.Random_index();
        alert(na.joke[index]);
      } else {
        alert("输入有误,请重新输入");
      }
    }
  </script>
```



# js-06-内置对象

###  Math

```js
var a = -3.54
//随机小数[0 ,1)
Math.random();
//向下取整
Math.floor(a);
//向上取整
Math.ceil(a);
//四舍五入
 Math.round( a );
//求绝对值
Math.abs(a);
//求多个数的最大值(最小值min)
var a =Math.max(2,4,7,10,9);
console.log(a);

//
```

案例:页面随机颜色

```js
function get_Random(){
	var a = Math.random();
    a = a *256;
    a = Math.floor(a);
    retrun a;
}
function get_rgb(){
    var r = get_Random();
    var g = get_Random();
    var b = get_Random();
    var color = `rgb(${r},${g},${b})`;
    return color;
}
//document.write( `<div style="height:50px;background:${get_rgb()}"></div>` )
document.onclick = function (){
    var color = get_rgb();
    document.div.style.backgroundColor = color;
}
```

### Data

时间间隔  时间戳

- **场景:要求显示绝对唯一的数值**
- Math.random() *  Date . now();

```js
var date = new Date();
//毫秒数(从--到现在的总毫秒数)
vsr a = date.valueOf();
date.getTime();
1*date
Date.now()
```

### Array

也是个对象类型

#### concat 数组拼接

- .concat([4,5,6]);拼接  返回新数组,原数组不变

#### slice 数组截取

- slice : 截取数组  返回新数组 ,原数组不变

  - arr.slice( 开始的下标(包括), 结束的下标(不包括) )

  ```js
  var arr = ["a","b","c","d","e"]
  开始的下标(包括), 结束的下标(不包括)
  var res = arr.slice(1,3) // b c
  colsole.log(res , arr);
  ```

#### splice 数组增删改

- splice 用于从数组的指定位置移除,添加,替换元素

  - arr.splice(开始的下标 , 要移除的个数)  **返回被删得数**
  - arr.splice(开始的下标 , 要移除的个数 , 添加的元素  , ) 

  ```js
  var arr = [1,2,3,4,5]
  arr = arr.splice(2,3)
  arr = arr.splice(1,0,,6,7,"abc")
  ```

#### 字符串转数组

- arr.split( " , ")

#### 数组转字符串

- arr.join(" , ")

- push 把一个或多个元素从数组后面添加
- unshift 从前面添加元素
- pop 从后面删除一个元素
- shift  从前面删除一个元素

```js
var  arr = [1,2,3,4,5]
//从数组后面添加一个或多个元素
var arr = arr.push(6,"abc",8);//返回数组长度
//从后面删除一个元素
var arr = arr.pop(); //返回被删除的元素
//从数组前面添加一个或多个元素
var arr = arr.unshift();//返回数组长度
//从前面删除一个元素
var arr = arr.shift();//返回被删除的元素
console.log(arr)
```

#### indexOf( )

- 查找元素 在数组内的下标

  ```js
  //找到返回下标,找不到返回-1
  var arr = [10,20,30,6,"abc"]
  var res = arr.indexOf(30)
  console.log(res); //2
  ```

#### findIndex(function(){})

- 查找数组满足条件的元素

  ```js
  var arr = [10,20,30,6,"abc"]
  var res = arr.findIndex(function(itme){
      return item >10
  })
  console.log(res);//
  ```

####  forEach()

- 遍历数组forEach()

  ```js
  var arr = [10,20,30,6,55]
  var sum = 0;
  var res = arr.forEach(function(itme,index , arr){
      console.log(itme,index , arr)
      sum += item;
  })
  console.log(res);
  ```

  #### filter( )

  - arr.filter( )   过滤数组满足条件的元素

  ```js
  var res = arr.filter( function(item, index ,arr){
      retume item > 10;
  })
  console.log(res)
  ```

  **伪数组 argument.forEach 没有forEach循环**

  #### 数组的复制

```js
var arr = ["a","b","c","d"]
var new_arr = [];
arr.forEach(function(item,index){
   new_arr.push(item);
})
arr.fiter(function(item,index,arr){
    //满足条件的元素要返回
    return arr.indexOf(item) != -1;
})
arr.concat();
arr.slice();
```

#### 对象的复制

```js
var obj = {name:"zz",age: 18,sex:"女"}
var new_obj = {}
for (var key in obj){
    new_obj[key]= obj[key];
}
```

### 字符串

1.不可变

2.查找 indexOf()

- 字符串中是否存在指定字符 存在就返回找到的下标，没有就-1

3.substring 截取字符串,不操作原字符串；返回截取出来的字符串；

 

## 总结

字符串
数组
对象

### 字符串

1.不可变  var a ="abc";  a =a + "123456";
 字符串 拼接 或 重新赋值  ,之前的字符串不是被覆盖,而是在内存中处于游离状态[占内存空间]
 所以要避免在原字符串之间的拼接,利于性能优化

2. 返回新字符串,对原字符串没有影响
   2.1  str.concat()  拼接字符串  数组
   2.2  str. substring()  截取通过下标    substring(开始下标包括 , 结束下标 不包括)
   2.3  str. substr() 截取通过下标  substr( 开始下标 , 截取个数)
   2.4  str. slice()  截取通过下标 与substring()同理, 
    slice 可以为负值,把负值和长度进行相加
   2.5  字符串 转数组   str.split("指定分隔符")
3. 查找字符
   3.1   str . indexOf("我们") 通过查字符  返回下标
   3.2   chatAt(0)   通过查下标  返回字符



### 字符串 与 数组 互转 

1. 字符串 转 数组  
   var arr = str . split("指定分隔的符号");
    	场景 :  地址解析  将字符串  转成 对象
   2. 数组 转 字符串   
      var str = arr.join("指定分隔符");



### 数组 

 arr = [ ]
1.数组也是个对象类型

2.返回新字符串,对原字符串没有影响
	2.1  arr . concat()  拼接字符串  数组
	2.2  arr . slice()  截取通过下标    slice( 开始下标(包括)  ,  结束下标(不包括) );

3.原元素数组上修改
    3.1  arr . splice()    arr.splice(开始的下标 , 要移除的个数 , 添加的元素  , )
		返回被删的元素 arr.splice(2 , 2 , "abc" , 7 , 8) 
    3.2  arr . push(1,2,"abc" )   从数组后面添加一个或多个元素 ,返回数组长度
    3.3  arr . unshift( 0,1,2)  从数组前面添加一个或多个元素 ,返回数组长度
    3.4  arr . pop()  从后面删除一个元素  返回被删除的元素
    3.5  arr . shift()  从前面删除一个元素  返回被删除的元素

4.查找元素
    4.1  arr . indexOf( )  查找元素  返回下标
    4.2  arr . findIndex( function( item ){ return item>10; } )  查找数组中满足条件的元素
    4.3  arr . filter( function( item , index ){ return item>10; } )  过滤数组中满足条件的元素

5.数组的遍历
	5.1  for( var i=0;i<arr.length; i++) { } 通过下标,得到数组项
        5.2  forEach( function( item , index ,arr){ sum += item; } )  

6.数组的复制
	声明一个数组－声明一个新的空数组
	6.1  遍历数组 forEach－推进 - 将 new_arr.push( item );
	6.2  过滤数组 filter()  - 满足条件 返回 return  arr.indexOf( item ) != -1;
	6.3  拼接数组  var new_arr = arr.concat(); 不传入参数,返回所有数
	6.4  截取数组 var new_arr = arr.slice(); 不传入参数 表截取所有

### 对象 

var obj = { } ;

1. 对象的复制
   1.1  遍历 对象  
   for (var key  in obj_1) {
     obj_2[key] = obj_1[key];
   }

​	



