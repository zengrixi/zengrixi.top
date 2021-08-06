---
layout: mypost
title: AtomineerProDocumentation破解使用
categories: [破解]
---

**AtomineerProDocumentation** 是国外的一款用于生成源代码注释的一款 VS 插件工具。

这款插件，支持 C、C++、C++/CLI、C#、Java 语言等，由此可以看出其强大，注释的风格可以灵活配置。

## 安装

软件是付费软件，具体安装方法直接查看官网即可。

## 破解

在软件安装后进入安装目录找到 AtomineerProDocumentation.dll （可以借助Everything等工具进行搜索）。

![dllPath](dllPath.png)

然后用dnSpy工具打开：

![dnSpy](dnSpy.png)

找到 Commands 中的 Initialise 函数，然后一路追踪到a函数中：

```c#
internal static bool a(bool A_0, bool A_1)
{
    int num = 0;
    ...
    if (Commands.c)
    {
        result = Prefs.b(A_0, false);
    }
    ...
    return result;
}
```

接着进入到b函数中，这个函数就是试用判断的实现了：

```c#
internal static bool b(bool A_0, bool A_1 = false)
{
    bool flag = true;
    int num = (DateTime.Today.Year - 2010) * 365 + DateTime.Today.DayOfYear << 8;
    int num2 = 0;
    try
    {
        num2 = Convert.ToInt32(Prefs.c(Prefs.i, "0", "-0"));
    }
    catch
    {
    }
    try
    {
        if (num2 > 40 && num2 < 50)
        {
            num2 = Prefs.b(Prefs.i, num);
        }
    }
    catch
    {
    }
    int num3 = num - num2 >> 8;
    if (num3 > 19)
    {
        try
        {
            Prefs.<>c__DisplayClass19_0 <>c__DisplayClass19_ = new Prefs.<>c__DisplayClass19_0();
            if (Prefs.h[0][0] == '@')
            {
                for (int i = 0; i < Prefs.h.Length; i++)
                {
                    StringBuilder stringBuilder = new StringBuilder();
                    for (int j = 0; j < Prefs.h[i].Length; j++)
                    {
                        stringBuilder.Append((char)((int)Prefs.h[i][j] ^ (16 | j % 16)));
                    }
                    Prefs.h[i] = stringBuilder.ToString();
                }
            }
            bool flag2 = num3 == Prefs.j;
            if (num3 > 29)
            {
                flag = false;
                Commands.a();
                if (flag2 | A_1)
                {
                    bool result = flag;
                    return result;
                }
                Prefs.j = num3;
                <>c__DisplayClass19_.a = string.Concat(new string[]
                                                       {
                                                           Prefs.h[0],
                                                           Environment.NewLine,
                                                           Prefs.h[1],
                                                           Environment.NewLine,
                                                           Environment.NewLine,
                                                           Prefs.h[2],
                                                           Environment.NewLine,
                                                           Environment.NewLine,
                                                           Prefs.h[5]
                                                       });
            }
            else
            {
                if (flag2 | A_0)
                {
                    bool result = flag;
                    return result;
                }
                Prefs.j = num3;
                if (num3 > 28)
                {
                    <>c__DisplayClass19_.a = Prefs.h[6] + Environment.NewLine + Environment.NewLine + Prefs.h[5];
                }
                else
                {
                    <>c__DisplayClass19_.a = string.Concat(new string[]
                                                           {
                                                               Prefs.h[3],
                                                               (30 - num3).ToString(),
                                                               Prefs.h[4],
                                                               Environment.NewLine,
                                                               Environment.NewLine,
                                                               Prefs.h[5]
                                                           });
                }
            }
            Dispatcher.CurrentDispatcher.BeginInvoke(new Action(<>c__DisplayClass19_.b), Array.Empty<object>());
        }
        catch
        {
        }
        return flag;
    }
    return flag;
}
```

根据代码逻辑只要不进入if (num3 > 19)即可，所以使用Ctrl+E修改变量int num3 = num - num2 >> 8;

![dnSpy2](dnSpy2.png)

修改完毕后保存为dll：

![dnSpy3](dnSpy3.png)

下次安装直接替换dll就可以实现破解了。
