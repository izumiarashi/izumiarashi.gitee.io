---
title: C#练习（二）—— 彩票生成
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/微信图片_20210424230557.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-05-18 15:52:27
category: 编程练习
tags: C#
summary: 数组应用
---


<!--more-->

## 题目

制作一个彩票生成器

红球：1-33，抽取6个，不能重复

蓝球：1-16，抽取1个

| 中奖条件         |
| ---------------- |
| 6红球+蓝球       |
| 6红球            |
| 5红球+蓝球       |
| 红球+蓝球共中5个 |
| 红球+蓝球共中4个 |
| 1蓝球            |



## 需求拆分

（1）购买彩票：

依次输入号码，超出可选范围时提示。

输入重复号码时提示。

记录7个数字

（2）抽取彩票

随机产生7个

（3）比较机选和自选两注彩票，返回中奖等级

先计算红篮球

## 初次尝试

```c#
static Random random1 = new Random();
static void Main()
{
	int[] arrRedChooseNum = InputRedLotNum();
	Console.WriteLine("请输入蓝色球号码"); //【错误】没有对输入数字正确性进行判断
	int blueChooseNum = int.Parse(Console.ReadLine());
	int[] arrRedLotNum = GetRandomRedNum();
	int blueLotNum = random1.Next(1,16); //【错误】随机数左等右不等
	int prizeFinal = CompareLotNum(arrRedChooseNum, arrRedLotNum, blueChooseNum, blueLotNum);
	if(prizeFinal > 0)
	{
		Console.WriteLine("获得{0}等奖。", prizeFinal);
		Console.ReadLine();
	}
	else
	{
		Console.WriteLine("你没有中奖。");
		Console.ReadLine();
	}
}
private static int[] InputRedLotNum()
{
	int[] arrRedChooseNum = new int[6];
	//【错误】开始想通过一个数组记录红球+蓝球，改为只记录红球后忘记修改数组长度
	for(int i = 0; i <= 5;)
	{
		Console.WriteLine("请输入第{0}个彩票号码",i+1);
		int lotNum = int.Parse(Console.ReadLine());
		if(Array.IndexOf(arrRedChooseNum, lotNum) >= 0)
			{ //if后有两行时记得大括号
				Console.WriteLine("该数字已存在。"); 
            //没检索到→还没有这个数→返回-1
				continue;
			}
		if(lotNum > 33 || lotNum <= 0)
			{
				Console.WriteLine("请输入正确的数字。");
				continue;
			}
		arrRedChooseNum[i++] = lotNum;
	}
	return arrRedChooseNum;
}
private static int[] GetRandomRedNum()
{
	int[] arrRedLotNum = new int[6];
	int randomNum;
	for(int i = 0; i <= 5;)
	{
		randomNum = random1.Next(1,33); //【错误】随机数左等右不等
		if (Array.IndexOf(arrRedLotNum, randomNum) < 0)
			arrRedLotNum[i] = randomNum;
			i++;
       		//【优化】i++是先赋值再自增，不用单独拉出来
        	//arrRedLotNum[i++] = randomNum;
	}
	Array.Sort(arrRedLotNum);
	return arrRedLotNum; //记住要返回值
}
private static int CompareLotNum(int[] arrRedChooseNum,int[] arrRedLotNum,int blueChooseNum,int blueLotNum)
{
	int countChoose = 0;
	int countRandom = 0;
	int prizeRed = 0;
	while(countChoose <= 5)
	{
		while(countRandom <= 5)
		{
			if(arrRedChooseNum[countChoose] == arrRedLotNum[countRandom])
			{
				prizeRed++;
				break;
			}
			else
				countRandom++;
		}
		countChoose++;
		countRandom = 0; //【错误】忘记初始化
	}
	if(blueLotNum == blueChooseNum)
	{
		switch(prizeRed)
		{
			case 3:
				return 5;
			case 4:
				return 4;
			case 5:
				return 3;
			case 6:
				return 1;
			default: //不要漏了default
				return 6;
		}
	}
	else if (blueLotNum != blueChooseNum && prizeRed == 6)
		return 2;
	else
		return 0;
}
```

## 标准答案

https://www.bilibili.com/video/BV12s411g7gU?p=67&spm_id_from=pageDriver P67

```c#
static void Main()
{
    int[] myTicket = BuyTicket();
    int[] randomTicket = CreateRandomTicket();
    int level = TicketEquals(myTicket, randomTicket);
    if(level != 0)//以下略
}
private static int[] BuyTicket()
{
	int[] ticket = new int[7];
    for(int i = 0;i < 6;i++)
    {
        Console.WriteLine("请输入第{0}个红球号码：", i+1)
        int redNumber = int.Parse(Console.ReadLine());
        if(redNumber < 1 || redNumber > 33)
            Console.WriteLine("购买的号码超过范围");
        else if(Array.IndexOf(ticket,redNumber) >= 0)
            Console.WriteLine("号码已经存在");
        else
            ticket[i++] = redNumber;
    }
    do
    {
        Console.WriteLine("请输入蓝球号码：");
   		int blueNumber = int.Parse(Console.ReadLine());
    	if (blueNumber >= 1 && blueNumber <= 16)
    		ticket[6] = blueNumber;
    	else
        	Console.WriteLine("号码超过范围");
    }while(blueNumber < 1 || blueNumber >16)
    return ticket;
}
static Random random = new Random();
private static int[] CreateRandomTicket()
{
    int[] ticket = new int[7];
    for(int i = 0; i < 6;)
    {
        int redNumber = random.Next(1,34);
        if(Array.IndexOf(ticket, redNumber) < 0)
            ticket[i++] = redNumber;
    }
    ticket[6] = random.Next(1,17);
    Array.Sort(ticket, 0, 6); //局部排序
    return ticket;
}
private static int TicketEquals(int[] myticket, int[] randomTicket)
{
    int blueCount = myTicket[6] == randomTicket[6]?1:0;
    int redCount;
    for(int i = 0; i < 6; i++)
    {
        if(Array.IndexOf(randomTicket, myTicket[i],0,6) >= 0)
        	redConut++; //使用indexof直接实现需求
    }
    int level;
    if(blueCount + redCount == 7)
        return 1;
    else if(redCount == 6)
        return 2;
    else if(blueCount + redCount == 6)
        return 3;
    else if(blueCount + redCount == 5)
        return 4;
    else if(blueCount + redCount == 4)
        return 5;
    else if(blueCount = 1)
        return 6;
    else
        return 0;
}
```

## 进一步简化

```c#
while(true)
{
	Console.WriteLine("请输入蓝球号码：");
	int blueNumber = int.Parse(Console.ReadLine());
	if (blueNumber >= 1 && blueNumber <= 16)
    {
        ticket[6] = blueNumber;
	   	break; //死循环+break，不用考虑while条件
    }
	else
    	Console.WriteLine("号码超过范围");
}
```

将blueCount声明为Bool，用switch+三元运算来判断中奖等级