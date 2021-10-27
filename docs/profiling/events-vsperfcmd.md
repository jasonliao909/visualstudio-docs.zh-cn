---
title: Events (VSPerfCmd) | Microsoft Docs
description: 使用 VSPerfCmd.exe 命令行工具中的“事件”选项控制 Windows 事件跟踪 (ETW) 日志记录。 查看语法参数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: eb139327-4783-4f2a-874c-efad377a7be4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 268efb7e76ea4b2357b0ef1047ee2076f340dc29
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735494"
---
# <a name="events-vsperfcmd"></a>Events (VSPerfCmd)
VSPerfCmd.exe“Events”选项控制 Windows 事件跟踪 (ETW) 日志记录 。 会将 ETW 数据保存到独立于探查器数据文件的 .etl 文件中。 可以使用 [VSPerfReport](../profiling/vsperfreport.md) /summary:etw 命令在报告中查看这些数据。

 在调用 VSPerfCmd Shutdown 命令停止分析之前，可以随时调用“Events”选项。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /events {On|Off} {Guid|ProviderName} [,Flags[,Level]
```

#### <a name="parameters"></a>参数
 **On**&#124;**Off** 开始或停止收集事件数据。

 `Guid` 提供程序控件的 GUID。

 `ProviderName` 向 Windows Management Instrumentation (WMI) 注册的提供程序的名称。

 `Flags` 以“0x”为前缀的十六进制标志值，由事件提供程序定义。

 `Level` 指定收集的数据量。 `Level` 由事件提供程序定义。

 “Events”选项将以下内核关键字识别为提供程序名称：

 **Process** 进程事件

 **Thread** 线程事件

 **Image** 映像加载和卸载事件

 **Disk** 磁盘 I/O 事件

 **File** 文件 I/O 事件

 **Hardfault** 硬页面错误

 **Pagefault** 软页错误

 **Network** 网络事件

 **Registry** 注册表访问事件

 请注意，内核提供程序只能处于启用状态。 在监视器关闭之前，既不能禁用它，也不能修改它的标志。

## <a name="remarks"></a>备注

> [!NOTE]
> 启用 CLR ETW 事件后，跟踪视图报告中还将收集额外的启动数据。 若要将启动事件从报告中排除，请使用以下命令：

```cmd
C:\<path>VSPerfCmd -events on, \".NET Common Language Runtime\", 0x7fffffff, 5
```

> [!IMPORTANT]
> 如果不排除启动事件，则由于这些事件未在托管对象格式 (MOF) 文件中列出，它们将在报告中显示为 GUID。 有关详细信息，请参阅 Microsoft 网站上的此页面：[托管对象格式 (MOF) 文件示例](https://msdn.microsoft.com/library/default.aspx)。

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
