#引用
http://wiki.ubuntu.com.cn/%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:MakeFile%E4%BB%8B%E7%BB%8D

# gmake 与 make
gmake 是GNU make的缩写，在大多数的linux系统中，make就是GNU Make，对于一些unix的系统，make指向系统自带的make，例如：BSD make.

#makefile介绍
make命令执行时，需要一个makefile文件来告诉他如何编译和链接程序。

#makefile规则
makefile的编写规则如下：
target ... : prerequisites ...
	command
	...
	...
target可以是一个目标文件(object file)，也可以是一个可执行文件，还可以是一个标签（label，也就是伪目标）。
prerequisties是生成target所需要的文件。
command是make需要执行的命令（任意的shell命令），command之前必须有个TAB建。
这是一个依赖关系的描述，生成target文件依赖于prerequisties的这些文件，如果依赖文件中的任何文件都比target要新，那么就会运行command重新生成target。

#makefile示例
```
shap : combinator.o circle.o rectangle.o
	gcc -o shap combinator.o circle.o rectangle.o

combinator.o : combinator.c circle.h rectangle.h
	gcc -c combinator.c
circle.o : circle.c circle.h
	gcc -c circle.c
rectangle.o : rectangle.c rectangle.h
	gcc -c rectangle.c

clean :
	del shap combinator.o circle.o rectangle.o
```

#make中使用变量
从上面的示例可以看到，很多重复的地方，可以使用变量来替代：
```
objects = combinator.o circle.o rectangle.o
shap : $(objects)
	gcc -o shap $(objects)

combinator.o : combinator.c circle.h rectangle.h
	gcc -c combinator.c
circle.o : circle.c circle.h
	gcc -c circle.c
rectangle.o : rectangle.c rectangle.h
	gcc -c rectangle.c

clean :
	del shap $(objects)
```

#make中的隐晦规则和伪目标
GNU的make相当强大，他可以自动推导出文件以及文件依赖关系后面的命令，对于每一个[.o]文件，他会自动把[.c]文件加到依赖关系中，甚至后面都有 gcc -c [.c]这样的命令，make一会自动推导(nmake中，只能推导依赖关系，好像没法推导命令)。
```
objects = combinator.o circle.o rectangle.o
shap : $(objects)
	gcc -o shap.exe $(objects)

combinator.o : circle.h rectangle.h
circle.o : circle.h
rectangle.o : rectangle.h

clean :
	-del shap.exe $(objects)
```
这里的.PHONY表示clean是一个伪目标。这里在del前加-，意味着也许某些文件会出问题，但不要管，继续做后面的事情

#makefile内容
makefile文件中有五个东西：显示规则，隐示规则，变量定义，文件指示和注释
显示规则：显示书写出来，如何生成目标文件，依赖文件和生成文件的命令
隐示规则：是由make命令推导出来，这样方便写出简洁的makefile
变量定义：可以定义一些变量，一般都是字符串变量，当make命令执行的时候，会把变量的值替换到使用的地方
文件指示：
	* 在一个makefile中引用另一个makefile，使用include <filename>;
	* 根据某些情况制定makefile中的有效部分
	* 定义一个多行的命令
注释：用#来写注释

#make的工作方式
- make命令会寻找当前目录下名为：GNUmakefile, makefile, Makefile的文件
- 读入所有的makefile
- 读入被include的makefile
- 初始化文件中的变量
- 推导隐晦规则，并分析所有规则
- 为所有文件建立依赖关系
- 根据依赖关系，决定哪些目标重新生成
- 执行生成命令