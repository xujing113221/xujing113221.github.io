---
title: Scene Graph Generation Note 3
abstract: 这是我的小秘密哦
message: 你知道密码吗？
wrong_pass_message: 你果然不知道密码！
date: 2020-10-21 22:31:57
top:
tags: 
    - Computer Vision
    - Deep Learning
    - Pytorch
categories:
    - [学习笔记, 计算机视觉]
password:
---

本文记录一下Hiwi的相关笔记, 第三部分。
<!--more-->

conda install pytorch=1.0
pip install cython
pip install matplotlib numpy scipy pyyaml packaging pycocotools tensorboardX tqdm pillow scikit-image
conda install opencv


### envriment
+ PATH 
export PATH=/home/xujing/miniconda3/envs/cl4vrd/bin:/home/xujing/miniconda3/condabin:/usr/local/cuda-10.0/bin:/home/xujing/.vscode-server/bin/58bb7b2331731bf72587010e943852e13e6fd3cf/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/snap/bin

+ PYTHONPATH
export PYTHONPATH=/home/xujing/Dokumente/ContrastiveLosses4VRD


### isuss

+ 如何解决 /Usr/lib/x86_64-Linux-gnu/libstdc++.so.6 Version GLIBCXX_3.4.22' Not Found
  ``` bash
  export LD_LIBRARY_PATH=/home/xujing/miniconda3/envs/dynsg/lib/
  ```

+ Q: ImportError: torch.utils.ffi is deprecated. Please use cpp extensions instead.
A:
```diff
- from torch.utils.ffi import create_extension
+ from torch.utils.cpp_extension import BuildExtension as create_extension
```

+ Q: ValueError: numpy.ufunc size changed, may indicate binary incompatibility. Expected 216 from C header, got 192 from PyObject
A: conda install numpy=1.17.4

+ 解决软连接参数过长
``` bash
find /data/scene_understanding/Visual_Genome/VG_100K/ -name "*.jpg" | xargs -i ln -s {} VG_100K
```

### reference
[PyTorch 学习笔记（六）：PyTorch的十八个损失函数](https://zhuanlan.zhihu.com/p/61379965)