# 全面系统 Python3入门+进阶课程

## 导学

### python 能做什么

- 爬虫
- 大数据
- 测试
- AI
- Web
- 脚本处理

### Python的特性

Python与Python的特点：

1.Python是一门编程语言，它只是众多编程语言中的一种。

2.语法简洁、优雅、编写的程序统一阅读。

3.跨平台，可以运行在Windows、Linux及MacOS

4.易于学习。

5.极为强大而丰富的标准库与第三方库，比如电子邮件，比如图形GUI界面。

6.Python是面向对象的语言。

### 我为什么喜欢Python

1. 简洁、灵活、优雅、哲学
2. 易于上手难于精通
3. Python既有动态脚本的特性，又有面向对象的特性，非常具有自己的特点

### Python的缺点

- 慢，相较于C、C++、Java，运行效率较慢
  - 编译型语言(C、C++)、解释性语言(JavaScript、Python)
  -  Java和C#在执行之前也有编译，但不会编译成机器码，而是中间代码，类型不是很明确
  - 运行效率与开发效率不可兼得

###  一个经典误区

世界不是只有Web，还有很多问题需要使用编程来解决。不要把思维局限在Web上，这只是编程的一个应用方向。

### python能做些什么？

几乎是万能的

1. 爬虫
2. 大数据与数据分析(Spark)
3. 自动化运维与自动化测试
4. Web开发：Flask、Django
5. 机器学习：Tensor Flow
6. 胶水语言：混合其他如C++、Java等来编程。能够把其他语言制作的各种模块(尤其是C/C++)很轻松地联结在一起

### 课程内容与特点

- 基础语法
- Pythonic
- Python高性能与优化
- 数据结构

### Python的前景

### 课程维护与提问

代码更新，知乎专栏https://zhuanlan.zhihu.com/oldtimes

## 第2章 Python环境安装

### 下载Python安装包与安装Python

win下载地址：https://www.python.org/downloads/windows/

点击安装 

第一步

- 选择Customize installation，自主安装
- 同时勾选 Add Python 3.7 to PATH，添加环境变量

第二步，直接选next

第三部，保持默认选项，可以修改安装目录，点击安装

## 第3章 理解什么是写代码与Python的基本类型

### 什么是代码，什么是写代码

代码是现实世界事物在计算机世界中的映射

写代码是将现实世界中的事物用计算机语言来描述

### 数字：整形与浮点型

Number:数字

- 整数、小数
- 整数、浮点数

整数：int

浮点数：float

其他语言：单精度(float)，双精度(double)，python中不分

其他语言：short，int，long

```python
type(1)  /# int #/
type(-1) /# int #/
type(1*1) /# int #/
type(2//2) /# int #/ 双斜杠得到 int，原因2//2结果是1
type(1.1) /# float #/
type(1+0.1) /# float #/
type(1+1.0) /# float #/
type(1*1.0) /# float #/
type(2/2) /# float #/ 单斜杠得到 float，原因2/2结果是1.0
```

/和//的区别

1/2 0.5

1//2 0

单斜杠是除法保留小数点，双斜杠是整除只保留整数部分

### 10、2、8、16进制

### 各进制的表示与转换

21：01

