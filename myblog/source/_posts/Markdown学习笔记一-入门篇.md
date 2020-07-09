---
title: 'Markdown学习笔记一: 入门篇'
date: 2020-07-08 22:18:17
tags: 'Markdown'
categories: 'Markdown学习笔记'
---

## 标题使用方法

```
#h1标题
##h2标题
###h3标题
####h4标题
#####h5标题
######h6标题
```
<!--more-->

#h1标题
##h2标题
###h3标题
####h4标题
#####h5标题
######h6标题

### 特例

```
h1标题
===
h2标题
---
```
****


## 自然段改行 `<br>`


### 方法一
这是第一自然段

这是第二自然段
### 方法二

这是第一自然段第一部分  
这是第一自然段第二部分

### 总结
```
### 方法一
这是第一自然段
(回车两下)
这是第二自然段
### 方法二
这是第一自然段第一部分  （空格两下）
这是第一自然段第二部分
```

*** 

## 引用表现


>添加 `>` 即可引用

****

## 为文章添加分割线`<hr>`

### 四种方法

```
 ---
 ***
 ___
 - - -
```

**注意与h2的区别*

```
这是第一自然段
(这里必须有个换行)
---
这是第二自然段
***
这是第三自然段
___
这是第四自然段
- - -
```
这是第一自然段

---
这是第二自然段
***
这是第三自然段
___
这是第四自然段
- - -

## 文字处理

### 方法
斜体：`*XXX*`， `_XXX_`
粗体：`**XXX**`, `__XXX__`
删除：`~~XXX~~`
下划线: `<u>XXX</u>`

###实现
```
这是一个*斜体举例*  
这是一个**粗体举例**
这是一个~~删除举例~~
这是一个<u>下划线举例</u>
```
这是一个*斜体举例*  
这是一个**粗体举例**
这是一个~~删除举例~~
这是一个<u>下划线举例</u>

*****

## 列表表示

### 方法

* 列表符号：-
* 列表符号：*
* 列表符号：+
* 列表符号：数字（有序）

### 举例

* **无序列表**
```
* 第一大项
* 第二大项
    * 第三小项
    * 第四小项
* 第五项
```
* 第一大项
* 第二大项
    * 第三小项
    * 第四小项
* 第五项

***

* **有序列表**
```
1. 数字项一
0. 数字项二
0. 数字项三
0. 数字项四
0. 数字项五
```

*注意：数字与顺序无关*

1. 数字项一
0. 数字项二
0. 数字项三
0. 数字项四
0. 数字项五

****

## 超链接


### 方法

~~~
http://www.google.com
<http://www.google.com>
[google](http://www.google.com)
[google](http://www.google.com "google wedsite") (推荐使用)
~~~

### 实现
http://www.google.com
<http://www.google.com>
[google](http://www.google.com)
[google](http://www.google.com "google wedsite")

***

## 代码高亮显示


### 方法

代码高亮显示符号： ```（推荐使用反单引号）
代码高亮显示符号：~~~

### 实现

* c语言例子 (三个'实现)
``` C
#include<stdio.h>

int main()
{
    printf("hello world!\n");
    return 0;
}
```
* python 例子（三个～实现）
~~~ python
print("hello world")
~~~

* 还有一种实现方法 `print("hello world")` 就是在这样：一个`

***

## 图片显示

### 方法

图片的引用与显示： `![alt文字说明](图片url 图片tittle)`

### 实现

* 纯图片显示
~~~
![LUH image](https://www.uni-hannover.de/typo3conf/ext/luh_website/Resources/Public/Images/Logo/luh_logo.svg "uni hannver png")
~~~
![LUH image](https://www.uni-hannover.de/typo3conf/ext/luh_website/Resources/Public/Images/Logo/luh_logo.svg "uni hannver png")

* 图片加超链接
~~~
[![LUH image](https://www.uni-hannover.de/typo3conf/ext/luh_website/Resources/Public/Images/Logo/luh_logo.svg "uni hannver png")](https://www.uni-hannover.de "uni hannover")
~~~
[![LUH image](https://www.uni-hannover.de/typo3conf/ext/luh_website/Resources/Public/Images/Logo/luh_logo.svg "uni hannver png")](https://www.uni-hannover.de "uni hannover")


*****

## 表格显示


### 方法

* 使用 `-` 和 `|` 实现
* 使用 `：` 实现 居左 居中 居右 

### 实现

* 普通表格

```
| th1 | th2 | th3 |
------|-----|-----
| td1 | td2 | td3 |
| td4 | td5 | td6 |
```

| th1 | th2 | th3 |
------|-----|-----
| td1 | td2 | td3 |
| td4 | td5 | td6 |

* 表格对齐

```
| 居左 | 居中 | 居右|
:-----|:---:|----:
| td1 | td2 | td3 |
| td4 | td5 | td6 |
```

| 居左 | 居中 | 居右|
:-----|:---:|----:
| td1 | td2 | td3 |
| td4 | td5 | td6 |

