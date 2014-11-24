---
layout: post
title: less is more than css
description: 使用 Less 编写 CSS 已经有一段时间了，今天终于抽出空来对总结一下。
headline: "Let's Fire up the Engines"
categories: personal
tags: 
  - blogging
  
**关于less**
  虽然一直以来css的书写习惯会让我们不太适应less，但只要你有一些css的语法基础和编程语法基础，相信学习less会是一件轻而易举的事情，偶尔换换书写方式也是别有一番趣味，更何况在代码繁多重复时，less确实可以让我们偷偷懒~

  **less**是一种动态样式语言，属于css预处理语言的一种，它使用类似css的语法，扩展了css的动态行为，如设置变量（Variables）、混合书写模式（mixins）、操作（operations）和功能（functions）等等，Less 可以运行在 Node、浏览器和 Rhino 平台上。网上有很多第三方工具帮助你编译 Less 源码。

 



**1、 变量**
Less 允许我们定义一个变量来保存值，这样可以方便的改变应用到变量的样式,然后应用到样式中，这样只要改变你定义的变量参数值就可以达到改变全局的效果。

**语法：**@变量名：值；
```
@color：#ccc；
.box{color:@color}  
p{colorl:@color}
```
**编译之后**
<pre><code>
.box{color：#ccc；}
p{color:#ccc;}
</pre></code>
note：Less 的变量叫做```常量```更加合适，因为它只能被定义一次。
### 2、混合
跟 javascript 的函数类似，可以定义带参数或者不带参数的混合之后，可以当做函数调用一样使用它。有了混合，我们就可以抽象出一些常用的代码以便复用了
- **没有传入参数**
``` 
.roundedCorners(@radius:5px){
    -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
  border-radius: @radius;
}
.corner-button{
  width:100px;
  height:100px;
  background-color:blue;
  
  .roundedCorners();//调用混合，因为定义的时候给了默认值5px，所以在没有传入新的值的时候都为5px
}
```
**编译之后:**不传参数
``` 
.corner-button{
  width:100px;
  height:100px;
  background-color:blue;
  -moz-border-radius:5px;
  -webkit-border-radius:5px;
  border-radius:5px;
}
``` 
- **传入参数**
``` 
.roundedCorners(@radius:5px){
    -moz-border-radius: @radius;
  -webkit-border-radius: @radius;
  border-radius: @radius;
}
.corner-button{
  width:100px;
  height:100px;
  background-color:blue;
  
  .roundedCorners(10px);//传入参数10px
}
```
**编译之后**
``` 
.corner-button{
    width:100px;
    height:100px;
    bakgroung-color:blue; 
    -moz-border-radius:10px;
  -webkit-border-radius:10px;
  border-radius:10px;}
```
- **不带任何参数**


``` 
.wrap(){
  text-wrap: wrap;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  word-wrap: break-word;
}
pre {
  .wrap;
}
```
**编译之后**

``` 
pre {
  text-wrap: wrap;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  word-wrap: break-word;
}
```
###3、匹配模式
不严谨地说可以理解成 javascript 的 if 分支，要满足条件才能匹配。下面我们来看一段生成三角形的 CSS 代码。

```
.triangle(@top,@width:5px,@color:#ccc){
  border-width:@width;
  border-color:transparent transparent @color transparent;
  border-style:dashed dashed soild dashed; //兼容 IE6 
}
.triangle(@bottom,@width:5px,@color:#ccc){
  border-width:@width;
  border-color:@color transparent transparent transparent;
  border-style:soild dashed dashed dashed;
}
```
上面代码是根据传入参数来生成一个三角形，如果调用```.triangle(top)```生成的就是朝上的三角形，如果调用```.triangle(bottom)```生成的就是朝下的三角形，

###4、嵌套规则
多层元素的样式规则写法
**html代码**
```
<div id="header">
          <h1><a href="">jbeauty</a></h1>
          <p>记述前端那些</p>
</div>
```

```
#header { color: black;
          p {
             font-size: 12px;
            }
          h1 {
               width: 300px;
               &:hover { text-decoration: none }
              }
          }


```
note:``` & ```符号的使用—如果你想写串联选择器，而不是写后代选择器，就可以用到&了. 这点对伪类使用如 :hover 和 :focus.


-------------------

####未完待续······

      




