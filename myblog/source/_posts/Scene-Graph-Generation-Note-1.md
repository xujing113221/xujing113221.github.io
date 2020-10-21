---
title: Scene Graph Generation Note 1
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
    - Motifs
categories:
    - [学习笔记, 计算机视觉]
password:
---

本文记录一下Hiwi的相关笔记。
<!--more-->

### how to make

```bash
ssh ssh1

ssh tntpc

ssh persephone

source ~/.git-prompt.sh

source ~/miniconda3/bin/activate
 :$PATH

export LANG=en_US.UTF-8
```

### neural-motifs

+ env

  1. conda
  2. conda install python=3.6
  3. conda install pytorch=0.3.0 torchvision=0.2.0 cuda90 -c pytorch
  4. conda install cython
  5. conda install h5py
  6. pycocotools:
      `git clone https://github.com/pdollar/coco.git | make | python setup.py build_ext install`
  7. conda install dill
  8. conda install pandas
  9. pip install overrides

+ dataset:
/data/scene_understanding/Visual_Genome/

+ pycharm:
sh ~/tmp/pycharm-community-2020.2.1/bin/pycharm.sh &
```bash
export PYTHONPATH=/home/xujing/Dokumente/neural-motifs/:/home/xujing/Dokumente/neural-motifs/lib/
```

### DYNSG

#### env

1. conda install pytorch=1.0.0 torchvision=0.2.1 cuda100 -c pytorch
2. opencv
   conda install -c https://conda.anaconda.org/menpo opencv
   pip install opencv-python
3. pip install easydict

export PATH=/usr/local/cuda-10.0/bin:$PATH

#### issues

1. _C.cpython-36m-x86_64-linux-gnu.so
   pip install -U torchvision==0.4.0

2. https://ucasfl.github.io/2017/12/21/fix-the-problem-of-that-usr-lib-x86-64-linux-gnu-libstdc-so-6-version-GLIBCXX-3-4-22-not-found/


export PYTHONPATH=/home/xujing/Dokumente/DynSG/fasterrcnn/lib/:/home/xujing/Dokumente/DynSG/

export PYTHONPATH=$PYTHONPATH:/home/xujing/miniconda3/envs/dynsg/lib/


### cuda

import torch

torch.cuda.is_available()
print(torch.version.cuda)
torch.backends.cudnn.enabled

python -c "import torch;print(torch.version.cuda)"

CUDA_VISIBLE_DEVICES=3

nvidia-smi

### conda

+ source activate $envname
+ source deactivate
+ conda list -e requeirment.txt
+ conda install --yes --file requirements.txt
+ conda env export > environment.yaml
+ conda env create -f environment.yaml
+ conda create -n py36 python=3.6 

### software

intern net: 
    firefox http://tntintern/

emial:
thunderbird

### linux command

check the size of path:
    du -h filepath  

screen:
    screen -S $Name
    screen -ls
    screen -r $id
    [detached] ctrl+a+d

### conda pip env transform

[conda环境转移复制和pip包的转移复制](https://www.jianshu.com/p/b86c17057da8?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)


### vnc 
1. on servers (cp202-03)
   vncserver -geometry 1920x1080 :8
2. on local (mac)
    ssh -fNCT -L 5902:cp202-03:5908 xujing@ssh1.tnt.uni-hannover.de
3. on vnc view
   connect: localhost:5902
4. kill 
   vncserver -kill :8

### ssh
+ [vscode通过跳板机(堡垒机)连接remote服务器](https://blog.csdn.net/dcz1994/article/details/103120254)

LocalForward 5902 cp202-03:5908


### reference

+ https://rowanzellers.com/neuralmotifs/
+ https://rowanzellers.com/scenegraph2/
+ [scene graph(visual relation) 简述](https://www.twblogs.net/a/5bbd3c892b71776bd30c2020/?lang=zh-cn)
+ [Object Detection and Classification using R-CNNs](https://www.telesens.co/2018/03/11/object-detection-and-classification-using-r-cnns/)
+ [Faster RCNN-PyTorch版本运行记录](https://www.pythonf.cn/read/82784)

