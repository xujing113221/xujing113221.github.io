---
title: 'Markdown学习笔记二 进阶篇'
date: 2020-07-09 11:23:40
tags: 'Markdown'
categories: 'Markdown学习笔记'
mathjax: true
katex: true
---

## 数学公式的使用

### 方法

使用Latex格式 [LaTeX公式编辑器](https://www.latexlive.com/)

+ 行内公式 : 使用一个$
+ 行外公式 : 使用 $$
+ 多行公式 : 使用引用 Latex 代码 

<!--more-->

### 实现

#### 行内公式 : 

```
这是一个行内公式:  $ \int \frac{1}{1+x^{2}}\mathrm{d}x= \arctan x +C $ 
```
这是一个行内公式:  $ \int \frac{1}{1+x^{2}}\mathrm{d}x= \arctan x +C $ 

#### 行外公式 : 

```
这是一个行外公式举例：$$y = x \cos \alpha + \cos \beta =2 \cos \frac{\alpha + \beta}{2}\cos \frac{\alpha - \beta}{2} $$
```

这是一个行外公式举例：$$y = x \cos \alpha + \cos \beta =2 \cos \frac{\alpha + \beta}{2}\cos \frac{\alpha - \beta}{2} $$

#### 多行公式 : 使用引用 Latex 代码 

```katex
\displaystyle
\left( \sum\_{k=1}^n a\_k b\_k \right)^2
\leq
\left( \sum\_{k=1}^n a\_k^2 \right)
\left( \sum\_{k=1}^n b\_k^2 \right)
```

```
f(x) = \int_{-\infty}^\infty
    \hat f(\xi)\,e^{2 \pi i \xi x}
    \,d\xi
```

$$
\displaystyle
\left( \sum\_{k=1}^n a\_k b\_k \right)^2
\leq
\left( \sum\_{k=1}^n a\_k^2 \right)
\left( \sum\_{k=1}^n b\_k^2 \right)
$$

$$
f(x) = \int_{-\infty}^\infty
    \hat f(\xi)\,e^{2 \pi i \xi x}
    \,d\xi
$$


## 绘制流程图

### 添加支持
Hexo 默认是不支持流程图的 Markdown 语法的，需要添加支持：
```bash
 $ npm install --save hexo-filter-flowchart
 ```

### 绘制流程图
```flow
st=>start: 用户登陆
op=>operation: 登陆操作
cond=>condition: 登陆成功 Yes or No?
e=>end: 进入后台

st->op->cond
cond(yes)->e
cond(no)->op
```


## 复选框列表

```Markdown
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported;
- [x] list syntax required (any unordered or ordered list supported);
- [x] this is a complete item;
- [ ] this is an incomplete item [test link](#);
- [ ] this is an incomplete item;
    - [ ] this is an incomplete item [test link](#);
    - [ ] this is an incomplete item [test link](#);
- [x] list syntax required (any unordered or ordered list supported);
- [x] this is a complete item;
- [ ] this is an incomplete item [test link](#);
- [ ] this is an incomplete item;
    - [ ] this is an incomplete item [test link](#);
```

- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported;
- [x] list syntax required (any unordered or ordered list supported);
- [x] this is a complete item;
- [ ] this is an incomplete item [test link](#);
- [ ] this is an incomplete item;
    - [ ] this is an incomplete item [test link](#);
    - [ ] this is an incomplete item [test link](#);
- [x] list syntax required (any unordered or ordered list supported);
- [x] this is a complete item;
- [ ] this is an incomplete item [test link](#);
- [ ] this is an incomplete item;
    - [ ] this is an incomplete item [test link](#);

参考链接 [Github Flavored Markdown task lists](http://editor.md.ipandao.com/examples/task-lists.html)

*可能由于渲染问题无法实现*


