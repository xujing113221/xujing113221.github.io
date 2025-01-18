---
title: AI人像生成模型学习笔记
date: 2024-03-21
tags:
  - AI
  - 人像生成
  - Stable Diffusion
  - 深度学习
categories: 
  - 技术学习
  - AI绘画
permalink: ai-portrait-study
---

本文记录了学习和使用AI人像生成模型的经验，包括主流模型介绍、实践工具准备、关键参数设置以及常见问题解决方案等内容。适合想要入门AI人像生成的新手参考。

<!-- more -->

## 一、人像生成模型概述

### 1.1 主流模型介绍
- Stable Diffusion：开源的图像生成模型，可进行微调和定制
- Midjourney：封闭但效果优秀的商业模型
- DALL-E：OpenAI开发的图像生成模型

### 1.2 技术原理简介
- 扩散模型（Diffusion Models）基本原理
- 潜在空间（Latent Space）的概念
- 文本到图像的生成过程

## 二、实践工具准备

### 2.1 基础环境配置
- Python 环境搭建
- CUDA驱动安装（支持GPU加速）
- 相关依赖库安装

### 2.2 常用工具
- Stable Diffusion WebUI
- ComfyUI
- ControlNet
- 各类模型权重文件

## 三、人像生成要点

### 3.1 提示词技巧
- 人物特征描述
- 场景氛围营造
- 艺术风格定义
- 构图要素控制

### 3.2 关键参数设置
- Steps（步数）：通常20-30步
- CFG Scale（提示词相关性）：建议7-9
- Sampler（采样器）：DPM++ 2M Karras
- 尺寸选择：建议512x768或768x512

## 四、进阶技巧

### 4.1 ControlNet应用
- OpenPose人体姿态控制
- Canny边缘检测引导
- Depth深度图控制
- Face Landmark面部特征控制

### 4.2 模型混合使用
- 基础模型选择
- LoRA模型叠加
- Embedding使用
- 模型合并技巧

## 五、常见问题与解决方案

### 5.1 人物问题
- 手部变形解决方法
- 面部细节优化
- 人体比例调整
- 多人构图技巧

### 5.2 技术问题
- 显存不足的解决方案
- 生成速度优化
- 批量生成方法
- 模型存储管理

## 六、实践案例分享

### 6.1 人像写实风格 