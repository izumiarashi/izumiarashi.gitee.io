---
title: Unity笔记（2）
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/unity.jpg'
date: 2020-09-14 21:35:24
cover: false
category: 笔记
tags: Unity
summary: 角色行为及动画
---

<!--more-->

# 角色移动

```C#
using System.Collections;
using UnityEngine;

public class Playermove : MonoBehaviour
{
    private CharacterController playercc;
    public float speed = 6;

    void Awake()
    {
        playercc = this.GetComponent<CharacterController>();
    }
  
    // Update is called once per frame
    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        if (Mathf.Abs(h) > 0.1f || Mathf.Abs(v) > 0.1) ;
            Vector3 targetDir = new Vector3(h, 0, v);
            transform.LookAt(targetDir + transform.position);
        playercc.SimpleMove(targetDir * speed);
    
    }
}

```



# 角色动画

### 动画模式

Inspector-Rig-Animation type：

None：不导入动画Animation Clip

Legacy：用于早期动画设置，其不支持状态机Animator，无法对动画进行编辑，导入完后直接用Animation播放

Generic：支持人形、非人形Model

Humanoid：只支持人形Model，导入后用Animator播放（设置后Hirearchy模型里面自动添加Animator组件）Generic一样