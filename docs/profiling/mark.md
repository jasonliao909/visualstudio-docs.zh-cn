---
title: 标记 | Microsoft Docs
description: 了解 VSPerfCmd.exe“Mark”选项如何在分析数据文件中插入指定的信息。
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 1d72cef3-bb09-4bbb-8864-6ea0ab623ff9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 3e37a739d5e6c799cbeaca0ddb5802be3a0a535b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736175"
---
# <a name="mark"></a>标记
VSPerfCmd.exe 的“标记”选项可以在分析数据文件中插入指定的信息 。 标记可能列在单独的 VSPerfReport 报表中或探查器 UI 的“标记报表”视图中。 标记可用于指定报表和视图筛选器中的起止点。

 “标记”选项是命令行上可指定的唯一选项。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Mark:MarkID,[MarkName]
```

#### <a name="parameters"></a>参数
 `MarkID` 用户定义的整数，在探查器视图和报表中列为标记 ID。 `MarkID` 不必是唯一的值。

 `MarkName` （可选）用户定义的字符串，在探查器视图和报告中作为标记名称列出。 如果未指定 `MarkName`，则标记列表中的“标记名称”字段为空。 需将包含空格或正斜杠（“/”）的字符串用引号引起来。

## <a name="example"></a>示例
 此示例插入了一个 ID 为 123、名称为“TestMark”的标记。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
VSPerfCmd.exe /Mark:123,TestMark
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
