---
layout: post
title: android的输入密码明文显示.
categories: [android]
tags: [android,安卓]
fullview: true
---

之前用过一个软件，忘记是啥了。

里面有个显示密码的按钮，按下就明文显示密码。松开就密文显示密码。

这个东西比起CheckBox其实更方便。CheckBox控制密码的显示方式，切换的时候还需要按两次。

用Button控制显然轻松的多。也更符合密文显示密码的要求。
于是自己就写了一个Demo。

<!-- more -->

先看布局文件，就一个TextView,一个EditText和一个Button而已。

<script src="https://gist.github.com/gulup/75c9af417d396567b311.js"></script>

只是为了演示，没有吧string写在xml里面。正常开发不推荐这样做。
上面的EditText设置了android:password=”true”。默认密码为密文显示。

就是”*****”这样的效果

具体实现类：

<script src="https://gist.github.com/gulup/53277e7d4b16f7591c09.js"></script>

下面是效果图：

![](http://gulup.github.io/public/img/20121206/1.png)

按钮按下之后：

![](http://gulup.github.io/public/img/20121206/2.png)

