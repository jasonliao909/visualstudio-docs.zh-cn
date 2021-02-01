---
title: 关闭 | Microsoft Docs
description: 了解“关闭”选项如何等待任何当前分析的进程结束或分离，然后关闭探查器和分析数据文件。
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: a1e37500-4ad1-4670-9737-3d9a20536386
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c7a0bf796c91ce339c82f7f698ed63afe90f9c1c
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720067"
---
# <a name="shutdown"></a>Shutdown
“关闭”选项会等待任何当前分析的进程结束或分离，然后关闭探查器和分析数据文件。 “关闭”选项必须是分析运行的最后一个命令。

 如果没有指定超时参数，则“关闭”选项将无限期等待。 如果指定了超时参数，则此选项将在指定的秒数后返回，而不会关闭探查器或数据文件。

 “关闭”选项必须是命令行中指定的唯一选项。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Shutdown[:Timeout]
```

#### <a name="parameters"></a>参数
`Timeout`
- （可选）如果指定，则此选项将在指定的秒数后返回，而不会关闭探查器或分析数据文件。

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
