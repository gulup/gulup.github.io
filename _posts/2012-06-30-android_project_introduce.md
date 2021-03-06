---
layout: post
title: android的项目结构和基本组件介绍
categories: [android]
tags: [android,安卓]
fullview: true
---

创建一个新的android项目的时候，会生成很多的文件夹。这些文件夹分别都有什么作用呢？

下面就来简单介绍一下。还是上一篇博文的HelloWrold项目。项目结构如下：

![](http://gulup.github.io/public/img/20120630/1.png)

由上而下，最重要的文件夹有以下几个：
`src`目录里面存放的是我们自己编写的java文件。

`gen`目录里面存放的是系统自动生成的Java文件，我们不必去改动，特别是`R.java`这个文件。

R.java是ADT工具根据你的应用中现有的资源文件去自动生成相对应的代码。
然后到下面的bin文件夹。里面存放的是编译好的各种资源，包括根据java文件编译好的class类文件和和res目录下面的各种图标文件等。

`res`文件夹，里面存放的是程序用到的所有资源文件，包括有应用用到的图标，图片，布局文件等。

<!-- more -->

项目根目录下面的`AndroidManifest.xml`这个xml文件。是程序的清单文件。
这个文件是每个程序都必须有的。里面标注了程序的名称，使用到的图标还有使用到的组件等等。
上面的就是项目结构的简单说明，其中的东西，以后会详细说明，

开发一个`android`程序不单单要认识程序的项目结构，还要知道程序开发中会使用到那些必要的基本组件。
上面说过。AndroidManifest.xml里面标注了程序的名称，使用到的图标还有使用到的组件等等。
下面就来简单介绍下android开发中的基本组件。

##Activity and View

`Activity`是android的程序里面的人机交互组件。类似于java里面的swing里面的jFrame.
通过添加各种组件来达到现实的效果。

`View`是android里面的各种容器控件，UI组件的父类。View就是你打开程序的时候真实看到的部分。
View可以通过结合Activity，使用Activity的`setContentView()`方法。把View显示出来。

来看下HelloWorldActivity.java里面的代码：

<script src="https://gist.github.com/gulup/f891334525f5f87e715f.js"></script>

`R.layout.activity_hello_world`这个对象是View的间接子类。

里面的`setContentView(R.layout.activity_hello_world)`;这个方法把`R.layout.activity_hello_world`这个对象显示出来。

程序就会打印HelloWorld在屏幕。
可以发现，还是和java的gui编程有很多相似之处的。

要使用Activity组件的话，就需要继承Activity这个类。
HelloWorld这项目的HelloWorldActivity.java就是继承的Activity类。

##Intent

`Intent`在android程序里面的作用不可谓不大。
程序间的数据访问可以使用ContentResolver。那么一个程序里面的各种组件之间的通信呢？
没错，就是需要Intent.

开发过web的兄弟知道，如果从一个Ahtml页面跳转到Bhtml并且传递数据方式有很多，最简单的就是重写url提交表单了。
而Intent的作用就类似。有两个Activity，A和B,你要再A启动B，并传递数据到B时，就要用到使用Intent了。

##Service

`Service`这个组件一般不作用于UI界面。因为他不需人机交互，人机交互的功能一般都Activity完成。

所以Service一般都运行于后台。它的作用是用于监控其他组件的运行状态和未其他组件提供后台服务等。
跟Activity一样，要想使用Service组件，必须继承Service类。

##BroadcastReceiver

`BroadcastReceiver`翻译过来就是广博消息接受器。

BroadcastReceiver的作用和一般的编程中的事件监听的功能类似。
但BroadcastReceiver监听的不是对象，是程序中的其他组件。

使用BroadcastReceiver也必须继承BroadcastReceiver类。
(后面详细说明)

##ContentProvider

`ContentProvider`是一个很好玩得组件。。java编程里面，每个程序都有一个进程和一个或多个线程。

而两个程序之间需要交换数据的话，可以通过数据库啊，本地文件啊等等的方法。
而android程序呢，每一个android程序运行的时候，都会开启一个新的Dalvik虚拟机（android程序的虚拟机，功能类似jvm）

而两个或多个程序之间需要传递数据的话。就要用到ContentProvider这个组件了。

比如A程序，需要访问B程序的数据，那么B程序就必须使用ContentProvider来打开我的数据入口，而A程序必须使用ContentResolver来访问B程序的数据。

上面的只是简单的组件介绍。更详细的以后会详细说明。

