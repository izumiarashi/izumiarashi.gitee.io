---
title: 【UE4笔记】蓝图-2
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/bg_32.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2022-11-09 21:27:37
category: UE4笔记
tags: 
- UE4
- 蓝图
summary: 对象引用 IsValid GetAllActorOfClass ForEachLoop
---
<!--more-->

https://www.bilibili.com/video/BV164411Y732 基于此教程

# 一、P40 06-1 对象引用、变量有效性

1、对象引用

类型转换后的内容可提升为变量，在别处引用，为蓝图通信使用。

在类A中创建自定义事件，在类B中引用时，需要创建类A的“对象引用”变量。再从该变量中拉出对应的自定义事件。

2、有效性Is Valid

在变量被赋值前就是无效的

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221109213935.png)

拓展：

bfs dfs 动态规划

STL容器

高内聚低耦合

二、P41 06-2 键盘控制物体自转

1、AddLocalRotation 当前位置为基础增加旋转

![1668049865935](image/note-UE-BluePrint02/1668049865935.png)

2、新增变量，按住Ctrl键拖到图表中

3、新建自定义事件，通过分支来实现类似FlipFlop的功能。

分支的优势：更加灵活，修改CanRotation默认值时不需要重新调整FilpFlop

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221110112457.png)

4、在人物控制的蓝图里，新增变量，把变量类型改为对象引用。

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221110113859.png)

5、判断有效性

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221110114715.png)

6、点击变量旁的眼睛可设置公有/私有变量

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221110114543.png)

7、然后需要在ThirdPersonCharacter的细节面板中，给指定对应的对象。

三、P42 07-1 点名系统

1、GetAllActorsOfClass 获取该类的所有演员→ **先选择ActorClass** →Get 指定某一个演员

替代的是上文中手动添加的对象引用RotationController

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221110152452.png)

拓展：注释节点——框选后按C

2、ForEachLoop 循环

Array Index 输出数值：当前执行的是第几个

Completed 完成后执行

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221110152816.png)

3、ForEachLoop 可被打断的循环

4、TextRender 文本渲染组件

在 细节-text-文本 中填写需要显示的字符

在 细节-Rendering-可视 中设置默认可视性

5、设置可视性 Set Visiblility

6、如图，可视性应该在时间轴前进行设置。因为时间轴是每一帧都会更新一次，而可视性只需要设置一次。变量同理。

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221114154910.png)

7、判断指定演员的变量内容

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221114204936.png)

8、Execute Console Command 执行控制台命令，用于执行关卡蓝图中的内容

![img](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221114205356.png)

【注意】

①GetAllActorOfClass/GetActorOfClass、ForLoop/ForEachLoop的区别。

②【勘误】如果将TrhidPersonCharacter传给启用/禁用输入为目标，则会使玩家失去控制权。目标应该是Actor自身（Self）

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20221114154347.png)

③记得添加GetPlayerController

④类型转换（Cast To）ThirdPersonController记得连接需要转换的object
