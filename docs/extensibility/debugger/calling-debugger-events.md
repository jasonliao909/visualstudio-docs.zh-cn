---
title: 调用调试器事件|Microsoft Docs
description: 调试会话中的事件按特定顺序发生。 本文列出了典型调试会话中发生的事件的调用顺序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 8472be00d961d5532f3e4c86e5cf63c268fb6be0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664617"
---
# <a name="call-debugger-events"></a>调用调试器事件
调试会话中的事件按特定顺序发生。

## <a name="discussion"></a>讨论 (Discussion)
 若要了解调试引擎 (DE) 与会话调试管理器 (SDM) 之间的调用模式，下面表示典型调试会话中发生的事件的调用顺序：

1. [附加和分离到程序](../../extensibility/debugger/attaching-and-detaching-to-a-program.md)

2. [启动调试器](../../extensibility/debugger/launching-the-debugger.md)

3. [终止程序](../../extensibility/debugger/terminating-a-program.md)

4. [创建断点](../../extensibility/debugger/creating-a-breakpoint.md)

5. [断点绑定或变为未绑定时](../../extensibility/debugger/when-a-breakpoint-binds-or-becomes-unbound.md)

6. [断点错误](../../extensibility/debugger/breakpoint-errors.md)

7. [命中断点](../../extensibility/debugger/hitting-a-breakpoint.md)

8. [删除断点](../../extensibility/debugger/deleting-a-breakpoint.md)

9. [进入中断模式](../../extensibility/debugger/entering-break-mode.md)

10. [在中断模式下单步执行](../../extensibility/debugger/stepping-in-break-mode.md)

11. [中断模式下的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

12. [异常处理](../../extensibility/debugger/exception-handling-visual-studio-sdk.md)

## <a name="see-also"></a>另请参阅
- [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)
