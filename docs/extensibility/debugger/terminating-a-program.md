---
title: 终止程序|Microsoft Docs
description: 本文介绍 IDE 如何使用调试引擎终止具有单个线程的单个程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: bbfe64c5f08cdf82001d1a7df0a80fbc3269c79de895ec499c49d8b5248532a6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306083"
---
# <a name="terminating-a-program"></a>终止程序
以下部分介绍单个程序与一个线程的终止。

## <a name="termination-process"></a>终止过程

1. DE 发送具有有效[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)的[IDebugThreadDestroyEvent2。](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)

2. DE 发送具有有效[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)的[IDebugProgramDestroyEvent2。](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

   IDE 进入设计模式。 调试引擎或运行时环境调用 [IDebugPortNotify2：：RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) 从端口中删除程序。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
