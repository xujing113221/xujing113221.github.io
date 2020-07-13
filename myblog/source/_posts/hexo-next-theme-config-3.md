---
title: Hexo NexT 主题配置三
date: 2020-07-10 18:32:08
tags: 
    - Hexo
    - NexT
categories: 
    - [学习笔记, Hexo创建博客]
---

{%note primary%}
本文提到的Hexo博客配置是基于：Hexo v4.2.1 和 NexT v7.8.0。请注意版本之间存在差异！
{%endnote%}
本文继续配置 Hexo-Next，进一步对博客进行美化，主要包括:

+ 添加热门文章排行榜
+ 添加结束标记
+ 添加动态特效
+ 显示近期文章(to do)
+ 添加RSS订阅

<!--more-->

## 添加热门文章排行榜

1. 在终端中执行如下代码：
```bash
$ hexo new page top
```
2. 在主题配置文件中添加如下代码：
```diff themes\next_config.yml
  menu:
    home: / || home
+   top: /top/ || signal
    tags: /tags/ || tags
    categories: /categories/ || th
    archives: /archives/ || archive
    about: /about/ || user
```
3. 在语言包中新增菜单中文：
```diff themes\next\languages\zh-CN.yml
  menu:
    home: 首页
    archives: 归档
    categories: 分类
    tags: 标签
    about: 关于
+   top: 排行榜
```
1. 然后在新增的排行榜页面内添加以下内容：
```javascript /source/hot/index.md
<div id="post-rank">
  <p>This will be overwritten.</p>
</div>

<script src="//cdn.jsdelivr.net/npm/leancloud-storage@4.6.1/dist/av-min.js"></script>
<script>
  var APP_ID = '********'  //输入个人LeanCloud账号AppID
  var APP_KEY = '*********'  //输入个人LeanCloud账号AppKey
  AV.init({
    appId: APP_ID,
    appKey: APP_KEY
  });

  var query = new AV.Query('Counter'); //表名
  query.descending('time');   //结果按阅读次数降序排序
  query.limit(10);          //最终只返回10条结果
  query.find().then( response => {
    var content = response.reduce( (accum, {attributes}) => {
      accum += `<p><div class="prefix">热度 ${attributes.time} ℃</div><div><a href="${attributes.url}">${attributes.title}</a></div></p>`
      return accum;
    },"")
    document.querySelector("#post-rank").innerHTML = content;
  })
  .catch( error => {
    console.log(error);
  });
</script>

<style type="text/css">
  #post-rank {
    text-align: center;
  }
  #post-rank .prefix {
    color: #ff4d4f;
  }
</style>
```

{% note warning %}
在[LeanCloud | JavaScript SDK 安装指南](https://leancloud.cn/docs/sdk_setup-js.html#hash-99064366)中查找最新版`JavaScript JDK`,更改上面代码的JS源，避免出现问题。
{% endnote %}

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
{%note info%}
需要安装 `theme-next-canvas-nest` 详见 [Theme NexT Canvas Nest](https://github.com/theme-next/theme-next-canvas-nest)
{%endnote%}

我说使用的这是这一款，介绍一下安装过程：
1. 在文件夹`themes/next/layout/_custom/` 中创建 `custom.swig`，如果没有`_custom` 自己创建一个， 在`custom.swig`中添加如下内容：
```swig themes/next/layout/_custom/custom.swig
{# 背景粒子漂浮聚合特效 #}
{% if theme.canvas_nest %}
    <script color="0,0,255" opacity="0.5" zIndex="-1" count="99" src="https://cdn.jsdelivr.net/npm/canvas-nest.js@1/dist/canvas-nest.js"></script>
{% endif %}
```
2. 在主题配置文件后面添加如下内容：
```swig
# 背景粒子漂浮聚合特效
canvas_nest: true
```
这样就好了。

### Three 三维动效
{%note info%}
需要安装 `theme-next-three` 详见 [Theme NexT Three](https://github.com/theme-next/theme-next-three)
{%endnote%}

### 随机三角丝带
{%note info%}
需要安装 `theme-next-canvas-ribbon` 详见 [Theme NexT Canvas Ribbon](https://github.com/theme-next/theme-next-canvas-ribbon)
{%endnote%}
### 添加加载特效
{%note info%}
需要安装 `theme-next-pace` ，详见 [Theme NexT Pace](https://github.com/theme-next/theme-next-pace)
{%endnote%}

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
## 添加RSS订阅
{%note info%}
本章参考：[Next -14- 为Hexo Next7.7.1 添加RSS （带按钮）]( https://www.zywvvd.com/2020/03/20/next/14_add_rss/next-add-rss/)
{%endnote%}

本博客使用NexT v7.8 版本，该版本已经去掉了RSS边栏显示，所以要自己为RSS添加代码。添加到你想要的边栏地方就好了。其余步骤就是修改配置文件了。

```swig xujing$ cd themes/next/layout/_partials/sidebar/site-overview.swig 
{# RSS #}
{% if theme.rss %}
   <div class="feed-link motion-element">
     <a href="{{ url_for(theme.rss) }}" rel="alternate">
       <i class="fa fa-rss"></i>
       RSS
     </a>
   </div>
 {% endif %}

{%- if theme.creative_commons.license and theme.creative_commons.sidebar %}
  <div class="cc-license motion-element" itemprop="license">
  {%- set ccImage = '<img src="' + url_for(theme.images + '/cc-' + theme.creative_commons.license + '.svg') + '" alt="Creative Commons">' %}
    {{ next_url(ccURL, ccImage, {class: 'cc-opacity'}) }}
  </div>
{%- endif %}
```


## 参考文章
+ [Hexo 搭建个人博客系列：主题美化篇](http://yearito.cn/posts/hexo-theme-beautify.html)
+ [NexT 中文使用说明](https://theme-next.iissnan.com/getting-started.html)
+ [Next -14- 为Hexo Next7.7.1 添加RSS （带按钮）]( https://www.zywvvd.com/2020/03/20/next/14_add_rss/next-add-rss/)