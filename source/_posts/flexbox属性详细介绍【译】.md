title: flexbox属性详细介绍【译】
date: 2015-10-20 09:59:15
categories: [web前端, css3]
tags: [css3, flexbox]
---
Flexbox布局的全称为CSS Flexible box布局模块，它是css3中新增加的一种布局方式，这种布局方式可以可以在不知道元素的尺寸大小的时候依然可以调整元素的对齐方式等。flexible box最主要的特点是外层的盒子可以根据屏幕的不同尺寸自动调整盒子中元素的大小以填充元素之间由于屏幕尺寸变化出现的空间。
许多设计师和前端工程师发现flexbox布局用起来很方便，因为这种布局在定位元素的时候很容易，而且对于很复杂的布局可以用更少的代码即可完成。flexbox布局的算法是基于direction的，而之前我们常用的块布局和行内布局是基于水平方向和垂直方向的。flexbox布局应当被应用到小型应用中，因为新的CSS Grid布局模型将被应用到大型布局中。
这篇文章将会重点教给您flex属性是怎样影响布局的。
<!--more-->
## 1、基础
在我们深入讲解之前先让我介绍一下flexbox模型的一些基础知识。flex布局包含一个父级盒子叫做flex container，flex container的孩子元素都被称作flex items，如下图所示，
flexbox布局2009年开始经过了多次更新，所以为了避免麻烦，我们将使用2014年9月份的语法，如果你需要兼容一些老版本浏览器的话可以阅读这篇文章https://css-tricks.com/using-flexbox/
### 支持最新的flexbox语法的浏览器有：
>Chrome 29+
Firefox 28+
Internet Explorer 11+
Opera 17+
Safari 6.1+ (prefixed with -webkit-)
Android 4.4+
iOS 7.1+ (prefixed with -webkit-)

## 2、应用
应用flexbox布局很简单，你只需要在父级元素上添加display属性即可：
{% code %}
.flex-container {
  display: -webkit-flex; /* Safari */
  display: flex;
}
{% endcode %}
如果你希望元素以行内显示，则应用下边的代码；
{% code %}
.flex-container {
  display: -webkit-inline-flex; /* Safari */
  display: inline-flex;
}
{% endcode %}
>Note：这是唯一一个需要在父级元素上设置的属性，设置这个属性之后，它所有的孩子元素都自动变为flex items。

目前有很多组织flexbox属性的方法，我所知的虽简单的并可以加快理解的方法是将其分成两部分，一部分为flex container，另一部分是flex items。下边我将依次介绍这些属性以及它们是如何影响布局的。
## 3、flexbox container属性
### flex-direction
这个属性的作用是指定通过设置flex container的main轴的方向来指定flex items的布局方向（row：横向，column：竖向）。
{% code %}
.flex-container {
  -webkit-flex-direction: row; /* Safari */
  flex-direction:         row;
}
{% endcode %}
通过设置row，flex items在ltr上下文中从左到右横向布局
如下图所示：
通过row-reverse，flex items在ltr上下文中从右向左横向布局
{% code %}
.flex-container {
  -webkit-flex-direction: row-reverse; /* Safari */
  flex-direction:         row-reverse;
}
{% endcode %}
如下图所示：
通过设置column，flex items从上到下纵向布局
{% code %}
.flex-container {
  -webkit-flex-direction: column; /* Safari */
  flex-direction:         column;
}
{% endcode %}
如下图所示：
通过row-reverse，flex items从下向上纵向布局
{% code %}
.flex-container {
  -webkit-flex-direction: column-reverse; /* Safari */
  flex-direction:         column-reverse;
}
{% endcode %}
默认值：row
### flex-wrap
flexbox最原始的概念是将它的子级元素布局为单独的一行。而flex-wrap的作用则是控制flex container的子元素是在一行还是在多行中显示，以及新的一行的布局方向。
{% code %}
.flex-container {
  -webkit-flex-wrap: nowrap; /* Safari */
  flex-wrap:         nowrap;
}
{% endcode %}
上边代码使子元素在一行中显示，元素宽度会随元素个数的增加逐渐减小，以适应container的宽度。
{% code %}
.flex-container {
  -webkit-flex-wrap: wrap; /* Safari */
  flex-wrap:         wrap;
}
{% endcode %}
上边代码使子元素在多行显示，遵循从左向右从上到下的顺序。
{% code %}
.flex-container {
  -webkit-flex-wrap: wrap-reverse; /* Safari */
  flex-wrap:         wrap-reverse;
}
{% endcode %}
上边代码使子元素在多行显示，遵循从左向右从下到上的顺序。
默认值：nowrap
### flex-flow
这个属性是flex-direction和flex-wrap的简写形式
{% code %}
.flex-container {
  -webkit-flex-flow: <flex-direction> || <flex-wrap>; /* Safari */
  flex-flow:         <flex-direction> || <flex-wrap>;
}
{% endcode %}
默认值：row nowrap
### justify-content
justify-conten的作用是使子元素沿着container的主轴进行布局
{% code %}
.flex-container {
  -webkit-justify-content: flex-start; /* Safari */
  justify-content:         flex-start;
}
{% endcode %}
上边代码会使子元素会以左边界为起点进行布局
{% code %}
.flex-container {
  -webkit-justify-content: flex-end; /* Safari */
  justify-content:         flex-end;
}
{% endcode %}
上边代码会使子元素会以右边界为起点进行布局
{% code %}
.flex-container {
  -webkit-justify-content: center; /* Safari */
  justify-content:         center;
}
{% endcode %}
上边代码会使子元素会以中间为起点分别向左右进行布局
{% code %}
.flex-container {
  -webkit-justify-content: space-between; /* Safari */
  justify-content:         space-between;
}
{% endcode %}
上边代码会使子元素平均分配到container中，其中第一个元素和最后一个元素在container的边界上,然后中间的元素平均分配余下的空间。
{% code %}
.flex-container {
  -webkit-justify-content: space-around; /* Safari */
  justify-content:         space-around;
}
{% endcode %}
上边代码会使子元素平均分配到container中，与上一个不同的地方在于，第一个元素和最后一个元素不再靠到container边界上，第一个和最后一个元素均与边界有相当于其他元素之间空间一半大小的空间。
默认值:flex-start
### align-items
与justify-content的作用类似，只不过这一属性控制的是沿着穿越轴(cross axis)的元素的布局，在这里是垂直方向。
{% code %}
.flex-container {
  -webkit-align-items: stretch; /* Safari */
  align-items:         stretch;
}
{% endcode %}
子元素会被拉伸直到填充满container的高或宽，方向为cross start-->cross end
{% code %}
.flex-container {
  -webkit-align-items: flex-start; /* Safari */
  align-items:         flex-start;
}
{% endcode %}
子元素会同时被布局到cross start，如果高度不够填充满container的话也不会被拉伸。
{% code %}
.flex-container {
  -webkit-align-items: flex-end; /* Safari */
  align-items:         flex-end;
}
{% endcode %}
子元素会同时被布局到cross end，如果高度不够填充满container的话也不会被拉伸。
{% code %}
.flex-container {
  -webkit-align-items: flex-center; /* Safari */
  align-items:         flex-center;
}
{% endcode %}
子元素会同时被布局到穿越轴(cross axis)，如果高度不够填充满container的话也不会被拉伸。
{% code %}
.flex-container {
  -webkit-align-items: baseline; /* Safari */
  align-items:         baseline;
}
{% endcode %}
子元素会同时根据自己的基线进行布局。对于基线的具体定义：http://www.w3.org/TR/css-flexbox/#flex-baselines
默认值:stretch
### align-content
align-content会调整元素沿cross axis的布局方式，与justify-content沿max axis调整单独的元素的方式类似。
{% code %}
.flex-container {
  -webkit-align-content: stretch; /* Safari */
  align-content:         stretch;
}
{% endcode %}
上边代码会使子元素的行与行之间分配相同的空间。
{% code %}
.flex-container {
  -webkit-align-content: flex-start; /* Safari */
  align-content:         flex-start;
}
{% endcode %}
上边代码会使子元素的各行都向cross start进行靠拢。
{% code %}
.flex-container {
  -webkit-align-content: flex-end; /* Safari */
  align-content:         flex-end;
}
{% endcode %}
上边代码会使子元素的各行都向cross end。
{% code %}
.flex-container {
  -webkit-align-content: center; /* Safari */
  align-content:         center;
}
{% endcode %}
上边代码会使子元素的各行都向container中间靠拢。
{% code %}
.flex-container {
  -webkit-align-content: space-between; /* Safari */
  align-content:         space-between;
}
{% endcode %}
上边代码会使子元素的各行分散开，其中第一行向cross start靠拢,最后一行向cross end靠拢,中间各行则根据空间大小平均分开。
{% code %}
.flex-container {
  -webkit-align-content: space-around; /* Safari */
  align-content:         space-around;
}
{% endcode %}
上边代码会使子元素的各行分散开，与space-between的不同指出在于第一行元素和第二行元素不会向两边靠拢，而是和其他元素一样根据空间大小进行平均分布。
默认值:stretch
>Note:这个属性只有在container中的元素有多行时才会起作用。

## 4、flexbox item属性
### order
order属性的作用是决定container中元素的布局顺序。默认的顺序是根据元素添加到container中的顺序。
{% code %}
.flex-item {
  -webkit-order: <integer>; /* Safari */
  order:         <integer>;
}
{% endcode %}
container的子元素会根据order的值重新排列，而无需我们手动修改html代码。
默认值:0
### flex-grow
这个属性可以改变container中某个元素的大小，如果所有子元素有相同的flex-grow值的话子元素会以相同大小分布在container中，如果其中一个元素的flex-grow值大于其他元素，相对其他元素来说这个元素会根据空间大小占据更大的空间，而其他元素也会根据空间大小相应的占据更小的空间。
默认值:0
>Note:flex-grow不允许使用负数

### flex-shink
这个属性可以改变container中某个元素的大小，如果所有子元素有相同的flex-shink值的话子元素会以相同大小分布在container中，如果其中一个元素的flex-shink值小于其他元素，相对其他元素来说这个元素会根据空间大小占据更大的空间，而其他元素也会根据空间大小相应的占据更小的空间。值为0的话元素会以原始大小进行显示。
默认值:1
>Note:flex-shink不允许使用负数

### flex-basis
flex-basis属性的作用是设置子元素宽度，如果所有元素宽度相加大于container宽度的话其他元素会根据空间相应的减小尺寸。
{% code %}
.flex-item {
  -webkit-flex-basis: auto | <width>; /* Safari */
  flex-basis:         auto | <width>;
}
{% endcode %}
默认值:auto
### flex
flex是flex-grow, flex-shrink和flex-basis属性的简写。
{% code %}
.flex-item {
  -webkit-flex: none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ]; /* Safari */
  flex:         none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ];
}
{% endcode %}
>Note: W3C 鼓励使用简写形式。

### align-self
align-self属性可以设定单个元素的布局方式，同时它会覆盖掉之前align-items设定的布局方式。
{% code %}
.flex-item {
  -webkit-align-self: auto | flex-start | flex-end | center | baseline | stretch; /* Safari */
  align-self:         auto | flex-start | flex-end | center | baseline | stretch;
}
{% endcode %}
默认值:auto
>Note: auto值会先根据item的父级元素所设定的align-items的值进行设置，如果父级元素没有的话默认使用stretch。

**Note: float、clear和vertical-align属性对flex item没有影响，它们不会使其脱离文档流。**

翻译自:https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties