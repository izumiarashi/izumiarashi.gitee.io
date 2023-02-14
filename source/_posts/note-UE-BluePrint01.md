---
title: 【UE4笔记】蓝图-1
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/bg_32.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2022-08-24 21:02:37
category: UE4笔记
tags: 
- UE4
- 蓝图
summary: 碰撞、触发盒、调用函数、蓝图通信
---
<!--more-->

https://www.bilibili.com/video/BV164411Y732 基于此教程

# 一、P27 01 开关门

1、门需要设置为可移动的

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105155137.png)

2、添加碰撞

双击模型，添加碰撞

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105161717.png)

3、TimeLine 时间轴

右键关键帧，可以选择插值类型

接口介绍

Play 正向播放

Play from Start 从起始帧开始正向播放

Stop 停止

Reverse 反向播放

Reverse From End 从最后一帧开始反向播放

Set New Time 从指定时间开始播放

NewTime 指定时间

Update 更新状态

Dierection 时间轴结束后触发

Direction 当前时间轴是正向还是反向

轨迹 输出轨迹、

4、拓展

SwitchOnETimeLineDirection

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221206154633.png)

时间轴向前时

时间轴向后时

# 二、P28 02-1 蓝图类实现开关门

1、蓝图类中，添加指定模型

添加组件→Static Mesh→细节中修改资源

2、添加蓝图类时，门不能是触发盒的父级。因为开关门不应当影响触发盒位置

3、世界坐标和相对坐标的节点

SetActorRotation：目标Self（整个蓝图类）旋转

SetWorldRotation：指定目标以世界坐标旋转

SetRelativeRotation：指定目标以相对坐标旋转

4、获取玩家输入

GetPlayerController → Enable Input →Keyborad "按键"

离开可操作范围时：Disable Input

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105134802.png)

5、FlipFlop

第一次触发时执行A，第二次执行B

6、开启鼠标控制

蓝图类里添加事件On Click → Player Controller

→ 世界设置 →Game Mode → Player Controller

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105143342.png)

→ （点加号）创建新蓝图 → 细节 → Mouse Interface

→ （勾选 Enable Mouse Click （可选 Show Mouse Curser 一直显示鼠标）

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105143408.png)

→ 回到蓝图类 → Set Show Mouse Curser 显示鼠标

# 三、P31 03-2 升降电梯

1、按住Alt键移动选中物体，即可复制

2、蓝图中，按住Ctrl再拖动连线可以更换接口，按住Alt点击连线可以将它删除

# 四、P32 03-3 双开自动门

3、GetRelativeLocation 获取当前数值，作为初始值赋值给Lerp

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105164539.png)

1、运行一次后，当前位置也会改变，因此要在进入流程前记录下当前值作为变量，再在Lerp处引用

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105165456.png)

但赋值的过程不应当在流程中，可以新建一个“事件开始时”节点，单次运行记录初始值。

2、开门的改变量，可以存为变量，然后使用“浮点+浮点”将初始位置与改变量相加，再赋给Lerp。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105170441.png)

3、反复触发开始/结束重叠导致门卡住

是由于没有指定是“玩家与触发盒重叠时”才“开门”，导致：

开门→门离开了触发盒→触发结束重叠时间→关门→门重新进入触发盒→开门

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105170321.png)

可参照 https://blog.csdn.net/ChaoChao66666/article/details/126153957 进行设置（下图）

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221105173745.png)

# 五、P35 04 拾取钥匙开门

1、门的蓝图类里添加bool变量，通过分支判断，变量为true时才能开门。**变量默认值设为false**

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109110013.png)

2、新建钥匙Key的蓝图类，拾取（靠近按E）后获取门蓝图中的bool值并改为true，然后销毁对象。

（1）获取类的所有actor，输出对象（OutActors）的数组

（2）设置数组中指定对象对应的值

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109110754.png)

（3）Destroy Acotr

3、拓展：开了门之后，未满足另一条件前不允许关门

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109112847.png)

# 六、P37 05-2 类型转换

1、Cast To ThirdPersonCharacter 针对指定目标触发

Cast Failed 非目标时触发

As Third Person Character 作为目标输出，获得目标类里的变量、事件

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109203138.png)

# 七、P38 05-3 创建自定义事件

1、新建事件图表，便于管理不同的功能

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109204905.png)

2、CharacterMovement：查看移动参数设置，单位厘米

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109210919.png)

3、创建自定义事件（custom event）在加速图表中设置（Set）最大移动速度，且**不指定变量的值**

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109211433.png)

4、想要触发事件时传参，则要把绿线连回自定义事件的节点中

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109211955.png)

5、在加速盒子的蓝图类中新增函数调用

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109212145.png)
