---
title: TargetCLR | Microsoft Docs
description: 了解“TargetCLR”选项如何指定应用程序中加载 CLR 的多个版本时要分析的公共语言运行时 (CLR) 的版本。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f9732480-287f-40f1-a4ff-b112e143b940
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 083f650992a931686e49d878df1e2c323bd45f3d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735671"
---
# <a name="targetclr"></a>TargetCLR
“TargetCLR”选项指定应用程序中加载 CLR 的多个版本时要分析的公共语言运行时 (CLR) 的版本。

 默认情况下，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具以应用程序加载的第一个 CLR 版本为目标。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe {/Launch:AppName | /Attach:PID} /TargetCLR[:ClrVersion] [Options]
```

#### <a name="parameters"></a>参数
 `ClrVersion` CLR 的版本号。 使用版本格式 vN.N.NNNNN。

## <a name="required-options"></a>必需选项
 “TargetCLR”选项只能与“启动”或“附加”选项一起使用。

 **Launch:** `AppName` 启动指定的应用程序并开始分析。

 **Attach：** `PID` 开始分析指定的进程。

## <a name="example"></a>示例
 在此示例中，使用 TargetCLR 选项以确保分析 CLR 版本 4.0.11003。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /TargetCLR:v4.0.11003
```
