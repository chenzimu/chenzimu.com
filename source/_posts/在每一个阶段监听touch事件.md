title: 在每一个阶段监听touch事件
date: 2015-10-28 09:47:53
categories: [web前端, javascript]
tags: [javascript, touch]
---
之前的swipeDetect函数有一个缺点，即该函数只能在整个手指滑动过程结束之后才能判断出滑动的方向，之后再调用回调函数。在此将其改进一下，当手指在start、move以及end使都可以触发回调函数，这样利用起来将更加灵活。

<!--more-->
## 改进的ontouch函数

<p data-height="268" data-theme-id="0" data-slug-hash="eprvZY" data-default-tab="html" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/eprvZY/'>eprvZY</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

>在touch事件的每一个阶段--'touchstart'、'touchmove'和'touchend'，均获取“触摸点”的方向以及移动距离，在'touchend'阶段遵循与swipeDetect函数相同的规则来判断手指的触摸方向。

## 图片滑动例子

<p data-height="268" data-theme-id="0" data-slug-hash="KdRWXO" data-default-tab="html" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/KdRWXO/'>KdRWXO</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

参考自:http://www.javascriptkit.com/javatutors/touchevents.shtml


