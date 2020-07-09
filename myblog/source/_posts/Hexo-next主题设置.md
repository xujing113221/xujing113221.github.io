---
title: Hexo next主题设置
date: 2020-07-09 14:04:34
tags: ['Hexo', 'NexT']
categories: 'Hexo NexT配置'
---


### 问题一：中文设置

打开 hexo 配置文件 _config.yml 修改

```yml
language: zh-CN
```
<!--more-->
### 问题二：tag标签设置

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



### 问题三：read more 设置问题

使用在Markdown文件中添加如下内容即可

```Markdown
<!--more-->
```


### 添加valine评论系统

### 开启阅读量


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

注意该搜索功能需要依赖 `hexo-generator-searchdb` 插件，依然还是使用命令 npm install `hexo-generator-searchdb --save` 来进行安装。然后 在 hexo 站点根目录配置文件 `_config.xml` 的末尾，加入以下代码即可。

```yml
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

### 代码可复制


### 参考文章

1. [Hexo NexT 主题 7.x 版本的使用配置与美化](https://xian6ge.cn/posts/6d7ed114/)
0. [Hexo博客+Next主题深度优化与定制](https://hasaik.com/posts/ab21860c.html)