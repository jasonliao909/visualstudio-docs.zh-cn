---
title: 如何：使用活动日志|Microsoft Docs
description: VSPackage 可以将消息写入活动日志。 了解如何使用活动日志在零售环境中调试 VSPackage。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7687d9174b9275cce791f39c05d41450e1687df7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600767"
---
# <a name="how-to-use-the-activity-log"></a>如何：使用活动日志
VSPackage 可以将消息写入活动日志。 此功能对于在零售环境中调试 VSPackage 特别有用。

> [!TIP]
> 活动日志始终打开。 Visual Studio最后 100 个条目以及具有常规配置信息的前 10 个条目的滚动缓冲区。

## <a name="to-write-an-entry-to-the-activity-log"></a>将条目写入活动日志

1. 在 方法中或在除 VSPackage 构造函数以外的任何其他方法中插入 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 此代码：

    ```csharp
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log == null) return;

    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,
        this.ToString(),
        string.Format(CultureInfo.CurrentCulture,
        "Called for: {0}", this.ToString()));
    ```

     此代码获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> 服务，并强制转换到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> 接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> 使用当前文化上下文将信息性条目写入活动日志。

2. 当 VSPackage 加载 (调用命令或打开窗口时，) 文本写入活动日志。

## <a name="to-examine-the-activity-log"></a>检查活动日志

1. 使用Visual Studio [/Log](../ide/reference/log-devenv-exe.md)命令行开关运行 ActivityLog.xml，以在会话期间将磁盘写入磁盘。

2. 关闭Visual Studio，在子文件夹查找活动日志，Visual Studio数据：

   <em> *%AppData%</em>\Microsoft\VisualStudio \\ \<version>\ActivityLog.xml*。

3. 使用任意文本编辑器打开活动日志。 下面是一个典型条目：

   ```
   Called for: Company.MyApp.MyAppPackage ...
   ```

## <a name="robust-programming"></a>可靠编程

由于活动日志是服务，因此活动日志在 VSPackage 构造函数中不可用。

在写入活动日志之前，应获取活动日志。 不要缓存或保存活动日志供将来使用。

## <a name="see-also"></a>另请参阅

- [/Log (devenv.exe) ](../ide/reference/log-devenv-exe.md)
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>
- <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>
- [VSPackages 故障排除](../extensibility/troubleshooting-vspackages.md)
- [VSPackages](../extensibility/internals/vspackages.md)
