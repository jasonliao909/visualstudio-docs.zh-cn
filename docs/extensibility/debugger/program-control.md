---
title: 程序控制|Microsoft Docs
description: 了解程序Visual Studio调试中的例程，例如执行、单步执行、继续和挂起/恢复线程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 42deca29129ed25aabf2f7dc1ce7cd40480abfe306eaf11c58be73a65193d4f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452454"
---
# <a name="program-control"></a>程序控制
在Visual Studio中，以下所有单步执行和继续例程都发生在程序级别：

- 设置下一条语句，即将计算机设置为要特定帧环境中执行的下一条指令

- 执行 ，即继续退出单步执行模式

- 单步执行下一条指令

- 继续执行当前单步执行模式

- 挂起程序包含的线程

- 恢复程序包含的线程

> [!NOTE]
> 查看调用堆栈是在线程级别实现的。 若要在查看线程的调用堆栈时枚举帧信息，必须实现 [IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md) 接口的所有方法。

## <a name="methods-of-program-control"></a>程序控制方法
 下表显示了 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 的方法，这些方法必须为 DE 控制和执行控制 (最小) 引擎实现。

|方法|说明|
|------------|-----------------|
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|继续从已停止状态运行程序包含的所有线程。 执行控制必需。|
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|继续从已停止状态运行程序包含的所有线程。 执行控制必需。|
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|在给定线程上执行步骤。 继续运行程序包含的所有其他线程。 执行控制必需。|

 对于多线程程序，还必须实现 [IDebugProgram2：：EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) 方法和 [IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md) 接口的所有方法。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)
