---
layout: post
title: javascript DOM 编程艺术 笔记一
description: 《javascript DOM 编程艺术》是一本很好的javascript入门书，这篇博文是我阅读这本书后，对共享onload事件，所做地一些笔记。
tags: [javascript]
comments: true
categories: personal
---


**javascript DOM 编程艺术共享onload事件**

当你需要网页加载时会触发一个onload事件，通常是直接把函数 ```window.onload``` 赋值。

<pre><code>
 window.onload = someFunction;
</code></pre>

但如果有多个函数的话，最后一个将会覆盖前面的所有函数。

<pre><code>
 window.onload = firstFunction;
 window.onload = secondFunction;//  将覆盖 firstFunction.
</code></pre>

解决上面覆盖的问题，需要创建一个匿名函数来容纳你的函数，然后把匿名函数绑定到onload事件上。如果需要绑定的函数很多的话，则不建议采用。

<pre><code>
  window.onload = function() {
      firstFunction();
      secondFunction();
  }
</code></pre>

接下来我们对上面的函数进行一个封装。

<pre><code>
function addLoadEvent (func) {
    var lodOnload = window.onload;
    if(typeof window.onload != "function") {
        window.onload = func;
    }else{
        window.onload = function() {
            oldOnload();
            func();
        }
    }
}
</code></pre>

操作:把现有的```window.onload```事件处理函数存入变量```oldOnload```中；如果这个事件处理函数还没绑定任何函数，就把新函数添加进去；如果已经绑定了，则追加到现有函数的末尾。
然后再引用```addLoadEvent```函数添加你的函数。这是一个具有弹性的方法，不论需要添加多少函数，在页面加载完毕时都可以得到执行。

<pre><code>
  addLoadEvent(firstFunction);
  addLoadEvent(secondFunction);
</code></pre>





