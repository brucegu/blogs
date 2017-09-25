---
title: 冒泡排序
tags: C/C++
---
# 冒泡排序
## 基本思路
冒泡排序是交换排序的一种，从数组(其长度为j)的起始位置开始，相邻的i，i+1的值进行进行比较，如果i的值大于i+1值，那么将他们进行交换，如此循环至数组结束，那么数值最大的值将位于数组末尾(j-1)。从数组起始再次比较，直至数组j-2处，如此循环直至数组起始位置。

## 算法实现
```
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
```
