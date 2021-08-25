---
title: Output | Microsoft Docs
description: 了解“Output”选项如何指定用于性能会话的分析数据文件的名称。 “Output”必须与“Start”选项配合使用。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5e286e61-4548-42cf-a635-e608c5edbe2b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c521362ecde12a5b996062f6f1e0d07992e26e06
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122107103"
---
# <a name="output"></a>输出
“Output”选项指定用于性能会话的分析数据文件的名称。 “Output”必须与“Start”选项配合使用。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName [Options]
```

#### <a name="parameters"></a>参数
 `FileName` 数据文件的名称。 接受完整和部分路径。 如果未指定路径，则在当前目录中创建该文件。

## <a name="required-options"></a>必需选项
 “Output”选项必须与“Start”选项一起使用。

 **Start:** `Method` 指定输出文件名。

## <a name="example"></a>示例
 在下例中，分析数据文件是在当前目录中创建的。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
