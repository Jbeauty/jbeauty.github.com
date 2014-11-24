#Less学习笔记

使用 Less 编写 CSS 已经有一段时间了，今天终于抽出空来对总结一下。

###Less 是什么？
举了例子。小时候家里包饺子（纯手动写 CSS)，和面、拌馅、揪面团、擀皮、包饺子、下锅样样都需要经过妈妈的手。长大了有了互联网之后，海淘了一台 ```KitchenAid PRO 550```(Less)，这下妈妈省多了。Less 就是辅助并减轻我们编写 CSS 工作量的一样语言工具。

###快速入门
Less 增加了诸如变量、混合、函数等一些高级功能，让我们写 CSS 能像写 javascript 一样更方面、更易维护、与扩充。Less 可以运行在 Node、浏览器和 Rhino 平台上。网上有很多第三方工具帮助你编译 Less 源码。

1、变量：跟 javascript 语言一样，Less 允许我们定义一个变量来保存值，这样可以方便的改变应用到变量的样式。

```
@base: #ff6600;
.box {
	color:@base;
}
p {
	color:@base;
}
```
编译之后

```
.box {
	color:#ff6600;
}
p {
	color:#ff6600;
}

```
note：Less 的变量叫做```常量```更加合适，因为它只能被定义一次。

2、混合：跟 javascript 的函数类似，可以定义带参数或者不带参数的混合之后，可以当做函数调用一样使用它。有了混合，我们就可以抽象出一些常用的代码以便复用了

```
.roundedCorners(@radius:5px) {
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
不传参数编译之后

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
比如传入10px 参数编译之后

```
.corner-button{
	width:100px;
	height:100px;
	background-color:blue;
	-moz-border-radius:10px;
	-webkit-border-radius:10px;
	border-radius:10px;
}
```
不带任何参数的混合

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
编译之后

```
pre {
	text-wrap: wrap;
	white-space: pre-wrap;
	white-space: -moz-pre-wrap;
	word-wrap: break-word;
}
```
				
3、匹配模式，不严谨地说可以理解成 javascript 的 if 分支，下面我们来看一段生成三角形的 CSS 代码。

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

4、嵌套规则，Less

HTML代码

```
 <ul class="news_list">
 	<li><a>测试新闻</a><span>2014年11月23日</span></li>
 	<li><a>测试新闻</a><span>2014年11月23日</span></li>
 	<li><a>测试新闻</a><span>2014年11月23日</span></li>
 </ul>
```

```
.news_list{
	width:600px;
	margin:30px auto;
	padding:0;
	list-style:none;
	li{
		height:30px;
		line-height:30px;
		background-color:pink;
		margin-bottom:5px;
	}
	a{
		float:left;
	}
	span{
		float:right;
	}
}
```

编译之后

```
.news_list {
	width:600px;
	margin:30px auto;
	padding:0;
	list-style:none;
}
.news_list li{
	height:30px;
	line-height:30px;
	background-color:pink;
	margin-bottom:5px;

}
.news_list a{
	float:left;
}
.news_list span{
	float:right;
}
```
也许你会问，为什么不把 ```a``` 和 ```span```写到 ```li``` 里边去呢，原因是如果标签元素的层次越多，CSS 匹配的次数就越多，效率就会更慢了。


