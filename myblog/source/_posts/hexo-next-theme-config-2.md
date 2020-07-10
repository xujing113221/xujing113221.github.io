---
title: Hexo NexT 主题配置二
date: 2020-07-09 22:29:36
tags: ['Hexo', 'NexT']
categories: 'Hexo NexT配置'
---

## 回到顶部按钮设置

在主题配置文件中搜索`back2top`,进行修改

```yml
back2top:
  enable: true
  # Back to top in sidebar.
  sidebar: false  # 是否在侧边栏显示
  # Scroll percent label in b2t button.
  scrollpercent: true   #显示百分比
  ```
<!--more-->

## 添加打赏功能

修改如下主题配置文件即可：
```yml
# Reward (Donate)
# Front-matter variable (unsupport animation).
reward_settings:
  # If true, reward will be displayed in every article by default.
  enable: true
  animation: false
  comment: 也不知道下面这个按钮有没有用.

reward:
  wechatpay: /images/wechatpay.png
  alipay: /images/alipay.png
  #paypal: /images/paypal.png
  #bitcoin: /images/bitcoin.png
  ```

## 代码可复制

过程有点复杂，参见：[Hexo NexT 代码块复制功能](https://www.jianshu.com/p/3e9d614c1e77) ，但是我没有成功。
会有如下问题：
```console
clipboard-use.js:8 Uncaught ReferenceError: $ is not defined
    at initCopyCode (clipboard-use.js:8)
    at clipboard-use.js:15
    at clipboard-use.js:16
```

我的解决方案：
  新版NexT的新功能吧，新版本[NexT](https://github.com/theme-next/hexo-theme-next)
  在主题配置文件中搜索 `copy_button` 修改如下内容：
``` yml
 # Add copy button on codeblock
  copy_button:
    enable: true
    # Show text copy result.
    show_result: true
    # Available values: default | flat | mac
    style: flat
```

测试代码：
```cpp
#include<iostream>
using namespace std;

int main()
{
    cout << "hello world!" << endl;
    return 0;
}
```

原来这么简单，害我搞了那么半天，这样子也蛮好看的！

## 开启相关文章推荐功能

开启相关文章推荐需要安装`hexo-related-popular-posts`模块，在站点根目录下使用如下命令安装模块，
```bash
npm install hexo-related-popular-posts --save 
```
然后在主题配置文件中修改如下内容：
```yml
# Related popular posts
# Dependencies: https://github.com/tea3/hexo-related-popular-posts
related_posts:
  enable: true
  title: 相关文章推荐 #Custom header, leave empty to use the default one
  display_in_home: false
  params:
    maxCount: 5
    #PPMixingRate: 0.0
    #isDate: false
    #isImage: false
    #isExcerpt: false
```
> 当前`hexo-related-popular-posts`版本`4..0.0`有安全漏洞，总是安装失败，[等待更新](https://www.npmjs.com/package/hexo-related-popular-posts)

## 添加版权信息

打开主题配置文件，搜索`creative_commons`修改如下内容:
```yml
creative_commons:
  license: by-nc-sa
  sidebar: true
  post: true
  language: deed.zh
```
> 参考文章 ： [使用Hexo的next主题，配置POST文章文末的版权信息](http://blog.amdoing.com/the-post-copyright-in-hexo-next/)

## 添加图片灯箱功能

添加灯箱功能，实现点击图片后放大聚焦图片，并支持幻灯片播放、全屏播放、缩略图、快速分享到社交媒体等，该功能由`fancyBox`提供，效果如下:
![随便一张图](https://cdn.pixabay.com/photo/2017/08/02/14/26/winter-landscape-2571788__480.jpg '随便一张图')

打开主题配置文件修改如下内容：
```yml
fancybox: true
```

## 文章加密设置

> 参考链接：https://github.com/MikeCoder/hexo-blog-encrypt/blob/master/ReadMe.zh.md

1. 首先在博客目录下输入如下命令，安装`hexo-blog-encrypt`
```bash
npm install --save hexo-blog-encrypt
```
2. 在**站点**配置文件中添加如下内容：
```yml
encrypt:
  enable: true
  default_abstract: 这是我的小秘密哦!
  default_message: 你知道密码吗？
```
3. 在文章开头添加如下内容
```Markdown
---
title: Hello World
tags:
- 作为日记加密
date: 2016-03-30 21:12:21
password: mikemessi
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
```
[我的加密测试博客](http://xujing113221.github.io/encrypt-test/)

## 参考文章

+ [Hexo 搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
+ [Hexo 入门与进阶](https://juejin.im/post/5e71b0b3e51d4526f363c83b#heading-32)
+ [Hexo+NexT(v7.0+) 搭建博客：功能强化](https://www.chingow.cn/posts/e0970dc8.html)
+ [npm 是什么？](https://www.npmjs.cn/getting-started/what-is-npm/)