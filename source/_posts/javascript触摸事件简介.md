title: javascript触摸事件简介
date: 2015-10-26 10:59:48
categories: [web前端, javascript]
tags: [javascript, touch]
---
## javascript触摸事件
在javascript中支持以下几个触摸事件:
1. touchstart,当用户触摸到屏幕表面时即触发这一事件,并在这一事件所对应的元素上创建一个“触摸点”。
2. touchmove,当用户在屏幕上移动“触摸点”时触发。
3. touchend，当用户“触摸点”离开屏幕时触发。
4. touchenter，当“触摸点”进入对应元素触发，不会冒泡。
5. touchleave,当“触摸点”离开对应元素触发，不会冒泡。
6. touchcancel，当“触摸点”不再被注册到触摸屏上时触发。
<!--more-->
这些事件可以绑定到任何元素上，并会自动传递一个包含“触摸点”细节的对象到事件函数中，利用element.addEventListener()来注册事件。
{% code %}
window.addEventListener('onload',function(){
    document.body.addEventListener('touchstart',function(e){
        alert(e.changedTouches[0].pageX) // alert pageX coordinate of touch point
    });
});
{% endcode %}
touchstart的回调函数中的event对象中包含了与触摸行为相关的所有信息。下边是一个将touchstart、touchmove与touchend相结合的例子:

<p data-height="268" data-theme-id="0" data-slug-hash="xwWNGY" data-default-tab="html" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/xwWNGY/'>xwWNGY</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

* e.preventDefault()的作用是防止触摸事件的默认行为的发生。对于touchstart和touchend来说，如果目标元素是一个a链接的话可以防止浏览器跳转到新页面，对于touchmove可以防止用户在目标元素内移动手指时使页面发生滚动。
* touchObj指代所有放到触摸屏上所有触发触摸事件的对象中的第一个“触摸点”，然后利用clientX获得“触摸点”相对于浏览器边缘的水平距离。通过在touchmove中使用可以获得每次移动的坐标相对于“触摸点”的水平相对距离。
* 即使手指离开事件绑定的元素，touchend依旧会触发并显示此时的x坐标。
## 触摸过程中的事件对象
1. changedTouches:包含了所有触发“触摸点”的触摸对象的集合，具体的有:
    1. touchstart,包含所有触摸到屏幕的所有“触摸点”
    2. touchmove,包含所有获得到“触摸点”后移动的对象
    3. touchend，包含所有将手指离开触摸屏的对象集合
    4. touchenter,包含所有在触摸事件中进入绑定元素范围的对象集合
    5. touchleave,包含所有在触摸事件中离开绑定元素范围的对象集合
2. targetTouches：一个包含绑定元素内部触发的触摸事件信息的集合
3. touches：所有“触摸点”的集合
4. altkey，布尔类型，表示在触摸事件发生时，是否按下alt。相似的还有ctrlKey、metaKey、shiftKey。
5. type,触发事件的类型
6. 触发事件所对应的目标元素

例如，在touchstart事件中，事件对象的touches属性可以获得目前所有的“触摸点”：
{% code %}
<script type="text/javascript">
        document.addEventListener('touchstart',function(e){
            var touchlist = e.touches;
            for(var i = 0;i < touchlist.length;i++){
                //do something with every touch point
            }
            e.preventDefault();
        });
</script>
{% endcode %}
触摸过程中每个触摸对象包含的属性:
1. identifier,可以唯一的代表某一个“触摸点”。起始值为0，每增加一个触摸点加1。加入你将两根手指放到屏幕上，这时就可以利用这一属性对每一根手指添加不同的事件。
2. screenX，用户“触摸点”相对于用户的设备屏幕左边缘的x坐标
3. screenY，用户“触摸点”相对于用户的设备屏幕上边缘的y坐标
4. clientX，用户“触摸点”相对于视窗左边缘的x坐标，不包括滚动条
5. clientY,用户“触摸点”相对于视窗上边缘的y坐标，不包括滚动条
6. pageX, 用户“触摸点”相对于视窗左边缘的x坐标，包括滚动条
7. pageY，用户“触摸点”相对于视窗上边缘的y坐标，包括滚动条
8. radiusX，触摸区域相对于x轴的椭圆区域的半径
9. radiusY，触摸区域相对于y轴的椭圆区域的半径
10. rotationAngle，由radiusX和radiusY所确定的椭圆区域绕中心点所转动的角度
11. force，返回加到触摸屏上的力量大小，数值为0-1
12. target，“触摸点”作用到的目标元素。

>Touches, changedTouches, 和 targetTouches之间的不同：Touches包含当前所有“触发点”的集合。changedTouches包含当前所发生的触摸事件的所有“触摸点”的集合，比如在一个touchmove事件中，changedTouches只包含当前正在move的“触摸点”，Touches则包含所有的“触摸点”，targetTouches只包含当前在绑定元素上触发的触摸事件。
>>When I put a finger down, all three lists will have the same information. It will be in changedTouches because putting the finger down is what caused the event
When I put a second finger down, touches will have two items, one for each finger. targetTouches will have two items only if the finger was placed in the same node as the first finger. changedTouches will have the information related to the second finger, because it’s what caused the event
If I put two fingers down at exactly the same time, it’s possible to have two items in changedTouches, one for each finger
If I move my fingers, the only list that will change is changedTouches and will contain information related to as many fingers as have moved (at least one).
When I lift a finger, it will be removed from touches, targetTouches and will appear in changedTouches since it’s what caused the event
Removing my last finger will leave touches and targetTouches empty, and changedTouches will contain information for the last finger

## 利用触摸事件移动元素

<p data-height="268" data-theme-id="0" data-slug-hash="OyvYVK" data-default-tab="html" data-user="chenzimu" class='codepen'>See the Pen <a href='http://codepen.io/chenzimu/pen/OyvYVK/'>OyvYVK</a> by chenzimu (<a href='http://codepen.io/chenzimu'>@chenzimu</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

参考自:http://www.javascriptkit.com/javatutors/touchevents.shtml

 
