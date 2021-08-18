---
title: 基于启动的附件|Microsoft Docs
description: 了解程序基于启动的附件，该程序是自动的，并遵循与手动附件类似的路径。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: f3839c1edb8b8406e5b5ae0645205f0316b88d62
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122065158"
---
# <a name="launch-based-attachment"></a>基于启动的附件
程序的基于启动的附件是自动的。 当托管程序的进程由 SDM 启动时，基于启动的附件将遵循类似于手动附件方法的路径。 有关信息，请参阅 [附加到程序](../../extensibility/debugger/attaching-to-the-program.md)。

## <a name="the-attaching-process"></a>附加过程
 主要区别在于 Attach 调用后 **的事件序列，** 如下所示：

1. 将 **IDebugEngineCreateEvent2** 事件对象发送到 SDM。 有关详细信息，请参阅 [发送事件](../../extensibility/debugger/sending-events.md)。

2. 在传递给 Attach 方法的 `IDebugProgram2::GetProgramId` **IDebugProgram2** 接口上调用 方法。

3. 发送 **IDebugProgramCreateEvent2** 事件对象以通知 SDM 已创建本地 **IDebugProgram2** 对象，以将程序表示给 DE。

4. 发送 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 事件对象以通知 SDM 为启动的进程创建了一个新线程。

## <a name="see-also"></a>请参阅
- [发送所需的事件](../../extensibility/debugger/sending-the-required-events.md)
- [启用要调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
