---
title: 启动后发送启动事件 |Microsoft Docs
description: 了解调试引擎附加到程序后，调试引擎向调试会话发送的启动事件系列。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: eb5d382d54d8263cfe0e72f2c828453b8c29aba097973e7c32f1640cc1d2d4a2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414943"
---
# <a name="send-startup-events-after-a-launch"></a>启动后发送启动事件
调试引擎 (DE) 附加到程序后，它会向调试会话发送一系列启动事件。

 发回到调试会话的启动事件包括：

- 引擎创建事件。

- 程序创建事件。

- 线程创建和模块加载事件。

- 加载完成事件，在代码加载并准备好运行，但在执行任何代码之前发送。

  > [!NOTE]
  > 继续此事件时，将初始化全局变量，并运行启动例程。

- 可能的其他线程创建和模块加载事件。

- 入口点事件，该事件指示程序已到达其主入口点，如 **main** 或 `WinMain` 。 如果将 DE 附加到已在运行的程序，则通常不会发送此事件。

  在编程中，取消第一次将会话调试管理器 (SDM 发送) 一个 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 接口，该接口表示一个引擎创建事件，后跟一个 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)，表示一个程序创建事件。

  这些事件通常后跟一个或多个 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 线程创建事件和 [IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md) 模块加载事件。

  当代码已加载并准备好运行，但在执行任何代码之前，DE 将发送 SDM a [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) load 完成事件。 最后，如果程序未在运行，则 DE 将发送 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 入口点事件，并发出信号表明程序已到达其主入口点，并且已准备好进行调试。

## <a name="see-also"></a>请参阅
- [控制执行](../../extensibility/debugger/control-of-execution.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
