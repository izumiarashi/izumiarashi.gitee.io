---
title: Unity笔记（3）
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/unity.jpg'
date: 2020-10-02 18:02:09
cover: false
category: 编程笔记
tags: Unity
summary: 摄像机跟随
---

<!--more-->

# 实现摄像机跟随

### （一）打组

将人物与摄像机形成父子物体或处于同一父物体下

### （二）Offset-相对静止

来源：https://www.bilibili.com/video/BV1k4411U78V?from=search&seid=17110298180744399614

注意检查拼写。

```C#
using UnityEngine;
using System.Collections;

public class 脚本名 : MonoBehaviour {

    public Transform playertransform;
    private Vector3 offset;

    
    void Start(){
        offset=transform.position-playertransform.position;
    }

    
    void Update(){
        transform.position = playertransform.position + offset;
    }
}
```

### （三）Vector3插值

1、面向固定

来源：https://www.bilibili.com/video/BV1Qt411M7KG?p=7

```c#
using UnityEngine;
using System.Collections;

public class 脚本名 : MonoBehaviour {

    private Transform player;
    public float speed = 2;

    // 使用标签查找对象，取其transform属性。
    void Start(){
        player = GameObject.FindGameObjectWithTag(Tags.player).transform; 
    // 注意FindGameObjectWithTag与FindGameObjectsWithTag的区别。
    }

    // 角色位置+插值=目标位置
    void Update(){
        Vector3 targetPos = player.position + new Vector3(0, 2.32f, -2.32f);
        // 通过打组确认插值时，vector3坐标要乘以对象的scale。
        transform.position = Vector3.Lerp(transform.position, targetPos, speed * Time.deltaTime);
        Quaternion targetRotation = Quaternion.LookRotation(player.position - transform.position);
        transform.rotation = Quaternion.Slerp(transform.rotation,targetRotation, speed * Time.deltaTime);
        //Slerp(当前旋转，目标旋转，旋转速度)
    }
}
```

2、始终位于角色背后

https://blog.csdn.net/qq_42434073/article/details/106712990

```c#
// Update is called once per frame
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FellowCamera : MonoBehaviour {
    private Transform targetPos;
    private Vector3 offsetPos;//固定位置
    private Vector3 temPos;//临时变量
	// Use this for initialization
	void Start () {
        targetPos=GameObject.FindGameObjectWithTag("Player").transform;//注意要将要跟随的物体标签设置为“Player”；
        offsetPos = this.transform.position - targetPos.transform.position;
	}
	void FixedUpdate () 
    {
        temPos = targetPos.position + targetPos.TransformDirection(offsetPos);
        this.transform.position = Vector3.Lerp(transform.position, temPos, Time.fixedDeltaTime*3);//插值跟随，fixedDeltaTime*3,"3"可以调节跟随的效果；
        transform.LookAt(targetPos);
    }
}
```



### （四）摄像机遇到墙壁时抬起

来源：https://www.bilibili.com/video/BV1Ui4y1j7Ey?from=search&seid=17110298180744399614