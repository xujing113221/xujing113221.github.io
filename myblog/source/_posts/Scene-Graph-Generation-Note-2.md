---
title: Scene Graph Generation Note 2
abstract: 这是我的小秘密哦
message: 你知道密码吗？
wrong_pass_message: 你果然不知道密码！
date: 2020-10-21 22:31:57
top:
tags: 
    - Computer Vision
    - Deep Learning
    - Pytorch
    - CUDA
categories:
    - [学习笔记, 计算机视觉]
password:
---

本文记录一下Hiwi的相关笔记, 第二部分。
<!--more-->

###  调试工具

[PyTorch代码调试利器: 自动print每行代码的Tensor信息](https://www.jiqizhixin.com/articles/2019-06-18-10)

### tenserbroad

+ for pytorch=1.2
pip install tensorboard
pip install tensorflow

+ for pytorch=0.4
pip install tensorboardX

### netron

+ https://lutzroeder.github.io/netron/
+ 


### VNC

ssh -fNCT -L 5902:cp202-03:5908 xujing@ssh1.tnt.uni-hannover.de

### MSDN

```bash
export PYTHONPATH=/home/xujing/Dokumente/MSDN/:/home/xujing/Dokumente/MSDN/faster_rcnn/

export PATH=/home/xujing/miniconda3/envs/msdn/bin:/home/xujing/miniconda3/condabin:/usr/local/cuda-8.0/bin:/home/xujing/.vscode-server/bin/e790b931385d72cf5669fcefc51cdf65990efa5d/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/snap/bin

conda install cudnn=7.1.2
```


### install

[Faster RCNN-PyTorch版本运行记录](https://www.pythonf.cn/read/82784)

git checkout pytorch1.0

cd lib
python setup.py build develop


### Blog
https://www.telesens.co/2018/03/11/object-detection-and-classification-using-r-cnns/

### reference
+ [基于深度学习的目标检测技术演进：R-CNN、Fast R-CNN、Faster R-CNN](https://www.cnblogs.com/skyfsm/p/6806246.html)



