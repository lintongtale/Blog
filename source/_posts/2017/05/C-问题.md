---
title: C++问题
date: 2017-06-03 18:44:06
comments: true
tags:
- c++
- 问题
categories:
- 编程
- c++
description:
- C++，那些年我们遇到的坑。
---
## 宏命令
	• #if _MSC_VER > 1000
	是指如果vc编译器的版本大于1000则这个语句被编译！
	• #ifndef __SOMEFILE_H__
	#define __SOMEFILE_H__
	…
	#endif
	可以保证同一个文件不会被多次包含（基于文件内容），依赖于宏名字不能冲突，适合于跨平台
	• #pragma once
	可以保证同一个文件不会被多次包含（基于文件物理位置），由编译器提供
## sstream
	• void clear ( iostate state = goodbit ) 清空该流的错误标记，oss.clear()！
	• void str ( const string & s ) 该方法是重新给ostringstream灌新值的意思，oss.str("")。

## 指针与引用
	• const int* 与 int* const <const T*类>
		○ const int* p = &a; 指向常量的指针，不能改变p所指向对象的值
		○ int* const p = &a; 常量指针，指针本身的值不可以改变
		○ const int* const p = &a; 一个指向常量对象的常量指针，既不可以改变指针本身，也不可以改变指针指向的对象
	• & 引用 C++对C语言的扩充。引用就是某一变量（目标）的一个别名，对引用的操作与对变量直接操作完全一样
	• const T&
		○ const int a = 10;
		○ const int& r = a;
	• const T*& 指向常量对象的指针的引用
	• T *const& 对常量指针的引用
	参考连接：
	http://blog.csdn.net/luoweifu/article/details/45600415

## #pragma region和#pragma endregion关键字
	用于定义拓展和收缩的代码区域的开头和结尾。
	
指定文件目录中正斜杠和反斜杠（“/”和“\\”）的区别
	• “/“正斜杠，posix标准，linux中用于指定文件目录，“./”中“.”表示当前目录
	• “\\”反斜杠，第一个“\”为转义字符，windows中用于指定文件目录，此外 windows 也支持“/”

C/C++ 中 extern 关键字详解 - chao_yu - 博客园
http://www.cnblogs.com/yc_sunniwell/archive/2010/07/14/1777431.html


# C++ Primer：C++ 基础
http://jennica.space/2017/01/13/cpp-primer-basic/
## 1、开始学习 C++
* 文件重定向：将标准输入输出与文件关联，运行命令 prog1 < infile > outfile，prog1 是编译后所产生的可执行文件，上述命令会从一个名为 infile 的文件中读取输入数据，并将输出结果写入到一个名为 outfile 的文件中。

# C++ 的一些规范
* 1、包含来自标准库的头文件时，用尖括号（<>）包含头文件名，对于不属于标准库的头文件，则用双引号（""）包围。
