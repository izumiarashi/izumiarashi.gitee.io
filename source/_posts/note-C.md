---
title: C#笔记(一)
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/v2-dd5961912671a8b7c9901bf645a3fbf2_720w.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-02-22 19:40:49
category: 笔记
tags: C#
summary: 基础概念、变量、运算、数据类型转换
---

<!--more-->

# 一、基础

*拓展：[用VSCode进行C#环境搭建](https://blog.csdn.net/weixin_45008173/article/details/104121347)*

[使用Visual Studio Code开发.NET Core看这篇就够了](https://www.cnblogs.com/yilezhu/p/9926078.html)

[vscode调试运行c#详细操作过程](https://blog.csdn.net/qq_40346899/article/details/80955788)

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

### 1、含义

在内存中开辟一块空间

```C#
变量类型 变量名；
```

### 2、命名规则

由字母、数字、下划线组成

不能以数字开头

不能使用保留关键字命名（变蓝的字）

*拓展：“[C# @符号的作用， 可定义关键字为变量名](https://www.cnblogs.com/yougmi/p/4549135.html)”*

### 3、建议命名规则

小写字母开头，包含多个单词，除第一个单词外其他单词首字母大写 【helloWorld】

增加类型前缀便于理解 【想声明字符串“age”：string strAge；】

## （二）赋值

### 1、含义

在开辟的空间中存储数据

```c#
变量名 = 数据;
```

### 2、注意事项

（1）变量在使用前必须赋值

（2）赋值的数据类型和变量声明时的类型必须相同

（3）同一变量名不可重复声明，但可重复赋值

*拓展（C++）：[声明、定义、初始化与赋值](https://blog.csdn.net/Marshalldong/article/details/88049034)*

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

### （四）占位符

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

### （五）转义符

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

## （六）运算符

详见python笔记

### 1、一元运算符

++ --

```c#
int n1 = 1;
++n1;
int n2 = 1;
n2++;
Console.WriteLine(n1,n2); //输出 2 2
int x1 = 1,x2 = 1;
Console.WriteLine(x1++); //输出 1
Console.WriteLine(++x2); //输出 2
```

### 2、二元运算符

**（1）赋值运算符**

右边结果复制一份给左边

```c#
int n1 = 2,n2 = 3;
//利用逗号，同时声明并赋值多个变量
```

**（2）算术运算符**

```c#
int x1 = 5,x2 = 2;
int y = x1/x2; //int型，对小数截断删除，输出2
//取模%用处
//（1）判断是否能被整除
bool y2 = x1/x2 == 0
//（2）获取整数个位
int y3 = x1 % 10;
```

算数运算符中只有“+”可以用于字符串的拼接

（3）比较运算符

```c#
string x1 = "1",x2 = "2";
bool x1 == x2; //比较文本内容
```

**（4）逻辑运算符**

&&  ||  !

**应用：**

移动到场地边缘时停下——当 玩家位于左侧/右侧 && 仍想往左侧/右侧移动 时→停下。

（5）快捷运算符 += *= /= %=

```c#
n1 = n1 + 3
//等价于
n1 += 3
```

### 3、三元运算符

数据类型 变量名 = 条件? 满足条件结果 :不满足条件结果

```c#
string str01 = 1>2?"ok":"no";
//两个结果类型必须是兼容的
```

### 4、优先级

## （七）数据类型转换

### 1、Parse

string类型 转换 为其他数据类型

```c#
string strNumber = "19";
int n1 = int.Parse(strNumber); //待转数据必须类似目标数据类型
```

### 2、ToString

任意类型 转换为 string类型

```c#
int n1 = 19;
string str = n1.ToString();
```

### 练习

输入四位整数，输出个十百千位相加的结果

```c#
Console.WriteLine("请输入四位整数：");
string strNumber = Console.ReadLine();
int number = int.Parse(strNumber);
int r = number % 10;
r += number / 10 % 10;
r += number /100 % 10;
r += number /1000 %10;
Console.WriteLine("结果为：" + r);
Console.ReadLine();
```

```c#
Console.WriteLine("请输入四位整数：");
string strNumber = Console.ReadLine();
//千位
char c1 = strNumber[0];
string s1 = c1.ToString();
int i1 = int.Parse(s1);
int r = i1;
//百十个位
r += int.Parse(strNumber[1].ToString());
r += int.Parse(strNumber[2].ToString());
r += int.Parse(strNumber[3].ToString());
Console.WriteLine("结果为：" + r);
Console.ReadLine();
```

### 3、隐式转换

小转大

```c#
byte b = 100;
int i = b;
```

### 4、显式（强制）转换

大转小，可能精度丢失

```c#
int i = 300; //300——100101100
byte b = (byte)i; //44——00101100
```

------

![image-20210301195612089](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210301195612089.png)

***float和decimal不能相加：内存存储结构不同***

快捷运算符不做类型提升

------

## （八）语句

### 1、选择语句

**（1）if-else**

-if后不加分号

-if后如果只有一句话，可以不加大括号

```c#
//错误案例
if(sex == "男");
{
    Console.WriteLine("你好，先生");
}
if(sex == "女");
{
    Console.WriteLine("你好，女士");
}
else
{
    Console.WriteLine("请输入正确的性别“男”、“女”。");
}
//输出“你好先生”、“请输入正确的性别“男”、“女”。因为if-else是一一对应

//解法：if(sex == "女")——else if(sex == "女")
```

**练习：**

用户在控制台录入两个数字，一个运算符，求结果。

```c#
//普通方案
Console.WriteLine("请输入第一个数：");
float n1 = float.Parse(Console.ReadLine());
Console.WriteLine("请输入第一个数：");
float n2 = float.Parse(Console.ReadLine());
Console.WriteLine("请输入运算符：");
string op = Console.ReadLine();
float result = 0; //需要初始化，否则会被视为result未赋值
if(op == "+" || op == "-" || op == "*" || op == "/")
{
	if (op == "+")
	{
		result = n1 + n2;
	}
	if (op == "-")
	{
		result = n1 - n2;
	}
	if (op == "*")
	{
		result = n1 * n2;
	}
	if (op == "/")
	{
		result = n1 / n2;
	}
    Console.WriteLine("运算结果为：" + result);
}
else
{
Console.WriteLine("请输入正确的运算符。");
}
//缺点：需要逐个判断+-*/，效率低
```

```c#
//优化方案
……
	if (op == "+")
	{
		result = n1 + n2;
	}
	else if (op == "-")
	{
		result = n1 - n2;
	}
	else if (op == "*")
	{
		result = n1 * n2;
	}
	else if (op == "/")
	{
		result = n1 / n2;
	}
……
```

**(2)switch-case**

①if是逐句进行到符合条件的一项，switch直接进入到符合条件的那一行。

②switch-case代码在三种分支以上时，代码可读性更强

③switch-case只能判断bool、char、string、整型、枚举或相应的可以为Null的类型

④不同case条件进行相同运算时，可以将其合并（见练习）

```c#
//题干同上文练习
switch(op)
{
    case "+":
        result = n1 + n2;
        break;
    case "-":
        result = n1 - n2;
        break;
    case "*":
        result = n1 * n2;
        break;
    case "/":
        result = n1 / n2;
        break;
    default:
        result = 0;
        break;
}
```

④switch-case只能判断确定的值，不能判断范围

```C#
//错误
switch(op)
{
    case op>10:
        result = "111";
        break;
	default:
		result = 0
}
```

**练习：**

输入月份，返回每月天数（2月为28）

```c#
Console.WriteLine("请输入月份：");
int month = int.Parse(Console.ReadLine());
int day = 0;// 要初始化变量
if(month>=1 && month <=12)
{
    switch(month)
    {
        case 2:
            day = 28;
            break;
        case 4:
        case 6:
        case 9:
        case 11:
            day = 30;
            break;
        //case 1:
        //case 3:
        //case 5:
        //case 7:
        //case 8:
        //case 10:
        //case 12:
            //day = 31;
            //break;
        //还有个default，不用把所有条件都写上
        default:
            day = 31;
            break;
    }
    Console.WriteLine(month + "月有" + day + "天。");
}
else
{
    Console.WriteLine("请输入正确的月份。");
}
Console.ReadLine();
```

