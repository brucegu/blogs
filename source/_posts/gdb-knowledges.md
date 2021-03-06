---
title: GDB知识
date: 2017-09-23 08:15:02
tags: 
    - gdb
categories:
    - C/C++
---
gdb的基础知识
<!-- more -->
# 引用
http://www.cnblogs.com/zzx1045917067/archive/2012/12/26/2834310.html

# 基本命令
在使用gdb命令之前，编译程序shap.exe时需要加入-g选项

命令|描述
--------|--------
gdb shap.exe | 启动命令
help list | 查看list命令
list(l) 5， l circle.c 5，l show_circle | 查看当前文件或指定文件第五行前后的代码
break(b) 5，b combinator.c:8 | 在当前文件或指定文件位置设置断点
tbreak n/func | 设置临时断点，到达后自动删除
break combinator.c:5 | 在combinator.c文件的第五行设置断点
break 0x606060 | 用于在内存某一地址设置断点
break 10 if i==3 | 设置条件断点
info breakpoints/watchpoints [n] | n表示断点编号，查看断点和观察点的情况
clear 10 | 清除对应行的断点
delete 3 | 清楚指定编号的断点
disable/enable + 断点编号,编号2 | 使对应编号的断点失效或生效
awatch/watch i | 设置观察点，当变量被读出或写入时程序被暂停
rwatch i | 设置一个观察点，当变量被读出时，程序被暂停
catch | 设置捕捉点捕捉程序运行时的一些事件。如：载入共享库或是C++的异常
tcatch | 捕捉后自动删除该捕捉点
info b | 查看断点
run(r) | 启动shap.exe
print(p) i | 查看变量
diplay exp | 显示表示的值，每当程序运行到断点处，就会显示表达式的值
info display | 显示当前要显示的表达式的情况
delete display No. | 删除要显示的表达式
disable/enable display No. | 使需要显示的表达式失效/生效
undisplay display No. | 用于结束表达式值的显示
watch i | 观察变量
next(n) | 非进入式单步运行
continue(c) | 继续运行
quit(q) | 退出gdb
step(s) | 进入式（会进入当前调用的子函数中）单步执行，但此函数编译时必须有debug信息
finish | 一直运行到函数返回，并打印函数返回时的堆栈地址和返回值及参数值等信息
until 3 | 运行到函数某一行
return 5 | 改变程序流程，直接结束当前函数，并将指定值返回
call func | 在当前位置执行指定的函数
set args arg1 arg2 | 设置运行参数
show args | 显示运行参数
set width 70 | 设置gdb的行宽
cd ../ | 切换工作目录

断点/观察点关系:
* 所有使用断点的操作都适合观察点
* 断点是CPU到达某一地址取指令时中断，观察点是CPU到某一地址读写数据时中断
* 观察点在多线程中左右非常有限，gdb只能观察一个线程中的表达式的值，无法检测非当前线程对表达式的改变

# 堆栈相关命令

# 跳转执行

# signal命令

# 调试已运行的程序
* 通过-pid参数来绑定制定的进程程序，sudo gdb -pid 3095
* 通过进程和进程号来绑定，sudo gdb shap.exe 3095
* 通过attach来附加进程，并通过detach来取消

# 线程
如果程序是多线程的，可以定义断点是否在所有线程上，还是指定的线程上。
```
break frik.c:13 thread 28 if bartab > lim 
```
可以通过"info threads"来查看程序中运行的线程信息。
当程序被gdb挺住时，所有的运行线程都会被停住，这方便查看运行程序的总体情况，恢复程序时，所有线程也会恢复运行。

# 调式core文件
