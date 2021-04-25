---
title: C#练习（一）——制作年历
img: 'C:\Users\wb.chenyihao\Pictures\满\微信图片_20210424230602.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-04-25 15:52:11
category: 编程练习
tags: C#
summary: 
---

<!--more-->

题目及答案来源: https://www.bilibili.com/video/BV12s411g7gU?p=54

## 题目

制作一个年历，输入年份即会输出该年所有月份的月历。

## 需求拆分

1、年历：执行12次月历

2、月历

（1）显示表头

（2）判断当月1日是星期几

（3）逢周六换行

（4）计算每月天数

3、判断每月1日星期几：DayOfWeek方法

4、每月天数：通过switch-case判断，对闰年的2月做特殊处理

5、判断闰年：能被4整除但不能被100整除，或者能被400整除

## 初次尝试

**错误**

卡在了输出日历的那一步

**原因**

·没有理解dayofweek方法的含义。

·不了解如何增加空格（tab）、换行（writeline）。

·对什么方法需要什么参数没有认真思考。

```c#
private static int getDay(int year,int month,int day)
{
	DateTime dt = new DateTime(year,month,day);
	return (int)dt.DayOfWeek;
}
private static int calendarMonth(int month)
{
	int dayCount;//##错误##不用声明需要返回的变量
	bool run = isLeapYear();//##错误##没有参数来源
	switch(month)
	{
		case 2:
			if(run = true)
			{
				dayCount = 29;
			}
			else
			{
				dayCount = 28;
			}
			break;
		case 4:
		case 6:
		case 9:
		case 11:
			dayCount = 30;
			break;
		default:
			dayCount = 31;
			break;
	}
	return dayCount;
}
private static bool isLeapYear(int year)
{
	bool run;
	if(year%4 == 0 && year !=100 || year == 400) 
	//##错误##不能被100整除写成了不等于100，400也是
	{
		run = true;
	}
	else
	{
		run = false;
	}
	return run;
}
```

## 标准答案

```c#
private static bool isLeapYear(int year)
{
	if(year % 4 == 0 && year % 100 != 0 || year % 400 == 0)
		return true;
	else
		return false;
}
private static int getDaysByMonth(int year,int month)
{
	if(month >= 1 && month <=12)
	{
		switch(month)
		{
		case 2:
			if(isLeapYear(year))//if（true）即执行
			{
				return 29;
			}
			else
			{
				return 28;
			}
		case 4:
		case 6:
		case 9:
		case 11:
			return 30;
		default:
			return 31;
		} 
	}
	else
	{
		return 0
	}
}
private static int getWeekByDay(int year,int month,int day)
{
	DateTime dt = new DateTime(year,month,day);
	return (int)dt.DayOfWeek;
}
private static void printMonthCalendar(int year, int month)
{
    //1、显示表头
    Console.WriteLine("{0}年{1}月",year,month);
    Console.WriteLine("日\t一\t二\t三\t四\t五");
    //2、根据1日星期数，打印空白
    int week = getWeekByDay(year,month,1);
    for(int i = 0;i < week;i++)
    	Console.Write"\t";
    //3、根据当月天数，打印日
    int days = getDaysByMonth(year, month);
    for(int i = 0;i < days;i++)
        Console.Write(i + "\t");
    	//4、逢周六换行
    	if(getWeekByDay(year,month,i) == 6) //参数使用i，不用额外声明日期变量
            Console.WriteLine();
}
static void Main()
{
    for(int i = 1; i<=12; i++)
    {
        printMonthCalendar(year,i);
        Console.WriteLine();
    }
}
```

## 进一步精简

精简闰年和计算日期数

```c#
private static bool isLeapYear(int year)
{
	return (year % 4 == 0 && year % 100 != 0 || year % 400 == 0);
}
private static int calendarMonth(int year,int month)
{
	if(month < 1 && month >12)
		return 0;
	switch(month)
	{
		case 2:
			return isLeapYear(year)? 29:28;
		case 4:
		case 6:
		case 9:
		case 11:
			return 30;
		default:
			return 31;
	} 
}
```

## 再次尝试

```c#
static void Main()
{
	Console.WriteLine("请输入要查询的年份：");
	int year = int.Parse(Console.ReadLine());
	for(int i = 1;i < 13;i++)
	{
		printCalendar(year,i,1);//#改进点#可以不用传day的参数
	}
	Console.ReadLine();
}
private static void printCalendar(int year,int month,int day)
{
	Console.WriteLine("{0}年{1}月",year,month);
	Console.WriteLine("日\t一\t二\t三\t四\t五\t六");
	int week = getDay(year,month,1);
	for(int i = 0;i < week; i++)
	{
		Console.Write("\t");
	}
	int days = calendarMonth(year,month);
	while (day <= days)
	{
		Console.Write("{0}\t",day);
		day++; //#改进点#可以直接使用for函数
		week++;
		if(week == 7)
		{
			Console.WriteLine();
			week = 0;
		}
	}
	Console.WriteLine();
}
private static int getDay(int year,int month,int day)
{
	DateTime dt = new DateTime(year,month,day);
	return (int)dt.DayOfWeek;
}
private static int calendarMonth(int year,int month)
{
	switch(month)
	{
		case 2:
			return isLeapYear(year)? 29:28;
		case 4:
		case 6:
		case 9:
		case 11:
			return 30;
		default:
			return 31;
	}
}
private static bool isLeapYear(int year)
{
	return(year%4 == 0 && year !=100 || year % 400 == 0);
}
```