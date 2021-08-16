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
ms.openlocfilehash: 592441e057e5b726f6fb474bf4dae66365203d73a64eb569b6e785ac1d1f2d48
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403341"
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
