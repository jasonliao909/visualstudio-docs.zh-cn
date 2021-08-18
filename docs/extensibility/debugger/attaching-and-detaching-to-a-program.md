---
title: 附加和分离程序 |Microsoft Docs
description: 了解如何发送正确的方法和事件顺序以及用于附加调试器的正确属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
- debug engines, detaching from programs
ms.assetid: 79dcbb9b-c7f8-40fc-8a00-f37fe1934f51
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1c4fa3240e5d2226b43e656bf2007dad9e21219a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051087"
---
# <a name="attaching-and-detaching-to-a-program"></a>附加和分离程序
附加调试器要求发送正确的方法和具有正确特性的事件的序列。

## <a name="sequence-of-methods-and-events"></a>方法和事件的序列

1. 会话调试管理器 (SDM) 调用 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。

    根据调试引擎 (DE) 进程模型，该方法将 `IDebugProgramNodeAttach2::OnAttach` 返回以下方法之一，该方法决定接下来会发生的情况。

    如果 `S_FALSE` 返回，则调试引擎已成功附加到该程序。 否则，将调用 [attach](../../extensibility/debugger/reference/idebugengine2-attach.md) 方法来完成附加过程。

    如果 `S_OK` 返回，则将在与 SDM 相同的进程中加载 DE。 SDM 执行以下任务：

   1. 调用 [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) 以获取 DE 的引擎信息。

   2. 共同创建 DE。

   3. 调用 [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)。

2. DE 使用特性向 SDM 发送 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) `EVENT_SYNC` 。

3. DE 使用特性向 SDM 发送 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) `EVENT_SYNC` 。

4. DE 使用特性向 SDM 发送 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) `EVENT_SYNC_STOP` 。

   从程序分离是一个简单的两步过程，如下所示：

5. SDM 调用 [分离](../../extensibility/debugger/reference/idebugprogram2-detach.md)。

6. DE 发送 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
