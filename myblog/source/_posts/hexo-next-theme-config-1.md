---
title: Hexo NexT 主题设置一
date: 2020-07-09 14:04:34
tags: 
    - Hexo
    - NexT
categories: 
    - [学习笔记, Hexo创建博客]
---

本文是我用Hexo配置NexT主题的笔记，主要内容有以下几点：
+ 中文设置
+ tag标签设置
+ read more 设置
+ tag标签设置
+ 添加valine评论系统
+ 不蒜子站点统计功能
+ 开启博客本地搜索
  
<!--more-->

### 中文设置

打开 hexo 配置文件 _config.yml 修改

```yml
language: zh-CN
```

### tag标签设置

1. 打开主题设置 `_config.yml`,  打开想要的属性

```yml
menu:
  home: / || fa fa-home
  #about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```

2. 打开terminal 输入如下内容, 例子： 给文章添加“categories”属性

```bash
$ hexo new page categories
INFO  Created: ~/Desktop/xujing113221.github.io/myblog/source/categor
```

3. 打开主题下的 `/source/categories/index.md` 

```Markdown
---
title: categories
date: 2020-07-09 15:05:00
---
```

添加如下内容

```Markdown
---
title: categories
date: 2020-07-09 15:05:00
type: "categories"
---
```



### read more 设置

使用在Markdown文件中添加如下内容即可

```Markdown
<!--more-->
```


### 添加valine评论系统

#### 注册LeanCloud

我使用的是[国际版](https://leancloud.app), 中国版需要实名认证，有点麻烦。

#### 创建应用

+ 点击创建应用按钮:
![创建应用](https://raw.githubusercontent.com/lanlan2017/images/master/Blog/Hexo/Next/Plugin/ValineCommentSystem/1.png)

+ 选择开发版
![选择开发版](https://raw.githubusercontent.com/lanlan2017/images/master/Blog/Hexo/Next/Plugin/ValineCommentSystem/2.png)

+ 进入设置 
![进入设置](https://raw.githubusercontent.com/lanlan2017/images/master/Blog/Hexo/Next/Plugin/ValineCommentSystem/3.png)

#### 配置应用

##### 设置Web安全域名，填入自己的域名

依次点击左侧边栏上的**设置**,**安全中心**,然后下拉页面,找到**Web 安全域名**,把你*站点的域名*填写进去。  
服务开关中仅保留 **数据存储**。

##### 获取APP ID 和 APP Key
依次点击左侧边栏上的**设置**, **应用 Keys**,然后复制下**AppID**和**AppKey**:

#### 修改Next主题配置文件

打开博客目录的next主题配置文件 `_config.yml` ，找到`Valine`，将上图的`APP ID` 和`APP Key`复制到对应位置。
```yml theme/next/_config.yml 
valine:
  enable: true
  appid: XXXXXXX-MdYXbMMI # Your leancloud application appid
  appkey: XXXXXXXXX # Your leancloud application appkey
  notify: false # Mail notifier
  verify: false # Verification code
  placeholder: Write something to me ... # Comment box placeholder
  avatar: retro # Gravatar style
  guest_info: nick,mail,link # Custom comment header
  pageSize: 10 # Pagination size
  language: zh-cn # Language, available values: en, zh-cn
  visitor: false # Article reading statistic
  comment_count: true # If false, comment count will only be displayed in post page, not in home page
  recordIP: false # Whether to record the commenter IP
  serverURLs: # When the custom domain name is enabled, fill it in here (it will be detected automatically by default, no need to fill in)
  #post_meta_order: 0
```

#### 如何删除评论

依次点击左侧边栏上的**存储**, **数据化结构**, **Comment**, 直接删除表：
![这样删除](https://raw.githubusercontent.com/lanlan2017/images/master/Blog/Hexo/Next/Plugin/ValineCommentSystem/20.png)

#### To do ：在LeanCloud上部署云引擎

可实现
+ 评论 邮件提醒功能
+ 登陆评论管理系统

[别人写的引擎](https://github.com/zhaojun1998/Valine-Admin)
[参考的博客](https://lanlan2017.github.io/blog/de4f7be8/)


#### 开启阅读量

在主题配置中搜索 `leancloud_visitors` ，更改如下配置：

```yml theme/next/_config.yml 
leancloud_visitors:
  enable: true
  app_id: xXXXXXXXxx # <your app id>
  app_key: xxxxxxx # <your app key>
  # Required for apps from CN region
  server_url: # <your server url>
  # Dependencies: https://github.com/theme-next/hexo-leancloud-counter-security
  # If you don't care about security in leancloud counter and just want to use it directly
  # (without hexo-leancloud-counter-security plugin), set `security` to `false`.
  security: true
```
参考文章：[Hexo Next主题 使用LeanCloud统计文章阅读次数、添加热度排行页面](https://blog.qust.cc/archives/48665.html)

### 不蒜子站点统计功能

打开主题配置文件，搜索`busuanzi`,修改如下内容：
```yml theme/next/_config.yml 
busuanzi_count:
  enable: true
  total_visitors: true #站点访问量
  total_visitors_icon: fa fa-user
  total_views: true   # 站点阅读量
  total_views_icon: fa fa-eye
  post_views: false  # 文章阅读数
  post_views_icon: fa fa-eye
```
{%note warning%}
如果开启了LeanCloud统计阅读次数，就不要打开不蒜子的 `post_views`.
{%endnote%}



### 开启博客本地搜索

提升读者用户体验，博客内肯定是需要一个全局搜索按钮的。当然hexo已经集成了几款开源的搜索插件，一般都使用的是 `local_search`.

搜索 `local_search` , 设置代码如下：

```yml
# Local search
# Dependencies: https://github.com/theme-next/hexo-generator-searchdb
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # unescape html strings to the readable one
  unescape: false
```

注意该搜索功能需要依赖 `hexo-generator-searchdb` 插件，依然还是使用命令 `npm install hexo-generator-searchdb --save` 来进行安装。然后 在 hexo 站点根目录配置文件 `_config.xml` 的末尾，加入以下代码即可。

```yml
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```


### 参考文章

1. [Hexo NexT 主题 7.x 版本的使用配置与美化](https://xian6ge.cn/posts/6d7ed114/)
0. [Hexo博客+Next主题深度优化与定制](https://hasaik.com/posts/ab21860c.html)
0. [Hexo Next主题 添加Valine评论系统 设置有新评论时自动发邮件提醒](https://lanlan2017.github.io/blog/de4f7be8/)
0. [Hexo Next主题 使用LeanCloud统计文章阅读次数、添加热度排行页面](https://blog.qust.cc/archives/48665.html)
1. [Hexo博客搭建之在文章中插入图片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)