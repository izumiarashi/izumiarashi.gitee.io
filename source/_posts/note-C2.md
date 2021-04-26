---
title: C#笔记(二)
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/v2-dd5961912671a8b7c9901bf645a3fbf2_720w.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-03-01 21:40:39
category: 笔记
tags: C#
summary:  方法
---

<!--more-->

# 一、方法

## （一）什么是方法

### 1、含义

对一系列语句的命名，表示**一个**功能和行为。有的语言称其为函数、过程。

### 2、目的

提高代码的可复用性和可维护性，代码层次结构更清晰。

## （二）语法

### 1、定义方法

```c#
[访问修饰符][可选修饰符]返回类型 方法名称(参数列表)
{
    方法体
    return 结果;
}
```

例

```c#
private static void test1()
{
    Console.WriteLine("hello");
}
```

### 2、调用方法

```c#
方法名称(参数);
```

C#编译器自动调用Main方法（主方法）

### 3、返回类型

①返回值：功能的结果

②类型：

数据类型（int、string、double、float……）：有返回值，方法体内**必须有**return关键字，且返回数据必须与返回类型兼容。

空（void）：无返回值，方法体内**可以有**return关键字，表示退出方法体。

```c#
private static float X1()
{
    return 2.0f;//返回值要与返回类型可兼容（显/隐式转换）
}

private static void X2()
{
    return;//void类型也可以写return关键字，不能有返回值
}
```

*方法的返回值类型显示在描述开头*

![image-20210421222045105](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210421222045105.png)

### <span id="jump1">4、return关键字</span>

return后的语句不在执行

```c#
static void Main()
{
	float a = X1(); //*记得加上(参数)
	Console.WriteLine("返回{0}",a);
}
private static float X1()
{
	Console.WriteLine("执行X1");
	return 20;
    Console.WriteLine("重复执行X1");
}
//输出“执行X1”、“返回20”
```

### 5、参数

①含义：方法定义者需要调用者传递的信息

②实参：**定义**方法时用的形式参数

③形参：**调用**方法时用的实际参数

实参与形参必须一一对应（数量、类型、顺序）

```c#
static void Main()
{
	X2(100,"200");
}

private static void X2(int a,string b)
{
	Console.WriteLine(a);
}
//输出100
```

## （三）方法重载

### 1、定义

方法名称相同，参数列表不同。

### 2、作用

不同条件下，解决同一类问题。减少调用者学习成本。

### 3、案例

输入分钟数，计算总秒数。

输入小时数、分钟数，计算总秒数。

输入天数、小时数、分钟数，计算总秒数。

**初次尝试**

缺点：仅有分钟时也要进行天、小时的传参

```c#
static void Main()
{
	Console.WriteLine("请输入天数：");
	int day = int.Parse(Console.ReadLine());
	Console.WriteLine("请输入小时数：");
	int hour = int.Parse(Console.ReadLine());
	Console.WriteLine("请输入分钟数：");
	int minute = int.Parse(Console.ReadLine());
	int second = GetSecondByMinute(minute,hour,day);
	Console.WriteLine("共{0}秒",second);
	Console.ReadLine();
}
private static int GetSecondByMinute(int minute,int hour,int day)
{
	minute += GetMinuteByHour(hour,day);
	return(minute*60);
}
private static int GetMinuteByHour(int hour,int day)
{
	hour += GetHourByDay(day);
	return(hour*60);
}
private static int GetHourByDay(int day)
{
	return(day*24);
}
```

**调整**

拆分成可独立使用的三个办法，调整逻辑顺序。

缺点：调用者需要记忆3种方法

```c#
private static int GetTotalSecondByMinute(int minute)
{
	return minute * 60;
}
private static int GetTotalSecondByMinuteHour(int minute,int hour)
{
    return GetTotalSecondByMinute(minute + hour * 60);
}
private static int GetTotalSecondByMinueHourDay(int minute,int hour,int day)
{
    return GetTotalSecondByMinuteHour(minute, hour + 24 * day);
}
```

**标准答案**

方法重载，将三个方法命名为同一个名称

### 4、补充

仅仅out和ref的区别不可以构成重载



## **综合练习：制作年历**

（见[C#练习（一）——制作年历](https://izumiarashi.github.io/2021/04/25/practice-C-Calendar)）



# 二、递归

## （一）含义

方法内部又调用自身的过程

```c#
//阶乘
private static GetFactorial(int num)
{
    if(num == 1)return 1;
    return num * GetFactorial(num - 1);
}
```

## （二）核心思想

**将问题转移给范围缩小的子问题**

## （三）特点

### 1、优点

复杂问题简单化

### 2、缺点

性能比循环差

### 3、适用场景

在解决问题过程时遇到相同问题时