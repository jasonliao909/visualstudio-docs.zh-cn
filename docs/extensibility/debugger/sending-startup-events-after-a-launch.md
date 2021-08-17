---
title: 启动后发送启动|Microsoft Docs
description: 了解调试引擎在将调试引擎附加到程序后发送到调试会话的一系列启动事件。
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
ms.openlocfilehash: c7449d7e4a9372482fd498c2275dc38f2d24aaad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042655"
---
# <a name="send-startup-events-after-a-launch"></a>启动后发送启动事件
将调试引擎 (DE) 附加到程序后，它会将一系列启动事件发送回调试会话。

 发回到调试会话的启动事件包括：

- 引擎创建事件。

- 程序创建事件。

- 线程创建和模块加载事件。

- 加载完成事件，在加载代码并准备好运行时，但在执行任何代码之前发送。

  > [!NOTE]
  > 当此事件继续时，将初始化全局变量并运行启动例程。

- 可能的其他线程创建和模块加载事件。

- 一个入口点事件，它指示程序已到达其主入口点，例如 **Main 或** `WinMain` 。 如果 DE 附加到已在运行的程序，则通常不会发送此事件。

  DE 首先以编程方式发送会话调试管理器 (SDM) [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 接口，该接口表示引擎创建事件，后跟 [IDebugProgramCreateEvent2（](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)表示程序创建事件）。

  这些事件通常后跟一个或多个 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) 线程创建事件和 [IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md) 模块加载事件。

  加载代码并准备好运行时，但在执行任何代码之前，DE 会向 SDM 发送 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) load complete 事件。 最后，如果程序尚未运行，DE 将发送 [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) 入口点事件，以指示程序已达到其主入口点并已准备好进行调试。

## <a name="see-also"></a>请参阅
- [控制执行](../../extensibility/debugger/control-of-execution.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
