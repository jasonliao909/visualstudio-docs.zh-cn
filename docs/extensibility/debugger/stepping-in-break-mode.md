---
title: 中断模式下的单步执行 |Microsoft Docs
description: 了解调试器处于中断模式时所发生的过程。 然后，调试器必须单步调试代码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0ed11d05e4351ac6ba76bc9aa10531a8a96ddf23
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075401"
---
# <a name="stepping-in-break-mode"></a>中断模式下的单步执行
以下部分介绍调试器处于中断模式下时所发生的过程，并且必须单步执行代码：

## <a name="stepping-process"></a>单步执行过程

1. 调用 [IDebugProgram2：： Step](../../extensibility/debugger/reference/idebugprogram2-step.md) ，并使用 [STEPKIND](../../extensibility/debugger/reference/stepkind.md) 和 [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) 参数执行步骤。

2. 步骤完成后，发送 [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) 作为停止事件。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
