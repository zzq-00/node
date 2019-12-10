## rem布局

* 等比缩放

## rem单位

* em：代表一个字符 例 1em=父亲的字体大小(px)
* rem单位：root(根)  em  代表HTML的字体大小 1rem=HTNL的字体大小(px)
* 控制是整个页面的px值

## 媒体查询

* 媒体查询：响应屏幕的变化
* @media 定义媒体查询关键词
* mediatype   媒体类型；查询不同的终端设备 all | screen | print
* and |not | only 
* (media featuer)  有width | min-width | max-width

@media  all | screen | print    and |not | only  (media featuer) {

​	}

```css
/*例：表示 查屏幕 且 最小宽度为320px，下面的CSS-code生效*/
@media screen and（min-width:320px）{
    html {font-size:14px;}
 	body { bockground：red；}
}
```

## 档位划分

```css
表示320px——540px  540px--640px 640--无穷大
@media screen and (min-width:320px) {}
@media screen and (min-width; 540px) {} 
@media screen and (min-width; 640px) {} 
```

## 资源引入

```css
<link rel="stylesheet" media="screen and (min-width:320px)" />
```

## 安装less

## less语法

* 变量@color:red;

* 运算 + - * /  

* 嵌套

  ```less
  header{
      width:100%;
      color:@color
      logo{
          heigth:44/30 rem;
          &::before{
              content:"";
          }
      }
  }
  ```

## 约定

* 约定1：UI设计的宽度，划分档位
* 约定2:1rem=各个档位最小值 / 10

### 第一种方法(不用)

* 档位划分

```
/*样式里写媒体查询*/
/*不好 屏幕缩放时,不能连续变化 间断性太大*/
@media screen and (min-width:320px){
    html{
        font-size:320px/10px;
    }
}
@media screen and (min-width:480px){
    html{
        font-size:480px/10px;
    }
}
```

### 第二种方法

* 导入flexible.js文件(是屏幕适配库)

```less
/*1.由于js文件 屏幕缩放变化是从0到最大,应设置合适的最大最小缩放
  2.文字字体显示在html行内,所以要给改变文字大小需设置最高权限*/
/*表示0-320这个宽度的固定 1rem=HTML的32px */
@media screen and (max-width:320px){
    html{
        font-size:320px/10px;
    }
}
/*表示680-无穷大这个宽度的固定 1rem=HTML的68px */
@media screen and (min-width:680px){
    html{
        font-size:68px;
    }
}

/*改变字体大小 加最高权限*/
font-size:14px !important;
```





