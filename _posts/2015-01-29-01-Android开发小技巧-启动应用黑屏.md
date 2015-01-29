---
layout: post
title: Android开发小技巧-应用启动时黑屏/白屏
categories: [android]
tags: [android,安卓,开发小技巧]
fullview: true
---

**开发小技巧**系列,收录了一些Android开发过程中的一些问题以及解决方案.   
本篇是小技巧系列的`第二篇`.

<!-- more -->    	

***

###启动应用时白屏/黑屏

在开发过程中,有时候可能会发现,启动应用的时候,会先黑屏/白屏(取决于你是用的`theme`)     
然后才会显示启动`Activity`的界面.     

但是呢,因为现在的手机的硬件越来越高,系统优化越来越好.      
导致启动的时候,这个闪动的过程很有可能被忽略掉.所以呢,开发过程中也可能被开发人员忽略掉了     

但是呢,这种闪动的情况呢,实际上是非常影响应用体验的.     

那么是什么原因造成这种情况的呢?     
究其根本呢,是因为Activity的生命周期执行到`onResume`这个方法时,才会开始与用户交互和展示布局给用户看.       
而`onCreate-onResume`这个生命周期期间的代码执行时间,就会导致了会先出现一个全黑/全白(取决于你的theme)先展示在界面上的结果.     

在此多提一句,在onCreate方法中,是不应该写太多的代码的,逻辑代码都应该放到其他地方处理,onCreate中应该只做ui控件的一些简单的初始化处理.     

***

* 解决方案      

要解决这个问题也不难.首先,在`res/values/styles.xml`中添加一个`style`.内容如下:

<script src="https://gist.github.com/gulup/fa94d734603813207623.js"></script>

`name`跟`parent`取决于你自己的style.    
其中两个`item`的作用就是全透明,消除title.   

然后在`AdnroidManifest.xml`中设置你的启动Activity:

<script src="https://gist.github.com/gulup/266ea24f224543561b4d.js"></script>

再次启动你的应用看看.问题就解决了.      

还可以在style中添加一个item:    
` <item name="android:background">your background img</item>`

这样的话,启动的时候,第一时间就会展示item设置的背景图片了.

