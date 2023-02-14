---
title: 【UE4笔记】蓝图-4
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/bg_32.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2022-11-24 18:12:37
category: UE4笔记
tags: 
- UE4
- 蓝图
summary: 函数、宏、事件；面向对象；obj、actor、pawn的区别
---
<!--more-->

https://www.bilibili.com/video/BV164411Y732 基于此教程

P50

# 函数、宏、事件

## 函数

可以直接被另一段程序引用的程序。

纯函数：没有执行流的函数，用于获取数据、临时计算，不能修改变量。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214230059.png)

## 宏

组合多个命令，使对话框选项更易于访问。


## 宏和函数的区别

函数可以在别的蓝图类中全局调用；而宏只能在当前蓝图中调用（蓝图宏库可被全局调用）。

函数默认拥有执行引脚；宏需要手动添加执行引脚，但可添加多个。

函数中不可使用Delay节点

## 函数和事件的区别

函数有返回值，事件没有。实现接口时，有返回值的会变成函数，没有返回值的会变成事件。

函数是执行，事件是触发

事件可以用于处理按键输入、碰撞等情况

函数不可以直接回调，事件可以做为回调函数（事件回调事件类似递归，函数只是单纯的重复多次执行）

事件可以用来发送网络消息，函数不行

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214231250.png)


# 面向对象的思想（封装、继承、多态）

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214231639.png)

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214231656.png)

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214232254.png)

创建子蓝图类

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214231833.png)

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214231905.png)

从而可以实现在子类中重写父类的功能

重写是继承后对父类方法的重写，而非重载：重载是在同一个类里，使用到了不同的参数实现同一个方法。

重载是一个类中的多态性表现，覆写是父类与子类之间的一种多态表现

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20230214232149.png)


# 类、Object、Actor、Pawn、Character、Component

类是抽象的，用于定义Object中方法和变量的模板，不占用内存。Object是实例化的类，占用存储空间。

Object是基类。

Actor是可以拥有功能，拥有组件的Objec。关卡蓝图也是一种Actor。

Pawn默认支持玩家输入，拥有控制权。

Character是特殊的Pawn，拥有常见的游戏角色所需要的组件，包括碰撞、重力、移动逻辑（CharacterMovement）。
