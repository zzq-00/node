## 传统布局

text-align 在传统布局中 表示 行内元素，行内块元素的水平方向排版【在flex布局中失效】

vertical-align  在传统布局中，表示文字与图片的垂直方向

# flex布局

* felx布局叫弹性布局，伸缩布局
* 会随着屏幕的大小变化
* 属性设置在父元素上，效果体现在亲生子元素上
* display:flex;  弹性布局的入口，用于容器的属性
* flex布局 的子元素设置了宽高就会生效，不需要考虑行内 行内块 元素

## flex-direction

* flex-direction:row | column | row-reverse | column-reverse;
  * row 默认值 表示设置主轴位水平方向,从左到右
  * column 表示设置主轴为垂直方向，从上到下

## justify-content

用于设置item在主轴上的对齐方式【控制水平方向排版】

* justify-content：start | end | center | space-around | space-between；
  * start 表示开始方向【如果主轴是水平方向 则从左到右对齐排版；如果主轴是垂直方向，则从上到下对齐排版】
  * end 表示末尾方向【如果主轴是水平方向 则从右到左；如果主轴是垂直方向，则从下到上】
  * center 表示居中方式排版
  * space-around 表示等比例瓜分空白区域
  * space-between 表示每行左右元素对齐，其他元素瓜分剩余空白区间

## align-item

用于控制交叉轴(侧轴)方向上(单行)的排版【通俗就是控制垂直方向排版】

align-item：flex-start | flex-end | center | stretch；

* start 开始
* center 居中(挤在一起居中)
* end 结束
* stretch 拉伸（主轴为水平方向，拉伸【不能设置高度。主轴为垂直方向，拉伸【不能设置宽度。）

## align-self

* 控制单个元素，自己在侧轴上的对齐方式
* 属性值与align-item一样
* 默认值为auto，可继承父元素align-item的属性
* **使用：配合flex属性，主轴方向自动划分份数，侧轴方向自动拉伸**



## align-content

用于实现  **多行** items整体侧轴方向

align-content：flex-start | flex-end | center | stretch | space-around | space-between；

* stretch  设置子项元素高度平分父元素的高度
* 需要设置换行

## flex-wrap

控制子元素是否换行

flex-wrap：nowrap | wrap ；

* 默认不换行，子元素宽度大于父元素的宽度时，子元素的宽度被压缩小

## flex：<number>

* 用于设置项目的属性，划分主轴上的剩余空间给子元素
* 份数：
  * 常规使用，整数。默认值 0 flex来表示占整体的多少份数，不设置宽(高)，在宽(高)方向全部进行剩余空间的划分
  * flex:20%;  分配剩余空间的百分比,使用%，必须加起来是百分之百
* **使用场景：左侧固定，右侧随意拉伸**

## order

定义子项目的排列顺序。

# 复习

felx布局

* 属性分类
  * 容器属性（）
    * display:flex; flex布局入口
    * flex-direction:row | column | row-reserve |coloumn-reserve
      * row  默认值 默认以水平方向为主轴，从左到右排【则侧轴就是垂直方向】
      * column  以垂直方向为主轴，从上到下排【则水平方向就作为侧轴】
    * justify-content：start | end |  content | space-between | spacearound
      * justify-content  表示主轴方向的排列
    * align-items : flex-start | flex-end | content |space-around | space-between | strecth
      * align-items  表示侧轴方向(单行)的排列对齐方式
      * 属性值 strecth 拉伸 **表侧轴方向的拉伸【拉伸不能设置高或宽】**
    * align-content 使用此属性时需要换行，表示多行的对齐方式 ，与align-items属性值一样
    * flex-wrap：nowrap | wrap； 默认不换行
      * **弹性布局默认不换行，如子元素的宽度超过父元素的宽度，则缩小宽度一行排列，使宽度无效，但宽度必须设置**
  * 项目属性（单个子元素）
    * flex：<number>
      * 份数：平分剩余空间
      * flex：1；表示每个子元素占1份
      * flex：20%；表示子元素占20%，**整行必须加起来是100%**
      * **使用场景：左右固定，中间随意拉伸**
    * align-self
      * 控制单个元素
      * 默认值为auto，会继承父元素的align-items属性
      * 如果父元素(容器)没有设置align-items，则align-self的默认值变为strecth拉伸
      * **使用：配合flex属性，主轴方向自动划分份数，侧轴方向自动拉伸**
    * order
      * 控制子元素的排列顺序
      * 可以为负值



