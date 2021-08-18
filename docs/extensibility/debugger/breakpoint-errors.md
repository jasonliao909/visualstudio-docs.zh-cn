---
title: 断点错误|Microsoft Docs
description: 了解断点尝试绑定到代码但失败时的过程，以及如何排查断点错误。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2c38817ce41131c936138078f0dc8787854a4116
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051048"
---
# <a name="breakpoint-errors"></a>断点错误
下面描述了断点尝试绑定到代码但失败时的过程。

## <a name="troubleshoot-a-breakpoint-error"></a>排查断点错误

1. 调试引擎 (DE) 将 [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) 发送到会话调试管理器 (SDM) 。

2. SDM 调用 [IDebugBreakpointErrorEvent2：：GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2**) 获取 `ppErrorBP` 错误断点。

3. SDM 调用 [IDebugErrorBreakpoint2：：GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md) 获取错误断点源自的挂起断点。

4. SDM 调用 [IDebugErrorBreakpoint2：：GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) 获取错误断点无法绑定的原因。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
