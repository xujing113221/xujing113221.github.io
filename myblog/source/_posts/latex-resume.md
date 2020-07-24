---
title: 如何使用LaTeX写简历
date: 2020-07-18 15:27:37
top: 
tags: 
    - LaTeX
    - Makefile
    - Shell
categories: 制作简历
related_posts:
---

作者最近在找实习，需要制作简历，Latex是一个很好的排版工具，就使用了这个来重新写简历。经过几天时间我写完了简历，完成了使用shell脚本自动化生成简历和Makefile。本人在德国留学，在外国找工作需要准备的文件很多，过程比国内要繁琐很多，尤其需要写推荐信。针对每一份工作申请，你要更改很多内容，比如信件的抬头，公司名称地址，申请职位等。如果在Word文件中更改，尤其大多数是复制粘贴，总会复制上原文字的格式，很麻烦。所以我写了一个shell脚本，在终端上进行复制输入，省去了很多不必要的麻烦，并且提高了效率。现在我修改一份简历只需要不到一分钟的时间。

本文记录一下如何使用我的LaTeX去生成简历已经简单的开发过程。
<!--more-->

## 准备工作

### 开发环境
我使用的是`Mac OS`系统，由于模版要求使用的是`LuaTeX(Version 1.10.0)`。关于LaTex的下载安装可以参考这篇内容：[LaTeX零基础入门教程](https://www.jianshu.com/p/3e842d67ada2)。关于如何使用LaTeX可以参考:[简单粗暴 LATEX](http://static.latexstudio.net/wp-content/uploads/2017/08/Note-by-LaTeX-cn.pdf)。

如果嫌麻烦的话你也可以在线修改你的LaTeX文件，省去了下载和配置的麻烦：[Overleaf](https://www.overleaf.com/project)就是很好的选择。

### 选择模版

我为什么选择LaTeX制作简历，就是因为他有很多好看的模版。LaTeX不仅可以制作简历，现在很多论文都是使用LaTeX来排版的。

可以在这里找到你喜欢的模版：[Overleaf - Templates](https://www.overleaf.com/latex/templates)

我选择的是这个模版：[posquit0/Awesome-CV](https://github.com/posquit0/Awesome-CV)。这个模版很简洁而且不光有简历，还有推荐信，省去了不少时间。然后我稍加更改，添加了一些小功能。你可以直接在`Overleaf`上修改,也可以通过git下载到本地进行修改。在终端输入下一命令即可：
``` bash
git clone https://github.com/posquit0/Awesome-CV.git
```

## 编写自己的简历

下载完喜欢的简历模版以后就是更改你自己内容了，以我选择的简历模版来说：在`resume.tex`修改你的简历内容，在`coverletter.tex`修改你的推荐信。`awesome-cv.cls`文件是模版文件，是控制你简历和推荐信的格式，对此文件修改就可以更改整体格式。

### 修改简历

1. 首先打开`resume.tex`文件我们看到的是第一句话就是：
```tex
%!TEX TS-program = xelatex
```
他使用的是`XeTeX`程序对文件进行编译的，对`fontspec`库的支持不是很好，我在电脑端编译总是报错。所以我更改成`LuaLaTeX`，当然如果你没报错就不必要更改，这只是我的解决方法。
```diff
- %!TEX TS-program = xelatex
+ %!TEX TS-program = luatex
```

2. 修改你的基本信息
```tex
% Available options: circle|rectangle,edge/noedge,left/right
% \photo[rectangle,edge,right]{./examples/profile}
\name{Byungjin}{Park}
\position{Software Architect{\enskip\cdotp\enskip}Security Expert}
\address{42-8, Bangbae-ro 15-gil, Seocho-gu, Seoul, 00681, Rep. of KOREA}

\mobile{(+82) 10-9030-1843}
\email{posquit0.bj@gmail.com}
\homepage{www.posquit0.com}
\github{posquit0}
\linkedin{posquit0}
% \gitlab{gitlab-id}
% \stackoverflow{SO-id}{SO-name}
% \twitter{@twit}
    ...
```
在这里就可以修改你的个人信息。

3. 修改你的内容
``` tex
%-------------------------------------------------------------------------------
%	CV/RESUME CONTENT
%	Each section is imported separately, open each file in turn to modify content
%-------------------------------------------------------------------------------
\input{resume/summary.tex}
\input{resume/experience.tex}
\input{resume/honors.tex}
\input{resume/presentation.tex}
\input{resume/writing.tex}
\input{resume/committees.tex}
\input{resume/education.tex}
\input{resume/extracurricular.tex}
```
在`resume`文件夹中找到相应的文件就可以修改你的内容了。注意`\input`的顺序决定你内容的顺序，你可以进行适当的修改。

### 修改推荐信
1. 修改你的个人信息，同简历一样。
2. 修改申请职位的信息和信件开头结尾格式
```tex
% The company being applied to
\recipient
  {Company Recruitment Team}
  {Google Inc.\\1600 Amphitheatre Parkway\\Mountain View, CA 94043}
% The date on the letter, default is the date of compilation
\letterdate{\today}
% The title of the letter
\lettertitle{Job Application for Software Engineer}
% How the letter is opened
\letteropening{Dear Mr./Ms./Dr. LastName,}
% How the letter is closed
\letterclosing{Sincerely,}
% Any enclosures with the letter
\letterenclosure[Attached]{Curriculum Vitae}
```
3. 更改的内容
在`\begin{cvletter}`下面添加你的推荐信内容

### 修改简历格式添加个性化

我对模版进行了少量的修改，比如
+ 添加双排格式
+ 修改日期格式
+ 添加项目关键字
+ 更改推荐信格式
+ 添加个人电子签名
+ 德语英语简历和推荐信

主要是对`awesome-cv.cls`文件进行修改，这章比较复杂我下一篇博客再说吧。

  
## 编写Makefile

可以参考这篇文章：[跟我一起写Makefile](https://seisman.github.io/how-to-write-makefile/overview.html)
LaTeX的Makefile文件很好写，主要使用的`LuaLaTeX`引擎进行编译，然后重命名输出的pdf文件。
```Makefile
lualatex -synctex=1 -interaction=nonstopmode $(RESUMEDE_IN).tex
mv $(RESUMEDE_IN).pdf $(OUTPUT)$(RESUMEDE_OUT).pdf
```
需要注意的是在每次使用`make`命令之前，需要在tex文件中修改相关信息，如申请职位，介绍信中的信件抬头。

## 编写Shell脚本，实现自动化生成简历

这一部分是实现自动填写简历和介绍信，自动生成德文版或英文版简历。如何编写Shell脚本可以在这里学习：[菜鸟教程 - Shell 教程](https://www.runoob.com/linux/linux-shell-variable.html)

使用方法很简单，但是我是在Mac OS上编写的所以不一定适合Windouw命令行。

```bash make.sh
$ ./make.sh
```
在终端中输入上面的命令，然后根据提示输入申请信息，如下
```
=== Please choice language:
        1.English       2.German        3.Both
1
=== Please tell me the name of you applicated Job:
System development for antenna measurement systems

=== Please tell me the information of your applicated Company:
Recipient:
Company: Rohde & Schwarz GmbH & Co. KG
Address: München
Postcode, location:

=== Please Choose the following options to tell me the Recipient:
        1. Dear Sir or Madam,
        2. Dear Mr. Family Name,
        3. Dear Ms. Family Name,
Input your choice nummber: 2
Tell me the name: Jing Xu

=== Please check your inputs!
If wrong, input 1. If right, input any key:
    ....
```

## 我的简历模版
{%note info%}
最后可以在我的GitHub上找到我更改好的LaTeX模版：[xujing113221/myRusume](https://github.com/xujing113221/myRusume)
{%endnote%}
**我的简历：**
![my resume](resume.png)
**我的推荐信：**
![my cover letter](coverletter.png)

## 参考文章

+ [简单粗暴 LATEX](http://static.latexstudio.net/wp-content/uploads/2017/08/Note-by-LaTeX-cn.pdf)。
+ [跟我一起写Makefile](https://seisman.github.io/how-to-write-makefile/overview.html)
+ [菜鸟教程 - Shell 教程](https://www.runoob.com/linux/linux-shell-variable.html)
+ [shell脚本----if（数字条件，字符串条件，字符串为空）](https://blog.csdn.net/yf210yf/article/details/9207147)

