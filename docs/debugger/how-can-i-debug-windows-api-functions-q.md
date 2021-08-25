---
title: 调试 Windows API 函数 | Microsoft Docs
description: 了解如何调试已加载 NT 符号的 Windows API 函数。 在 32 位代码中，使用函数名的修饰形式来设置断点。
ms.custom: SEO-VS-2020
ms.date: 06/03/2020
ms.topic: how-to
f1_keywords:
- vs.debug.api
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], Windows API functions
- NT symbols and debugging Windows API functions
- Windows API functions, debugging
- Windows API, debugging API functions
- APIs, debugging
ms.assetid: 7c126f57-62ab-4d94-9805-632d696ba1f0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a9c42db8145b619f6806ee9c4505e09b684efb2d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122044010"
---
# <a name="how-can-i-debug-windows-api-functions"></a>如何调试 Windows API 函数？
如果要调试加载了 NT 符号的 Windows API 函数，必须执行以下步骤。

### <a name="to-set-a-breakpoint-on-a-windows-api-function-with-nt-symbols-loaded"></a>若要在加载了 NT 符号的 Windows API 函数中设置断点

- 在[函数断点](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)中，输入函数名以及函数所在 DLL 的名称（请参阅[上下文运算符](../debugger/context-operator-cpp.md)）。 在 32 位代码中，使用函数名的修饰形式。 例如，若要给”MessageBeep” 设置断点，你必须输入如下内容。

    ```cpp
    {,,USER32.DLL}_MessageBeep@4
    ```

     若要获取修饰名，请参阅[查看修饰名](/previous-versions/5x49w699(v=vs.140))。

     可以测试修饰名称并在反汇编代码中查看它。 在 Visual Studio 调试器的函数中暂停时，在“代码编辑器”或“调用堆栈”窗口中右键单击该函数，然后选择“转到反汇编”。

- 在 64 位代码中，可以使用未修饰名。

    ```cpp
    {,,USER32.DLL}MessageBeep
    ```

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
- [调试本机代码](../debugger/debugging-native-code.md)
