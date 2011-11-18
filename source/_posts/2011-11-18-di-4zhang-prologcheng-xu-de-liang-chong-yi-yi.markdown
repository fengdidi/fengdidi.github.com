---
layout: post
title: "第4章:Prolog程序的两种意义"
date: 2011-11-18 19:24
comments: true
categories: 
---

###单词谜题
在进行下一章之前，我想先把上一章加分习题的第二题答案给大家揭晓一下，因为台北小码农给我反应说这一道题有点难了，连学过Prolog的人都不一定会做。确实，这是一道难题，但是这道题的难点不在于程序本身逻辑上的复杂或者是用到了什么高级的语法，这道题的难点在于你必须要清楚地理解Prolog程序的意义才能得出答案。好了，先给大家看一下答案的程序：
	solution(L1,L2,L3,L4,L5,L6,L7,L8,L9,L10,L11,L12,L13,L14,L15,L16):-
		word(L1,L2,L3,L4,L5),
		word(L9,L10,L11,L12,L13,L14),
		word(L1,L6,L9,L15),
		word(L3,L7,L11),
		word(L5,L8,L13,L16).
以上就是这个单词谜题的答案。在编写Prolog程序的时候，之前有编程基础的朋友一定要摒弃之前编程的习惯，因为像C,Java这样的程序语言，程序员解决问题的方式实际上是把解决问题的步骤用程序一步一步地表示出来。换句话说，就是程序员要用程序语言告诉电脑应当怎样一步一步地做，才能找到问题的答案。Prolog不是这样，Prolog程序员让程序解决一个问题时，只需要把想要得到的答案的形式表述出来，Prolog系统会自动帮你找答案。就像上面这个程序一样，你告诉Prolog系统，答案应该是什么样子的呢？首先，我们要将5个单词填入表格中，同时，单词和单词之间有可能共享同一个英文字母。所以这儿有两个“约束”，一个约束是单词字母的个数，第二个约束是单词里面可以出现的字字母。让我们先写水平排列的两个单词：
	word(L1,L2,L3,L4,L5), <-----单词1
	word(L9,L10,L11,L12,L13,L14)	<-----单词2
之后，我们加上竖直的三个单词：
	word(L1,L6,L9,L15), <-----单词3
	word(L3,L7,L11),	<-----单词4
	word(L5,L8,L13,L16)	<-----单词5
单词1和单词3共享字母“L1”,单词4和单词1共享字母“L3”,单词4和单词2共享字母“L12”，依次类推，我们可以把所有的约束都写出来。这样，我们就告诉Prolog系统最后的答案长得什么样儿了。有了答案的形式，Prolog就会用我之前提到的三个策略(回溯，变量重命名，模式匹配)来找出答案。

###程序的意义
上述的程序其实昭示了Prolog程序的其中一个意义：陈述性意义(declarative meaning)。Prolog程序具有陈述性意义就在于Prolog都是描述的逻辑学上的一个事实或者是一个规则。例如：
	mother(pam,bob).
这句程序语句陈述了一个事实：pam是bob的妈妈。再看：
	grandmother(X,Y):-mother(X,Z),father(Z,Y).
这个语句陈述的是一个规则：当X是Z的母亲并且Z是Y的父亲时，X是Y的母亲。当我们在Prolog系统上输入“grandmother(X,bob)”这样的查询时，实际上就是让Prolog根据自己知道的逻辑规则来试图证明你的查询。这就是程序的陈述性意义。

程序的第二个意义是过程性意义。想Java和C这样的语言一样，Prolog的程序也具有过程性意义，即解决问题的步骤。在举例子之前，我先讲一个在Prolog里面常用的语句："write"，它的作用是向显示屏输出信息。它的参数可以是任意类型的数据，数字，字符串，甚至一个Prolog的规则都可以直接被输出。另外一个语句是"nl"，它的作用是使Prolog的屏幕输出换行。下面给一个程序，你就能理解"write"和"nl"的作用了：
	write('I have a dream'),nl,
	write('that my four little children will one day live in a nation'),nl,
	write('where they will not be judged by the color of their skin'),nl,
	write('but by the content of their character.'),nl,
	write('This is form Martin Luther King').
Prolog会这样输出：
	I have a dream
	that my four little children will one day live in a nation
	where they will not be judged by the color of their skin
	but by the content of their character.
	This is form Martin Luther King
	true.
上面这个程序其实就揭示了Prolog程序的过程性意义，它告诉Prolog系统：要想输出上面这一段话，首先要输出'I have a dream'，然后换行，接着输出’that my four little children will one day live in a nation‘，然后换行，依次类推。它实际上是告诉了Prolog系统一个解决问题的步骤。这就是程序的过程性意义。

其实，就Prolog本身的意义来说，编写Prolog程序的时候是不提倡加入太多的过程性意义的，尽量要以描述性意义为主，因为Prolog本身就是一个描述性语言。但是，程序员们在实际开发的时候发现，他们离不开过程性意义的程序，因为现实生活中解决问题本身就是需要步骤的，例如你想从北京到泰安，你要先从北京到天津，然后从天津到沧州，然后从沧州到济南，最后从济南到泰安。所以，在Prolog里面就不可避免的出现过程性意义为主的程序。

##加分习题
1. 下面我们来试着把单词谜题的答案打印的屏幕上，你要写一个规则”print_solution“，试着把答案这样打印：
		word1 is XXXXXX
		word2 is XXXXXX
		word3 is XXXXXX
		word4 is XXXXXX
		word5 is XXXXXX
之后，试着解释一下你写的程序的过程性意义和陈述性意义。
	