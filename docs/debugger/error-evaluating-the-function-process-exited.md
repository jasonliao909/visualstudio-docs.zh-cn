---
description: 完整消息文本：评估函数“function”时，目标进程退出并生成代码“code”。
title: 评估函数 &apos;function&apos; 时，目标进程退出并生成代码 &apos;code&apos; | Microsoft Docs
ms.date: 4/06/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.process_exit_during_func_eval
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 680fc682c39ee919038da551a4d4cbbffbf6c168
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154490"
---
# <a name="error-the-target-process-exited-with-code-39code39-while-evaluating-the-function-39function39"></a>错误：评估函数“function”时，目标进程退出并生成代码“code”

完整消息文本：评估函数“function”时，目标进程退出并生成代码“code”。

为更轻松地检查 .NET 对象的状态，调试器会自动强制调试的进程运行其他代码（通常是属性 getter 方法和`ToString`函数）。 在大多数情况下，这些函数会成功完成或引发可由调试器捕获的异常。 但是，在某些情况下，由于异常跨越内核边界、需要用户消息循环或不可恢复，因此无法捕获。 结果，执行代码的属性 getter 或 ToString 方法或者显式终止进程 (例如，调用`ExitProcess()`) 或引发不能被捕获的未经处理异常 (例如， `StackOverflowException`)，从而终止调试的进程并结束调试会话。 如果你遇到此错误消息，就是发生了这个问题。

此问题的一个常见原因是，当调试器计算调用自身的属性时，可能会导致堆栈溢出异常。 堆栈溢出异常无法恢复，目标进程将终止。

## <a name="to-correct-this-error"></a>更正此错误

此问题有两个可能的解决方案。

### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>解决方法 #1：阻止调试器调用 getter 属性或 ToString 方法 

错误消息将告诉你调试器尝试调用的函数的名称。 使用此函数的名称，你可以尝试从 **即时** 窗口重新计算该函数以调试该求值。 从 **即时** 窗口求值可以进行调试，因为与 **自动/局部变量/监视** 窗口的隐式求值不同，调试器将在未经处理的异常处中断。

如果可以修改此函数，可以阻止调试器调用 getter 属性或`ToString`方法。 尝试以下任一项：

* 将方法更改为除 getter 属性或 ToString 方法之外的其他类型的代码，问题将会消失。
    \- 或 -
* （对于 `ToString`） 为类型定义 `DebuggerDisplay` 特性，调试器将计算 `ToString` 之外的值。
    \- 或 -
* （对于属性 getter）为属性定义 `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` 特性。 如果您的方法因为 API 兼容性而要保留属性，这很有用，但它应该真是一个方法。

如果您不能修改此方法，您可以在备用的指令处中断目标进程，然后重试求值。

### <a name="solution-2-disable-all-implicit-evaluation"></a>解决方法 #2：禁用所有隐式计算

如果前面的解决方案未解决问题，请转到“工具” > “选项”，并取消选中“调试” > “常规” > “启用属性计算和其他隐式函数调用”设置    。 这将禁用大多数隐式函数计算，应该可以解决问题。
