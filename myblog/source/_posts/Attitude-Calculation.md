---
title: AHSR 传感器姿态解算
permalink: 转链接
abstract: 这是我的小秘密哦
message: 你知道密码吗？
wrong_pass_message: 你果然不知道密码！
date: 2022-01-20 16:31:11
top:
tags: 
    - AHSR
    - IMU
    - Sensor
categories: 技术文档
password: meituan
wrong_pass_message: 你果然不知道密码！
wrong_hash_message: 秘密你是看不了，给你看个大宝贝吧！
---

学习内容：

+ Madgwick 与 Mahony 
+ ahrs

## AHRS 

AHRS 航姿参考系统 Attitude and heading reference system

IMU 惯性测量单元 Inertial Measurement Unit

按照习惯，推导过程中使用的导航坐标系为东北天坐标系（ENU），IMU的载体坐标系为载体坐标系为：右、前，上 $$(X,Y,Z)$$,欧拉角的旋转顺序为：![[公式]](https://www.zhihu.com/equation?tex=Z),![[公式]](https://www.zhihu.com/equation?tex=X),![[公式]](https://www.zhihu.com/equation?tex=Y)(偏航、俯仰，滚转)。



## 算法

Explicit Complementary Filter(ECF) 互补滤波算法  Mahony

Gradient Descent Filter(GD) 梯度下降算法 madgwick



Extended Kalman Filter(EKF) 姿态融合算法

[IMU加速度、磁力计校正－－椭球拟合](https://blog.csdn.net/shenshikexmu/article/details/70143455)



### 准备工作

#### 坐标系

***右手系***

手机坐标系： 右前上

大地坐标系：东北天

#### 四元素到旋转矩阵

将向量从机体坐标系 *b* 到大地坐标系 *R* 的 姿态矩阵 $𝐶^𝑅_𝑏$:

​							$C_{b}^{R}=\left[\begin{array}{lll}1-2\left(q_{2}^{2}+q_{3}^{2}\right) & 2\left(q_{1} q_{2}-q_{0} q_{3}\right) & 2\left(q_{1} q_{3}+q_{0} q_{2}\right) \\ 2\left(q_{1} q_{2}+q_{0} q_{3}\right) & 1-2\left(q_{1}^{2}+q_{3}^{2}\right) & 2\left(q_{2} q_{3}-q_{0} q_{1}\right) \\ 2\left(q_{1} q_{3}-q_{0} q_{2}\right) & 2\left(q_{2} q_{3}+q_{0} q_{1}\right) & 1-2\left(q_{1}^{2}+q_{2}^{2}\right)\end{array}\right]$

从大地坐标系 *R* 转换到机体坐标系 *b* 的坐标转换矩阵 $𝐶^𝑏_𝑅$:

​							$C_{R}^{b}=\left[\begin{array}{lll}1-2\left(q_{2}^{2}+q_{3}^{2}\right) & 2\left(q_{1} q_{2}+q_{0} q_{3}\right) & 2\left(q_{1} q_{3}-q_{0} q_{2}\right) \\ 2\left(q_{1} q_{2}-q_{0} q_{3}\right) & 1-2\left(q_{1}^{2}+q_{3}^{2}\right) & 2\left(q_{2} q_{3}+q_{0} q_{1}\right) \\ 2\left(q_{1} q_{3}+q_{0} q_{2}\right) & 2\left(q_{2} q_{3}-q_{0} q_{1}\right) & 1-2\left(q_{1}^{2}+q_{2}^{2}\right)\end{array}\right]$

其中：

​							$q_{0}=\cos \left(\frac{1}{2} \theta\right), q_{1}=\sin \left(\frac{1}{2} \theta\right) u_{x}, q_{2}=\sin \left(\frac{1}{2} \theta\right) u_{y}, q_{3}=\sin \left(\frac{1}{2} \theta\right) u_{z}$



#### 旋转矩阵到欧拉角



#### 安卓获取欧拉角

![1641471164063-image](/Users/xujing/Desktop/1641471164063-image.png) 参考：[SensorManager](https://developer.android.google.cn/reference/android/hardware/SensorManager?hl=en#getOrientation(float[],%20float[]))

![截屏2022-01-06 21.28.50](/Users/xujing/Library/Application Support/typora-user-images/截屏2022-01-06 21.28.50.png)

![截屏2022-01-06 21.26.26](/Users/xujing/Library/Application Support/typora-user-images/截屏2022-01-06 21.26.26.png)

参考：[无人机飞控算法-姿态估计-欧拉角-旋转矩阵-四元数](https://zhuanlan.zhihu.com/p/336357646)

### Mahony 互补滤波算法



### Madgwick 梯度下降算法

$\boldsymbol{f}\left({ }_{E}^{s} \hat{q}_{t},{ }^{E} \hat{\boldsymbol{y}},{ }^{s} \hat{\boldsymbol{y}}_{t}\right)=\hat{\boldsymbol{M}}_{t}{ }^{E} \hat{\boldsymbol{y}}^{T}-{ }^{s} \hat{\boldsymbol{y}}_{t}^{T}=\left[\begin{array}{c}2\left(q_{1} q_{3}-q_{0} q_{2}\right)-a_{x} \\ 2\left(q_{0} q_{1}+q_{2} q_{3}\right)-a_{y} \\ 2\left(\frac{1}{2}-q_{1}^{2}-q_{2}^{2}\right)-a_{z} \\ 2 b_{x}\left(\frac{1}{2}-q_{2}^{2}-q_{3}^{2}\right)+2 b_{z}\left(q_{1} q_{3}-q_{0} q_{2}\right)-m_{x} \\ 2 b_{x}\left(q_{1} q_{2}-q_{0} q_{3}\right)+2 b_{z}\left(q_{0} q_{1}+q_{2} q_{3}\right)-m_{y} \\ 2 b_{x}\left(q_{0} q_{2}+q_{1} q_{3}\right)+2 b_{z}\left(\frac{1}{2}-q_{1}^{2}-q_{2}^{2}\right)-m_{z}\end{array}\right]$





$\frac{\partial f\left({ }_{E}^{S} \hat{q}_{t},{ }^{E} \hat{y},{ }^{S} \hat{y}_{t}\right)}{\partial q}=J\left({ }_{E}^{S} \hat{q}_{t},{ }^{E} \hat{y},^{S}, \hat{y}_{t}\right)$

$=\left[\frac{\partial \boldsymbol{f}\left({ }_{E}^{S} \hat{q}_{t},^{E} \hat{\boldsymbol{y}},^{S} \hat{\boldsymbol{y}}_{t}\right)}{\partial q_{0}} \frac{\partial \boldsymbol{f}\left({ }_{E}^{S} q_{t},{ }^{E_{\hat{y}}},{\boldsymbol{y}}, \boldsymbol{y}_{t}\right)}{\partial q_{1}}\frac{\partial \boldsymbol{f}\left({ }_{E}^{S} \hat{q}_{t},^{E} \hat{\boldsymbol{y}},^{S} \hat{\boldsymbol{y}}_{t}\right)}{\partial q_{2}} \frac{\partial \boldsymbol{f}\left({ }_{E}^{S} q_{t},{ }^{E_{\hat{y}}},{\boldsymbol{y}}, \boldsymbol{y}_{t}\right)}{\partial q_{3}}\right]$

$=\left[\begin{array}{cccc}-2 q_{2} & 2 q_{3} & -2 q_{0} & 2 q_{1} \\ 2 q_{1} & 2 q_{0} & 2 q_{3} & 2 q_{2} \\ 0 & -4 q_{1} & -4 q_{2} & 0 \\ -2 b_{z} q_{2} & 2 b_{z} q_{3} & -4 b_{x} q_{2}-2 b_{z} q_{0} & -4 b_{x} q_{3}+2 b_{z} q_{1} \\ -2 b_{x} q_{3}+2 b_{z} q_{1} & 2 b_{x} q_{2}+2 b_{z} q_{0} & 2 b_{x} q_{1}+2 b_{z} q_{3} & -2 b_{x} q_{0}+2 b_{z} q_{2} \\ 2 b_{x} q_{2} & 2 b_{x} q_{3}-4 b_{z} q_{1} & 2 b_{x} q_{0}-4 b_{z} q_{2} & 2 b_{x} q_{1}\end{array}\right]$



参考：[Madgwick算法详细解读]( https://www.cnblogs.com/ilekoaiq/p/8849217.html)

## 代码

https://github.com/xioTechnologies/Fusion

https://os.mbed.com/users/gke/code/UAVXArm-GKE//file/90292f8bd179/attitude.c/



[四元数、欧拉角、旋转矩阵之间互相转换C++源码](https://blog.csdn.net/zhuoyueljl/article/details/70789472)



## 参考

+  [基于AHRS的三类姿态解算算法对比(含代码)-基于手机端惯性传感器的航迹推算算法(下)](https://zhuanlan.zhihu.com/p/133700397)
+  [Madgwick AHRS算法笔记](https://blog.csdn.net/m0_37142194/article/details/81784761)
+  [几种经典非线性滤波算法简单概括（EKF，UKF，CKF，PF)](https://blog.csdn.net/gangdanerya/article/details/105066174)
+  [AHRS算法好博文](https://blog.csdn.net/qq_35987777/article/details/102771346)
+  [Mahony姿态解算算法笔记（一)](https://zhuanlan.zhihu.com/p/342703388)
+  [从四元数到旋转矩阵](https://blog.csdn.net/loongkingwhat/article/details/88427828)
+  [平方根倒数速算法](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%96%B9%E6%A0%B9%E5%80%92%E6%95%B0%E9%80%9F%E7%AE%97%E6%B3%95)
