---
title: C#笔记
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/v2-dd5961912671a8b7c9901bf645a3fbf2_720w.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-02-22 19:40:49
category: 笔记
tags: C#
summary: bilibili大学一年级
---

<!--more-->

# 一、基础

```c#
using System; //引入命名空间

namespace 333 //定义命名空间（类的住址，对类进行划分，避免重名）
{
    class Program //定义类
	{
		static void Main() //定义方法、程序的入口方法
		{
    		Console.Title = "222"
			Console.Writeline("111"); //控制台.写一行：将文本写入控制台中
			Console.Readline(); //控制台.读一行：将输入到控制台中的文本读取到程序
		}
	}
}
```

Console 是一个“**类**”（工具、部门）

Writeline、Readline 是“**方法**”（功能），需要加括号

Title是“**属性**”

代码写入“文本文件”.cs

→生成.exe：在.csproj文件中添加

```xml
<RuntimeIdentifier>win10-x64</RuntimeIdentifier
```

------

Ctrl+K+D 格式化全篇代码

Ctrl+K+F 格式化选中的代码，默认格式化光标所在当前行

Ctrl+K+C 注释选中

Ctrl+K+U 取消注释

------

# 二、变量

## （一）思考

程序在哪运行？内存

程序处理的是什么？数据

——变量就是内存中开辟的一块用于存储数据的空间

## （二）数据类型

### 1、容量单位

（1）位bit（比特）：电脑**记忆体中**最小单位，每一位可为0**或**1

（2）字节Byte：电脑**存储中**最小单位

注：网速单位为Mbps（兆位/秒）是**速率单位**，换算为存储单位应处以8

### 2、整型（整数）

取值范围取决于二进制：1个字节→8个位置→00000000~11111111

**1字节：**有符号sbyte（-128~127）、无符号byte（0~255）

**2字节：**有符号short（-32768~32767）、无符号ushort（0~65535）

**4字节：**有符号int，无符号unit

**8字节：**有符号long，无符号ulong

### 3、非整型（小数）

**4字节：**单精度浮点类型float，精度7位 【1.2f】

**8字节：**双精度浮点类型double，精度15-16位 【1.2d】

**16字节：**128位数据类型decimal，精度28-29位 【1.2m】

注意：

（1）赋值需要后缀f、d、m，不加默认为d

（2）浮点运算会有舍入误差：

​	1.0f - 0.9f !=0.1f

​	因为二进制无法精确表示1/10

​	精度要求较高时应使用decimal

### 4、字符

**字符char：**2字节，存储单个字符（ASCII码），使用**单引号** （单个汉字可为1字符）

**字符串string：**存储文本，使用**双引号** （a可以是字符或字符串，ab只能是字符串）

**布尔类型bool：**1字节，true、false