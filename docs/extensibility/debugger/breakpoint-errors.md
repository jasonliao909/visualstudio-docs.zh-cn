---
title: 断点错误 |Microsoft Docs
description: 了解断点尝试绑定到代码但失败以及如何解决断点错误的过程。
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
ms.workload:
- vssdk
ms.openlocfilehash: 12e8efc7fc110f3f5c20c92d97cf3692094ef6aa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055228"
---
# <a name="breakpoint-errors"></a>断点错误
下面描述了当断点尝试绑定到代码但失败时的过程。

## <a name="troubleshoot-a-breakpoint-error"></a>解决断点错误

1. 调试引擎 (DE) 将 [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) 发送到会话调试管理器 (SDM) 。

2. SDM 调用 [IDebugBreakpointErrorEvent2：： GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2 * * `ppErrorBP`) 以获取错误断点。

3. SDM 调用 [IDebugErrorBreakpoint2：： GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md) 以获取从中发出错误断点的挂起断点。

4. SDM 调用 [IDebugErrorBreakpoint2：： GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) 以获取错误断点绑定失败的原因。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
