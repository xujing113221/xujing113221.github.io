---
title: Hexo 写作技巧
date: 2020-07-10 16:11:15
tags: 
  - Hexo
  - Markdown
categories: Hexo创建博客
related_posts:
---

本文记录Hexo相关书写技巧，使博客内容更加丰富界面更加美观，主要内容有以下几点：
+ 代码块进阶用法
+ note 标签
+ label 标签
+ button 按钮
+ tab 标签
+ 草稿和发布

<!--more-->

## 代码块进阶用法

语法规则

```
··· [language] [title] [url] [link text]
code snippet
···
```

其中，各参数意义如下：

+ langugae：语言名称，引导渲染引擎正确解析并高亮显示关键字
+ title：代码块标题，将会显示在左上角
+ url：链接地址，如果没有指定 link text 则会在右上角显示 link
+ link text：链接名称，指定 url 后有效，将会显示在右上角
+ url 必须为有效链接地址才会以链接的形式显示在右上角，否则将作为标题显示在左上角。以 url 为分界，左侧除了第一个单词会被解析为 language，其他所有单词都会被解析为 title，而右侧的所有单词都会被解析为 link text。

如果不想填写 title，可以在 language 和 url 之间添加至少三个空格。

测试代码：
```cpp hello.cpp http://google.com this is google website
#include<iostream>
using namespace std;

int main()
{
    cout << "hello world!" << endl;
    return 0;
}
```

可以在站点配置文件中设置 highlight.auto_detect: true 来开启自动语言检测高亮。

如果设置语言为 diff，可以在代码前添加 + 和 - 来使用如上所示的高亮增删行提示效果，在展示代码改动痕迹时比较实用。
```diff _config.yml
 highlight:
   enable: true
   line_number: false
-  auto_detect: false
+  auto_detect: true
   tab_replace:
```

## note 标签

通过 note 标签可以为段落添加背景色，语法如下：
```html
{% note [class] %}
文本内容 (支持行内标签)
{% endnote %}

or

<div class="note warning">文本内容 (支持行内标签)</div>
```
支持的 class 种类包括 `default` `primary` `success` `info` `warning` `danger`，也可以不指定class。

各种 class 种类的效果如下:

{% note default %}
default note tag
{% endnote %}

{%note primary %}
primary note tag
{% endnote %}

{%note success %}
success note tag
{% endnote %}

{% note info %}
info note tag
{% endnote %}


<p class="note warning">warning note tag</p>

{% note danger %}
danger note tag
{% endnote %}


更多配置可在主题配置文件中设置
```yml
note:
  # Note 标签样式预设
  style: modern  # simple | modern | flat | disabled
  icons: false  # 是否显示图标
  border_radius: 3  # 圆角半径
  light_bg_offset: 0  # 默认背景减淡效果，以百分比计算
```


## label 标签

通过 label 标签可以为文字添加背景色，语法如下：
```md
{% label [class]@text  %}
```

支持的 class 种类包括 default primary success info warning danger，默认使用 default 作为缺省。

使用示例如下：

```markdown
I heard the echo, {% label default@from the valleys and the heart %}
Open to the lonely soul of {% label info@sickle harvesting %}
Repeat outrightly, but also repeat the well-being of
Eventually {% label warning@swaying in the desert oasis %}
{% label success@I believe %} I am
{% label primary@Born as the bright summer flowers %}
Do not withered undefeated fiery demon rule
Heart rate and breathing to bear {% label danger@the load of the cumbersome %}
Bored
```
I heard the echo, {% label default@from the valleys and the heart %}
Open to the lonely soul of {% label info@sickle harvesting %}
Repeat outrightly, but also repeat the well-being of
Eventually {% label warning@swaying in the desert oasis %}
{% label success@I believe %} I am
{% label primary@Born as the bright summer flowers %}
Do not withered undefeated fiery demon rule
Heart rate and breathing to bear {% label danger@the load of the cumbersome %}
Bored

## button 按钮
```
{% button /path/to/url/, text, icon [class], title %}

其中， 图标 ID 来源于 [FontAwesome](https://fontawesome.com/v4.7.0/icons/) 

# eg.
{% btn #, 文本 %}
{% btn #, 文本 & 标题,, 标题 %}
{% btn #, 文本 & 图标, home %}
{% btn #, 文本 & 大图标 (固定宽度), home fa-fw fa-lg %}
```

## tab 标签

tab 标签用于快速创建 tab 选项卡，语法如下
```
{% tabs [Unique name], [index] %}
  <!-- tab [Tab caption]@[icon] -->
  标签页内容（支持行内标签）
  <!-- endtab -->
{% endtabs %}
```

{% btn #, 小按钮, home fa-fw, 回到顶部%}

其中，各参数意义如下：

+ Unique name: 全局唯一的 Tab 名称，将作为各个标签页的 id 属性前缀
+ index: 当前激活的标签页索引，如果未定义则默认选中显示第一个标签页，如果设为 - 1 则默认隐藏所有标签页
+ Tab caption: 当前标签页的标题，如果不指定则会以 Unique name 加上索引作为标题
+ icon: 在标签页标题中添加 Font awesome 图标
  
```markdown
{% tabs Tab标签列表 %}
  <!-- tab 标签页1 -->
    标签页1文本内容
  <!-- endtab -->
  <!-- tab 标签页2 -->
    标签页2文本内容
  <!-- endtab -->
  <!-- tab 标签页3 -->
    标签页3文本内容
  <!-- endtab -->
{% endtabs %}
```

{% tabs 编程语言 %}
  <!-- tab Cpp -->
    ```cpp hello.cpp
    #include <iostream>
    using namespace std;

    int main()
    {
        cout << "hello world!" << endl;
        return 0;
    }
    ```
  <!-- endtab -->
  <!-- tab C -->
    ``` C hello.c
    #include <stdio.h>
    
    int main()
    {
        printf("hello world!\n");
        return 0;
    }
    ```
  <!-- endtab -->
  <!-- tab Java -->
    ``` java hello.java
    const class hello{
        static const void main(String args[]){
            System.out.println("hello world!");
            return 0;
        }
    }
    ```
  <!-- endtab -->
{% endtabs %}

## 草稿和发布

{%note info%}
本章内容参考自 [Hexo+NexT(v7.0+) 搭建博客：内容优化](https://www.chingow.cn/posts/bd723aed.html)
{%endnote%}

一般我们使用`hexo new <title>`来建立文章，这种建立方法会将新文章建立在 **source/_posts** 目录下，当使用 `hexo generate` 编译文件时，会将其 HTML 结果编译在 `public` 目录下，之后`hexo server`将会把 `public` 目录下所有文章发布。

Hexo 提供 draft 机制，它的原理是新文章将建立在 **source/_drafts** 目录下，因此并不会将其编译到 **public** 目录下发布，而且提供了很友好的预览功能。
```bash
$ hexo new draft <title>	# 新建草稿文章
$ hexo s --draft	        # 预览草稿文章
```
将草稿发布为正式文章：
```bash
$ hexo P <filename>
```

其中 <filename> 为不包含 md 后缀的文章名称。它的原理只是将文章从 **source/_drafts** 移动到 **source/_posts** 而已。

## 参考链接
+ [Hexo 搭建个人博客系列：写作技巧篇](http://yearito.cn/posts/hexo-writing-skills.html)
+ [Hexo建站日志 (6) - 添加文章书写样式](http://dinghongkai.com/2017/12/19/Blog-development-6-Customized-Style-of-Writing/)
+ [Hexo 博客美化配置](http://ylong.net.cn/hexo_conf.html)
+ [Hexo+NexT(v7.0+) 搭建博客：内容优化](https://www.chingow.cn/posts/bd723aed.html)