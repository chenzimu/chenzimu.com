title: javascript变量和函数提升
date: 2015-12-25 11:27:35
categories: [javascript]
tags: [变量声明, 变量提升, 函数提升]
---
要明确变量声明、初始化、变量声明提升以及函数声明和函数表达式的概念及区别。
<!--more-->
## 变量声明和提升
先看两个简单的例子，这两个例子是我们都比较熟悉的，也很简单。
{% code %}
var chenzimu1 = 1024;
alert(chenzimu1);

var chenzimu2 = 1024;
(function() {
    alert(chenzimu2);
})();
{% endcode %}
>两段代码都如我们所想，都弹出1024

下边这个例子就有点诡异了，对于不熟悉js的人来说可能结果与自己料想的并不一样。
{% code %}
var chenzimu = 1024;
(function() {
    alert(chenzimu);
    var chenzimu = 2015;
})();
{% endcode %}
>这段代码或许和你想的不一样，它弹出的是undefined,why?

### 变量的声明被提升了

在当前作用域中，无论变量在作用域的什么位置声明，变量声明都会被提升到作用域的最顶层。
>这里有一个需要注意的地方，只有变量的声明被提升了，如果变量同时初始化了值的话，变量的初始化是不会被提升的。

#### 变量声明、初始化及变量声明提升
{% code %}
var chenzimu;//变量声明
var chenzimu = 1024;//变量初始化
function chenzimu() {
    var a = 1;
    var b = 2;
};
//变量声明提升，但初始化不提升，则上边函数等同于
function chenzimu() {
    var a;
    var b;
    a = 1;
    b = 2;
};
{% endcode %}
所以回到前边的例子:
{% code %}
var chenzimu = 1024;
(function() {
    alert(chenzimu);
    var chenzimu = 2015;
})();
{% endcode %}
>上边代码中，对于var chenzimu = 2015;由于变量提升会变成:
{% code %}
var chenzimu = 1024;
(function() {
    var chenzimu;
    alert(chenzimu);
    chenzimu = 2015;
})();
{% endcode %}
所以，浏览器弹出的值是undefined

## 函数提升

### js中创建函数的方法
js中两种最常用的创建函数的方法是函数声明和创建匿名函数表达式。

**1. 函数声明**

{% code %}
function fn(){}
{% endcode %}

**2. 函数表达式**

{% code %}
var fn = function() {};
{% endcode %}

在js中函数声明的提升与变量是相同的，即函数的声明被提升到了函数所在作用域的最上方。如下边这个例子：

{% code %}
sayHello();//调用成功
function sayHello(){
    console.log('Hello');
}
{% endcode %}

再看下边一个例子:

{% code %}
var a = function() {
    console.log('a');
};
function a() {
    console.log('a1');
}
a();
{% endcode %}

可能有人会认为上边的代码会输出a1,但是它输出的却是a。因为由于变量声明和函数声明的提升，上边的代码变成了这样：

{% code %}
var a;//变量声明提升
function a() {//函数声明提升
    console.log('a1');
}
a = function() {
    console.log('a');
};
a();//输出a
{% endcode %}

> 注意，函数声明的提升是将函数名和函数体一块儿进行提升的。

