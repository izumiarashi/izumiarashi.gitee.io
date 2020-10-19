---
title: Unity手柄实现
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/bg_32.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2020-10-05 12:01:05
category: 笔记
tags: Unity
summary: 转载
---

<!--more-->

转自https://www.cnblogs.com/jiuxuan/p/7453762.html



1、创建background

2、添加摇杆img

3、代码实现

```C#
1 using System.Collections;
 2 using System.Collections.Generic;
 3 using UnityEngine;
 4 using UnityEngine.EventSystems;
 5 using UnityEngine.UI;
 6 
 7 public class ScrollCircle : ScrollRect
 8 {
 9     // 半径
10     private float _mRadius = 0f;
11 
12     // 距离
13     private const float Dis = 0.5f;
14 
15     protected override void Start()
16     {
17         base.Start();
18 
19         // 能移动的半径 = 摇杆的宽 * Dis
20         _mRadius = content.sizeDelta.x * Dis;
21     }
22 
23     public override void OnDrag(PointerEventData eventData)
24     {
25         base.OnDrag(eventData);
26             
27         // 获取摇杆，根据锚点的位置。
28         var contentPosition = content.anchoredPosition;
29 
30         // 判断摇杆的位置 是否大于 半径
31         if (contentPosition.magnitude > _mRadius)
32         {   
33             // 设置摇杆最远的位置
34             contentPosition = contentPosition.normalized * _mRadius;
35             SetContentAnchoredPosition(contentPosition);
36         }
37 
38         // 最后 v2.x/y 就跟 Input中的 Horizontal Vertical 获取的值一样 
39         var v2 = content.anchoredPosition.normalized;
40     }
41 }
```