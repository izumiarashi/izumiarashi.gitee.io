---
title: Python基础学习笔记（一）（可能有二）
img: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210127162525133.png'
cover: true
coverImg: 'https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210127163046019.png'
date: 2021-01-20 19:30:07
category: 编程笔记
tags: 
- python
summary: 了解计算机原理
---

# 一、基础介绍

## （一）计算机做什么？

计算、记录结果。

厂商设置的内置计算、用我们的想法进行计算

*无解问题：图灵停机*

计算思维？

计算是什么？

知识是什么？

陈述性知识：定义

程序性知识：方法recipe

固定程序计算机

存储程序计算机

![基础集齐结构](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210111213518900.png)

控制单元：通过程序计数器，按照指令序列顺序执行，让数据进入ALU

ALU 算术逻辑单元：简单计算并存回内存，每过一段时间执行测试指令

测试指令：改变程序计数器，是系统跳到代码的某一个地方，改变程序执行的代码位置

完成程序并输出

原语：任何计算只需要6种原语

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



*配置python环境https://www.jianshu.com/p/506debe61423*

*1、记得右下角设置语言模式*

*2、yapf设置需要添加args*

```python
"python.formatting.yapfArgs": [
        "--style={based_on_style: pep8, indent_width: 4}"
    ], 
```



# 二、编程语言

## （一）种类

### 1、低级编程语言

移动数据；执行简单的ALU操作：加、减、比较；根据比较结果跳转。

检查器进程处理：确认语法和静态语义→解释器进程执行

![image-20210114200811915](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210114200811915.png)

### 2、高级编程语言

分为两种

（1）编译型语言：检查后，通过编译器转化为低级代码（基本计算机指令）。代码执行更快，如果有bug会难以找到

![image-20210114200752507](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210114200752507.png)



（2）解释型语言：将源代码转换成一种内部中间数据结构，然后按序逐句转换成低级编程语言。代码执行稍慢，找bug更简单。

![image-20210114201653288](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210114201653288.png)

## （二）数据对象Object

可以使用type()查看对象类型

### 1、标量对象scalar

**（1）整数int、浮点数float、布尔bool**

​	为什么要区分整数运算和浮点数运算？

*因为整数运算的结果永远是精确的，而浮点数运算的结果不一定精确，因为计算机内存再大，也无法精确表示出无限循环小数，比如 0.1 换成二进制表示就是无限循环小*。

​	True和False首字母大写才是布尔类型，因为python是大小写敏感型语言。

**补充：**

![来源：http://www.weixueyuan.net/a/380.html](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210126222954511.png)

拓展一：浅谈Python里面None True False之间的区别https://blog.csdn.net/weixin_30709043/article/details/112883256 ：

“0值的整型/浮点型，空字符串(‘ ')，空列表([]),空元组({})，空集合(set())都是等价于False,但是不等于None。”、“0.3 == 3 * 0.1 为False”

拓展二：Python中的True和False与bool()函数https://blog.csdn.net/liuweiyuxiang/article/details/89336980

*“None 为 False、数字类型（整型、浮点型……）0为False、列表类型（list、tuple……）长度为0为False、str类型长度为0的为False、Map类型（字典）条目个数为0的为False，其余都为True”*

*拓展三：round()函数https://www.runoob.com/python/func-number-round.html*

**（2）表达式expression**

①基本语法<对象object><运算符operator><对象object>

②运算符：

|                    | 运算符 | 描述                                                         | 表达式 |
| ------------------ | ------ | ------------------------------------------------------------ | ------ |
| 算术运算符         | +      | 加                                                           |        |
|                    | -      | 减                                                           |        |
|                    | *      | 乘                                                           |        |
|                    | /      | 除，python3.0中总是返回浮点数                                |        |
|                    | %      | 取模-返回除法余数                                            |        |
|                    | **     | 幂-返回x的y次幂                                              |        |
|                    | //     | 整除-向下取商的整数部分。进行floor除法，操作数有浮点数时返回浮点数，反之返回整数 |        |
| 比较运算符         | ==     | 是否相等                                                     |        |
|                    | !=     | 是否不相等                                                   |        |
|                    | <>     | 是否不相等                                                   |        |
|                    | >      | 是否大于                                                     |        |
|                    | <      | 是否小于                                                     |        |
|                    | >=     | 是否大于等于                                                 |        |
|                    | <=     | 是否小于等于                                                 |        |
| 赋值运算符         | =      | 赋值                                                         |        |
|                    | +=     | 加法赋值，将a+b的值赋给a                                     | a += b |
|                    | -=     | 减法赋值                                                     |        |
|                    | *=     | 乘法赋值                                                     |        |
|                    | /=     | 除法赋值                                                     |        |
|                    | %=     | 取模赋值                                                     |        |
|                    | **=    | 幂赋值                                                       |        |
|                    | //=    | 取整赋值                                                     |        |
| 位运算符           | &      | 按位与运算符：参与运算的两个值相应位都为1，则该位结果为1，否则0 |        |
|                    | \|     | 按位或运算符：对应的两个值的二进位有一个为1，则结果位为1     |        |
|                    | ^      | 按位非运算符：对应的两个值二进位不同时，结果为1              |        |
|                    | ~      | 按位取反运算符：对数据的每个二进制位取反，1变0，0变1         |        |
|                    | <<     | 左移动运算符：运算数a的各二进位全部左移b位，高位丢弃，低位补0 | a<<b   |
|                    | >>     | 右移动运算符：运算数a的各二进位全部右移b位                   | a>>b   |
| 逻辑运算符         | and    | 布尔“与”：a和b都为True时，返回True，否则False                |        |
|                    | or     | 布尔“或”：a或b中有一个为True时，返回True，否则为False        |        |
|                    | not    | 布尔“非”：如果a为True，返回为False。如果a为False，返回为True |        |
| 成员运算符         | in     | 指定序列b中找到值a则返回True，否则返回False                  | a in b |
|                    | not in | 指定序列中没有找到值则返回True，否则返回False                |        |
| 身份运算符         | is     | 判断两个标识符是否引用自同一对象                             | b is a |
|                    | is not | 判断两个标识符是否引用自不同对象                             |        |
| *拓展：身份运算符* |        | *https://jingyan.baidu.com/article/7c6fb428d6876e80652c9069.html* |        |



![运算优先级](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210127214727508.png)

**（3）类型转换**

float(3)→3.0

int（3.9）→3

**例**

```python
b = a+c  # 注释的'#'前要空两格，后要空一格
```

此时赋值b后存储的是一个数值而非公式，之后改变a或c不会改变b的值

```python
b = 10
c = b >9
print(c)
```

结果是bool型——True.而不是int型——10.

*拓展：空格的用法https://www.imooc.com/article/265705*



### 2、非标量对象

**（1）字符串str**

①'abc'、"abc"、'123'、str(123)

​	3 * 'a'→返回'aaa'

​	'aaa' + str(123)→返回'aaa123' 

②通过len()查看字符串长度

③单双引号没有区别，可以减少使用转义符\

```python
"I'm a otaku."  # 双引号

'I\'m a otaku.' # 单引号

'''
多行注释里的单双引号也可成套换用
'''
```

*拓展：字符串、转义符https://www.runoob.com/python/python-strings.html*

④索引indexing

![image-20210120203648688](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210120203648688.png)

切片slicing

![image-20210120203620984](https://izumi-blog.oss-cn-shanghai.aliyuncs.com/img/image-20210120203620984.png)

返回的值为开始值到**结束值-1**

拓展：

str[i:j:k]表示从i到j-1中每间隔k取一次值

z = 'abcdefg'

z[:3] 返回'abc'

z[1:] 返回'bcsefg'

z[:] 返回'abcefg'

z[1:5:2] 返回'bdf'

z[::3] 返回'adg'

# 三、简单脚本

## （一）直线式程序：按顺序执行命令

获取输入值

```python
a = input('hint message')  # python 3.x将raw_input改为input，并将原先的input删除
```

输出值

```python
x = 3
print(x*x)  # 返回运算结果9而非公式

```

## （二）分支式程序：通过测试来做决定顺序

### 1、分支结构Branching structure：条件语句conditional

**if()**

```python
import time  # 模块要放在首行
x = int(input('输入一个数字：'))  #要将输入值转为数值，否则报错
if x % 2 == 0:  # %表示余数。
    print('偶数')
else:
    print('奇数')
time.sleep(3)  #延时
print('计算结束')

```

**elif()**

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

一段代码中有多个if()，会逐一进行；有多个elif()，则会在满足条件后跳出if()。

*if()领头大哥各自为政，elif()作为小弟服从大哥。*

### 2、循环结构looping structure：循环语句lteration

**（1）while():**

①要点

​	需要在循环外部对循环变量初始化

​	需要通过测试造成循环变量变化，从而能够停止程序

②猜测检验方法Guess and check：对有限可能的问题有效

```python
# 求立方根
x = int(input('输入一个数字：'))
i = 0
while i**3 < abs(x):
    i = i + 1
if i**3 != x:
    print('这不是一个完全立方数')
else:
    if x < 0:
        i = -i
    print('立方根为' + str(i))  # 字符串必须接字符串，不能str+int

```

**（2）for循环：python提供的特殊机制**

①构成

for <标识符identifier> in <序列sequence>:

​	<代码块codeblock>

​	break语句：基于测试结果提示何时跳出循环

​	值域：作为序列

​		range(m) = [0,1,2,3...m-1]

​		range(m, n) = [m,m+1...n-1]

②测试完序列所有的数，或执行break语句后，结束循环

```python
# 求立方根v2.0
x = int(input('输入一个数字：'))
for i in range(0, abs(x)+1):  # 因为值域取m到n-1，所以需要给abs(x)加1
    # 值域中间需要空格 (m, n)
    if i**3 == abs(x):  # 小心赋值和等于混用
        break
if i**3 != x:  # 不能确定结束循环是因为break语句还是因为执行完了序列
    print('这不是一个完全立方数')
else:
    if x < 0:
        i = -i
    print('立方根为' + str(i))  # 字符串必须接字符串，不能str+int

```

**例**

```python
school = 'Massachusetts Institute of Technology'
# 值域为字符串时，会逐个检索字符串的每一个字符，循环结束后输出'done'
numVowels = 0
numCons = 0

for char in school:
    if char == 'a' or char == 'e' or char == 'i' \  # 句末转义符表示换行
       or char == 'o' or char == 'u':
        numVowels += 1
    elif char == 'o' or char == 'M':
        print char  # python3.0中取消了print语句而引入print()函数，所以print后必须加括号
    else:
        numCons -= 1

print 'numVowels is: ' + str(numVowels)  # 注意'i' != 'I'
print 'numCons is: ' + str(numCons)  

```

