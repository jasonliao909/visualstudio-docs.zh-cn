---
title: 启动后附加|Microsoft Docs
description: 程序启动时，调试会话已准备好将调试引擎附加到程序。 选择用于与调试引擎通信的设计方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 01043ad1f04ddb36acc50ac0d3a36247e8461a23e420ef70366f4625506ee4e5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452545"
---
# <a name="attach-after-a-launch"></a>启动后附加
程序启动后，调试会话已准备好将调试引擎附加到 (DE) 程序。

## <a name="design-decisions"></a>设计决策
 由于共享地址空间中的通信更容易，因此必须在两种设计方法之间选择：在调试会话和 DE 之间设置通信。 或者，设置 DE 与程序之间的通信。 在下列选项之间选择：

- 如果设置调试会话与 DE 之间的通信更合理，则调试会话将共同创建 DE 并要求 DE 附加到程序。 此设计将调试会话和 DE 一起放在一个地址空间中，将运行时环境和程序一起放在另一个地址空间中。

- 如果设置 DE 与程序之间的通信更合理，则运行时环境将共同创建 DE。 此设计将 SDM 保留为一个地址空间，将 DE、运行时环境以及程序一起放在另一个地址空间中。 此设计是 DE 的典型设计，该 DE 通过解释器实现，用于运行脚本化语言。

    > [!NOTE]
    > DE 如何附加到程序取决于实现。 DE 与程序之间的通信也依赖于实现。

## <a name="implementation"></a>实现
 以编程方式，当会话调试管理器 (SDM) 首先接收表示要启动的程序的 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 对象时，它会调用 [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) 方法，并将 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) 对象传递给该对象，该对象稍后用于将调试事件传递回 SDM。 然后 `IDebugProgram2::Attach` ， 方法调用 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。 有关 SDM 如何接收接口的信息 `IDebugProgram2` ，请参阅 [通知端口](../../extensibility/debugger/notifying-the-port.md)。

 如果 DE 需要在与正在调试的程序相同的地址空间中运行：因为 DE 通常是运行脚本解释器的一部分，所以 `IDebugProgramNodeAttach2::OnAttach` 该方法返回 `S_FALSE` 。 `S_FALSE`返回指示它已完成附加过程。

 但是，如果 DE 在 SDM 的地址空间中运行：方法返回 ，或者 `IDebugProgramNodeAttach2::OnAttach` `S_OK` [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 接口在与正在调试的程序关联的 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 对象上未实现。 在这种情况下， [最终调用 Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) 方法以完成附加操作。

 在后一种情况下，必须对传递给 方法的对象调用 [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) 方法，将 存储在本地程序对象中，然后在此对象上调用该方法时返回 `IDebugProgram2` `IDebugEngine2::Attach` `GUID` `GUID` `IDebugProgram2::GetProgramId` 此方法。 `GUID`用于跨各种调试组件唯一标识程序。

 在返回 的方法中，用于程序的 将传递给该方法，它是在本地程序对象上 `IDebugProgramNodeAttach2::OnAttach` `S_FALSE` 设置 `GUID` `IDebugProgramNodeAttach2::OnAttach` `GUID` 的方法。

 DE 现已附加到程序，并准备好发送任何启动事件。

## <a name="see-also"></a>另请参阅
- [直接附加到程序](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [通知端口](../../extensibility/debugger/notifying-the-port.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [附加](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)
