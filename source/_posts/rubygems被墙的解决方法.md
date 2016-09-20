title: rubygems被墙的解决方法
date: 2016-02-22 14:10:17
categories: [web前端]
tags:   [ruby,sass]
---
今天在安装sass的时候碰到了一个问题，就是rubygems死活连不上，于是花了5块钱买了个shadowsocks账号结果还是连不上，这样sass还是没法安装，于是google了一下发现淘宝提供了一个cdn的地址。具体使用方法如下:
<!--more-->
## 可以先尝试翻墙，如果可以的话就不用下边这个方法了
## 利用淘宝提供的镜像
**在命令行中输入下边代码**
{% code %}
gem sources --remove https://rubygems.org/
gem sources -a https://ruby.taobao.org/
{% endcode %}
**利用下边的代码查看目前所有的source**
{% code %}
gem sources -l
{% endcode %}
**添加完成之后再用命令安装sass即可**
{% code %}
gem install sass
{% endcode %}