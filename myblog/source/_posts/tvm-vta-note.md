---
title: Note TVM/VTA
date: 2020-07-27 16:11:15
tags: 
    - TVM
    - VTA
    - Python
categories: 
    - [学习笔记, TVM]
top: false
---

I've been learning a lot about TVM this week and I visited the [TVM website](https://tvm.apache.org). I also read a lot of [tutorials](https://tvm.apache.org/docs/) and code. I found it very interesting. It just so happens that I have Raspberry Pie 3b, so I tried the tutorial code on my ubuntu computer and it worked perfectly.
<!--more-->

## What is TVM
[Apache(incubating) TVM](https://tvm.apache.org/about) is an open deep learning compiler stack for CPUs, GPUs, and specialized accelerators. It aims to close the gap between the productivity-focused deep learning frameworks, and the performance- or efficiency-oriented hardware backends. TVM provides the following main features:
+ Compilation of deep learning models in Keras, MXNet, PyTorch, Tensorflow, CoreML, DarkNet into minimum deployable modules on diverse hardware backends.
+ Infrastructure to automatic generate and optimize tensor operators on more backend with better performance.

![](https://tvm.apache.org/images/main/tvm-stack.png)

## Install TVM on Ubuntu

{% note info %}
Reference article: [Docs » Installation » Install from Source](https://tvm.apache.org/docs/install/from_source.html)
{% endnote %}

I have `Ubuntu 18.04.2 LTS` on my PC.

+ Get Source from Github
``` bash
git clone --recursive https://github.com/apache/incubator-tvm tvm
```
+ Build the Shared Library
```bash
sudo apt-get update
sudo apt-get install -y python3 python3-dev python3-setuptools gcc libtinfo-dev zlib1g-dev build-essential cmake libedit-dev libxml2-dev
```
+ Use cmake to build the library
  + copy the cmake/config.cmake to the directory
    ``` bash
        mkdir build
        cp cmake/config.cmake build
    ```
  + Edit `build/config.cmake` to customize the compilation options
    Because i have no NVIDA GPU on my pc,so don't need to set `USE_CUDA ON`
    ``` bash
        set(USE_GRAPH_RUNTIME ON) 
        set(USE_GRAPH_RUNTIME_DEBUG ON)
        set(USE_LLVM ON)
        set(USE_VTA_FSIM ON)  # enable VTA Simulator 
    ```
+ Build tvm and related libraries.
    ```bash
        cd build
        cmake ..
        make -j4
    ```
+ Set the environment variable for Python
```bash
export TVM_HOME=~/tvm
export PYTHONPATH=$TVM_HOME/python:$TVM_HOME/python:$TVM_HOME/topi/python:${TVM_HOME}/vta/python:${PYTHONPATH}
export VTA_HW_PATH=$TVM_HOME/3rdparty/vta-hw
```
+ To update the environment variables, execute `source ~/.bashrc`.

## configuration my Raspberry pi 

My raspberry pi model is `Raspberry Pi 3 Model B Rev 1.2`.

### Setup my Raspberry pi 3b
1. Prepare Raspberry pi 3 and an 8GB TF. and download [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/), i choiced `Raspberry Pi OS (32-bit) with desktop`.
2. Formatting TF ，write Pi images to TF using `Win32DiskImager`.
3. No display start-up method
   1. Create a new empty `ssh` file in the memory card boot disk, in order to turn on the ssh function.
   2. Create a new `wpa_supplicant.conf` text file in the memory card boot disk, write wifi configuration.
    ``` conf
    country=DE
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
        ssid="my wifi name"
        psk="my wifi password"
        key_mgmt=WPA-PSK
        priority=1
    }
    ```
4. Find the IP adress of your respberry pi in rounter. contect your resperry pi via `ssh`
   ```bash
    ssh pi@<ip adress> # password: raspberry
   ```
5. Use VNC to connect raspberry pi. Command `sudo raspi-config` to configuration.

### Install TVM on Raspberry pi
+ We only need to build tvm runtime on the remote device.
``` bash
cd ~
git clone --recursive https://github.com/apache/incubator-tvm tvm
cd tvm
mkdir build
cp cmake/config.cmake build
cd build
cmake ..
make runtime -j4
```
+ set environment varibles in `~/.bashrc` file.
```conf
export PYTHONPATH=$PYTHONPATH:~/tvm/python
```
+ To update the environment variables, execute `source ~/.bashrc`.


## Environment Building

### Ubuntu
1. [LLVM](http://llvm.org)
    ``` bash
    cd ~
    wget https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
    tar -xvf clang+llvm-10.0.0-armv7a-linux-gnueabihf.tar.xz
    rm clang+llvm-10.0.0-armv7a-linux-gnueabihf.tar.xz
    mv clang+llvm-10.0.0-armv7a-linux-gnueabihf clang_9.0.0
    sudo mv clang_10.0.0 /usr/local
    ```
    set environment varibles
    ```conf ~/.bashrc
    export PATH=/usr/local/clang_10.0.0/bin:$PATH
    export LD_LIBRARY_PATH=/usr/local/clang_10.0.0/lib:$LD_LIBRARY_PATH
    ```
2. Cross Compiler
   we need `/usr/bin/arm-linux-gnueabihf-g++`
    ``` bash
    sudo apt-get install g++-arm-linux-gnueabihf
    /usr/bin/arm-linux-gnueabihf-g++ -v
    ```
### python

1. Pytorch
    ```bash
    sudo pip3 install torch torchvision 
    ```
2. onnx
   pytorch->onnx->tvm
   ``` bash
   pip3 install onnx
   ```
3. python-opencv
   ```bash
    pip3 install opencv-python 
    pip3 install opencv-contrib-python 
   ```
   
### other tool
1. Neron
   1. online: https://lutzroeder.github.io/netron/
   2. download: https://github.com/lutzroeder/netron/find/main
2. CUDA (i dont use it.because i have no NVIDA GPU)
3. [opencv](https://docs.opencv.org/master/d9/df8/tutorial_root.html) 
   1. download zip source form https://github.com/opencv/opencv/releases
   2. install contri
    ```bash
    sudo apt-get install build-essential
    sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
    sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev lib
    ```
   3. cmake 
    ``` bash
        cd ~/opencv-3.4.3  
        mkdir build 
        cd build 
        cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..  
        make -j7 
        sudo make install
    ```

## Deploy model on raspberry pi

{%note info%}
Reference :[Deploy the Pretrained Model on Raspberry Pi](https://tvm.apache.org/docs/tutorials/frontend/deploy_model_on_rasp.html)
{%endnote%}
I run this [tutorials code](https://tvm.apache.org/docs/_downloads/83dedc6352b4016772e17480ef01345d/deploy_model_on_rasp.py) on Ubuntu 
1. Connect Raspberry pi via ssh
   ```bash
   ssh pi@192.168.2.105
   ```
2. Start an RPC server on Raspberry pi
   ```bash
   python3 -m tvm.exec.rpc_server --host 0.0.0.0 --port=9090
   INFO:RPCServer:bind to 0.0.0.0:9090 # RPC server started successfully
   ```
3. Run code on Unbuntu
   ```bash
    python3 python3 deploy_model_on_rasp.py
   ```
4. result
   1. Raspberry pi
    ```bash
    INFO:RPCServer:connection from ('192.168.2.108', 57062)
    INFO:RPCServer:load_module /tmp/tmppv_8msd5/net.tar
    INFO:RPCServer:Finish serving ('192.168.2.108', 57062)
    ```
   2. Ubuntu
    ![](https://github.com/dmlc/mxnet.js/blob/master/data/cat.png?raw=true 'in_data x') 
    ![](../image/tvm_plane.jpg 'in_data y')   
    Model : MXNet `resnet18_v1`
    ```bash Run model on raspberry pi via RPC
    Time for model loading is 281.33s
    Time for build graph  is 1.09s
    Time for model running is 1.33s
    x TVM prediction top-1: tiger cat
    y TVM prediction top-1: airliner
    ```
    ```bash Run model on local pc
    Time for model loading is 0.90s
    Time for bulid graph is 0.03s
    Time for model running is 0.10s
    x TVM prediction top-1: tiger cat
    y TVM prediction top-1: airliner
    ```

Running model on Raspberry Pi is significantly slower than running it on Ubuntu, mainly because it is too slow to load model through RPC. But it works.
Deploy model on raspberry pi through LLVM, deploy model on FPGA through VTA. 
    
## Reference
+ [Apache (incubating) TVM An End to End Deep Learning Compiler Stack](https://tvm.apache.org)
+ [VTA: 开源AI芯片栈](https://zhuanlan.zhihu.com/p/39635145)
+ [VTA：一个开放、高度可定制化的深度学习加速器平台](https://www.infoq.cn/article/vta-release-announcement/)
+ [菜鸟驿站 - Docker 教程](https://www.runoob.com/docker/docker-tutorial.html)
+ [Docker —— 从入门到实践](https://wiki.jikexueyuan.com/project/docker-technology-and-combat/)
+ [一步一步解读神经网络编译器TVM(一)——一个简单的例子](https://oldpan.me/archives/the-first-step-towards-tvm-1)
+ [一步一步解读神经网络编译器TVM(二)——利用TVM完成C++端的部署](https://oldpan.me/archives/the-first-step-towards-tvm-2)
+ [树莓派入门（一） - 下载安装系统镜像，Raspbian和Centos](https://blog.csdn.net/zhshh123/article/details/85051969)
+ [Raspberry Pi - Install Clang 9 and compile C++17 and C++20 programs](https://solarianprogrammer.com/2018/04/22/raspberry-pi-raspbian-install-clang-compile-cpp-17-programs/)
