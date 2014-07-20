---
layout: post
title: javascript DOM 编程艺术共享onload事件
description:  共享onload事件
---


javascript DOM 编程艺术共享onload事件
第一种方法：网页加载是会触发一个onload事件，直接把 window.onload赋值。但如果有多条函数的话，最后一条将会覆盖前面的所有函数。
 window.onload=firstFunction（）;

第二种方法：创建一个匿名函数来容纳你的函数，然后把匿名函数绑定到onload事件上。如果需要绑定的函数很多的话，则不建议采用。
  window.onload=function(){
      firstFunction（）；
      secondFunction（）；
  }

第三种方法：先写一个函数，把函数绑定到onload事件上，然后再引用addLoadEvent函数添加你的函数。这是一个具有弹性的方法，不论需要添加多少函数，在页面加载完毕时都可以得到执行。
操作:
把现有的window.onload事件处理函数存入变量lodOnload中；
如果这个事件处理函数还没绑定任何函数，就把新函数添加进去；
如果已经绑定了，则追加到现有函数的末尾。
function addLoadEvent(func){
    var lodOnload=window.onload;
    if(typeof window.onload !="function"){
        window.onload=func;
    }else{
        window.onload=function(){
            oldOnload();
            func();
        }
    }
}

  addLoadEvent(firstFunction）；
  addLoadEvent(secondFunction）；


