---
title: SDK (Visual Studio异常) |Microsoft Docs
description: 了解引发异常时发生的过程。 本文介绍涉及的所有步骤。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3763c38fa99f28ac2af52ef821aac2c623720b4c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096617"
---
# <a name="exception-handling-visual-studio-sdk"></a>SDK (Visual Studio异常) 
下面描述了引发异常时发生的过程。

## <a name="exception-handling-process"></a>异常处理过程

1. 首次引发异常时，但在由正在调试的程序中的异常处理程序处理异常之前，调试引擎 (DE) 将 [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) 作为停止事件发送到会话调试管理器 (SDM) 。 如果仅在调试包的"异常 (对话框中指定的异常设置指定用户) 在首次出现异常通知时停止，则发送 `IDebugExceptionEvent2` 。

2. SDM 调用 [IDebugExceptionEvent2：：GetException](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) 获取 exception 的 属性。

3. 调试包调用 [IDebugExceptionEvent2：：CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) 来确定要呈现给用户的选项。

4. 调试包会询问用户如何通过打开"第一机会异常"对话框来处理异常。

5. 如果用户选择继续，SDM 将调用 [IDebugExceptionEvent2：：CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)。

    - 如果方法返回 S_OK，则调用 [IDebugExceptionEvent2：:P assToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)。

         -或-

         如果方法返回S_FALSE，则调试的程序将有机会处理异常。

6. 如果正在调试的程序没有针对第二个可能异常的处理程序，DE 会以 EVENT_SYNC_STOP `IDebugExceptionEvent2` 。 

7. 调试包会询问用户如何通过打开"第一机会异常"对话框来处理异常。

8. 调试包调用 [IDebugExceptionEvent2：：CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) 来确定要呈现给用户的选项。

9. 调试包会询问用户如何通过打开第二机会异常对话框来处理异常。

10. 如果方法返回 S_OK，则 调用 `IDebugExceptionEvent2::PassToDebuggee` 。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)
