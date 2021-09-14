---
title: 附加到 Program |Microsoft Docs
description: 了解如何Visual Studio程序注册到相应端口后实现附加到程序的调试器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 70576204c655725ea68908424b6caad145cf21f0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600982"
---
# <a name="attach-to-the-program"></a>附加到程序
使用适当的端口注册程序后，必须将调试器附加到要调试的程序。

## <a name="choose-how-to-attach"></a>选择附加
 会话调试管理器有三种方法 (SDM) 附加到正在调试的程序。

1. 对于调试引擎通过[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)方法 (（例如) ）的一般方法启动的程序，SDM 从与要附加到的程序关联的[IDebugProgramNode2 对象获取 IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口。 [](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 如果 SDM 可以获取 `IDebugProgramNodeAttach2` 接口，则 SDM 将调用 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。 `IDebugProgramNodeAttach2::OnAttach`方法返回 `S_OK` 以指示它未附加到程序，并且可以尝试其他附加到程序。

2. 如果 SDM 可以从要附加到的程序获取 [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md) 接口，则 SDM 将调用 [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md) 方法。 对于由端口供应商远程启动的程序，此方法很典型。

3. 如果无法通过 或 方法附加程序，SDM 将加载调试引擎 (如果尚未通过调用) 加载，则调用 `IDebugProgramNodeAttach2::OnAttach` `IDebugProgramEx2::Attach` `CoCreateInstance` [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。 对于端口供应商在本地启动的程序，此方法很典型。

    自定义端口供应商还可以在自定义端口供应商的 方法实现中 `IDebugEngine2::Attach` 调用 `IDebugProgramEx2::Attach` 方法。 通常情况下，自定义端口供应商在远程计算机上启动调试引擎。

   当会话调试管理器调用 Attach 方法时 (SDM) 附件。 [](../../extensibility/debugger/reference/idebugengine2-attach.md)

   如果在要调试的应用程序的同一进程中运行 DE，则必须实现 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)的以下方法：

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  调用 `IDebugEngine2::Attach` 方法后，在 方法的实现中执行 `IDebugEngine2::Attach` 以下步骤：

1. 将 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 事件对象发送到 SDM。 有关详细信息，请参阅 [发送事件](../../extensibility/debugger/sending-events.md)。

2. 对传递给该方法的[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)对象调用[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) `IDebugEngine2::Attach` 方法。

     这会返回 `GUID` 用于标识程序的 。 必须存储在表示 DE 的本地程序的 对象中，并且必须在接口上调用 方法 `GUID` `IDebugProgram2::GetProgramId` 时返回 `IDebugProgram2` 。

    > [!NOTE]
    > 如果实现 `IDebugProgramNodeAttach2` 接口，则程序的 `GUID` 将传递给 `IDebugProgramNodeAttach2::OnAttach` 方法。 `GUID`这用于方法返回 `GUID` 的程序 `IDebugProgram2::GetProgramId` 。

3. 发送 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 事件对象，以通知 SDM 已创建本地对象以将程序 `IDebugProgram2` 表示给 DE。 有关详细信息，请参阅 [发送事件](../../extensibility/debugger/sending-events.md)。

    > [!NOTE]
    > 这不是传递到 `IDebugProgram2` 方法中的同一 `IDebugEngine2::Attach` 对象。 以前传递 `IDebugProgram2` 的对象仅由端口识别，是一个单独的 对象。

## <a name="see-also"></a>另请参阅
- [基于启动的附件](../../extensibility/debugger/launch-based-attachment.md)
- [发送事件](../../extensibility/debugger/sending-events.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)
- [附加](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [附加](../../extensibility/debugger/reference/idebugengine2-attach.md)
