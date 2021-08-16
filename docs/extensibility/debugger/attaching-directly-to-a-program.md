---
title: 直接附加到程序|Microsoft Docs
description: 了解如何Visual Studio IDE 中的过程将调试引擎附加到已在Visual Studio的进程。
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
ms.openlocfilehash: 189a5e56e189240b014249e7e4b980bf3e8cce034c3647b59711d7a6ae2e84e1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403354"
---
# <a name="attach-directly-to-a-program"></a>直接附加到程序
想要在已运行的进程中调试程序的用户通常遵循此过程：

1. 在 IDE 中，从"工具 **"** 菜单中选择"调试 **进程"** 命令。

    这将显示“进程”  对话框。

2. 选择一个进程，然后单击" **附加"** 按钮。

    将出现 **"附加到进程"** 对话框，列出 (计算机上安装) ES 的所有调试引擎。

3. 指定用于调试所选进程的 ES，然后单击"确定 **"。**

   调试包启动调试会话，并传递 ES 列表。 调试会话反过来将此列表以及回调函数传递给所选进程，然后要求进程枚举其正在运行的程序。

   在以编程方式响应用户请求时，调试包会实例化会话调试管理器 (SDM) ，并传递所选 ES 的列表。 调试包连同列表一起向 SDM 传递 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) 接口。 调试包通过调用 [IDebugProcess2：：Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)将 ES 列表传递给所选进程。 然后，SDM 在端口上调用 [IDebugProcess2：：EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) 以枚举进程中运行的程序。

   从此时开始，每个调试引擎都完全按照启动后附加中详述的附加到[](../../extensibility/debugger/attaching-after-a-launch.md)程序，但两个例外。

   为了提高效率，为与 SDM 共享地址空间而实现的 DES 已分组，以便每个 DE 都有一组要附加到的程序。 在这种情况下 [，IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) 调用 [IDebugEngine2：：Attach，](../../extensibility/debugger/reference/idebugengine2-attach.md) 并将要附加到的程序数组传递给它。

   第二个例外是，附加到已运行的程序的 DE 发送的启动事件通常不包括入口点事件。

## <a name="see-also"></a>另请参阅
- [启动后发送启动事件](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
