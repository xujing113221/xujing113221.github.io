---
title: LaTeX 学习笔记
date: 2020-07-24 00:55:03
top:
tags: LaTeX
categories: [学习笔记, LaTeX排版]
password: latex
---

本文介绍我学习LaTeX的学习笔记。
<!--more-->

## 准备工作 
{%note info%}
这篇文章介绍的很全：[LaTeX零基础入门教程](https://www.jianshu.com/p/3e842d67ada2)
[Learn LaTeX in 30 minutes](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
[简单粗暴 LATEX](http://static.latexstudio.net/wp-content/uploads/2017/08/Note-by-LaTeX-cn.pdf)
{%endnote%}

在这里我推荐一些实用的小工具：
+ [快速制作LaTex表格](https://www.tablesgenerator.com)
+ [LaTex工具生成器](https://www.latexlive.com/)
  
## 多文件编写

+ \input

它完全相当于C/C++语言中的#include，可以理解为只起一个文本替换的作用。
因而，它可以嵌套使用。可以在任何位置使用（特别强调一下：可以在导言区使用）。
但是，任何一个子文件修改后，都需要对全文进行重新编译。所以对于编译有好几百页的书籍来说用它来管理章节是不太方便的（但是各个章节内部可以使用它），但对于论文，这点额外时间完全可以接受。

由于它只是一个文本替换，因而如果想只编译某些章节，那么所有的自动编号都会根据现在的内容重新编排。即如果第一章有3个公式，那么第二章的第一个公式应该是“公式4”，如果我把第一章的\input注释掉，那么第二章第一个公式会是“公式1”。同样的情况还出现在图标、章节等所有自动编号上。

+ \include

为了实现不改变最终效果（编号等资源的显示）的部分章节调试，可以使用\include和与之配套的\includeonly。
它类似于编程中编译好的库文件。

它只能用在正文区，用来引入正文。
每个\include的部分开始时会新起一页。
在某个部分修改的时候，针对宿主文件的重新编译不会影响其他文件。因而很节约编译时间。

如果只想在生成的文件中显示部分章节，不需要对正文区的\include 做任何操作，只需要在导言区写诸如\includeonly{chapter1,chapter3,chapter14}的一句就可以了。它表示只生成第1、3、14章。并且它不会因为把显示中间的章节，就把它们的自动编号空过去（但是如果在正文区注释掉了，那就另当别论了）。
+ [latex分文件编写技巧](https://blog.csdn.net/yanxiangtianji/article/details/13169699)

## 自定义命令

\newcommand：新定义一个命令，如果该命令已有定义，则报错；
\renewcommand：重定义一个命令，如果该命令未定义，则报错；
\providecommand：如果该命令未定义，则定义一个新的命令；否则，啥也不干。

[在 TeX 和 LaTeX2e 中定义新命令](https://liam.page/2017/07/30/define-a-new-command-with-different-amount-of-parameters-in-LaTeX/)


[Configure Visual Stuido Code as LaTeX IDE](http://ddswhu.me/posts/2018-04/vs-code-for-latex/)

http://texdoc.net/texmf-dist/doc/generic/pgf/pgfmanual.pdf
https://njuwfang.github.io/2018/10/23/Latex-Tikz/

+ [latex 中的长度单位，尺寸](https://blog.csdn.net/robert_chen1988/article/details/52739825)

+ [LaTeX入门(三)——Hello world!](https://zhuanlan.zhihu.com/p/56016409)