title: javascript事件代理简单介绍
date: 2016-02-26 11:14:15
categories: [javascript, web前端]
tags: [javascript, 事件]
---
javascript事件是实现web页面交互的基础。
<!--more-->
### 事件代理
在JavaScript中事件代理包括两个：一个是事件冒泡，一个是事件捕捉，之所以出现这两种类型的事件代理是由于当年的浏览器大战。关于事件代理和事件冒泡的想起介绍请看这里[Javascript中事件的发生顺序](http://chenzimu.com)。
### 事件代理的作用
假如有一个表格，表格中有几十个单元格，如果要给每个单元格绑定点击事件的话就会产生性能问题，这时候就可以事件代理中的事件冒泡，将点击事件绑定到table元素上，当点击某个单元格的时候，点击事件就会冒泡到table元素上从而触发table元素上的点击事件，然后再根据当前触发该点击事件的目标元素执行相应的操作。
### 兼容性问题
上边的方法很简单，唯一一个需要注意的地方就是该如何确定当前触发事件的目标元素，因为IE和其他浏览器在这一问题上有不同，所以需要写一个确定目标元素的函数，如下：

    function getEventTarget(e){
        var e = e || window.event;
        return e.target || e.srcElement;
    }
    function doSomething(e) {
        var target = getEventTarget(e);
        if(/判断当前目标元素是否正确/){
            //dosomething
        }
    }
    
> e代表的是传入到触发事件回调函数中的事件对象，函数的返回值是当前触发事件的目标元素。