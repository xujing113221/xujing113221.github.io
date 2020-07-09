---
title: Hexo next主题设置
date: 2020-07-09 14:04:34
tags: ['Hexo', 'NexT']
categories: 'Hexo NexT配置'
---


### 问题一：中文设置

page : 612 

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

```Markdown
<!--more-->
```



###  修改背景，颜色样式等

转自 [Hexo NexT 主题 7.x 版本的使用配置与美化](https://xian6ge.cn/posts/6d7ed114/)

1. 打开 `themes/next/_config.yml`，找到 `custom_file_path`，打开 style 处的注释
2. 打开 `themes/hexo-theme-next/source/css/_data/style.styl`，添加如下代码。(没有_data 目录自行新建)

```css
//添加背景图片
body { background:url(/images/backGround.jpg)}
//改掉题头颜色
.site-meta {
  background: #F0D784; //修改为自己喜欢的颜色
}
//主标题颜色
.brand{
  color: #2f9833
  }
//副标题颜色
.site-subtitle{
  color: #47b54a
}
//页脚统计文字颜色
.footer{
  color: #F0D784
}
//修改页脚备案链接颜色
.footer a{
  color: #F0D784
}
//修改页脚统计人数的颜色
.footer .with-love{
  color: #F0D784
}
```

0. 如果出现编译出错，关闭 1. 中的 style，然后打开 'themes/next7/source/css/main.styl'，末尾添加

``` css
@import "_data/styles.styl";
```
