---
title: .NET Introduce
date: 2017-09-27 08:00:00
tags:
---

.NET Framework, .NET Core 和 .NET Standard 一直没搞清楚，正好今天查询一番搞清楚了。
<!-- more -->
## 引用
https://docs.microsoft.com/en-us/dotnet/standard/net-standard

## 介绍
.NET Standard 是一份标准，它不是一个具体实现。.NET Framework是.NET Standard的实现。.NET Core也是.NET Standard的实现。.NET Standard的实现还有不少，参考上面的[链接](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)。
举个例子：
```csharp
public interface StandardAPI
{
    void Ping();
    void Pong();
}

public interface NetCoreAPI : StardardAPI
{
    void Shoot();
}

public interface NetFrameworkAPI: StardardAPI
{
    void Fire();
}
```
在创建应用程序或者类库的时候，考虑一下他的应用环境，选择不同的.NET Stardard实现即可。