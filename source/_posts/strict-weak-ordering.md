---
title: strict weak ordering
date: 2018-11-19 14:06:10
tags:
    - algorithm
categories:
    - C/C++
---
strict weak ordering是非常重要的概念，特别是在std::map中，以非内置类型（例如：struct）作为key的时候，如果不提供key_compare的实现，编译无法通过。
<!-- more -->
# std::map::key_compare
key_compare是一个接受两个参数返回值为bool类型的函数，例如：comp(a, b)，如果想a在b前面，那么就要返回true。comp需要遵守strict weak ordering的函数定义。
map对象使用它去决定容器中元素的顺序和判断两个元素的key是否等价（如果!comp(a,b) && !comp(b,a)，那么a=b）。map中没有两个元素的key是一样的。

# 维基百科的定义
strict weak ordering是集合S上的二元关系R，这个集合是一个strict partial order（严格偏序关系）。它有以下特性：
- 反自反性：对所有S中的x，xRx 为false；
- 非对称性：对所有S中的x，如果xRy，那么yRx为false；
- 传递性：对所有S中的x，y，z，如果xRy， yRz，那么 xRz；
- 不可比的传递性：对于所有S中的x，y，z，如果x和y不可比( !(xRy)&&!(yRx) )，并且y和z也不可以比，那么x和z也不可比。

# std::map中，strict weak ordering具体实现
map::key_compare默认使用less<T>，它的实现为a < b；也就是说map中默认使用“小于号”来实现，我们只需要重载自定义对象的“小于号”操作符即可，或者提供一个key_compare对象。下面是一个key_compare对象的例子：
```c
struct S
{
    int age;
}

struct comp
{
    bool operator() ( const T& lS, const T& rS ) const
    {
        return lS.age > tS.age;
    }
}

std::map<T, int, comp> mapInstance;

```
对于一般的数值比较满足strict weak ordering的有“小于号”和“大于号”，默认less<T>使用“小于号”，而上面的例子就使用“大于号”来实现的。