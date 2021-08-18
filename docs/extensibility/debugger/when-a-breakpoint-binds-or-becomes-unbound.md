---
title: 断点绑定或变为未绑定|Microsoft Docs
description: 了解未绑定断点。 当在调用时无法绑定断点时，断点的绑定时间和创建时间会有所不同。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 6ffceee9c4f4ae79548e9ed1622a03a2240d9fcaba35e35a7f2aae10446f2071
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448437"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>断点绑定或变为未绑定时
当在调用 [IDebugPendingBreakpoint2：：CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md) 方法时无法绑定断点时，断点的绑定时间和创建时间会有所不同。

## <a name="methods-called"></a>调用的方法
 SDM (会话) 调用以下方法：

1. [IDebugEngine2：：CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE 返回 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)。

2. [IDebugPendingBreakpoint2：：Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。

3. [IDebugPendingBreakpoint2：：Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)。

4. [IDebugPendingBreakpoint2：：Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)方法并返回S_OK。 DE 发送 [IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) 或 [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)。

5. [IDebugBreakpointBoundEvent2：：GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) 和 [IDebugBreakpointBoundEvent2：：EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) 方法，用于验证和获取绑定断点。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
