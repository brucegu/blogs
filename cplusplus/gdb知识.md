# 引用
http://www.cnblogs.com/zzx1045917067/archive/2012/12/26/2834310.html

# 基本命令
在使用gdb命令之前，编译程序shap.exe时需要加入-g选项
* 启动命令
进入gdb命令
```
gdb shap.exe
```
* 查看帮助文档
查看list命令
```
help list
```
* 查看源代码
l（list）命令可以查看源代码。
查看当前文件或指定文件第五行前后的代码。
```
l 5
l combinator.c 5
l circle.c 5
l show_circle
```
* 下断点
在当前文件或指定文件位置设置断点。
```
b 5
b combinator.c:8
```
* 查看断点
```
info b
```
* 启动shap.exe
```
r
```
* 查看变量
```
p i
```
* 观察变量
```
watch i
```
* 单步运行
```
n
```
* 继续运行
```
c
```
* 退出gdb
```
q
```
# 断点

## 设置/取消断点
命令格式|例子|作用
--------|--------|--------
break + 行号| break n | 在当前文件第n行设置断点
tbreak + 行号或函数名| break n/func | 设置临时断点，到达后自动删除
break + filename:行号 | break combinator.c:5 | 在combinator.c文件的第五行设置断点
break + <0x...> | break 0x606060 | 用于在内存某一地址设置断点
break + n + if + 条件 | break 10 if i==3 | 设置条件断点
info breakpoints/watchpoints [n] | info break | n表示断点编号，查看断点和观察点的情况
clear + 断点行号 | clear 10 | 清除对应行的断点
delete + 断点编号 | delete 3 | 清楚指定编号的断点
disable/enable + 断点编号,编号2 | disable 1 | 使对应编号的断点失效或生效
awatch/watch + 变量 | awatch/watch i | 设置观察点，当变量被读出或写入时程序被暂停
rwatch + 变量 | rwatch i | 设置一个观察点，当变量被读出时，程序被暂停
catch | | 设置捕捉点捕捉程序运行时的一些事件。如：载入共享库或是C++的异常
tcatch | | 捕捉后自动删除该捕捉点

## 断点/观察点关系
* 所有使用断点的操作都适合观察点
* 断点是CPU到达某一地址取指令时中断，观察点是CPU到某一地址读写数据时中断
* 观察点在多线程中左右非常有限，gdb只能观察一个线程中的表达式的值，无法检测非当前线程对表达式的改变
