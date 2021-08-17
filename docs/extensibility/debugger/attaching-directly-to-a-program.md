---
title: 直接附加到程序 |Microsoft Docs
description: 了解 Visual Studio 如何实现使用 Visual Studio IDE 中的此过程将调试引擎附加到已在运行的进程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 6645b02a5ab842309b54a6c1d4a7f36519b018a8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073417"
---
# <a name="attach-directly-to-a-program"></a>直接附加到程序
如果用户想要在已运行的进程中调试程序，则通常执行以下过程：

1. 在 IDE 中，从 "**工具**" 菜单中选择 "**调试进程**" 命令。

    这将显示“进程”  对话框。

2. 选择一个进程，然后单击 " **附加** " 按钮。

    此时将显示 " **附加到进程** " 对话框，其中列出了计算机上 (DEs) 的所有调试引擎。

3. 指定用于调试所选进程的 DEs，然后单击 **"确定"**。

   调试包将启动调试会话，并将 DEs 的列表传递给它。 然后，调试会话会将此列表与回调函数一起传递到选定的进程，然后要求进程枚举其正在运行的程序。

   以编程方式为响应用户请求，调试包将会话调试管理器实例化 (SDM) 并将所选 DEs 的列表传递给它。 除了列表，调试包还将 SDM 传递到 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) 接口。 调试包通过调用 [IDebugProcess2：： Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)将 DEs 列表传递到选定的进程。 然后，SDM 调用端口上的 [IDebugProcess2：： EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) 来枚举进程中运行的程序。

   从此时开始，每个调试引擎都附加到程序中，这与 [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)的详细信息完全相同，但有两个例外。

   为提高效率，为与 SDM 共享地址空间而实现的 DEs 进行了分组，以便每个 DE 都具有一组要附加到的程序。 在这种情况下， [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) 调用 [IDebugEngine2：： Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) ，并向其传递要附加到的程序数组。

   第二个例外是，通过附加到已在运行的程序而发送的启动事件通常不包括入口点事件。

## <a name="see-also"></a>请参阅
- [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
