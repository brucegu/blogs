---
title: 常用数列概念
tags: sequence
categories:
    - math
date: 2017-09-25 16:44:48
---

编程中经常会用到的一些数学知识和公式。

<!-- more -->
## 斐波那契数列
斐波那契数列，又称黄金分割数列，因数学家Leonardoda Fibonacci以兔子繁殖为例而引入，故又称兔子数列。在数学上，斐波那契数列被以如下递归的方法定义：F(0) = 0, F(1) = 1, F(n) = F(n-1) + F(n-2) (n>=2, n∈N*)，这个数列从第三项开始，每一项是前两项的和。
```
1, 1, 2, 3, 5, 8 ...
```

## 等比数列求和
一个数列，如果任意一项与前一项的比值是一个常数，用q来代表这个常数，且任一项不为0，即A(n)/A(n-1)=q（n为自然数），这个数列叫等比数列，其中常数q叫公比。
### 通项公式：
a<sub>n</sub> = a<sub>1</sub> * q<sup>(n-1)</sup>;
### 求和公式：
S<sub>n</sub> = a<sub>1</sub> * n (q=1)
S<sub>n</sub> = a<sub>1</sub> * (q<sup>n</sup>-1)/(q-1) (q != 1)
### 求和推导：
（1）S<sub>n</sub>=a<sub>1</sub>+a<sub>2</sub>+a<sub>3</sub>+...+a<sub>n</sub> (公比为q)
（2）qS<sub>n</sub>=a<sub>1</sub>q + a<sub>2</sub>q + a<sub>3</sub>q +...+ a<sub>n</sub>q = a<sub>2</sub>+ a<sub>3</sub>+ a<sub>4</sub>+...+ a<sub>n</sub>+ a<sub>(n+1)</sub>
（3）S<sub>n</sub>-qS<sub>n</sub>=(1-q)S<sub>n</sub>=a<sub>1</sub>-a<sub>(n+1)</sub>
（4）a<sub>(n+1)</sub>=a<sub>1</sub>q<sup>n</sup>
（5）S<sub>n</sub>=a<sub>1</sub>(1-q<sup>n</sup>)/(1-q)（q≠1)

## 等差数列求和
一个数列，从第二项开始，每一项与前一项的差等于同一个常数，那么这个数列叫等差数列。
### 通项公式：
a<sub>n</sub> = a<sub>1</sub> + (n-1)d;
### 求和公式：
S<sub>n</sub> = (a<sub>1</sub> + a<sub>n</sub>) * n / 2;
### 推导过程：
S<sub>n</sub> = a<sub>1</sub> + ... + a<sub>n</sub>
S<sub>n</sub> = n * a<sub>1</sub> + ( 0 + 1 + 2 ... + (n-1) ) * d
S<sub>n</sub> = n * a<sub>1</sub> + n * (n-1) * d / 2
S<sub>n</sub> = (n * a<sub>1</sub> + n * a<sub>1</sub> + n * (n-1) * d) /2
S<sub>n</sub> = n * (a<sub>1</sub> + a<sub>n</sub>) / 2
