---
layout: post
title: Android布局加载流程浅析
categories: [android]
tags: [android,安卓,布局]
fullview: true
---

最近在思量[gCore](https://github.com/gulup/gCore)里面的控件初始化功能.      
是否能有别的方式进行空间的分辨率适配,和初始化优化工作.      
于是便顺便记录下`Activity`初始化过程和`setContentView`.设置`Activity`的布局过程.   

!<-- more -->   

***

##布局加载and控件初始化流程     
每个Activity的界面布局都是写在一个xml文件中,然后我们调用了`setContentView`这个方法.     
最后我们写好的布局就会呈现在界面上.那么到底这里面都经历了一些什么呢?

我们跟踪源码来一步一步看看,先来看看setContentView方法:  

<script src="https://gist.github.com/gulup/964d67aa6b4f7a7e1677.js"></script>       

可以看到,setContentView这个方法,其实不是Activity里面实现的.是通过`getWindow`返回的对象调用的方法.       

再来看看`getWindow`跟它的相关方法:        

<script src="https://gist.github.com/gulup/40add7c5d0e9035fa4c1.js"></script>

getWindow方法返回一个`Window`的之类对象.该对象在`attach`方法里面通过`PolicyManager.makeNewWindow(this);`初始化.     

`PolicyManager`,通过普通方法,跟不进去源码,因为这个是SDK的隐藏API.我们打开下面的路径跟进去看看:      
`your sdk path\sdk\sources\sdk_version\com\android\internal\policy`     
通过上面的路径就可以找到这个类,前提是你的SDK有下载源码.没下载的点开SDK Manager下载:     
![](http://gulup.github.io/public/img/20150202/1.jpg)   

打开`PolicyManager`查看,很遗憾,现在新的SDK里,源码都被屏蔽了..:      
<script src="https://gist.github.com/gulup/2dabdeed92a79222b425.js"></script>    

不要紧,通过查看资料和旧的SDK,可以看到原本因该是这样的:      
<script src="https://gist.github.com/gulup/25d3fb494a3c2f4b6a1b.js"></script>       
可以看到,其实最后是通过`IPolicy`接口的实现类调用的`makeNewWindow`.      
查了一下,发现最终的实现类是`Policy`类:      
<script src="https://gist.github.com/gulup/75a17933757b22c69b07.js"></script>       
有点绕啊.我们再来看看`PhoneWindow`这个类,最后找到,setContentView的实现其实是在这里:          
<script src="https://gist.github.com/gulup/e5f257ec9016bf686665.js"></script>       

我们来分析下这个方法的逻辑,上半段的判断逻辑不是我们本篇的讨论范围,所以简单说一下.       
`DecorView`是整个Activity的一个根View.我们的布局文件生成的View最终都会在这个View的底下展开.     
所以,当`mContentParent`为空时,会调用`installDecor`这个方法,初始化`DecorView`和`mContentParent`.         
如果不为空时,就删除所有在根节点上的所有View.然后再去添加我们的布局的View.       

布局的初始化的重点在于`mLayoutInflater.inflate(layoutResID, mContentParent);`       

`mLayoutInflater`是`android.view.LayoutInflater`        

可以回到eclipse跟踪下源码了,可以看到这个方法一开始的实现是这样的:       
<script src="https://gist.github.com/gulup/4f015aa7218c293fbbac.js"></script>  

`parser`就是我们传入的布局文件的xml对象了.再来看看里面的具体实现:       

<script src="https://gist.github.com/gulup/f725f02a30fd95e39e4b.js"></script>       

看着有点长,其实最后每个空间的初始化是在这里`rInflate`:      

<script src="https://gist.github.com/gulup/2f646e534a9722b7bcc0.js"></script>       

这个方法通过循环遍历xml文件,并根据每个元素的attr,去初始化每个控件.      
其中可以查看`viewGroup.generateLayoutParams(attrs)`,一路跟进去:     
<script src="https://gist.github.com/gulup/38fe714d782721e4a2f7.js"></script>       
看到熟悉的属性了吧.就是宽高属性.其他居中什么的属性,就不说了.        

最后,当布局加载完毕之后,我们回到`setContentView`方法里面看:     
`cb.onContentChanged();`        
最后就会调用这个回调,通知界面发生变化.而这个CallBack.其实就是Activity本身实现的.        

好了.布局加载的流程,简单的分析了一遍.那么,是否可以在其中做一些什么呢?       
下一遍写写看,怎么修改下gCore的界面初始化逻辑.

