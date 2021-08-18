---
title: 进程|Microsoft Docs
description: 本文介绍进程在调试器体系结构中的定义和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], processes
ms.assetid: a6a1efdc-b243-40c8-a778-6f69f6b018be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 6bc1ab72f9771ea8557b3f6688f2253744e322f7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122065171"
---
# <a name="processes"></a>进程
在调试器体系结构中，进程 *：*

- 是一组程序容器。 它非常类似于Windows进程，它是一组线程的容器。

- 可以按名称、标识符或物理标识符来标识自身。

- 可以枚举所有正在运行的程序 (及其线程) 。

- 可以描述自身、运行它的端口以及包含该端口的计算机。

- 可以创建一个或多个程序、终止它创建的任何程序，或导致程序停止。

- 由 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) 接口表示，该接口在进程启动时创建。 进程由会话调试管理器 (SDM) [LaunchSuspended 。](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)

  调试包可以通过调用 Attach 将调试引擎 (DE) 附加到进程，这意味着 DE[](../../extensibility/debugger/reference/idebugprocess2-attach.md)附加到它可以处理的进程中运行的所有可能的程序。 例如，如果公共语言运行时 DE 附加到进程，则它仅附加到运行托管代码的程序。

## <a name="see-also"></a>请参阅
- Programs 
- [线程](../../extensibility/debugger/threads.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试包](../../extensibility/debugger/debug-package.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [附加](../../extensibility/debugger/reference/idebugprocess2-attach.md)
