---
title: DebugBreak 和 __debugbreak | Microsoft Docs
description: 了解如何使用 DebugBreak 函数和 __debugbreak 内部函数使程序中断，就像设置了断点一样。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DebugBreak
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], DebugBreak function
- DebugBreak function
- breakpoints, DebugBreak function
ms.assetid: 9787c795-df94-4f48-bc8d-3bf899b67421
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 707c660b658a4f1c34ab0faf345ff64c5063dc8f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640729"
---
# <a name="debugbreak-and-__debugbreak"></a>DebugBreak 和 __debugbreak
可以在代码中的任意点调用 [DebugBreak](/windows/win32/api/debugapi/nf-debugapi-debugbreak) Win32 函数或 [__debugbreak](/cpp/intrinsics/debugbreak) 内部函数。 `DebugBreak` 和 `__debugbreak` 具有与在该位置设置断点相同的效果。

 由于 `DebugBreak` 是对系统函数的调用，因此必须安装系统调试符号，以确保中断后显示正确的调用堆栈信息。 否则，调试器可能在显示一条调用堆栈信息后就停止显示。 如果使用 `__debugbreak`，则不需要符号。

## <a name="see-also"></a>请参阅
- [编译器内部函数](/cpp/intrinsics/compiler-intrinsics)
- [调试器安全](../debugger/debugger-security.md)
- [调试本机代码](../debugger/debugging-native-code.md)
- [指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
