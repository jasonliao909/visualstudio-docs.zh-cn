---
title: 堆栈帧 |Microsoft Docs
description: 本文介绍 Visual Studio 中调试器体系结构中堆栈帧的定义和角色。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: dc6c10f00f12d1ee8df9918530a3b04d6ba5ef4e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600830"
---
# <a name="stack-frames"></a>堆栈帧
在调试程序体系结构中， *堆栈帧*：

- 是堆栈的抽象，它提供线程的执行上下文。 线程总是在函数内执行。 堆栈帧保存函数的局部变量和参数。 为了 Visual Studio 调试，要调试的语言或环境必须支持堆栈帧。

- 既可标识并描述自身，也可以返回关联的线程。 堆栈帧还可以返回表示当前指令指针的代码上下文，以及关联的文档和表达式计算上下文。

- 具有描述局部变量和参数的名称、类型和值以及出现在各种 IDE 调试窗口中的属性。

- 由 [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) 接口表示，此接口通常由调试引擎创建 (取消) 或虚拟机作为执行线程的结果。

## <a name="see-also"></a>另请参阅
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)
