---
title: 返回到在中断时调用了 MFC 的函数 | Microsoft Docs
description: 了解如何在 Visual Studio 调试器中执行停止时返回到调用了 MFC 的函数。
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.mfc
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- functions [C++], debugging
- function calls, returning to calling function
- debugging [MFC], returning to calling function
- debugging [MFC], functions
- Break command
- programs, halting
- functions [debugger]
ms.assetid: d254a5a9-afbd-4923-9d7a-7422d824cabf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5cdb2ffd30b8fcf1a0dd8a9b1df8e2be21057db1
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129972539"
---
# <a name="how-to-get-back-to-the-function-that-called-mfc-if-halted"></a>如何：返回到在中断时调用了 MFC 的函数

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

如果你使用了“调试”菜单上的“中断”命令来暂停程序，结果结束在 MFC 上，而且你可以确认问题在代码中，则可以使用“调用堆栈”窗口来向后定位到函数 。 有关详细信息，请参阅[如何：使用“调用堆栈”窗口](../debugger/how-to-use-the-call-stack-window.md)。

有时，代码可能在消息泵中中断。 在这种情况下，调用堆栈中没有用户代码。 若要避免此问题，可以使用断点（也许加上条件和命中次数）而非“中断”命令。 有关详细信息，请参阅 [Breakpoints and Tracepoints](/previous-versions/ktf38f66(v=vs.100))。

## <a name="navigate-to-the-function-from-which-mfc-was-called"></a>导航到从中调用了 MFC 的函数

- 使用“调用堆栈”窗口。

## <a name="see-also"></a>请参阅

- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)