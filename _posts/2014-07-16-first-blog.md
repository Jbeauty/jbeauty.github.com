---
layout: post
title: 原生JS实现几个常用HTML DOM增强API
description:  常用的javascript 工具函数

---

**getElementsByClassName()**

<pre><code>

/**
* 获取指定类名的元素对象集合
* @param {Object} node 父节点
* @param {String} classname 指定类名 
* @return {[Object]}目标对象集合
*/
function getElementsByClassName(node,classname) {
//如果浏览器支持则直接使用
  if (node.getElementsByClassName) { 
    return node.getElementsByClassName(classname);
  } else {
    return (function getElementsByClass(searchClass,node) {
        if ( node == null )
          node = document;
        var classElements = [],
            els = node.getElementsByTagName("*"),
            elsLen = els.length,
            pattern = new RegExp("(^|\\s)"+searchClass+"(\\s|$)"), i, j;
        for (i = 0, j = 0; i < elsLen; i++) {
          if ( pattern.test(els[i].className) ) {
              classElements[j] = els[i];
              j++;
          }
        }
        return classElements;
    })(classname, node);
  }
}

</code></pre>

**addLoadEvent()**

<pre><code>
/**
* 方便的将在文档加载后运行的函数添加到window.onload中
* @param {function} func 待运行函数
*/
function addLoadEvent(func){
    var oldOnload = window.onload;
    //typeof 返回String类型
    if(typeof window.onload != 'function'){
        window.onload = func;
    }else{
        window.onload = function(){
            oldOnload();
            func();
        }
    }
}

</code></pre>

**addClass()**

<pre><code>
/**
* 为指定元素结点添加新类名
* @param {Object} element 元素结点
* @param {String} value 类名
*/
function addClass(element,value){
    if(!element.className){
        element.className = value;
    }else{
        newClassName = element.className;
        //多个类名间添加空格
        newClassName += '  ';
        newClassName += value;
        element.className = newClassName;
    }
}

</code></pre>
