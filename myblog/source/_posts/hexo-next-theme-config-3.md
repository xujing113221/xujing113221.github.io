---
title: Hexo NexT 主题配置三
date: 2020-07-10 18:32:08
tags: ['Hexo', 'NexT']
categories: Hexo创建博客
---

本文继续配置 Hexo-Next，进一步对博客进行美化，主要包括:

+ 修改博客字体
+ 添加结束标记
+ 添加动态特效
+ 显示近期文章(to do)

<!--more-->

## 修改博客字体

在 [Google Fonts](https://fonts.google.com) 上找到心仪的字体，然后在主题配置文件中搜索`font:`为不同的应用场景配置字体：
``` yml themes\next\_config.yml
 # Font options:
  # `external: true` will load this font family from `host` above.
  # `family: Times New Roman`. Without any quotes.
  # `size: x.x`. Use `em` as unit. Default: 1 (16px)

  # Global font settings used for all elements inside <body>.
  global:
    external: true
    family: Noto Sans SC
    size:

  # Font settings for site title (.site-title).
  title:
    external: true
    family: Cedarville Cursive
    size:

  # Font settings for headlines (<h1> to <h6>).
  headings:
    external: true
    family: Noto Serif SC
    size:

  # Font settings for posts (.post-body).
  posts:
    external: true
    family:

  # Font settings for <code> and code blocks.
  codes:
    external: true
    family: Courier
```

## 添加结束标记

新建布局模板文件`post-end-tag.swig`，添加如下代码：
```swig themes\next\layout\_macro\post-end-tag.swig
<div>
  {% if not is_index %}
    <div style="text-align:center;color:#bfbfbf;font-size:16px;">
      <span>-------- 本文结束 </span>
      <i class="fa fa-{{ config.post_end_tag.icon }}"></i>
      <span> 感谢阅读 --------</span>
    </div>
  {% endif %}
</div>
```
在文章布局模板中添加如下代码：
```diff themes\next\layout\_macro\post.swig
{#####################}
{### END POST BODY ###}
{#####################}

+ {% if config.post_end_tag.enabled and not is_index %}
+   <div>
+     {% include 'post-end-tag.swig' %}
+   </div>
+ {% endif %}

{% if theme.wechat_subscriber.enabled and not is_index %}
  <div>
    {% include 'wechat-subscriber.swig' %}
  </div>
{% endif %}
```

在站点配置文件末尾添加如下代码：
``` yml hexo/_config.yml
post_end_tag:
  enabled: true  # 是否开启文末的本文结束标记
  icon: paw # 结束标记之间的图标
```

## 添加动态特效

### 粒子漂浮聚合
需要安装 `theme-next-canvas-nest` 详见 [Theme NexT Canvas Nest](https://github.com/theme-next/theme-next-canvas-nest)

我说使用的这是这一款，介绍一下安装过程：
1. 在文件夹`hexo/source/_data` 中创建 `footer.swig`，如果没有`_data` 自己创建一个， 在`footer.swig`中添加如下内容：
```swig hexo/source/_data/footer.swig
<script color="0,0,255" opacity="0.5" zIndex="-1" count="99" src="https://cdn.jsdelivr.net/npm/canvas-nest.js@1/dist/canvas-nest.js"></script>
```
2. 在主题配置文件中搜索`custom_file_path:`修改如下内容：
```diff
# Define custom file paths.
# Create your custom files in site directory `source/_data` and uncomment needed files below.
custom_file_path:
  #head: source/_data/head.swig
  #header: source/_data/header.swig
  #sidebar: source/_data/sidebar.swig
  #postMeta: source/_data/post-meta.swig
  #postBodyEnd: source/_data/post-body-end.swig
- #footer: source/_data/footer.swig
+ footer: source/_data/footer.swig
  #bodyEnd: source/_data/body-end.swig
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  #style: source/_data/styles.styl
```

这样就好了。

### Three 三维动效
需要安装 `theme-next-three` 详见 [Theme NexT Three](https://github.com/theme-next/theme-next-three)

### 随机三角丝带
需要安装 `theme-next-canvas-ribbon` 详见 [Theme NexT Canvas Ribbon](https://github.com/theme-next/theme-next-canvas-ribbon)

### 添加加载特效
需要安装 `theme-next-pace` ，详见 [Theme NexT Pace](https://github.com/theme-next/theme-next-pace)


### 鼠标点击特效

1. 下载 `礼花特效` 保存在` themes/next/source/js/cursor/ ` 
   
2. 在主题自定义布局文件中添加以下代码：
```js themes\next\layout\_custom\custom.swig
{# 鼠标点击特效 #}
{% if theme.cursor_effect == "fireworks" %}
<script async src="/js/cursor/fireworks.js"></script>
{% elseif theme.cursor_effect == "explosion" %}
<canvas class="fireworks" style="position: fixed;left: 0;top: 0;z-index: 1; pointer-events: none;" ></canvas>
<script src="//cdn.bootcss.com/animejs/2.2.0/anime.min.js"></script>
<script async src="/js/cursor/explosion.min.js"></script>
{% elseif theme.cursor_effect == "love" %}
<script async src="/js/cursor/love.min.js"></script>
{% elseif theme.cursor_effect == "text" %}
<script async src="/js/cursor/text.js"></script>
{% endif %}
```

3. 如果 `custom.swig` 不存在，需要手动新建并在布局页面中 body 末尾引入：
   
```diff themes\next\_config.yml
    ...
    {% include '_third-party/exturl.swig' %}
    {% include '_third-party/bookmark.swig' %}
    {% include '_third-party/copy-code.swig' %}

+     {% include '_custom/custom.swig' %}
    </body>
</html>
```

4. 在主题配置文件中添加如下代码：
```yml themes\next\_config.yml
# mouse click effect: fireworks | explosion | love | text
cursor_effect: fireworks
```

## 显示近期文章 (未完成)
{%note info%}
+ 本章参考来自 [Hexo+NexT(v7.0+) 搭建博客：主题美化](https://www.chingow.cn/posts/c7372a12.html)
+ [Hexo: 给博客添加近期文章板块](https://postgres.fun/20190116150800.html)
+ [swig安装搭建与测试](https://blog.csdn.net/chenglinhust/article/details/41206511?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)
{%endnote%}

我没实现 总是有Bug， 看了看代码也不行。

主要添加内容：
```swig /next/layout/_partials/sidebar/site-overview.swig
{# Blogroll #}
{%- if theme.recent_posts %}
  <div class="links-of-blogroll motion-element {{ "links-of-blogroll-" + theme.recent_posts_layout  }}">
  <div class="links-of-blogroll-title">
    <!-- modify icon to fire by szw -->
    <i class="fa fa-history fa-{{ theme.recent_posts_icon | lower }}" aria-hidden="true"></i>
    {{ theme.recent_posts_title }}
  </div>
  <ul class="links-of-blogroll-list">
    {%- set posts = site.posts.sort('-date') %}
    {%- for post in posts.slice('0', '3') %}
      <li class="links-of-blogroll-item">
        <a href="{{ url_for(post.path) }}" title="{{ post.title }}" target="_blank">{{ post.title }}</a>
      </li>
    {%- endfor %}
  </ul>
  </div>
{%- endif %}
```

``` yml /theme/next/_config.yml
# 近期文章
recent_posts_title: 近期文章
recent_posts_layout: block
recent_posts: true
```

## 参考文章
+ [Hexo 搭建个人博客系列：主题美化篇](http://yearito.cn/posts/hexo-theme-beautify.html)
+ [NexT 中文使用说明](https://theme-next.iissnan.com/getting-started.html)
