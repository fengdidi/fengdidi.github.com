---
layout: post
title: "第1章:配置开发环境"
date: 2011-11-15 20:08
comments: true
categories: [Prolog]
---

这道习题几乎没有代码内容，它的主要目的是让你在计算机上安装好Prolog。你应该尽量照着说明进行操作。

##安装SWI-Prolog
###MacOS
1. 找一个你最喜欢的文本编辑器。在Mac系统下，TextMate也许是最好的选择，但是它是需要花钱购买的，如果你不想买的话，可以使用一些免费的文本编辑器比如Kod。需要注意的是，这写编辑器本身都是不支持Prolog代码高亮的，如果你想要这个功能，你需要下载针对这些文本编辑器的插件，其中TextMate的插件可以在这里下载到[TextMate Bundle](http://netcetera.org/cgi-bin/tmbundles.cgi "Title")
2. 下载[SWI-Prolog](http://www.swi-prolog.org/download/stable "Title")，请选择适合你系统版本的链接。下载解压之后双击安装包，等待一段时间以后，你的Prolog就安装好了。SWI-Prolog是Prolog的一个实现，作者是来自阿姆斯特丹大学的Jan，之所以选择这个Prolog实现作为开发的环境，一个原因是因为它很稳定，运行速度也算是可以，更重要的原因是它的开发文档写的很详细。这个Prolog的实现不是功能最多的，但是我个人认为是最好用的，也是最适合Prolog的初学者使用。
3. 当你安装好Prolog以后，进入命令终端，输入：<pre><code>swipl</code></pre>你应当看见下图：
!["alt"](/images/chapter1_1.png "title")

###Windows
1. 第一步同样是找一个自己喜欢的文本编辑器，个人推荐Notepad++，你可以轻易的在Google上搜寻到下载地址。
2. 下载[SWI-Prolog](http://www.swi-prolog.org/download/stable "Title")，选择Windows的安装包，下载解压之后双击安装包，等待一段时间以后，你的Prolog就安装好了。
3. 与MacOS不同的是，在Windows下，你可以不必去命令行下面输入"swipl",你可以直接双击桌面上的快捷方式就可以打开SWI-Prolog了。打开以后的界面应该和MacOS下的界面类似。

###Linux
我相信使用Linux系统的朋友应该都懂得如何安装一个小小的软件吧？所以在这里就不赘述了～

##Hello World!
好像在大部分的程序语言的时候，第一个要编写的程序都是“Hello World!”。虽然“Hello World”程序不能显示出Prolog的特性，我在这里也姑且做一个“Hello World!”的程序吧，目的是让大家试一下你们刚才下载的SWI-Prolog是否工作。

按照之前的方法进入SWI-Prolog，在命令行下输入：
	writeln('Hello World!').
需要注意的是，这行代码一定要以英文中的句号"."来结尾，Prolog中的“.”和C语言中的“;”一样，都是代表一段代码的结尾。再者，Hello World!字符串一定要以单引号来包裹。
如果输入正确的话，你将看到如下输出：
	Hello World!
	true.
这里的“Hello World!”很好理解，这是我们要求程序输出的，那么那个奇怪的“true”是哪里来的呢？请注意，在Prolog终端输入的时候，没一个语句都是以“?-”这样两个字符开头的，它代表我们输入的程序代码其实是对Prolog系统的一个查询（问询），一旦用户输入了查询，Prolog系统会运用它的知识库来判定这个查询是真(true)是假(false). writeln是Prolog系统自己定义的一个语句, 它的作用是向当前的显示设备输出一个字符串并且换行, 所以很显然, 这个语句是真的, 因为Prolog知道有这个语句. 这就是为什么程序的最后有一个"true". 有意思的是,因为整个过程中Prolog都是在试图证明这个语句是真是假, 向屏幕输出"Hello World!"这件事实际上是执行这个语句的"副作用"(side effect)!在Prolog中, 很多任务都是靠副作用来实现的, 包括输入输出, 甚至是参数的传递.

好了, 到这里, 这一章就算是结束, 因为这一章讲的内容很基本, 我就不提供习题了. 下一章我们将正式开始学习有关Prolog语言的知识! 敬请期待!