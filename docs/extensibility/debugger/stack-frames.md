---
title: 堆栈帧|Microsoft Docs
description: 本文介绍堆栈帧在调试器体系结构中的定义和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- stack frames, debugging
- debugging [Debugging SDK], stack frames
- stack frames
ms.assetid: b5e439d4-1e9d-4e13-9cad-bb8b136d4ca8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77b503afcc38ab9427e5268097655433007de5d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898547"
---
# <a name="stack-frames"></a>堆栈帧
在调试器体系结构中，堆栈 *帧*：

- 提供线程执行上下文的堆栈的抽象。 线程始终在函数内执行。 堆栈帧保存函数的局部变量及其参数。 若要使用堆栈Visual Studio，要调试的语言或环境必须支持堆栈帧。

- 可以标识和描述自身，并可以返回关联的线程。 堆栈帧还可以返回表示当前指令指针以及关联的文档和表达式计算上下文的代码上下文。

- 具有描述局部变量和参数的名称、类型和值的属性，这些属性显示在各种 IDE 调试窗口中。

- 由 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) 接口表示，该接口通常由调试引擎 (DE) 或虚拟机（由于执行线程而创建）。

## <a name="see-also"></a>另请参阅
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
