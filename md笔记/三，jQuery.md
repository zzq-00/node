注意:通过js阻止a标签跳转

```js
<a href="javascript: ;"></a>
a.onclick = function(){
  return false;
}
```



# jQuery-01

本质:将js中用来操作页面中元素的属性,方法,事件,动画....封装成了一个js文件(js库).

1. jQuery 优点
   1. 让代码更高效
   2. 链式编程,
   3. 隐式迭代(遍历元素)

## jQuery操作页面的元素

1.先要引入jQuery文件(js文件)
2.下载: https://jquery.com
	production  jQuery v3.4.1(压缩模式)
	develpment  jQuery v3.4.1(开发)
3.在网页中引入jQuery文件

## jQuery写法

### JS页面加载写法

1.如果用原声js操作页面中的元素, 若将原声的js代码写到页面元素前,不能操作,需要加上

```js
window . onload = function(){  操作代码 }
```

### 1.jQuery页面加载写法

1.使用jQuery操作页面元素, 若将jQuery放在html代码前 , 不能操作页面,若想操作需要加以下方式

```js
//第一种方式
$(document).ready(function(){
    $('div').hide();
})
//第二种方式
$(function(){ 
    操作的代码
    $('div').hide();
})
```

### 2.$ 介绍 

1. $ 其实是jQuery的别名
2. $ 是jQuery中的顶级对象

### 3.dom对象和jQuery对象

1. 通过**jQuery方式**获取的元素,那么得到就是jQuery对象, 都是**伪数组**的形式

2. 通过**js方式**获取的元素,获取的是**dom对象**

   ```js
    window.onload = function() {
       //   var div = document.querySelector('div')
       //   div.style.display = 'none';
       console.log(div); //DOM节点
       console.dir(div); //打印的是div对象
   
     }
   $(function() {
       var div = $('div');
       console.dir(div); //是伪数组的形式保存的对象
     })
   ```

3. 总结
   jQuery对象只能使用jQ里的属性和方法
   js对象只能使用js里的属性和方法
   想要使用,需要相互转换 

### 4. 相互转换方式

1. jQ对象 --- Dom对象 

   $("对象")[0]

   $('对象').get[0]

```js
		 //======jQuery方式
  $(function() {
    //获取到div
    var div = $('div');
    //第一种方式 : 将jq对象转成Dom对象
    $('div')[0]
    console.dir(div[0]); //放回DOM对象

    //第二种方式 : 将jq对象转成Dom对象
    $('div').get[0];
    console.log(div.get[0]);
  })
```

2. DOM 对象 --- jQ对象 转换方式

```js
$(dom对象)
$(this)
```

### 5.获取页面元素---选择器

```js
$('css选择器');
//标签选择器 , 类选择器 , ID选择器 后代(空格) ,子代(>),伪(:)类.....
//必须有引号
```

a.  jQuery 自己的获取页面的元素---选择器

```js
$('li:first')     //li:first-child
$('li:last')      //li:last-child
//eq(索引),索引从0开始 
$('li:eq(2)')       //li:nth-chiild(2)---结构第二个
```

### 6.获取页面元素---方法

(['选择器'])  表示里面的可以写,也可以不写

```js
//1.直接父元素
$('对象').parent();
//1.1直接.间接父元素
$('对象').parents(['选择器 ']);//获取父元素里的指定的父元素
//2.直接子元素
$('对象').children(['选择器']);//获取直接子元素.类似于css中的子代选择器
//3.直接,间接子元素
$('对象').find('选择器');//获取指定的直接和间接子元素.类似于css中的后代选择器
//4.获取兄弟元素
$('li').siblings(['选择器']); //获取当前元素的所有兄弟元素
//5.获取类名,返回布尔值
$('li').hasClass('类名');//获取当前元素有没有这个类名.返回布尔值
//6.获取指定索引的标签(元素)
$('li').eq(index); 
//7.获取下标
$('li').index();//返回下标值

```

### 7.操作元素样式--css()

隐式迭代:jQuery自己内部就可以将数组进行遍历,不需要手动遍历(for)

```js
//原声js方式
  //1.1 通过style设置标签样式
  //1.2 通过添加类名给标签设置样式
  //元素 . className = 'bg-red';
  //元素 . classList .add('bg-red')
     var div = document.querySelector('div');
     div.style.background = '#222';
     div.className = "bg-red";
     div.classList.add('bg-red')

```

```js
//jQuery方式
  $('对象').css("属性", "值");
  $('对象').css({
    属性: 值,
    属性: 值,
  });

```

### 8.操作元素样式--通过类 名

```js
1.添加类样式
//js中 className('类名1  类名2') classList.add('类名1','类名2')
$('对象').addClass('类名1  类名2');
$('div').addClass("box");
2.移除类样式
$('对象').removeClass(); //移除所有样式
$('对象').removeClass('类名'); //移除指定类名的样式
3.toggle
$('对象').toggleClass(); //如果有该样式就移除,没有就添加

```

### jQ动画效果 -显示 ,隐藏

- 方法名([speed],[easing].[fn])
  - speed参数1 . 动画的速度类型('slow' , 'normal','fast',或者毫秒值1000)
  - easing参数2 .指定动画切换效果,('linear','swing')
  - fn参数3 . 动画完成后执行的回调函数

1. 元素显示 和隐藏

   ```js
   1.hide([speed],[easing].[fn])
   $('div').hide(1000); //隐藏
   2.show([speed],[easing].[fn]);
   $('div').show(1000); //显示
   3.toggle([speed],[easing].[fn]);
   $('div').toggle();//元素切换
   
   ```

2. 滑动slide

   通过改变高度隐藏显示

   ```js
   1.从上往下显示 改变元素高度
   slideDowm([speed],[easing].[fn]);
   $('div').slideDown(1000);//显示 
   2.从下往上隐藏 改变元素高度
   slideUp([speed],[easing].[fn]);
   $('div').slideUp(1000);//隐藏
   3.$('div').slideToggle(1000);//切换
   
   ```

3. 淡入淡出fade

   通过控制元素改变透明度

   ```js
   1.fadeOut([speed],[easing].[fn]);//隐藏
   2.fadeIn([speed],[easing].[fn]);//显示
   3.fadeToggle([speed],[easing].[fn]);//切换
   4.fadeTo(['参数1'],'opacity',['参数1'],['参数1']);//变淡
   参数1.动画速度
   参数2.代表透明度 取值 0-1,必须设置
   参数3.代表切换效果
   参数4.回调函数
   
   ```

4. 自定义动画

   - animate(params,[ ], [ ],[ ])
     - animate不能设置颜色类的效果
     - width:200,  不用加单位

   ```js
   animate({
     属性:值,
     属性:值
   },1000)
   
   ```

## 案例

1. 导航栏移入移除,显示和隐藏菜单





.toFixed(number) 保留几位小数

修改事件  .change(function(){})

# jQuery-02

## 1.动画排队问题

1. 排队问题 : 动画没结束,下一个就开始了,闪动太快
2. **解决** :  在动画执行之前,使用 **stop() **方法

## 2.操作标签内的属性

- 通过jQ的方式获取/设置标签**固有的属性**

  - **$(' ').prop( )**

  ```js
  <div class="box" id="div"></div>
  //1.获取div上固有的属性值
  $('div').prop('属性');
  $('div').prop('class');//box
  //2.重新设置属性值
  $('div').prop('属性','新设置的属性值');
  $('div').prop('class','box_1')
  ```

- 通过jQ方式获取/设置标签**自定义的属性**

  - **$(' ').attr( )**

  ```js
  <div class="box" id="div" data-name="张三" name='李四'></div>
  1.获取自定义属性值
   $('对象').attr('属性');
   $('对象').attr('name');//李四
  2.设置自定义属性值
   $('对象').attr('属性','属性值');
   $('对象').attr('data-name','张娜');
  ```

## 3.获取标签中的值

- 获取表单控件的值
  - **$(' ').val()**

```js
1. 获取表单里的值
 $('input).val();
2.设置表单里的值
 $('input).val(值);
```

- 获取 / 设置 普通标签里的值

  - **$( ) . text( )**
  - //特点与原声js中的innerText 一样

  ```js
  1.获取div里的内容   
    $('div').text()
  2.设置div的内容
    $('div').text('新加的div文字')
  ```

  - $().html()
  - 特点与原声js中的innerHtml 一样

  ```js
  1.能够获取div下的所有(内容+标签)
    $('div').html()
  
  2.能购设置div下的所有(内容+标签)
    $('div').html('<span>我是新增的span标签</span')
  ```

## 4.jQ对象的遍历

- jQ对象 . each(function( i , item) {}
  - 形参:
    - i  : 代表下标索引
    - item : 每一个Dom对象节点

## 5.创建元素

- jQ对象 . html

```js
$('html标签')
$('<span></span>')
```

## 6.添加元素

1. 添加的是子元素

- $(' ').append(创建的元素)
  - 将创建的元素添加到父元素**末尾**
- $(' ').prepend(创建的元素)
  - 将创建的元素添加到父元素**开始**

2. 添加兄弟元素

   - $(' ').after(创建的元素)
     - 添加到当前元素 **后**
   - $(' ').before(创建的元素)
     - 添加到当前元素 **前**

3. 删除元素

   ​    $('div:nth-child(2)').remove() //删除当前元素

   ​    $('div:nth-child(2)').empty() //清空当前元素的内容

   ​    $('div:nth-child(2)').html('') //清空当前元素的内容



# jQuery-03

## 1.操作缓存数据

- f方法 : 变量 数组 对象 本地存储  自定义属性(prop  attr)
- jQ对象 .  data()

```js
jQ对象 .  data('属性名')  //获取 页面看不到
jQ对象 .  data('属性名','属性值') //设置
```

## 2.jQ遍历方式

- 语法: $ .each (object , function( index , element ){ })
  - object  .要遍历的 数组获取对象
  - index   遍历的下标
  - element  遍历的元素 Dom

```js
 var  arr = [1,2,3,4,5]
    //遍历方法   $.each
    $.each(arr, function(i,item){
        console.log(i); //下标索引
        console.log(item);  //每一项得值        
    })
    //2. 能不能通过 $.each 获取li里的值 ?
    $.each( $('li'),function(i,item){
        console.log(i,item); 
        console.log(item); //每一个li标签
        console.log( $(item).text() );//每一个li标签的 值      
    })
```

**区别**

- $.each   遍历数据  通常遍历**数组或对象**
- jQ对象 . each  遍历数据  通常用来**遍历jQ对象**

## 3.获取元素 大小

- js中  :位置 :offsetLeft   实际大小;offsetWidth  内容区域大小clientWidth

- 获取的是内容区域大小

  ```js
  jQ对象 . width();//获取 width
  jQ对象 . height();
  jQ对象 . width(400);//设置 不用加单位
  ```

- 获取元素大小 width+padding

  ```js
  $('.box').innerWidth();//width+padding
  ```

- 获取元素实际大小  width+padding+border

  ```js
  $('.box').outerWidth();//width+padding+border
  ```

- 获取元素大小  width+padding+border +magin

  ```js
  $('.box').outerWidth(true); //width+padding+border +magin
  ```

## 4.获取元素 位置

```js
1.获取的是当前元素现对于整个页面的距离(跟父元素无关)
    $('.one').offset() ; //返回对象  left  top
    $('.one').offset().left  //距左的位置

2.如当前父元素与定位 ,则是距离父元素的位置 ,如没有定位 就参照整个文档
    $('.one').position(); //返回对象 left  top
		$('.one').position().top;//距上的位置
```

- scrollTop 用来获取内容区域滚动出去的距离
  - 如果获取内容区域滚动出去的距离,**需要注册scroll事件**

```js
    //js滚动出去的距离

    //先注册scroll事件
    $('.box').scroll(function(){
        //获取.one 滚动出去的距离
        $('.one').scrollTop()  //值
    })
```

## jQ注册事件

```js
$('div').click(function(){});
特点 :给事件源绑定一个事件

```

- on的方式

  ```js
  //第一种
  $('div').mouseenter(function(){
    $(this).css('background','red');
  })
  $('div').click(function(){
    $(this).css('background','pink');
  })
  
  //第二种  on 的方式 注册事件
  $('div').on('事件类型',处理程序)   ---绑定一个事件
  $('div').on({                     ---绑定多个事件
    事件类型: 处理程序,
    事件类型: 处理程序,
    事件类型: 处理程序
  })
  
  $('div').on('click',function(){
    $(this).css('background','red');
  })
  
  $('div').on({
    mouseenter:function(){
      $(this).css('background','red');
    },
    click:function(){
      $(this).css('background','pink');
    }
  })
  
  ```

## 委托方式注册事件

- 注意 :如果页面中的元素是动态创建的,那么给该动态创建的元素注册时间的时候必须使用委托方式

- 使用 : 动态创建的元素 ,必须用 on方式注册

  ```js
  //委托方式 注册事件
  //给选择器注册了事件,让他去执行
  $('.box').on('事件类型','选择器',function(){ })
  
  //动态创建元素
  var div = $('<div class="one"></div>');
  //添加标签
  $('.box').append(div);
  //注册事件委托 
  $('.box').on('click','.one',function(){
    alert(1);
  })
  
  ```

## 解绑事件

语法 : jQ对象 . off( )

- 如果off里没有设置任何参数 , 代表将该对象中的所有事件都解绑

  ```js
  //js中解绑方法
  document.querySelector('div').onclick = null;   document.querySelector('div').removeEventListener('click',function(){})
  
  
  $('div').on({
    click:function(){
      alert(1);           
    },
    mouseenter:function(){
      alert(2);           
    }
  })
  
  //1.解绑事件
  $('div').off('click'); //解绑click事件
  $('div').off(); //解绑所有
  
  //2.解绑委托事件
  $('.box').off("click",'.one')
  
  ```

## one()注册事件

- 只能执行一次 ,就不需要解绑

  ```js
   $('div').one('click',function(){
    	alert(1);
   })
  
  ```

## 自动触发事件

```js
$('div').click(function(){
  alert(1);
})
1.第一种方式 : 自动触发方式
//事件源 . 事件类型();
$('div').click();
2.第二种方式 : 自动触发方式
//事件源.trigger('事件类型'); 
$('div').trigger('click'); 

```

## 自调用函数

```js
//自调用函数 : 让函数自己调用自己
( function fn(){
  alert(1)
} )()

( function fn(n){
  alert(n)
} )(11)   //弹出11


```

## jQ事件对象参数

```js
//事件对象参数 : 当在执行某个事件的时候,会将用户的一些行为动作数据保存起来
$('div').click(function(e){
e.stopPropagation();
})

```

## 拷贝对象

- 语法 : $ .extend([deep] ,targetObject , currentObject)
- 参数 
- deep: 布尔类型的值.默认值是false,该参数用来设定拷贝对象的时候是深拷贝还是浅拷贝
  - deep得值 :默认值false,代表是浅拷贝
  - deep得值 : true,,代表是深拷贝
    - 不管是浅拷贝还是深拷贝,如果原来对象中和被拷贝对象中相同的属性,会被覆盖
    - 不管是浅拷贝还是深拷贝,如果原来对象中存在不同和被拷贝对象中不同的属性,不会被覆盖
    - 浅拷贝:在拷贝过程中遇到对象, 将对象地址赋值给,你变我也变
    - 深拷贝: 将对象赋值  ,你变我不变
- targetObject : 用来接收拷贝对象的
- currentObject : 别拷贝的对象

## 多库共存 

- 伪类比年其他js文件中的命名和JQuery中的 $ 命名冲突

- 避免冲突方法

  - 将 $ 用 JQuery 代替

  - 自定义方式  

    ```js
    var getelement = $ . noConflict();
    getelement('div')  =======>$('div') jQuery('div')
    
    ```

## 插件介绍



t