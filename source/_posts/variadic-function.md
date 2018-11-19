---
title: variadic function
date: 2018-11-19 14:06:10
categories:
    - C/C++
---
variadic function是可变参数的函数。
<!-- more -->
# 函数声明
```c

void test ( int count, ... );

```

# 使用可变参数
c++中可以使用宏va_list, va_start, va_arg, va_end来使用可变参数。

```c

void test ( int count, ... )
{
    va_list ap;
    va_start( ap, count );

    cout << "void test( int " << count << ", ";
    for ( int i = 0; i < count; i++ )
    {
        cout << "int " << va_arg( ap, int ) << ", "; //第二个参数是可变参数的类型
    }
    cout << " )" << endl;

    va_end( ap );
}

```