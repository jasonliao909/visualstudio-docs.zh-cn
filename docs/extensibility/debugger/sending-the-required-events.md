---
title: 发送所需的事件|Microsoft Docs
description: 了解创建调试引擎并将其附加到调试过程中的程序时所需的有序Visual Studio事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b04ca7ed68b975bc68fa509cdc75dc507b9603d6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902262"
---
# <a name="send-the-required-events"></a>发送所需的事件
使用此过程发送所需的事件。

## <a name="process-for-sending-required-events"></a>发送所需事件的过程
 在 DE 中创建调试引擎并将其附加到程序时 (需要) 事件：

1. 初始化 DE 以调试进程中的一个或多个程序时，将 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 事件对象发送到会话调试管理器 (SDM) 。

2. 当要调试的程序附加到时，将 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 事件对象发送到 SDM。 此事件可能是停止事件，具体取决于引擎设计。

3. 如果程序在进程启动时附加到 ，请将 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 事件对象发送到 SDM，以通知 IDE 新线程。 此事件可能是停止事件，具体取决于引擎设计。

4. 当正在调试的程序完成加载或附加到程序完成时，将 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 事件对象发送到 SDM。 此事件必须是停止事件。

5. 如果要调试的应用程序已启动，则当即将执行运行时体系结构中的第一个代码指令时，将 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 事件对象发送到 SDM。 此事件始终是停止事件。 单步执行调试会话时，IDE 在此事件上停止。

> [!NOTE]
> 许多语言使用全局初始值设置程序或外部预编译 (CRT 库或_Main) 代码开头的代码。 如果要调试的程序的语言在初始入口点之前包含这些类型的元素之一，则此代码将运行，并且当到达用户入口点（如 **main** 或 ）时，将发送入口点 `WinMain` 事件。

## <a name="see-also"></a>另请参阅
- [启用要调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
