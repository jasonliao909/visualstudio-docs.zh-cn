---
title: LineOff | Microsoft Docs
description: 了解使用 VSPerfCmd 启动应用程序时，VSPerfCmd 的“LineOff”选项如何禁止收集行号数据。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 76082063-20ef-47ae-ad64-81b43b654865
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 89b9217460e7f64fb085d674486583bf424e6b1c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641512"
---
# <a name="lineoff"></a>LineOff
默认情况下，使用采样分析方法时，探查器将收集源代码行号和行号偏移量数据。 使用 VSPerfCmd 启动应用程序时，VSPerfCmd 的“LineOff”选项会禁止收集行号数据。 指定“LineOff”后，将在函数级别收集分析数据。

 只能将“LineOff”与“Launch”选项一起使用，且只有在使用 Start:Sample 选项将探查器初始化为采样后才能这样使用。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Launch:AppName /LineOff [Options]
```

#### <a name="parameters"></a>参数
 None

## <a name="required-options"></a>必需选项
 只能在包含“Launch”选项的命令行上使用“LineOff”选项。

 **Launch:** `AppName` 启动指定的应用程序并开始使用采样方法进行分析。

## <a name="example"></a>示例
 此示例启动应用程序和探查器，并禁止行级采样。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /LineOff
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
