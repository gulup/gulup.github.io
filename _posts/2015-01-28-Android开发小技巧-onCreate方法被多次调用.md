---
layout: post
title: Android开发小技巧-onCreate方法被多次调用
categories: [android]
tags: [android,安卓,开发小技巧]
fullview: true
---

`Android`从发布到现在,已经多个年头了.   
Android的API也越来越多,系统也越来越完善.    
但开发过程中,难免会遇到一些大大小小的问题.      

**开发小技巧**系列,收录了一些Android开发过程中的一些问题以及解决方案.   
本篇是小技巧系列的`第一篇`.

<!-- more -->		

***

###onCreate方法被多次调用

在开发过程中,有时候会遇到,启动一个`Activity`的时候,Activity的生命周期重复调用.      
主要体现在onCreate等方法被重复调用2次或以上.

有时候这种情况不会被发现,而被忽略掉了.      
但却是一种安全隐患,如果在onCreate等方法中的一些方法或参数,被重复调用or初始化.   
这样就可能影响这个Activity的逻辑.   

而一般造成这种情况的原因呢,是因为手机横竖屏切换时造成的.    

即是说,当前手机界面是竖屏的.但是你的Activity的`screenOrientation`却并没有指定.  
即是由系统决定并改变当前Activity的方向时.这就很有可能触发多次调用onCreate的问题.    

特别是使用了`noTitle`的`style`的话.百分之90的情况下都会重复调用. 

***
* 解决方案

要解决这个问题也不难.   
首先,最简单的办法就是,指派Activity的`screenOrientation`,指定其为横屏/竖屏.      

但是如果你不想写死Activity的屏幕方向的话.   
那么,可以在`AndroidManifest.xml`中修改Activity的配置,添加以下内容:  
`android:configChanges=”orientation|screenSize|keyboardHidden”`

那么就可以解决onCreate被重复调用的问题了!.  

