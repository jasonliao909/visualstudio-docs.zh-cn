---
title: 通知端口|Microsoft Docs
description: 了解启动程序后如何通知端口。 本文包含详细说明。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1aaa319f0c6cd545e1f319ab7c8c510f694529d7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664856"
---
# <a name="notify-the-port"></a>通知端口
启动程序后，必须通知端口，如下所示：

1. 当端口收到新的程序节点时，它会将程序创建事件发送回调试会话。 事件带有一个表示程序的接口。

2. 调试会话在程序中查询调试引擎的标识符 (DE) 可附加到。

3. 调试会话检查 DE 是否位于该程序的允许的 DES 列表中。 调试会话从解决方案的活动程序设置（最初由调试包传递给它）获取此列表。

    DE 必须位于允许列表中，否则 DE 不会附加到程序。

   以编程方式，当端口首次接收新的程序节点时，它会创建一个 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 接口来表示程序。

> [!NOTE]
> 这不应与调试引擎稍后在 DE (`IDebugProgram2` 创建的接口) 。

 端口通过 COM 接口将 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 程序创建事件发送回会话调试管理器 (SDM `IConnectionPoint`) 。

> [!NOTE]
> 这不应与 接口混淆 `IDebugProgramCreateEvent2` ，该接口稍后由 DE 发送。

 除了事件接口本身，端口还发送[IDebugPort2、IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)和[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)接口，这些接口分别表示端口、进程和程序。 [](../../extensibility/debugger/reference/idebugport2.md) SDM 调用 [IDebugProgram2：：GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) 获取可调试程序的 DE 的 GUID。 GUID 最初从 [IDebugProgramNode2 接口](../../extensibility/debugger/reference/idebugprogramnode2.md) 获取。

 SDM 检查 DE 是否位于允许的 DES 列表中。 SDM 从解决方案的活动程序设置（最初由调试包传递给它）获取此列表。 DE 必须位于允许列表中，否则不会附加到程序。

 知道 DE 的标识后，SDM 即可将其附加到程序。

## <a name="see-also"></a>另请参阅
- [启动程序](../../extensibility/debugger/launching-a-program.md)
- [启动后附加](../../extensibility/debugger/attaching-after-a-launch.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
