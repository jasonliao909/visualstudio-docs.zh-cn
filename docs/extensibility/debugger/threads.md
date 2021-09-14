---
title: 线程|Microsoft Docs
description: 本文介绍中调试器体系结构中线程的定义和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], threads
- threading [Debugging SDK]
ms.assetid: 2243d24a-c3d2-41d1-abbb-6db21a2db9ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 58eed8c14faebfa60f2c87846ceefb7d93ac3a79
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600799"
---
# <a name="threads"></a>线程数
在调试器体系结构 *中，线程*：

- 是计算的基本单位。 线程在单个调用堆栈的上下文中按顺序执行其指令，从一个代码上下文移动到下一个代码上下文。

- 可以标识自身及其运行的程序。 线程可以命名、挂起并恢复。 线程还可以枚举其关联的堆栈帧，在某些情况下，可以移动到另一个堆栈帧。 给定堆栈帧的上下文后，线程可以返回其关联的逻辑线程（如果有）。 线程具有可在 IDE 的"线程"窗口中显示的属性，例如挂起计数。

- 由 [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) 接口表示，该接口通常由调试引擎 (DE) 或虚拟机上执行程序而创建。

## <a name="see-also"></a>另请参阅
- Programs 
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
