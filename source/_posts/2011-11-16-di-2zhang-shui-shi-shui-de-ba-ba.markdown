---
layout: post
title: "第2章:谁是谁的爸爸"
date: 2011-11-16 20:57
comments: true
categories: 
---

##家谱
假设我们有这样一个家谱图：

!["alt"](/images/chapter2_1.png "family-tree")

我们现在的任务是将这个家谱图写成程序代码的形式。请打开你最喜欢的文本编辑器，输入以下代码。
	male(di).
	male(jianbo).
	female(xin).
	female(yuan).
	female(yuqing).
	father(jianbo,di).
	father(di,yuqing).
	mother(xin,di).
	mother(yuan,yuqing).
	grandfather(X,Y):-father(X,Z),father(Z,Y).
	grandmother(X,Y):-mother(X,Z),father(Z,Y).
	daughter(X,Y):-father(X,Y),female(Y).
这段代码里面的每一行都代表一个子句(clause)。其中带有“:-”的子句叫做规则(rule)，不带有":-"的子句叫做事实(fact)。另外，在Prolog里面诸如"di"和"jianbo"这类以小写英文字母开头的名称我们称它们为原子(atom)，以大写英文字母为开头的名称我们称它们为变量，例如上面程序里面的"X"和"Y"。顾名思义，原子是常量，即它的值是不可变的，而变量的值可以改变。最后需要讲的是，在Prolog里面","代表逻辑关系中的"且"，我们回在后面的章节里面看到，";"代表逻辑关系里面的"或"。

已经被这些名称搞得头晕了？没关系，我会在之后的教程里面详细的介绍Prolog的数据类型和术语，在这里，你只需有初步的了解即可。

保存上述代码到你的磁盘的某个地方，例如在Mac系统里，我把它存到“～/prolog/chapter2.pl”,然后依照第一章里面讲的那样，进入SWI-Prolog。在SWI-Prolog里面输入如下查询：
	?- consult('path/to/your/chapter2.pl').
在我的电脑里，我应该这么输入：
	?- consult('~/prolog/chapter2.pl').
这里"consult"的意思是让SWI-Prolog加载你编写的程序，然后编译它。输入完这句查询以后，敲击回车键，你应该得到如下输出：
	% /Users/fengdi/prolog/chapter2.pl compiled 0.00 sec, 3,816 bytes
	true.
如果你得到了上述的输出，那么恭喜你，你的第一个程序完成了。如果你得到的是其他的错误的输出，请重新检查你的程序代码是否输入正确(不过要记得，千万不要因为想要保证代码输入的不出错而直接复制粘贴代码，那样的话你学不到真正的东西)。下面，让我们考验一下我们的SWI-Prolog现在都知道些什么。在SWI-Prolog里面输入下面一个查询：
	grandfather(X,yuqing).
令人惊讶的事情发生了！你得到了下列输出：
	X = jianbo.
你的电脑告诉你，"yuqing"的祖父是"jianbo"。现在请看之前我们编写的"chapter2.pl"程序代码，我们在程序里根本没有明确的说明谁是谁的祖父，我们只是给了一个规则：
	grandfather(X,Y):-father(X,Z),father(Z,Y).
我们说，当X是Z的父亲并且Z是Y的父亲的时候，X是Y的祖父。然后我们问，yuqing的祖父是谁，Prolog就能自动帮我们找到答案！

下面再看一个例子：
	parent(keyuan,jianbo).
	parent(jianbo,di).
	parent(di,yuqing).
	
	ancestor(X,Y):-parent(X,Y).
	ancestor(X,Y):-parent(X,Z),ancestor(Z,Y).
在这个例子里面，我们定义了一个回溯的规则"ancestor"，规则可以这样解读：我们可以说X是Y的祖先基于两个条件：X是Y的parent，或者存在一个Z，使得X是Z的parent并且Z是Y的祖先。请读者仔细的想一下，是不是这个道理呢？为了证明我们的程序的正确性，我们输入一下查询：
	?- ancestor(keyuan,yuqing).
Prolog会返回：
	true.
这证明了我们的程序是正确的，因为根据常识，keyuan是yuqing的曾祖父，所以keyuan是yuqing的祖先。

好了，今天的新内容就讲到这里，下面是一个习题，你可以自己试验一下。

##加分习题
1. 试着用Prolog描述一下你的家谱，并且做一些简单的查询。(小提示：在编写你的家谱的时候，你可以试着用一些新的事实，比如:"sister(your_sister,you)""brother(your_brother,you)"等等）