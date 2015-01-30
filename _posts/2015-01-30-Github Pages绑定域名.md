---
layout: post
title: Github Pages绑定域名
categories: [other,web]
tags: [随笔]
fullview: true
---

折腾了一天,总算把Github Pages绑定我自己的域名给搞定了.      
新域名[gulup.cn](http://gulup.cn)       
顺便就写一下是怎么搞的吧.       

***
* 1-首先你要有个自己的域名(这不废话么..)
    
* 2-Ping下你的Github Pages的`ip`:     
    ![](http://gulup.github.io/public/img/20150130/1.jpg)  		

<!-- more -->

* 3-去你的域名提供商或者第三方DNS解析网站里面哪里添加解析,这里我使用的是百度云加速:       
    ![](http://gulup.github.io/public/img/20150130/2.png)		
    
    一般添加两个A记录,主机名填`@`和`www`就够了.其他的自己斟酌.

* 4-解析完之后,可以先ping一下看看是不是生效了:
    ![](http://gulup.github.io/public/img/20150130/3.jpg)		

* 5-之后就在你的Github Pages的项目的根目录下添加一个文件`"CNAME"`.    
    就叫这个名字,没有后缀什么的.里面填上你要绑定的域名,不需要添加`http://`      
    直接写域名就好了:
    ![](http://gulup.github.io/public/img/20150130/4.png)  		

    记得commit到github上.   
    然后来github的setting上看看
    ![](http://gulup.github.io/public/img/20150130/5.png)  		
     
    好了.完成了.然后就可以使用你的绑定域名打开Github Pages了
    
    