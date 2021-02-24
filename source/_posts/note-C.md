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

*拓展：[用VSCode进行C#环境搭建](https://blog.csdn.net/weixin_45008173/article/details/104121347)*

[使用Visual Studio Code开发.NET Core看这篇就够了](https://www.cnblogs.com/yilezhu/p/9926078.html)

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

~~→生成.exe：在.csproj文件中添加：~~

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

​	加减时应对阶

### 4、字符

**字符char：**2字节，存储单个字符（ASCII码），使用**单引号** （单个汉字可为1字符）

**字符串string：**存储文本，使用**双引号** （a可以是字符或字符串，ab只能是字符串）

**布尔类型bool：**1字节，true、false

# 三、语法

## （一）声明

1、含义：在内存中开辟一块空间

```C#
变量类型 变量名；
```

2、命名规则

由字母、数字、下划线组成

不能以数字开头

不能使用保留关键字命名（变蓝的字）

*拓展：“[C# @符号的作用， 可定义关键字为变量名](https://www.cnblogs.com/yougmi/p/4549135.html)”*

3、建议命名规则

小写字母开头，包含多个单词，除第一个单词外其他单词首字母大写 【helloWorld】

增加类型前缀便于理解 【想声明字符串“age”：string strAge；】

## （二）赋值

1、含义：在开辟的空间中存储数据

```c#
变量名 = 数据;
```

2、注意事项：

（1）变量在使用前必须赋值

（2）赋值的数据类型和变量声明时的类型必须相同

（3）同一变量名不可重复声明，但可重复赋值

## （三）调试

在可能出错的语句增加断点

*拓展：[VS Code 调试完全攻略（2）：步进逐行调试](http://blog.yidengxuetang.com/post/202005/27/)”*

## 练习：

```c#
using System;

namespace First
{
	class gun
	{
		static void Main()
		{
			Console.WriteLine("请输入枪的名称：");
			string gunName = Console.ReadLine();
			Console.WriteLine("请输入枪的弹匣容量：");
			String gunVolume = Console.ReadLine();
			Console.WriteLine("请输入枪的伤害：");
			string gunDmg = Console.ReadLine();
			Console.WriteLine(gunName + "的弹匣容量为" + gunVolume + "，伤害为" + gunDmg);
            //拼接容易影响代码可读性
            Console.Read();
		}
	}
}
```

### 拓展：占位符

{位置编号}

从0开始，编号不能大于参数列表长度

```c#
string str = string.Format("{0}的弹匣容量为{1}，容量为{2}。",gunName,gunVolume,gunDmg);

//或者
Console.WriteLine("枪的名称：{0}",gunName); 
//只有在控制台中能用，一般都用Format

//标准数字字符串格式化：以某种格式显示占位符中数据
Console.WriteLine("金额：{0:c}",10);
	//"0：C"为货币格式，输出￥10
Console.WriteLine("金额：{0:d2}",1);
	//"0:d2"不足2位用0填充，输出01
Console.WriteLine("{0:f1}",1.25);
    //"0:f1"根据指定精度，输出1.3
Console.WriteLine("{0:p0}",0.1);
	//"0:p0"以百分数显示，输出10%
	//"0:p1"输出10.0%
```

### 拓展：转义符

```c#
Console.WriteLine("你好，\"世界\"");
//转义引号 \" \'

char a = '\0';
//char类型空字符不能用''，需要转义0
//string空字符串可以用""表示

Console.WriteLine("达拉崩吧\r\n巴拉巴拉");
//新增行\n，回到行首\r
```

![转义符](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210224231556322.png)

### 源代码(.cs)

电脑只能识别机器码（0 1）

①源代码

——②**CLS**（公共语言规范）**第一次编译**【目的：跨语言】

​		定义.NET平台上运行的语言必须支持的规范，避免不同语言特性产生的错误，实现语言间互操作

——③**CIL**（通用中间语言）.exe .dll

——④**CLR**（公共语言运行库）**第二次编译**【目的：优化、跨平台】

​		是程序运行环境，负责内存分配、垃圾收集、安全检查等

——⑤机器码 0 1

![image-20210224232818924](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210224232818924.png)

发展史：

机器语言0 1→汇编语言→高级语言