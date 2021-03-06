---
layout: post
title: Ajax操作XML文件节点的问题
categories: [web]
tags: [web,ajax,前端]
fullview: true
---

今晚在写Ajax的时候发现一个问题。

Ajax通过操作XML文件的时候，获取根节点上的所有节点

使用`getElementsByTagName(rootNode)[0].childNodes;`
返回的是根节点下的所有元素。

其中会包含换行，文本节点等所有元素。

而如果只想操作根节点下的子节点元素的话。那在非IE内核的浏览器上就会出现错误。

<!-- more -->

比如。我有如下XML：
<script src="https://gist.github.com/gulup/fff2d6ab3025ed6dc0a0.js"></script>

我用`getElementsByTagName(“allcity”)[0].childNodes;`然后添加到一个select上。
在ie上没问题。效果如下：

![](http://gulup.github.io/public/img/20120610/1.png)

但是在非ie的浏览器上，比如`chrome`和`opera`上，就会出现无法识别根节点上的子节点的内容：
![](http://gulup.github.io/public/img/20120610/2.png)

究其原因，是因为上面所说的。childNodes返回的是根节点下的所有节点。其中包含有换行，文本节点等。而根据下标来操作childNodes返回对象的节点的时候，标准操作是操作每一种节点的。而ie则自动帮你识别成操作元素节点。（非标准），而非ie内核的浏览器根据标准操作则会识别每一种节点。
想要根据下标来直接操作元素节点的话。得先判断一下是否一个元素节点。
以上面的XML文件为例：


<script src="https://gist.github.com/gulup/127633f5134a0bdcb697.js"></script>


其中nodeType的值1就代表元素节点。而2代表属性节点，3则代表文本节点。
使用判断后，chrome运行程序没有任何问题。

![](http://gulup.github.io/public/img/20120610/3.png)