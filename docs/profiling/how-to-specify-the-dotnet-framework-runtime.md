---
title: 指定 .NET Framework 运行时 | Microsoft Docs
description: 了解应用程序如何由使用不同的 .NET Framework 运行时版本生成的模块构成。
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Profiling Tools, .NET Framework versions
- .NET Framework versions,profililng
ms.assetid: d39f3579-719a-4f47-a97d-5b4232fe4c64
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 3c4a102e7d18f7a580cb012f46e9a5c737106d2a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735468"
---
# <a name="how-to-specify-the-net-framework-runtime"></a>如何：指定 .NET Framework 运行时

.NET Framework 4 发布后，应用程序可以由使用不同的 .NET Framework 运行时版本生成的模块构成。 默认情况下，Visual Studio 分析工具会分析应用程序加载的第一个运行时。 用探查器启动应用程序时，以及将探查器附加到已在运行的应用程序时，可以指定要分析的运行时。

## <a name="to-specify-the-net-framework-run-time-to-profile-when-starting-an-application-with-the-profiler"></a>用探查器启动应用程序时指定要分析的 .NET Framework 运行时

1. 在“性能资源管理器”中，右键单击性能会话，单击“属性”，然后单击“高级”。

     “目标 CLR 版本”列表框显示“自动”以及计算机上安装的 .NET Framework 运行时版本 。

2. 执行以下步骤之一：

    - 单击要分析的 CLR 版本。

    - 单击“自动”分析应用程序加载的第一个版本。

## <a name="to-specify-the-net-framework-run-time-to-profile-when-attaching-the-profiler-to-an-application"></a>将探查器附加到应用程序时指定要分析的 .NET Framework 运行时

1. 在“分析”菜单上，指向“探查器”，然后单击“附加/分离”  。

2. 在“将探查器附加到进程”对话框中，单击要分析的进程。

     “目标 CLR 版本”列表框显示“自动”以及计算机上安装的 .NET Framework 运行时版本 。

3. 执行以下步骤之一：

    - 单击要分析的 CLR 版本。

    - 单击“自动”分析探查器附加到应用程序时加载的版本。
