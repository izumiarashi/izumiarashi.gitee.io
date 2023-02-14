---
title: 【UE4笔记】蓝图-3
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/bg_32.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2022-11-15 21:27:37
category: UE4笔记
tags: 
- UE4
- 蓝图
summary: 角色控制权、上车下车 MultiGate
---
<!--more-->

https://www.bilibili.com/video/BV164411Y732 基于此教程

# 一、P45 09 切换多个角色控制权

1、获得玩家控制权

（1）方法一

单击ThirdPersonCharacter，选中蓝图类（双击会变成选中模型）

→在细节面板中找到Pawn-自动控制玩家(SeeAutoPossessAI)

→设置为玩家0，则玩家0自动获得该角色的控制权

选中后，将不会在出生点处刷出角色

（2）方法二

左上角“窗口”→世界场景设置→GameMode

→创建“游戏模式覆盖”

→ThirdPersonGamemode

→放置玩家出生点。如果有多个出生点，会在随机出生点出现。

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221118160816.png)

→默认pawn类选择要生成的角色

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221122113212.png)

（3）切换玩家控制权

删除玩家出生点

→放置多个ThirdPersonCharacter

→在关卡蓝图中添加ThirdPersonCharacter的对象引用

→添加Multigate，依次执行Out1、2、3、4、5**一次**

→添加GetPlayerController，从引脚中拉出Possess（控制），用于实时更改控制的角色

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221122114049.png)

2、MultiGate

默认Out0、1、2、3、4**各执行一遍**

Reset 重置执行顺序

Is Random **不重复的**随机执行一遍引脚

Loop 所有节点走完一遍后，会重置节点的状态从而可以重新走

3、混合设置视图目标 Set View Target With Blend

使切换时镜头运动更加顺滑

注意逻辑关系，应该是先运动镜头，然后再切换控制权。

New View Target 要切换至的目标

Blend Time 混合过度时间

4、延迟 Delay

延迟进行到下一节点，不能在函数中使用。

5、重叠——用于整理节点

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221122152810.png)

其中，同类的引用可以合并。子类可以赋值给父类的引用，比如可以将New View Target中演员（Actor）的引用改为角色（Pawn）。

拓展：C++继承

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221122155122.png)

6、拓展：宏、函数、事件的区别 https://blog.csdn.net/weixin_33359523/article/details/112878272

7、防止一直按1导致bug

（1）方法一：开始切换时禁用输入，切换完成启用输入

（2）方法二：新增一个判断变量，初始为True，执行后为False，当完成切换视角后再改为True。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124160406.png)

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124160851.png)

# 二、P46 10 角色上下车

## 1、更改控制权到车上

（1）在汽车蓝图类中创建自定义事件

（2）在ThirdPersonCharacter蓝图类中添加对自定义事件的触发，还有汽车的对象引用变量Vehicle。（参考笔记2-对象引用）

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123102640.png)

（3）此时，变量Vehicle是空值。当玩家可以与车产生交互时，需要对该变量赋值。

首先需要取到ThirdPersonCharacter中这一变量，随后为其赋值，值为Self（汽车蓝图类自身）。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123102625.png)

（4）当重新处于不可上车的状态时，则将Self赋值删去，重新赋予空值即可。

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123102918.png)

## 2、让角色上车

（1）新建一个碰撞体，用于标识上车位置。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123104327.png)

（2）在蓝图中获取碰撞体的**场景变换**（GetWorldTransform），然后**拆分变换**(BreakTransform)。因为角色不需要与碰撞体的缩放一致。

随后在设置Actor变换，将碰撞体的位置信息赋予玩家角色。

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123104539.png)

（3）此时需要将ThirdPersonCharacter作为目标传入，则需要将目标引脚拉至自定义事件，添加对象引用。

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123104758.png)

注意：为了使下车时可以将控制权改回角色，需要将变量类型由Actor改为Pawn

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123112141.png)

再在ThirdPersonCharacter的蓝图类中传出Self。

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123104901.png)

## 3、碰撞处理

由于车和人都有碰撞体积，放在一起时会不断发生挤压。因此要将角色的碰撞关闭。

使用SetActorEnableCollision（设置Actor启用碰撞）

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123105143.png)

4、将人物挂接到碰撞体

（1）使用Attach To Component (附加到组件-目标是Actor)

注意：有2种附加到组件

①“目标是Actor”将别的Actor挂到组件上

②“目标是场景组件”将组件挂到别的目标上

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221123110320.png)

（2）“保持相对”“保持场景”

由于两个目标没有位于同一个蓝图类中，因此坐标轴的数据都是基于世界坐标系。

因此需要选择“保持场景”。

## 4、角色下车

1、将上车的操作进行相反的操作（移动到下车点的碰撞体、开启碰撞、开启）

2、汽车转弯时rotation是倾斜的，下车时如果仍保留这个旋转参数则会使视角倾斜。

因此需要拆分引脚，仅仅传入z轴方向rotation。

# 三、P47 11 下车后减速

1、Vehicle Movement 轮式载具移动组件4驱

汽车移动功能所必须的组件，是手制动输入和油门输入需要的目标

2、Set Handbreak Input 设置手制动输入

拉起手刹

3、Set Throttle Input 设置油门输入

可更改Throttle参数来控制油门

下车时应该将它只为0

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124164244.png)

4、下车时需要关闭键盘的油门输入，否则会覆盖掉我们置为0的Throttle数值。

则需要一个bool变量，在上车时置为true、下车后置为false，从而通过branch在下车后打断键盘对油门的输入。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124165000.png)

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124164917.png)

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124164846.png)

5、未知的问题：对油门的输入和手刹的输入需要放在Delay前面，否则会失效

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221124172609.png)
