---
layout: post
title: J2ME上的script-各种脚本引擎的介绍和在游戏中的应用(1)
categories: [j2me]
tags: [j2me,game,rpg,游戏]
fullview: true
---

脚本语言，相信大家都不陌生。

j2me上开发游戏，脚本的使用还是挺广泛的。

甚至，能用一个脚本去写一个游戏，而程序主体只需要控制重绘。

当然，需要你有这样的功底，设计好游戏的引擎。


j2me上的脚本引擎也有不少，我在找这些引擎的时候，就搜索到很多，什么`Fscript` ，`Gscript`的，这样的脚本引擎真不少。

但是，相信最多人知道的就是使用`lua`的`kahlua`这个引擎了，这个引擎最后更新在2009年。是开源的。

熟悉lua的，只需要把引擎配置在项目里，就可以只用lua去做各种操作。

<!-- more -->

但是，可能是我笨吧，我使用起来感觉有点力不从心。

所以本文不多介绍`kahlua`，关于`kahlua`的介绍和项目源码下载，请自行百度吧。

 

我要详细介绍的是国人创作的几个引擎。这几个引擎，能搜索到的资料都很少很少。

首先说说一位名叫CoCoMo的大大的`ScriptEdit`这个引擎。

这个引擎的最新版本是2.0的，使用的脚本是作者原创的类C的一种脚本，用起来确实方便，引擎还带有编译器，把脚本编译成二进制文件

但是可惜已经很久没有更新过了。这个引擎的资料也很少，找到这个引擎的时候只能看作者的示例脚本和引擎源码去分析脚本的操作原理。

 

第二个是叫xiaoxin的大大开发的`SnakeScript`。

Snake的最新版本是1.2。跟ScriptEdit很类似，而且使用起来更简便。可以并发运行脚本，动态设定脚本优先级。动态加载和卸载脚本。

而且这个引擎还带有引擎和脚本的帮助文档，使用起来简便多了。

 

最后一个叫`DreamScript`，是国内一位开发工作者姜赫姜老师的个人作品，这个引擎的语法和引擎与脚本之间的调用都比较成熟。

关于姜老师的DreamScript，大家可以去他的博客看看他的详细介绍，毕竟原作者写的介绍，肯定比起我这个使用者写的要深刻得多。

而且姜老师的博客里的文章都能给你提供不错的思路。（虽然讲的实质内容东西很少。。。）

姜老师的blog：
(失效了~~)

以上三个引擎都是开源的，本文只是简单介绍下以上三个引擎，下一篇会给出ScriptEdit和SnakeScript的下载和详细介绍ScriptEdit和SnakeScript的示例使用，和在游戏中的作用。

至于DreamScript，大家可以发邮件给姜老师，我会先征得姜老师的同意才放出下载。毕竟姜老师也没有在他的blog放下载。。（囧）