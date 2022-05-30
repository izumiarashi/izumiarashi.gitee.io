---
title: C#笔记(二)
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/v2-dd5961912671a8b7c9901bf645a3fbf2_720w.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-03-01 21:40:39
category: 编程笔记
tags: C#
summary:  方法、递归、数组
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
private static void Test1()
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

### `<span id="jump1">`4、return关键字)`</span>`

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

方法重载，将三个方法命名为同一个名称。使能在不同条件下，用单一方法解决同一类问题。

```C#
private static int GetTotalSecond(int minute)
{
	return minute * 60;
}
private static int GetTotalSecond(int minute,int hour)
{
    return GetTotalSecond(minute + hour * 60);
}
private static int GetTotalSecond(int minute,int hour,int day)
{
    return GetTotalSecond(minute, hour + 24 * day);
}
```

### 4、补充

返回值不同，但参数相同，不可构成重载

仅仅out和ref的区别不可以构成重载（见后文）

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

例：逐层检索每个文件夹中的文件，直到没有子文件夹

## （三）特点

### 1、优点

复杂问题简单化

### 2、缺点

性能比循环差

### 3、适用场景

在解决问题过程时遇到相同问题时

### **练习**

按以下规律的数列，当参数为8时结果为多少？

1-2+3-4+5-6……

```c#
private static int GetValue(int num)
{
	int i = 0;
	if(num >= i)
	{
		i++;
		return i + GetValue(i); //堆栈溢出，以为上面将i初始化了
	}
	else
		return 0;
}
```

#### **拓展：堆栈溢出**

![](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210429101213367.png)

无限次的递归，没有对边界进行约束

**分析原因：**递归应该是从大到小拆分问题，而不是从1开始循环

**修改：**

```c#
static void Main()
{
	Console.WriteLine("请输入一个大于0的数");
	int num = int.Parse(Console.ReadLine());
	int sum = GetValue(num);
	if(sum == 0)
	{
		Console.WriteLine("请正确输入大于0的数。");
	}
	else
	{
		Console.WriteLine("按规律求和的结果为{0}",sum);
	}
	Console.ReadLine();
}
private static int GetValue(int num)
{
	if(num == 1)
		return 1;
	if(num > 1 && num % 2 == 0)
		return -1*num + GetValue(num - 1);
	else if(num > 1 && num % 2 != 0)
		return num + GetValue(num - 1);
	else
    	return 0;
}
```

**优化：**将数字是否合规的判断提前

```c#
static void Main()
{
	Console.WriteLine("请输入一个大于0的数");
	int num = int.Parse(Console.ReadLine());
	if(num <= 0)
	{
		Console.WriteLine("请正确输入大于0的数。");
	}
	else
	{
		int sum = GetValue(num);
		Console.WriteLine("按规律求和的结果为{0}",sum);
	}
	Console.ReadLine();
}
private static int GetValue(int num)
{
	if(num == 1)
		return 1;
	if(num % 2 == 0)
		return -num + GetValue(num - 1);
	else
		return num + GetValue(num - 1);
}
```

# 三、数组

## （一）含义

从Array派生的，一组**数据类型相同**的**变量组合**，是一种**空间连续**的**数据结构**

元素通过索引（位置的序号）进行操作

**例**

| 数组 | 5 | 1 | 4 | 0      | 7 |
| ---- | - | - | - | ------ | - |
|      |   |   |   | 空一格 |   |
| 索引 | 0 | 1 | 2 | 3      | 4 |

存储默认值（int-0、float-0.0、char-\0、bool-false、string-null）表示空一格

## （二）使用

### 1、数组的写法

```c#
//声明 不用写赋值号"="
int[] a;
//初始化 new 数据类型[容量]
a = new int[3];
//赋值 通过索引读写元素
a[0] = 1;
a[1] = 2;
a[2] = 3;

//初始化 + 赋值
string[] array01 = new string[2]{"a","b"};//可以不用写明容量
//声明 +初始化 + 赋值
bool[] array02 = {true,true,false};
```

```c#
//for(int i = 0; i < 3; i++) 
//如果对数组长度的定义有变，则需要在循环里重新修改i的范围。将常数范围改为"数组名.Length"可以避免这个问题
for(int i = 0; i < a.Length; i++)
{
    Console.WriteLine(a[i]);
}
```

### 练习

录入学生总数、学生成绩

```c#
private static float[] CountStudentResult()
{
	Console.WriteLine("请输入学生人数：");
	int count = int.Parse(Console.ReadLine());
	float[] resultArray;
	resultArray = new float[count];
	for(int i = 0; i < count;) //记得加分号
	{
		Console.WriteLine("请输入{0}号学生成绩",i+1); 
		float score = float.Parse(Console.ReadLine());
		if(score > 100 || score < 0)
			Console.WriteLine("请输入正确的成绩（0-100）");
		else
			resultArray[i++] = score;
        	//如果先前声明的是i=1，那么此处应填i-1，否则读不到数组第一位
	}
	return resultArray;//返回数组时不用加[]
}
```

计算最大值

```c#
static void Main()
{
	Console.WriteLine("请输入第一个数");
	float a = float.Parse(Console.ReadLine());
	Console.WriteLine("请输入第二个数");
	float b = float.Parse(Console.ReadLine());
	Console.WriteLine("请输入第三个数");
	float c = float.Parse(Console.ReadLine());
	float max = GetMaximum(new float[]{a,b,c});//【简略写法】
	Console.WriteLine("最大值为{0}",max);
	Console.ReadLine();
}
private static float GetMaximumZ(float[] array)
{
	int i = 0;
	float maxNum = array[i];
	for(;i < array.Length;i++)
	{
	if(maxNum < array[i])
		maxNum = array[i];
	}
	return maxNum;
}
```

计算某月某日是当年的第几天

```c#
static void Main()
{
	Console.WriteLine("请输入年：");
	int year = int.Parse(Console.ReadLine());
	Console.WriteLine("请输入月：");
	int month = int.Parse(Console.ReadLine());
	Console.WriteLine("请输入日：");
	int day = int.Parse(Console.ReadLine());
	int count = GetDayCount(year, month, day);
	Console.WriteLine("天数为{0}",count);
	Console.ReadLine();
}
private static int GetDayCount(int year,int month,int day)
{
	int	daysOfFeb = isLeapYear(year)? 29:28;
	int[] days = {31,daysOfFeb,31,30,31,30,31,31,30,31,30,31};
    //或者用if语句直接替换数组内容
    //if(isLeapYear(year))days[1] = 29;
	int count = 0;
	for(int i = 0;i+1 < month;i++)
	{
		count += days[i];
	}
	count += day;
	return count;
}
```

### `<span id="jump2">`2、foreach `</span>`

从头到尾依次读取数组元素

```c#
//foreach(元素类型 变量名 in 数组名称)
int[] array = {1,2,3,4};
foreach(int ii in array)
{
    Console.WriteLine(ii);
}
//输出
//1
//2
//3
//4
```

（1）优点：简单方便

（2）缺点：

    ①不能读取局部元素

    ②不能修改元素

    ③只能遍历实现enumerable接口的集合对象

### 3、扩展：父子类型

声明父类类型，赋值子类对象

```c#
Array arr01 = new int[2];
Array arr02 = new string["1"];
```

定义方法时使用，方便传参

```c#
private static void Father(Array arr01)
{
    ……
}
```

### 4、常用方法及属性

【索引】Array.IndexOf()

找第一个匹配项的索引

```c#
int[] arr01 = new int[]{222,333,444,555};
int index = Array.IndexOf(arr01,444)；
    //返回2
int index = Array.IndexOf(arr01,333)；
    //返回-1
```

【数组长度】数组名.Length

【清除元素值】Array.Clear

【复制元素】Array.copy、数组名.CopyTo

【克隆】数组名.Clone

```c#
Array arr01 = new int[2];
int[] obj01= (int[])arr.Clone();//arr.Clone返回值为object，需要显式转换
```

【查找元素】Array.IndexOf、Array.LastIndexOf

【排序】Array.Sort(数组名)

    从小到大排序

Array.Sort(数组名, 起始索引, 长度)

    从起始索引开始数一定长度，然后对这部分的数组排序

【反转】Array.Reverse
