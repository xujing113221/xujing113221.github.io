---
title: Hexo NexT 主题配置二
date: 2020-07-09 22:29:36
tags: ['Hexo', 'NexT']
categories: 'Hexo NexT配置'
---

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
<!--more-->

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
``` C++
#include<iostream>
using namespace std;

int main()
{
    cout << "hello world!" << endl;
    return 0;
}
```

原来这么简单，害我搞了那么半天，这样子也蛮好看的！

