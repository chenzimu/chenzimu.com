title: 用javascript的touch事件实现滑动
date: 2015-10-27 09:14:30
categories: [web前端, javascript]
tags: [javascript, touch]
---
首先我们先定义一下究竟什么样的行为算是一次滑动，当手指朝某一方向划过屏幕触发'touchstart'和'touchend'事件之后，有两个变量值可以供我们使用：一个是手指滑动的距离，另一个是手指滑动的时间。通过这两个值的变化我们就可以确定是否为滑动事件以及滑动的方向了。
<!--more-->
## 向右滑动例子
这里我们以向右滑动为例，我们约定，当手指在200ms时间内由左向右水平移动至少150px的距离时视作一次向右滑动。同时还要设置一个垂直方向的100px以内的移动距离，避免当用户在向右上方滑动手指时不被判断为右滑动。

<p data-height="268" data-theme-id="0" data-slug-hash="OyvGga" data-default-tab="html" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/OyvGga/'>OyvGga</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>


## 滑动检测函数完整版

<p data-height="268" data-theme-id="0" data-slug-hash="zvWXpo" data-default-tab="html" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/zvWXpo/'>zvWXpo</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

参考自:http://www.javascriptkit.com/javatutors/touchevents.shtml





