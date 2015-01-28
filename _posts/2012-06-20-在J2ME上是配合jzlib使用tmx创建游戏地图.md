---
layout: post
title: 在J2ME上是配合jzlib使用tmx创建游戏地图
categories: [j2me]
tags: [j2me,game,rpg,游戏]
fullview: true
---

Tiled制作的tmx文件的容量较小。是游戏中使用外部地图数据的首选啊。
Android和ios上的很多引擎都支持直接使用Tiled制作的tmx地图文件。
但是J2me上没有，起码我是没找到。。

没办法，去看了下Tiled的源码，然后copy了下里面的代码。自己搞一个咯。
Tmx地图文件有几种数据压缩方式，有`Gzip`，`Zlib`等等。
其中使用Zlib压缩的tmx文件的容量是最小的。
!more!

一个16x16图块大小，40x40大小的地图，分4层保存数据。地面层，对象层，天空层，事件层，或者还有第五第六层。
只保存使用到的数组，保存成txt的话，需要30k或更多，如果地图大一点的。。那就更不敢想象了。

而如果使用tmx的话只需要3k不到。
Tmx文件其实是一个标准的xml文件。里面有各种节点。保存着关于地图的各种数据。而我们在me上操作嘛。最基本的，只需要里面的data数据罢了。
这里的数据指的是地图使用到数组。
而Tiled的压缩还包含了base64的加密
工作原理应该是这样：
保存地图数据>Zlib压缩数据>Base64加密数据。
读取地图数据>Base64解密数据 >Zlib解压缩数据。
而j2me上并没有Zlib这个类。我们可以使用jzlib这个开源的项目。这个项目支持j2me上使用Gzip和Zlib压缩和解压缩数据。
具体的功能可以下载项目源码自己看看。

来制作个test地图来试试。例如：测试地图使用的地图数组是。我们就要在程序里面读取地图文件获取到这个数据：
1,2,3
4,5,6
7,8,9
看图：

![](http://gulup.github.io/public/img/20120620/1.png)

设置里面记得要选择保存为Zlib:

![](http://gulup.github.io/public/img/20120620/2.png)

完了之后保存好tmx文件，里面的内容如下：

![](http://gulup.github.io/public/img/20120620/3.png)

我们要用到的是data里面的信息：

![](http://gulup.github.io/public/img/20120620/4.png)

有人可能会说了，你本来只有9个数字，怎么压缩了反而变多了。。

不用急。。数据量小的时候你看不出他的特点。。我只是测试下而已，当你实质使用的时候，地图数据就不止9个数字了。。。那就看出压缩效果了。。。

说回来正题。。

Tmx文件保存之后，xml文件不能直接解析，因为里面我们只需要用到data的数据。其他可以不要。所以可以修改下tmx文件。当然，你可以自己操作xml标签节点，那就不用修改了。也可以自己写一个操作类。把data标签里面的文本节点截取出来就好了。新的sdk里面好像更新了很多xml的api，我也没具体去看。亲们自己定吧。

我还是修改下好了。把里面不要的东西都删除掉：

![](http://gulup.github.io/public/img/20120620/5.png)

Ok,数据进一步减小了。嘿嘿。

我从Tiled的源码里面copy了些代码下来，加了几句代码，写了个unZlib类，里面有个方法，根据你给出的地图大小，返回二维byte数组的。当然，使用的方法有很多，你也可以直接在tmx里面留下地图大小的数值，直接读取。

我的做法是把数值放在脚本里传递的。

看代码吧：

<script src="https://gist.github.com/gulup/6f805ec43ab3ca40cf2d.js"></script>

上面的代码基本都是copy了Tiled的代码的。不要鄙视我。能copy为什么不copy呢？对吧。

unTmx方法里面直接仿照Tiled里面的方法写的。这里面只用到了Base64里面的解密数据的方法，至于压缩Zlib数据的方法和其他的东西，可以自己去看Tiled的源码。

这里面的ZInputStream就是jzlib里面的类，用法跟javase的InflaterInputStream一样，具体的可以参照se的InflaterInputStream和查看jzlib的代码。
来看下测试的结果，Test一段代码，把地图数据直接传递看看：

<script src="https://gist.github.com/gulup/bc2e6736f78667a25b8b.js"></script>

程序后台输出：
![](http://gulup.github.io/public/img/20120620/6.png)

很好，把地图数据全部还原了。

数据能拿到了。那么游戏里面就能画地图了。呵呵。

到底是用tmx还是使用txt呢？还是自己写一种地图文件，让自己的游戏来解析呢？这个因人而异啦。

其实如果地图数据并不是太多的话。个人觉得使用txt也没啥。30k的txt,jar包打好之后并没有明显增加jar包的体积。里面的数据会被压缩。30k，只压缩到1k左右。

使用tmx只是方便点使用tiled制作的地图文件罢了。

亲们自己取舍吧。
