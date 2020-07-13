---
title: Hexo NexT 主题配置四
date: 2020-07-11 13:32:00
tags: 
    - Hexo
    - NexT
categories: 
    - [学习笔记, Hexo创建博客]
---

{%note primary%}
本文提到的Hexo博客配置是基于：Hexo v4.2.1 和 NexT v7.8.0。请注意版本之间存在差异！
{%endnote%}
本文主要介绍我在NexT主题配置中遇到的小问题，以及主题的进一步美化，深入Next代码进行个性化配置。

+ 页脚设置
+ 多级分类
+ 修改博客字体
+ 版权声明个性化设置
+ 添加看板娘功能
+ 解决不蒜子显示问题

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

{%note info%}
本章参见[yearito's Blog | Hexo搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
{%endnote%}

![效果图](copyright.png "效果图")

+ 先找到 {%label success@themes/next/layout/_partials/post/post-copyright.swig %}  添加如下内容：
```diff themes/next/layout/_partials/post/post-copyright.swig 
<!-- JS库 clipboard 拷贝内容到粘贴板-->
<script src="https://cdn.bootcss.com/clipboard.js/2.0.1/clipboard.min.js"></script>
<!-- JS库 sweetalert 显示提示信息-->
<script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
<div>
<ul class="post-copyright">
  <li class="post-copyright-title">
   <strong>{{ __('post.copyright.title') + __('symbol.colon') }} </strong>
    {{page.title}}             // 只显示文章标题 
    <a href="{{page.permalink}}">{{page.title}}</a>  // 显示带链接的文章标题
  </li>
  <li class="post-copyright-author">
    <strong>{{ __('post.copyright.author') + __('symbol.colon') }} </strong>
    {{- page.author or author }}
  </li>
  <!-- 引用链接 -->
  <li class="post-copyright-link">
    <strong>{{ __('post.copyright.link') + __('symbol.colon') }}</strong>
    <a href="{{ post.url | default(post.permalink) }}" title="{{ post.title }}">
      {{ post.url | default(post.permalink) }}
    </a>
    <span class="copy-path" title="点击复制引用链接">
      <i
        style="cursor: pointer"
        class="fa fa-clipboard"
        data-clipboard-text="[{{ post.author | default(author) }}'s Blog | {{ post.title }}]({{ post.permalink }})"
        aria-label="{{ __('post.copy_success') }}">
      </i>
    </span>
  </li>
      ....

</ul>
</div>
      ....
<script>
  var clipboard = new ClipboardJS(".fa-clipboard");
  clipboard.on("success", function(target) {
    var message = document.createElement("div");
    message.innerHTML =
      '<i class="fa fa-check-circle message-icon"></i><span class="message-content">' +
      target.trigger.getAttribute("aria-label") +
      "</span>";
    swal({
      content: message,
      className: "copy-success-message",
      timer: 1000,
      button: false
    });
  });
</script>
```

+ 在主题语言配置文件中 添加如下内容：
```diff themes/next/languages/zh-CN.yml
+ copy_success: 复制成功
  copyright:
+   title: 本文标题
    author: 本文作者
    link: 本文链接
    license_title: 版权声明
    license_content: "本博客所有文章除特别声明外，均采用 %s 许可协议。转载请注明出处！"
```
+ 找到{%label info@themes/next/source/css/_common/components/post/post-copyright.styl%} 添加如下内容：
```css
.swal-overlay {
  background-color: transparent;
}

.copy-success-message {
  box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.15);
  border-radius: 4px;
  width: auto;
  margin: 16x 0px;
  vertical-align: top;
}

.copy-success-message .swal-content {
  margin: 0px 0px !important;
  padding: 10px 16px;
  line-height: 1em;
}

.copy-success-message .message-icon {
  color: #52c41a;
  margin-right: 8px;
}

.copy-success-message .message-content {
  font-size: 14px;
}
```

## 添加看板娘功能

{% note info %}
本章参考链接：
+ [live2d-widget-models](https://github.com/xiazeyu/live2d-widget-models)
+ [live2d模型用户配置](https://l2dwidget.js.org/docs/class/src/index.js~L2Dwidget.html#instance-method-init)
+ [live2d模型中文说明](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md)
+ [yearito's Blog | Hexo搭建个人博客系列：主题美化篇](http://yearito.cn/posts/hexo-theme-beautify.html)
+ [添加一个萌物](https://fjkang.github.io/2017/12/08/%E6%B7%BB%E5%8A%A0%E4%B8%80%E4%B8%AA%E8%90%8C%E7%89%A9/)
+ [Hexo添加Live2D看板娘+模型预览](https://blog.csdn.net/wang_123_zy/article/details/87181892)
{% endnote %}

在站点根目录下执行以下命令安装依赖：
```bash
$ npm install --save hexo-helper-live2d
```
在站点配置文件中添加以下下配置项
```yml _config.yml
# Live2D
# https://github.com/EYHN/hexo-helper-live2d
live2d:
  enable: true
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/ Relative)

  # 脚本加载源
  scriptFrom: local # 默认从本地加载脚本
  # scriptFrom: jsdelivr # 从 jsdelivr CDN 加载脚本
  # scriptFrom: unpkg # 从 unpkg CDN 加载脚本
  # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 从自定义地址加载脚本
  tagMode: false # 只在有 {{ live2d() }} 标签的页面上加载 / 在所有页面上加载
  log: false # 是否在控制台打印日志

  # 选择看板娘模型
  model:
    use: live2d-widget-model-z16 #使用模型
    #live2d-widget-model-shizuku #live2d-widget-model-tororo #live2d-widget-model-epsilon2_1
    #live2d-widget-model-hibiki #live2d-widget-model-z16
  display:
    position: right # 显示在左边还是右边
    width: 200 # 宽度
    height: 360 # 高度
  mobile:
    show: false
  react:
    opacityDefault: 0.7 # 默认透明度
  dialog:
    enable: true #添加对话框
    hitokoto: true
```
这个时候还不会有看板娘的显示，在 [live2d-widget-models](https://github.com/xiazeyu/live2d-widget-models) 手动下载喜欢的样式。

因为修改了站点配置文件，所以需要重启服务器才能预览模型效果。

{%note success%}
这个功能挺好玩的，操作也简单。但是我还是喜欢简洁点的网页，哈哈哈哈。
{%endnote%}

## 文章评论功能
Next 主题中已经集成了[widgetpack](https://widgetpack.com/)的星级评分系统，用户无须再安装或引入插件脚本，只需在 widgetpack 中注册账号并修改主题配置即可，应用效果如下：

```yml themes/next_config.yml
# Star rating support to each article.
# To get your ID visit https://widgetpack.com
rating:
  enable: true
  id: #<app_id>
  color: fadb14
```
在`widgetpack`左边栏中找到`Rating`的`Setting` 修改`Vote via`为除了`Social`以外其他两种方式，就可以开启匿名评分了
![widgetpack设置](widgetpack.png)
{%note info%}
  不想再写了，这个功能很简单，看这个人的博客就好 [yearito's Blog | Hexo搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
{%endnote%}

## 解决不蒜子显示问题
{%note info%}
本章内容参考:[解决live2d看板娘和busuanzi不蒜子计数冲突](http://boyinthesun.cn/post/error-live2d-busuanzi/)
{%endnote%}

+ 下载[busuanzi.pure.mini.js](busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js)到本地存储在文件夹`themes/next/source/js/`中
+ 修改`busuanzi.pure.mini.js` 将`b.style.display="none"`中`none`去掉。
+ 修改如下代码：
```diff themes/next/layout/_third-party/statistics/busuanzi-counter.swig
{%- if theme.busuanzi_count.enable %}
<div class="busuanzi-count">
-  <script{{ pjax }} async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
+  <script async src="/js/busuanzi.pure.mini.js"></script>
```

## 结束语

自此关于Hexo写博客的主题就告一段落了，我对Next主题配置差不多了。这是我第一次写博客，就是记录一下这个我开始使用Hexo写博客的过程，在此期间我看到了很多优秀的博客，给予了我很多帮助，我也借鉴了很多内容，希望我都备注上了。谢谢大家！

刚开始写博客，结构和内容有点乱，希望大家见谅，有什么问题希望大家给我写评论告诉我！后面我会慢慢写，写好每一篇博客！

后面我会写一下我学习和生活中的知识和经验，分享给大家，同时也给自己留下笔记，整理一下我的知识。希望未来越来越好！

## 参考文章

+ [Hexo 搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
+ [LeanCloud | JavaScript SDK 开发指南](https://leancloud.cn/docs/leanstorage_guide-js.html)
+ [LeanCloud | JavaScript SDK 安装指南](https://leancloud.cn/docs/sdk_setup-js.html#hash-99064366)

