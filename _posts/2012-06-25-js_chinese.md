---
layout: post
title: js向后台传中文乱码的解决办法
categories: [web]
tags: [web,js]
fullview: true
---

今晚练习Ajax验证注册的时候遇到一个问题。

js向后台post验证用户名的时候，传递的参数是中文的话，去到后台就会乱码。

例如表单得到:

<script src="https://gist.github.com/gulup/f992fde4315971debd4a.js"></script>

此时，在后台打印username的值就变成了？？？？

<!-- more -->

百度了一下，解决方法各异。

我用的是这种：

<script src="https://gist.github.com/gulup/0c62fcd3b7ab1f493c6b.js"></script>

然后在后台就这样：

`String username = java.net.URLDecoder.decode(request.getParameter("username") , "UTF-8");`

这样传递的乱码问题就能解决了。

附带一个小问题。是刚发现的。

我用response输出返回的字符串”false”和”true”来判断是否已经存在用户名。

发现，后台的输出的确没错，一直都是输出“true”。到了jsp上，也alert(xmlHttp.responseText)看了下，得到的结果也的确是“true”.

但是js上判断if(“true”==xmlHttp.responseText)却一直是false.

后来发现原来问题出在response.getWriter()的输出方法上。我用了println();

多了个换行。alert()输出却不能发现。纠结。