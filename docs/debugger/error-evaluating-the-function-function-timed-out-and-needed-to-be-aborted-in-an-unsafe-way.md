---
title: 计算函数 &apos;function&apos; 超时，需要以不安全方式中止 | Microsoft Docs
description: 完整消息文本：计算函数“function”超时，需要以不安全方式中止。
ms.date: 06/18/2021
ms.topic: error-reference
ms.custom: contperf-fy21q4
f1_keywords:
- vs.debug.error.unsafe_func_eval_abort
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d47f16e6f428b5f36953218c0519c61fe650f72f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737162"
---
# <a name="error-evaluating-the-function-39function39-timed-out-and-needed-to-be-aborted-in-an-unsafe-way"></a>错误：计算函数“function”超时，需要以不安全方式中止

完整消息文本：计算函数“function”超时，需要以不安全方式中止。 这可能会损坏目标进程。

为更轻松地检查 .NET 对象的状态，调试器会自动强制调试的进程运行其他代码（通常是属性 getter 方法和 ToString 函数）。 在大多数方案中，这些函数可以快速完成，使调试更加容易。 但是，调试器不会在沙盒中运行应用程序。 因此，调用停止响应的本机函数的属性 getter 或 ToString 方法可能会导致无法恢复的长时间超时。 如果你遇到此错误消息，就是发生了这个问题。

此问题的一个常见原因是，当调试器评估属性时，它只允许执行被检查的线程。 因此，如果属性正在等待其他线程在调试的应用程序内运行，并且它以 .NET 运行时无法中断的方式等待，则会出现此问题。

## <a name="to-correct-this-error"></a>更正此错误

有关此问题的几种可能解决方案，请参阅以下部分。

## <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>解决方法 #1：阻止调试器调用 getter 属性或 ToString 方法

错误消息将告诉你调试器尝试调用的函数的名称。 如果可以修改此函数，就可以阻止调试器调用 getter 属性或 ToString 方法。 尝试以下任一项：

* 将方法更改为除 getter 属性或 ToString 方法之外的其他类型的代码，问题将会消失。
  \- 或 -
* （对于 ToString）为类型定义 [DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md) 特性，调试器将计算 ToString 之外的值。
  -或-
* （对于属性 getter）为属性添加 [System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)](/dotnet/api/system.diagnostics.debuggerbrowsableattribute) 特性。 如果你的方法因为 API 兼容性而要保留属性，那么这是非常有用的，它应该是值得你考虑的方法。

## <a name="solution-2-have-the-target-code-ask-the-debugger-to-abort-the-evaluation"></a>解决方法 #2：让目标代码要求调试器中止计算

错误消息将告诉你调试器尝试调用的函数的名称。 如果属性 getter 或 ToString 方法有时无法正确运行，特别是问题在于代码需要另一个线程来运行代码的情况下，实现函数可以调用 [System.Diagnostics.Debugger.NotifyOfCrossThreadDependency](/dotnet/api/system.diagnostics.debugger.notifyofcrossthreaddependency)，请求调试器中止函数计算。 使用此解决方案，仍然可以显式计算这些函数，但默认行为是在发生 NotifyOfCrossThreadDependency 调用时停止执行。

## <a name="solution-3-disable-all-implicit-evaluation"></a>解决方法 #3：禁用所有隐式计算

如果前面的解决方案未解决问题，请转到“工具” > “选项”，并取消选中“调试” > “常规” > “启用属性计算和其他隐式函数调用”设置    。 这将禁用大多数隐式函数计算，应该可以解决问题。

## <a name="solution-4-check-compatibility-with-third-party-developer-tools"></a>解决方案 #4：检查与第三方开发人员工具的兼容性

如果使用的是 Resharper，请参阅此[问题](https://youtrack.jetbrains.com/issue/RSRP-476824)以获取建议。

## <a name="solution-5-enable-managed-compatibility-mode"></a>解决方案 #5：启用托管兼容模式

如果切换到旧版调试引擎，则可以消除此错误。 转到“工具” > “选项”，然后选择设置“调试” > “常规” > “使用托管兼容模式”    。 有关信息，请参阅[常规调试选项](../debugger/general-debugging-options-dialog-box.md)。
