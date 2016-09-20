title: em和rem简介
date: 2015-11-12 12:38:44
categories: [web前端, css]
tags: [css, em ,rem]
---
em和rem两个单位都是根据页面中的字体大小来决定其他元素的属性大小，如padding、margin等，这两个单位给我们带来了很多的灵活性，但是它们也有一些不同的地方。
<!--more-->
## rem
对于rem来说，元素各个属性的大小是根据根结点（通常指html元素）的字体大小来决定的。假如html字体的大小为16px，而一个div的字体大小设置为18px，该div的padding设置为10em,则浏览器就会将其padding解析为160px。
## em
对于em来说，元素各个属性的大小是根据当前元素的字体大小来决定的。假如html字体大小为16px，一个div的字体大小设置为18px，该div的padding设置为10em，则浏览器会将其padding解析为180px。
## 继承对于em的影响
对于一个元素如果没有设置font-size的话，它会继承父级元素的字体大小，所以这给em的运用带来了一些容易出错的地方。
### 例子
假如有一个页面html的默认字体大小为16px,在页面中添加一个div，给该div添加padding值为2em，由于该div没有设置font-size，那它会继承html元素的字体大小16px，相应的它的padding会被解析为32px----2*16
<p data-height="268" data-theme-id="0" data-slug-hash="qOLWEz" data-default-tab="result" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/qOLWEz/'>qOLWEz</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
如果在上个例子的基础上在div外层添加一层div并将其font-size设置为2em，所以外层div的字体大小就被解析为32px，而内层div不再继承html字体的大小，而是继承外层div字体大小32px，此时内层div的padding值变为32 * 2 = 64px。
<p data-height="268" data-theme-id="0" data-slug-hash="KdbPpQ" data-default-tab="result" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/KdbPpQ/'>KdbPpQ</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
再进一步，给内层div设置font-size为1.5em,此时内层div由于设置了font-size，则该div自身的字体大小会变为1.5 * 32 = 48px，而padding则会根据该div自身的font-size被解析为48 * 2 = 96px。
<p data-height="268" data-theme-id="0" data-slug-hash="MaZgaB" data-default-tab="result" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/MaZgaB/'>MaZgaB</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

>>从上边的例子可以看出只要某个元素自身设置了font-size的值就不会再继承父级的font-size大小了，其自身各个属性的值如果单位为em的话，它们的参考值均为font-size的大小。
