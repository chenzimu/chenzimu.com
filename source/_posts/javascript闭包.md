title: javascript闭包
date: 2014-12-30 10:42:45
categories: [javascript]
tags: [javascript, 闭包]
---
闭包的概念很难懂，这篇文章也只是我的一个学习笔记吧，其中尤其是闭包在循环中的运用尤其最难理解。
综合来说的:闭包是一个函数，在函数的上下文中有变量由于被引用，即使函数返回也不会销毁，这样的函数就是一个闭包。
<!--more-->
## 语义范围
语义范围通俗讲就是我们在定义一个函数时从function开始一直到这个函数结束的整个代码段的范围。如：
{% code %}
var x = 'global';
function outer(){
    var y = 'outer';

    function inner(){
        var x = 'inner';
    }
}
{% endcode %}

inner函数被outer函数包围着，而outer函数又被全局上下文包围着，这样就形成了所谓的语义层级，如图所示：

![](http://7xnniz.com1.z0.glb.clouddn.com/closurelexical.png)

>这样outer函数的语义范围=outer自身的语义范围+inner的语义范围+global的语义范围，outer的语义范围=outer自身的语义范围+global的语义范围

## 变量环境(执行上下文)
对于全局来说有一个全局的执行上下文，每定义一个函数，该函数也会生成自己的新的执行上下文，这与语义范围是相对应的，每一个执行上下文就像一个仓库，用来存储在相应语义范围中所定义的变量。如下所示：
{% code %}
//执行上下文:x : undefined
var x = 'global';
//执行上下文:x : 'global'
function outer(){
    //执行上下文: y : undefined
    var y = 'outer';
    //执行上下文: y : 'outer'

    function inner(){
        //执行上下文 : x : undefined
        var x = 'inner';
        //执行上下文 : x : 'inner'
    }
}
{% endcode %}

## [[scope]]属性
当在一个执行上下文中定义新的函数的时候，就会创建新的函数对象，这个函数对象内部有一个名为[[scope]]的属性，这个属性指代的就是当前的执行上下文。而且该scope属性会对其外层的语义范围内的变量进行引用防止被javascript的垃圾回收机制所回收，这样该函数就会从全局开始继承每一层所包含的变量。

>这应该就是一些教程中所说的闭包就是函数中的函数的原因吧。

如下所示:
{% code %}
//执行上下文:x : undefined
var x = 'global';
//执行上下文:x : 'global'
function outer(){
    //执行上下文: y : undefined,[外层语义范围]x : 'global'
    var y = 'outer';
    //执行上下文: y : 'outer',[外层语义范围]x : 'global'

    function inner(){
        //执行上下文 : x : undefined,[外层语义范围]y : 'outer',[外层语义范围]x : 'global'
        var x = 'inner';
        //执行上下文 : x : 'inner',[外层语义范围]y :'outer',[外层语义范围]x : 'global'
    }
}
{% endcode %}

## 一个闭包的基础例子
{% code %}
function sayHello(name){
    var text = 'Hello ' + name;
    var helloAlert = function(){
        alert(text);
    };
    return helloAlert;
}
var hello = sayHello('Chenzimu');
hello();
{% endcode %}

>在javascript中，可以将一个函数引用变量看作是对一个函数的引用以及对一个闭包的隐式引用。代码中匿名函数定义在函数sayHello中形成了一个闭包。

## 更多闭包的例子

### 例一
{% code %}
function say2015(){
    var num = 2014;
    var sayAlert = function(){
        alert(num);
    };
    num++;
    return sayAlert;
};
var say = say2015();
say();
{% endcode %}

>这个例子展示了闭包中本地变量是通过引用而不是复制获取的。

### 例二
{% code %}
function setupSomeGlobals(){
    var num = 666;
    alertNum = function(){
        alert(num);
    };
    incNum = function(){
        num++;
    };
    setNum = function(x){
        num = x;
    };
};
setupSomeGlobals();
alertNum();
incNum();
alertNum();
setNum(888);
alertNum();
setupSomeGlobals();
alertNum();       
{% endcode %}

>例子中三个全局函数都引用了同一个闭包，因为三个函数都有对num的引用，即都对setupSomeGlobals()的引用(因为num是setupSomeGlobals作用域中的变量)。
>>注意：当再次执行setupSomeGlobals函数时，就会创建一个新的闭包，则之前执行过的函数和得到的值都会被覆盖掉。（在javascript中，当在一个函数中定义另一个函数时，每次外部函数的执行都会导致内部函数的重新初始化创建。）

### 例三(较难理解)

{% code %}
function buildList(list){
var result = [];
for(var i = 0;i < list.length;i++){
    var item = 'item' + list[i];
    result.push(
        function(){
            alert(item + ' ' + list[i]);
        }
    );//引用函数pointer
}
return result;
}
function testList(){
    var fnlist = buildList([1,2,3]);
    fnlist[0]();
    fnlist[1]();
    fnlist[2]();
}

testList();
{% endcode %}

>在for循环中使用闭包得到的结果会和我们想象中的不一样，上边的例子中，当testList函数运行时，会先执行buildList([1,2,3])，在for循环中匿名函数并没有立即执行，而是先push进了result数组，当执行fnlist时，fnlist使用的是for循环执行结束之后的i的值，即3，而后边的list[3]自然是undefined(因为[1,23]的长度为3)

### 例四

{% code %}
function newClosure(someNum,someRef){
    var num = someNum;
    var anArray = [1,2,3];
    var ref = someRef;
    return function(x){
        num += x;
        anArray.push(num);
        alert('num: ' + num + '\nanArray ' + anArray.toString() + '\nref.someVar ' + ref.someVar);
    };
}

var closure1 = newClosure(40,{someVar : 'closure1'});
closure1(5);
var closure2 = newClosure(1000,{someVar : 'closure2'});
closure2(100);
{% endcode %}

>上边的例子显示每次对newClosure函数的调用都生成一个闭包，两个闭包之间不会相互影响。

参考自:http://www.javascriptkit.com/javatutors/closures.shtml
       https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures


