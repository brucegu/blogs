---
title: C/C++ 基础知识
date: 2017-09-23 08:12:02
tags: 
    - GCC
categories:
    - C/C++
---
什么是GCC, gcc, g++，他们之间的关系是什么，gcc和g++的区别是什么
<!-- more -->
# 说明
以下内容非原创，皆来源于网络。

# GCC，gcc 与 g++
## 介绍
* GCC：GNU Complier Collection，它可以编译C，C++等语言
* gcc：GCC中的GNU C Complier
* g++：GCC中的GNU C++ Complier

本质而言，gcc和g++并不是编译器，也不是编译器的集合，他们只是一种驱动器，根据要编译的文件类型，调用对应的GNU的编译器而已，比如，用gcc
编译一个文件，会有以下几个步骤：
1. Call a preprocessor, like cpp
2. Call an actual compiler, like cc or cc1
3. Call an assembler, like as
4. Call a linker, like ld

由于编译器是可以更换的，所以gcc不仅仅可以编译C文件，所以，更准确的说法是：gcc调用complier，而g++调用C++ compiler。

## gcc 与 g++区别：
- 对于*.c和*.cpp文件，gcc分别当作c和cpp文件编译
- 对于*.c和*.cpp文件，g++都当作cpp文件编译
- 使用g++编译文件时，g++会自动链接标准库STL，而gcc不会
- gcc在编译c文件的时候，可以使用的预定义宏是比较少的
- gcc在编译cpp文件时/g++在编译c和cpp文件时，会加入一些额外的宏：这些宏如下：
    - #define __GXX_WEAK__ 1
    - #define __cplusplus 1
    - #define __DEPRECATED 1
    - #define __GNUG__ 4
    - #define __EXCEPTIONS 1
    - #define __private_extern__ extern

在使用gcc编译cpp文件时，为了能够使用STL，需要加参数 -lstdc++，这并不代表gcc -lstdc++与g++等价，他们的区别不仅仅是这个。

## 常用命令参数
* -g turn on debugging (so GDB gives more friendly output)
* -Wall turn on most warning
* -O和-O2 turn on optimizations
* -o name of the output file
* -c output an object file
* -I specify an included directory
* -L specify a lib directory
* -l link with a library
