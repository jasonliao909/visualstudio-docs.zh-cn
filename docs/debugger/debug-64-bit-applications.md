---
title: 调试 64 位应用程序 | Microsoft Docs
description: 了解如何使用 Visual Studio 调试 64 位应用程序。 有一些用于排查意外调试延迟的提示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], 64-bit
- 64-bit debugging
ms.assetid: db648e5f-6375-4e2d-aa98-eb7261958927
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: dc3a841d97b3479eb30d26d66608827e1a771d20
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122066819"
---
# <a name="debug-64-bit-applications"></a>调试 64 位应用程序
您可以调试运行于本地计算机或远程计算机上的 64 位应用程序。

 若要调试在远程计算机上运行的 64 位应用程序，请参阅[远程调试](../debugger/remote-debugging.md)。

 若要在本地调试 64 位应用程序，Visual Studio 将使用 64 位辅助进程 (msvsmon.exe) 执行不能在 32 位 Visual Studio 进程内执行的低级别操作。

 使用 .NET Framework 3.5 或更早版本的 64 位进程不支持混合模式调试。

## <a name="debug-a-64-bit-application"></a>调试 64 位应用程序
 若要尝试调试 64 位应用程序：

1. 创建一个 Visual Studio 解决方案，例如 C# 控制台应用程序。

2. 使用配置管理器将配置设置为 64 位。 有关详细信息，请参阅[如何：将项目配置为面向平台](../ide/how-to-configure-projects-to-target-platforms.md)。

3. 此时将启动 64 位版本的远程调试器 (msvsmon.exe)。 只要具有 64 位配置的解决方案处于启用状态，它就会运行。

4. 开始调试。 此体验应该与调试 32 位配置的应用程序的体验相同。 如果出现错误，请参阅下面的“疑难解答”一节。

## <a name="troubleshooting-64-bit-debugging"></a>64 位调试疑难解答
 可能会出现错误：“64 位调试操作花费的时间比预期要长。” 在这种情况下，则说明 Visual Studio 已向 64 位版本的 msvsmon.exe 发送请求，返回该请求的结果花费了较长的时间。

 出现此错误的主要原因有两个：

- 你的计算机上所安装的网络安全软件导致网络堆栈不可靠，并且该网络安全软件已删除通过 localhost 的数据包。 请尝试禁用全部的网络安全软件，然后查看该问题是否解决。 如果问题解决，那么请发送报告给你的网络安全软件供应商，说明该软件正在干扰 localhost 通信。

- 你遇到了 Visual Studio 无响应或其他性能问题。 如果该问题定期发生，你可收集 Visual Studio (devenv.exe) 和辅助进程 (msvsmon.exe) 的转储并将其发送给 Microsoft。 有关报告问题的详细信息，请参阅 [How to Report a Problem with Visual Studio](../ide/how-to-report-a-problem-with-visual-studio.md)。

## <a name="see-also"></a>请参阅

- [64 位应用程序](/dotnet/framework/64-bit-apps)
- [配置 64 位的程序](/cpp/build/configuring-programs-for-64-bit-visual-cpp)
- [Visual Studio IDE 64 位支持](../ide/visual-studio-ide-64-bit-support.md)
- [使用转储文件](../debugger/using-dump-files.md)
- [远程调试](../debugger/remote-debugging.md)