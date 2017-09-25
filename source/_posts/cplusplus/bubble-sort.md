---
title: 冒泡排序
tags: C/C++
date: 2017-09-25 14:17:49
---
冒泡排序是交换排序的一种，是排序算法中最简单，复杂度最高的一种。
<!-- more -->
# 冒泡排序
## 基本思路
冒泡排序是交换排序的一种，从数组(其长度为j)的起始位置开始，相邻的i，i+1的值进行进行比较，如果i的值大于i+1值，那么将他们进行交换，如此循环至数组结束，那么数值最大的值将位于数组末尾(j-1)。从数组起始再次比较，直至数组j-2处，如此循环直至数组起始位置。

## 算法实现
算法实现可以从[practices](https://github.com/brucegu/practices/tree/master/algorithm/sort)中找到。
```
void bubble_demo()
{
    int data[] = { 10, 20, 11, 30, 9, 5, 12, 29 };
    bubble( data, lengthof(data, int) );
    print_int_array( data, lengthof(data, int) );
}

void bubble( int *data, int length )
{
    for (int i = 0; i < length-1; i++)
    {
        for (int j = 0; j < length-i-1; j++)
        {
            if (data[j] > data[j+1]) swap( data, j, j+1 );
        }
    }
}

void swap( int *data, int i, int j )
{
    int tmp = data[i];
    data[i] = data[j];
    data[j] = tmp;
}

void print_int_array( int *data, int length )
{
    printf( "data:\n" );
    for (int i=0; i<length; i++)
    {
        printf( " %d", data[i] );
    }
}
```
