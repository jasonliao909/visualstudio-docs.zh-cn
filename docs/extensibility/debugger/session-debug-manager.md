---
title: 会话调试管理器|Microsoft Docs
description: 了解会话调试管理器，该管理器管理跨任意数量计算机的多个进程中的多个调试引擎调试程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- session debug manager, unifying session views
- session debug manager, broadcasting
- debugging [Debugging SDK], session debug manager
- session debug manager
- session debug manager, debug engine multiplexing
- session debug manager, delegating
ms.assetid: fbb1928d-dddc-43d1-98a4-e23b0ecbae09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3ecfcf276339a54c4c77157101b03b9297d54512
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159563"
---
# <a name="session-debug-manager"></a>会话调试管理器
会话调试管理器 (SDM) 管理任意数目的调试引擎 (DE) ，这些引擎在任意数目的计算机中调试多个进程中任意数目的程序。 除了作为调试引擎多路复用器外，SDM 还提供与 IDE 的调试会话的统一视图。

## <a name="session-debug-manager-operation"></a>会话调试管理器操作
 会话调试管理器 (SDM) DE。 计算机上可以同时运行多个调试引擎。 为了对 DES 进行多路复用，SDM 会包装来自 IDE 的多个接口，并作为单个接口将它们公开给 IDE。

 为了提高性能，不会多路复用某些接口。 相反，它们直接从 DE 使用，并且对这些接口的调用不会通过 SDM。 例如，用于内存、代码和文档上下文的接口不会多路复用，因为它们引用特定 DE 调试的特定程序中的特定指令、内存或文档。 该通信级别无需涉及任何其他 DE。

 并非所有上下文都如此。 对表达式计算上下文接口的调用通过 SDM。 在表达式计算期间，SDM 包装它向 IDE 给出的 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口，因为在计算该表达式时，它可能会涉及多个 DES，这些 DES 正在同一进程中调试程序，这些 DES 可能在同一线程上运行。

 SDM 通常充当委派机制，但它可能充当广播机制。 例如，在表达式计算期间，SDM 充当广播机制，通知所有 DES 它们可以在指定的线程上运行代码。 同样，当 SDM 收到停止事件时，它会广播到应停止运行的程序。 调用步骤时，SDM 将广播到可以继续运行的程序。 断点也会广播到每个 DE。

 SDM 不跟踪当前程序、线程或堆栈帧。 进程、程序以及线程信息与特定的调试事件一起发送到 SDM。

## <a name="see-also"></a>请参阅
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)
