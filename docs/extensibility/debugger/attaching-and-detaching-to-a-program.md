---
title: 附加和分离到程序|Microsoft Docs
description: 了解如何使用用于附加调试器的适当属性发送正确的方法和事件序列。
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
ms.openlocfilehash: 678b2a3582eef3b803a838728a43a7e1444de064b3e29778fd5f077ab7c386f7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121324153"
---
# <a name="attaching-and-detaching-to-a-program"></a>附加和分离到程序
附加调试器需要发送具有正确属性的正确方法和事件序列。

## <a name="sequence-of-methods-and-events"></a>方法和事件的顺序

1. 会话调试管理器 (SDM) [调用 OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。

    根据调试引擎 (DE) 模型，该方法返回以下方法之一，该方法确定 `IDebugProgramNodeAttach2::OnAttach` 接下来会发生什么。

    如果 `S_FALSE` 返回 ，则调试引擎已成功附加到程序。 否则，将调用 [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) 方法以完成附加过程。

    如果 `S_OK` 返回 ，则 DE 将加载到与 SDM 相同的进程中。 SDM 执行以下任务：

   1. 调用 [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) 获取 DE 的引擎信息。

   2. 共同创建 DE。

   3. 调用 [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)。

2. DE 使用 属性 [将 IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 发送到 `EVENT_SYNC` SDM。

3. DE 使用 属性将 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 发送到 `EVENT_SYNC` SDM。

4. DE 使用 属性将 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 发送到 `EVENT_SYNC_STOP` SDM。

   从程序分离是一个简单的两步过程，如下所示：

5. SDM 调用 [Detach](../../extensibility/debugger/reference/idebugprogram2-detach.md)。

6. DE 发送 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
