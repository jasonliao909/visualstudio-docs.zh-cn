---
title: 在中断模式下单步执行|Microsoft Docs
description: 了解调试器进入中断模式时发生的过程。 然后，调试器必须分步执行代码。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 8a67a3e38c8a1b492f851b575d7c92740f68b7225e16fb56dd3759eb5e0ae482
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448476"
---
# <a name="stepping-in-break-mode"></a>在中断模式下单步执行
以下部分介绍调试器进入中断模式并且必须逐步执行代码时发生的过程：

## <a name="stepping-process"></a>单步执行过程

1. 使用[STEPKIND](../../extensibility/debugger/reference/stepkind.md)和[STEPUNIT](../../extensibility/debugger/reference/stepunit.md)参数调用[IDebugProgram2：：Step](../../extensibility/debugger/reference/idebugprogram2-step.md)以执行步骤。

2. 完成此步骤后，发送 [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) 作为停止事件。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
