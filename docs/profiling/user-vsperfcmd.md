---
title: User (VSPerfCmd) | Microsoft Docs
description: 了解“User”选项如何指定拥有被分析进程的帐户的域和用户名。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ee1a478e-374d-4f30-ae28-d260b9d4723a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 015cca1c11050f2bd34fa5b6eb8292b014b61856
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122140787"
---
# <a name="user-vsperfcmd"></a>User (VSPerfCmd)
**User** 选项指定拥有被分析进程的帐户的域和用户名。 仅在进程以已登录用户外的用户身份运行时才需要此选项。 进程所有者在 Windows 任务管理器的“进程”选项卡上的“用户名”列中列出。

 只能在包含 **Start** 选项的命令行上指定 **User** 选项。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName /User:[Domain\]UserName [Options]
```

#### <a name="parameters"></a>参数
 `Domain` 用户域的名称。

 `UserName` 用户的名称。

## <a name="required-options"></a>必需选项
 **User** 选项只能与 **Start** 选项一起使用。

 **Start：** `Method` 将探查器初始化为指定的分析方法。

## <a name="example"></a>示例
 下面的示例演示 **User** 选项的用法。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /User:SYSTEM
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
