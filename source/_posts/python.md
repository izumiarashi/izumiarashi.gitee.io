---
title: Python零点五基础学习笔记
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/5a6e6c21cacd351.jpg'
cover: false
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/20180413101445_VXV2l.png'
date: 2021-01-20 19:30:07
category: 笔记
tags: 
- python
summary: 入门数据分析第一步
---

计算机做什么？

计算、记录结果。

厂商设置的内置计算、用我们的想法进行计算

无解问题：图灵停机

计算思维？

计算是什么？

知识是什么？

陈述性知识

程序性知识：方法recipe

固定程序计算机

存储程序计算机

![image-20210111213518900](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210111213518900.png)

控制单元：通过程序计数器，按照指令序列顺序执行，让数据进入ALU

ALU 算术逻辑单元：简单计算并存回内存，每过一段时间执行测试指令

测试指令：改变程序计数器，是系统跳到代码的某一个地方，改变程序执行的代码位置

完成程序并输出

原语

任何计算只需要6种原语

图灵完备

原语集

原语结构

语法Syntax: Determines whether a string is legal

*cat dog man*

静态语义Static semantics:  Determines whether a string has meaning 

*I are big*

形式语义（全语义）Semantics: Assigns a meaning to a **legal** sentence

哪里会出错？

语法错误：常见但容易发现

静态语义错误：编译型语言在执行前就会指出，解释型语言程序会持续地执行然后指出。

没有语法和静态语义错误，但表达的意思不是我们想要的

程序崩溃、循环运行、结果不符合预期——通过防御性编程来避免



配置python环境https://www.jianshu.com/p/506debe61423

1、记得右下角设置语言模式

2、yapf设置需要添加args

```python
"python.formatting.yapfArgs": [
        "--style={based_on_style: pep8, indent_width: 4}"
    ], 
```

“选择”

低级编程语言

移动数据；执行简单的ALU操作：加、减、比较；根据比较结果跳转。

检查器进程处理：确认语法和静态语义→解释器进程执行

![image-20210114200811915](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210114200811915.png)

高级编程语言

编译型语言：检查后，通过编译器转化为低级代码（基本计算机指令）。代码执行更快，如果有bug会难以找到

![image-20210114200752507](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210114200752507.png)



解释型语言：将源代码转换成一种内部中间数据结构，然后按序逐句转换成低级编程语言。代码执行稍慢，找bug更简单。

![image-20210114201653288](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210114201653288.png)

数据对象Object

type()查看对象类型

#### 标量对象scalar

整数int、浮点数float、布尔bool

为什么要区分整数运算和浮点数运算呢？因为整数运算的结果永远是精确的，而浮点数运算的结果不一定精确，因为计算机内存再大，也无法精确表示出无限循环小数，比如 0.1 换成二进制表示就是无限循环小

"no newline at end of file"报错——换行保存

表达式expression

基本语法<object><operator><object>

赋值 =

等于 ==

是否等于 !=

与and或or非not

类型转换

float(3)→3.0

int（3.9）→3

```python
b = a+c
```

此时赋值b后存储的是一个数值而非公式，之后改变a或c不会改变b的值

```python
b = 10
c = b >9
print(c)
```

结果是bool型，true.而不是int型，10.

#### 非标量对象

字符串str：'abc'、"abc"、'123'、str(123)

3 * 'a'→返回'aaa'

'aaa' + str(123)→返回'aaa123' 

len()查看字母串长度

单双引号没有区别，可以减少使用转义符\

```python
"I'm a otaku."  # 双引号

'I\'m a otaku.' # 单引号

'''
多行注释里的单双引号也可成套换用
'''
```

索引indexing

![image-20210120203648688](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210120203648688.png)

切片slicing

![image-20210120203620984](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210120203620984.png)

返回的值为开始值到**结束值-1**

补充：str[i:j:k]表示从i到j-1中每间隔k取一次值

z = 'abcdefg'

z[:3] 返回'abc'

z[1:] 返回'bcsefg'

z[:] 返回'abcefg'

z[1:5:2] 返回'bdf'

z[::3] 返回'adg'

获取输入值

```python
a = input('hint message')  #python 3.x将raw_input改为input，并将原先的input删除
```

输出值

```python
x = 3
print(x*x)  #返回运算结果9而非公式
```

直接（直线型）程序：按顺序执行命令

分支结构Branching structure：通过测试来做决定

条件语句conditional

```python
import time  #模块要放在首行
x = int(input('输入一个数字：'))
if x % 2 == 0:  # %表示余数。注释前要空两格。
    print('偶数')
else:
    print('奇数')
time.sleep(3)  #延时
print('计算结束')
```

↓输入值为str，要转为数值

![image-20210120212817847](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210120212817847.png)

```python
if x > 2:
    if x == 3:
        print('3')
    else:
        print('>2 and no 3')
elif x == 2:
    print('2')
else:
    print('<2')
```

循环lteration

looping structure

while():

