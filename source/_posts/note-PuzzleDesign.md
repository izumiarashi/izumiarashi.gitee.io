---
title: 【GDC笔记】关卡解谜
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20211022154250356.png'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-10-13 15:32:30
category: 策划笔记
tags: 
- 关卡设计
- GDC1
summary:
---
<!--more-->

https://www.youtube.com/watch?v=B36_OL1ZXVM

https://www.bilibili.com/video/BV1gY411b79A

## 一、什么是有趣？什么是机制？

推拉的箱子、敌人

## 二、“Working Memory”

![合理的玩家内存占用](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20220409201227.png)

重复的规则会减少占用内存“会者不难”

→释放的空间需要用新规则填充，维持flow

## 三、谜题特征

（一）手工谜题

有限的

重复技巧少

解法多元

体验不确定，更多惊喜

（二）程序化谜题

无限谜题

技巧有限

解法固定

谜题诞生于系统

体验是确定的

## 四、噪声

*——占用玩家内存但是对解谜无效的消息*

![噪声](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20220409202141.png)

（1）使关卡更不直观，需要花费时间去解决

（2）使关卡的通过难以通过试错来通过

（3）让关卡难度虚高

（4）识别噪声不等于解谜

（5）熟练后运用技巧去识别噪音

## 四、《LineLight》启示

（一）**简化**——减少噪声，创造清晰、联系紧密的谜题

描述解法，去除所有未提及的元素

1、拆解关卡

2、去除无关元素

3、回顾，继续简化

4、至少两次的检查

（二）**删去**无用的的关卡

思考每个关卡的目的（教学、巩固、体验、休息、打破节奏……）

没有目的那就是平庸的关卡

要敢于去认定一个关卡的平庸

（三）专业玩家

（对于解谜游戏来说）知道解法但无法执行不是有趣的体验

（四）**分离**动作和谜题

二者相互冲突：

动作→随机性、娱乐

解谜→固定性、专心

玩家需要知道解谜需要的是什么

（五）让解法更**清晰**

觉得解法不对、偶然通关后不理解解法、玩家尝试进行不可能动作

拉远各元素间的距离

删除无关元素

![让人知道躲进右上角是唯一解](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20220409204532.png)

（六）玩家信任

玩家会对一个类型的游戏有一个预期，不要打破这一类游戏的“潜规则”

（七）全面设计vs有趣

全面设计：穷尽所有可能的设计

乐趣：展现掌控感、技巧或理解力

对设计师有趣≠对玩家有趣

## 四、如何设计谜题

**（一）如何设计关卡**——关卡不是想出来的，是由**机制**衍生的

**（二）如何设计机制**

→经验、直觉、幸运

①各式不同

②各种形式交互

③有趣

→敢于删减

→多尝试

→用较少的机制做较多的谜题

**（三）解句**——围绕单一的解法制作关卡

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20220409210231.png)

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20220409210354.png)

如何得到解句？

→尝试把一些机制放在一起

→测试，观察，记录

→好的机制自然会产生好的谜题

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20220409210603.png)



如何判断关卡好坏？


推荐阅读

《Thinking,fast and slow》
