---
title: 【UE4笔记】错题本
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/bg_32.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2022-12-06 18:12:37
category: UE4笔记
tags: 
- UE4
- 蓝图
summary: 总结日常制作中遇到的坑
---
<!--more-->

https://www.bilibili.com/video/BV164411Y732 基于此教程

# 无限循环

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221206220250.png)

LoopTimes=0

CostInOnePress=1

第一次进入循环时，没有问题。

第二次进入时，由于LoopTime没有回到默认值，导致始终不等于CostInOnePress

解决办法：退出循环后重置LoopTimes

或者使用Do Once节点

# 字符串转数组

https://blog.csdn.net/qq_42408452/article/details/112835789

ParseIntoArray

# 蓝图类预览中隐藏白球

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221207111024.png)

# 相机平滑移动

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230202221034.png)
