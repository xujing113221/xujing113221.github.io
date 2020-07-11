---
title: Hexo NexT 主题配置四
date: 2020-07-11 13:32:00
tags: 
    - Hexo
    - NexT
categories: 
    - [学习笔记, Hexo创建博客]
---

本文主要介绍我在NexT主题配置中遇到的小问题，以及主题的进一步美化。

+ 页脚设置
+ 多级分类
+ 添加热门文章排行榜

<!--more-->

## 页脚设置

### Mist主题 页脚居中问题

解决方案：

```diff themes/next/source/css/_schemes/Mist/_layout.styl
.footer-inner {
-  text-align: left;
+  text-align: center;

  +mobile() {
    text-align: center;
    width: auto;
  }
}
```

### 不蒜子访客统计 个性化 

这里就不弄了，等我学会了html，我在搞。 默认的就挺简洁好看的。

在 这个文件{%label primary@themes/next/layout/_third-party/statistics/busuanzi-counter.swig %}修改就可以的实现个性化了.

## 多级分类
{% note info %}
详见 [Front-matter](https://hexo.io/zh-cn/docs/front-matter.html)
{% endnote %}

举例
```md
categories:
- [Diary, PlayStation]
- [Diary, Games]
- [Life]
```
这篇文章同时包括三个分类： PlayStation 和 Games 分别都是父分类 Diary 的子分类，同时 Life 是一个没有子分类的分类。



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

## 参考文章

+ Hexo [搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
+ [LeanCloud | JavaScript SDK 开发指南](https://leancloud.cn/docs/leanstorage_guide-js.html)
+ [LeanCloud | JavaScript SDK 安装指南](https://leancloud.cn/docs/sdk_setup-js.html#hash-99064366)