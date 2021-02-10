---
title: 控制台 | Microsoft Docs
description: 使用 VSPerfCmd.exe 的“Console”选项在新的命令提示符窗口中启动指定的应用程序。 必须将它与“Launch”选项一起使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: e825ba66-1383-46ad-8712-396bc9c14036
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 242a5234c2b7368a992676e12ecbdcd5ea36219f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955406"
---
# <a name="console"></a>控制台
VSPerfCmd.exe“Console”选项在新的命令提示符窗口中启动指定的应用程序。 “Console”只能与 VSPerfCmd“Launch”选项一起使用。 如果应用程序不是命令行应用程序，“Console”不起作用。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Launch:AppName /Console
```

#### <a name="parameters"></a>参数
 None

## <a name="required-options"></a>必需选项
 只能在同时包含“Launch”选项的命令行上指定“Console”。

 **Launch:** `AppName` 启动探查器以及由 `AppName` 指定的应用程序。

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
