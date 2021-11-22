---
layout: mypost
title: Powershell定时清理回收站
categories: [PowerShell]
---

电脑使用时间久了自然会产生许多的垃圾文件，作为一个程序员当然不用自己去手动清理回收站啦，于是就产生了下面这个脚本。

```powershell
$Days = 14
$Shell = New-Object -ComObject Shell.Application
$Global:Recycler = $Shell.NameSpace(0xa)
foreach ($item in $Recycler.Items()) {
    $DateDel = $Recycler.GetDetailsOf($item, 2) -replace "\u200f|\u200e", "" | get-date
    If ($DateDel -lt (Get-Date).AddDays(-$Days)) { Remove-Item -Path $item.Path -Confirm:$false -Force -Recurse }
}
```

代码很简单就不做过多解释了，然后再添加到任务计划中，每天用户登录时启动一次就好。

Happy PowerShelling!