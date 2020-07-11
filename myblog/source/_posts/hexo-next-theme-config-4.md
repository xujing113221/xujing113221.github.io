---
title: Hexo NexT 主题配置四
date: 2020-07-11 13:32:00
tags: 
    - Hexo
    - NexT
categories: 
    - [学习笔记, Hexo创建博客]
---

本文主要介绍我在NexT主题配置中遇到的小问题，以及主题的进一步美化，深入Next代码进行个性化配置。

+ 页脚设置
+ 多级分类
+ 修改博客字体
+ 版权声明个性化设置

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
## 版权声明个性化设置

我主要就想添加个文章标题在版权信息处，剩下的可以依据个人想法自行添加。

![效果图](copyright.png "效果图")

+ 先找到 {%label success@themes/next/layout/_partials/post/post-copyright.swig %}  添加如下内容：
```diff themes/next/layout/_partials/post/post-copyright.swig 
<div>
<ul class="post-copyright">
+  <li class="post-copyright-title">
+   <strong>{{ __('post.copyright.title') + __('symbol.colon') }} </strong>
+    {{page.title}}             // 只显示文章标题 
+    <a href="{{page.permalink}}">{{page.title}}</a>  // 显示带链接的文章标题
+  </li>
  <li class="post-copyright-author">
    <strong>{{ __('post.copyright.author') + __('symbol.colon') }} </strong>
    {{- page.author or author }}
  </li>

      ....

</ul>
</div>
```

+ 在主题语言配置文件中 添加如下内容：
```diff themes/next/languages/zh-CN.yml
 copyright:
+   title: 本文标题
    author: 本文作者
    link: 本文链接
    license_title: 版权声明
    license_content: "本博客所有文章除特别声明外，均采用 %s 许可协议。转载请注明出处！"
```


## 参考文章

+ Hexo [搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
+ [LeanCloud | JavaScript SDK 开发指南](https://leancloud.cn/docs/leanstorage_guide-js.html)
+ [LeanCloud | JavaScript SDK 安装指南](https://leancloud.cn/docs/sdk_setup-js.html#hash-99064366)