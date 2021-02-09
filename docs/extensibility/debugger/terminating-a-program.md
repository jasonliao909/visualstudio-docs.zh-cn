---
title: 终止程序 |Microsoft Docs
description: 本文介绍 IDE 如何使用调试引擎，通过单个线程终止单个程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0f44cb287945576d361d0318eaeafa42de99871d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895903"
---
# <a name="terminating-a-program"></a>终止程序
以下部分介绍了单个程序的终止，其中包含一个线程。

## <a name="termination-process"></a>终止进程

1. DE 发送具有有效[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)的[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) 。

2. DE 发送具有有效[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)的[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 。

   IDE 进入设计模式。 调试引擎或运行时环境调用 [IDebugPortNotify2：： RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) 从端口中删除程序。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
