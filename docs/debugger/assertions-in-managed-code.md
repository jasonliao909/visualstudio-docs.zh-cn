---
title: 托管代码中的断言 | Microsoft Docs
description: 了解有关断言作为 Visual Studio 中 C#、Visual Basic 或 F# 托管代码的调试工具的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], assertions in managed code
- Trace.Assert method
- debugging managed code, assertions
- Debug.Assert method
- Debug.Listeners property
- assertions, side effects
- Trace.Listeners property
- assertions, managed code
ms.assetid: 70ab2522-6486-4076-a1a9-e0f11cd0f3a1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- dotnet
ms.openlocfilehash: 937c6474aab6ea1171eccf6914e4e850a8e4bb3b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641271"
---
# <a name="assertions-in-managed-code"></a>托管代码中的断言
断言（或 `Assert` 语句）测试一个你指定为 `Assert` 语句的自变量的条件。 如果该条件的计算结果为 true，则不会执行任何操作。 如果条件的计算结果为 false，则断言失败。 如果正使用调试版本运行，程序将进入中断模式。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> 在本主题中
 [System.Diagnostics 命名空间中的断言](#BKMK_Asserts_in_the_System_Diagnostics_Namespace)

 [Debug.Assert 方法](#BKMK_The_Debug_Assert_method)

 [Debug.Assert 的副作用](#BKMK_Side_effects_of_Debug_Assert)

 [跟踪和调试需求](#BKMK_Trace_and_Debug_Requirements)

 [断言参数](#BKMK_Assert_arguments)

 [自定义断言行为](#BKMK_Customizing_Assert_behavior)

 [在配置文件中设置断言](#BKMK_Setting_assertions_in_configuration_files)

## <a name="asserts-in-the-systemdiagnostics-namespace"></a><a name="BKMK_Asserts_in_the_System_Diagnostics_Namespace"></a>System.Diagnostics 命名空间中的断言
 在 Visual Basic 和 Visual C# 中，可使用位于 <xref:System.Diagnostics> 命名空间中的 <xref:System.Diagnostics.Debug> 或 <xref:System.Diagnostics.Trace> 的 `Assert` 方法。 <xref:System.Diagnostics.Debug> 类方法未包含在程序的“发布”版本中，因此它们不会增加发布代码的大小或降低发布代码的速度。

 C++ 不支持 <xref:System.Diagnostics.Debug> 类方法。 可将 <xref:System.Diagnostics.Trace> 类与条件编译（如 `#ifdef DEBUG`... `#endif`）一起使用来达到相同的效果。

 [在本主题中](#BKMK_In_this_topic)

## <a name="the-debugassert-method"></a><a name="BKMK_The_Debug_Assert_method"></a> Debug.Assert 方法
 自由使用 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 方法来测试代码正确时应为 true 的条件。 例如，假设已编写一个整数除法函数。 根据数学规则，除数绝不能为零。 可使用断言来对此进行测试：

```VB
Function IntegerDivide(ByVal dividend As Integer, ByVal divisor As Integer) As Integer
    Debug.Assert(divisor <> 0)
    Return CInt(dividend / divisor)
End Function
```

```csharp
int IntegerDivide ( int dividend , int divisor )
{
    Debug.Assert ( divisor != 0 );
    return ( dividend / divisor );
}
```

 在调试器下运行该代码时，将计算断言语句，但在发行版中，不会进行比较，因此不会产生额外开销。

 以下是另一个示例。 您有一个实现支票帐户的类，如下所示：

```VB
Dim amount, balance As Double
balance = savingsAccount.balance
Debug.Assert(amount <= balance)
SavingsAccount.Withdraw(amount)
```

```csharp
float balance = savingsAccount.Balance;
Debug.Assert ( amount <= balance );
savingsAccount.Withdraw ( amount );
```

 在从该帐户中取钱之前，您需要确保帐户余额大于准备取出的金额。 可以编写用于查看余额的断言：

```VB
Dim amount, balance As Double
balance = savingsAccount.balance
Trace.Assert(amount <= balance)
SavingsAccount.Withdraw(amount)
```

```csharp
float balance = savingsAccount.Balance;
Trace.Assert ( amount <= balance );
savingsAccount.Withdraw ( amount );
```

 请注意，在创建代码的发布版时，对 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 方法的调用会消失。 这意味着检查余额的调用在发布版中消失。 若要解决此问题，应将 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 替换为在发布版本中不会消失的 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>：

 与对 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> 的调用不同，对 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 的调用会增加发行版的开销。

 [在本主题中](#BKMK_In_this_topic)

## <a name="side-effects-of-debugassert"></a><a name="BKMK_Side_effects_of_Debug_Assert"></a> Debug.Assert 的副作用
 在使用 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 时，确保 `Assert` 中的任何代码不会更改程序的结果（如果移除 `Assert`）。 否则，可能会意外地引入一个只在程序的发行版中出现的 Bug。 对于包含函数或过程调用的断言要特别小心，如下面的示例：

```VB
' unsafe code
Debug.Assert (meas(i) <> 0 )
```

```csharp
// unsafe code
Debug.Assert (meas(i) != 0 );
```

 乍一看，使用 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 似乎很安全，但假设每次调用函数 meas 时，该函数都会更新计数器。 当生成发行版时，由于消除了对 meas 的调用，因此计数器将不会获得更新。 这是一个带副作用的函数的示例。 消除对具有副作用的函数的调用会导致一个只出现在发行版中的 Bug。 若要避免此类问题，请不要将函数调用放在 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 语句中。 改用临时变量：

```VB
temp = meas( i )
Debug.Assert (temp <> 0)
```

```csharp
temp = meas( i );
Debug.Assert ( temp != 0 );
```

 甚至在使用 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> 时，可能仍需要避免将函数调用置于 `Assert` 语句中。 此类调用应该是安全的，因为在发布版中不会清除 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> 语句。 但是，如果你习惯了避免使用此类结构，则在使用 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 时出错的可能性就会很小。

 [在本主题中](#BKMK_In_this_topic)

## <a name="trace-and-debug-requirements"></a><a name="BKMK_Trace_and_Debug_Requirements"></a> 跟踪和调试需求
 如果使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 向导创建项目，则默认情况下，“发布”和“调试”配置中都定义了 TRACE 符号。 默认情况下，只在调试版本中定义 DEBUG 符号。

 否则，若要使 <xref:System.Diagnostics.Trace> 方法能够正常工作，程序必须在源文件的顶部放置下列项之一：

- Visual Basic 中的 `#Const TRACE = True`

- Visual C# 和 C++ 中的 `#define TRACE`

  或者，程序必须是用 TRACE 选项生成的：

- Visual Basic 中的 `/d:TRACE=True`

- Visual C# 和 C++ 中的 `/d:TRACE`

  如果需要在 C# 或 Visual Basic 发行版中使用 DEBUG 方法，您必须在“发布”配置中定义 DEBUG 符号。

  C++ 不支持 <xref:System.Diagnostics.Debug> 类方法。 可将 <xref:System.Diagnostics.Trace> 类与条件编译（如 `#ifdef DEBUG`... `#endif`）一起使用来达到相同的效果。 可以在“\<Project> 属性页”对话框中定义这些符号。 有关详细信息，请参阅[为 Visual Basic 调试配置更改项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)或[更改 C 或 C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

## <a name="assert-arguments"></a><a name="BKMK_Assert_arguments"></a> 断言参数
 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> 和 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> 最多有三个自变量。 第一个参数是强制的，它是要检查的条件。 如果调用仅带一个参数的 <xref:System.Diagnostics.Trace.Assert(System.Boolean)?displayProperty=fullName> 或 <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=fullName>，则 `Assert` 方法将检查条件，并且如果结果为 false，则向“输出”窗口输出调用堆栈的内容。 下面的示例显示 <xref:System.Diagnostics.Trace.Assert(System.Boolean)?displayProperty=fullName> 和 <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=fullName>：

```VB
Debug.Assert(stacksize > 0)
Trace.Assert(stacksize > 0)
```

```csharp
Debug.Assert ( stacksize > 0 );
Trace.Assert ( stacksize > 0 );
```

  第二个和第三个自变量（如果有）必须是字符串。 如果调用带有两个或三个自变量的 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> 或 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>，则第一个自变量为条件。 该方法检查此条件，如果结果为 false，则输出第二个和第三个字符串。 下面的示例演示与以下两个自变量一起使用的 <xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String)?displayProperty=fullName> 和 <xref:System.Diagnostics.Trace.Assert(System.Boolean,System.String)?displayProperty=fullName>：

```VB
Debug.Assert(stacksize > 0, "Out of stack space")
Trace.Assert(stacksize > 0, "Out of stack space")
```

```csharp
Debug.Assert ( stacksize > 0, "Out of stack space" );
Trace.Assert ( stacksize > 0, "Out of stack space" );
```

  下面的示例演示与以下三个自变量一起使用的 <xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String,System.String)?displayProperty=fullName> 和 <xref:System.Diagnostics.Trace.Assert(System.Boolean,System.String,System.String)?displayProperty=fullName>：

```VB
Debug.Assert(stacksize > 0, "Out of stack space. Bytes left:" , Format(size, "G"))
Trace.Assert(stacksize > 0, "Out of stack space. Bytes left:" , Format(size, "G"))
Trace.Assert(stacksize > 0, "Out of stack space. Bytes left:", "inctemp failed on third call" )
```

```csharp
Debug.Assert ( stacksize > 100, "Out of stack space" , "Failed in inctemp" );
Trace.Assert ( stacksize > 0, "Out of stack space", "Failed in inctemp" );
```

 [在本主题中](#BKMK_In_this_topic)

## <a name="customizing-assert-behavior"></a><a name="BKMK_Customizing_Assert_behavior"></a> 自定义断言行为
 如果在用户界面模式中运行应用程序，则当条件失败时，`Assert` 方法将显示“断言失败”对话框。 断言失败时发生的操作由 <xref:System.Diagnostics.Debug.Listeners%2A> 或 <xref:System.Diagnostics.Trace.Listeners%2A> 属性控制。

 可以通过向 <xref:System.Diagnostics.TraceListener> 集合添加 `Listeners` 对象、从 <xref:System.Diagnostics.TraceListener> 集合中移除 `Listeners` 或者重写现有 <xref:System.Diagnostics.TraceListener.Fail%2A?displayProperty=fullName> 的 `TraceListener` 方法来自定义输出行为，使其变得不同。

 例如，可以替代 <xref:System.Diagnostics.TraceListener.Fail%2A?displayProperty=fullName> 方法来对事件日志进行写入而不是显示“断言失败”对话框。

 若要通过此方式自定义输出，您的程序必须包含侦听器，并且必须从 <xref:System.Diagnostics.TraceListener> 继承并重写其 <xref:System.Diagnostics.TraceListener.Fail%2A?displayProperty=fullName> 方法。

 有关详细信息，请参阅[跟踪侦听器](/dotnet/framework/debug-trace-profile/trace-listeners)。

 [在本主题中](#BKMK_In_this_topic)

## <a name="setting-assertions-in-configuration-files"></a><a name="BKMK_Setting_assertions_in_configuration_files"></a> 在配置文件中设置断言
 你可以在程序配置文件和代码中设置断言。 有关详细信息，请参阅<xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>或<xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>。

## <a name="see-also"></a>请参阅

- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>
- <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>
- [调试器安全](../debugger/debugger-security.md)
- [跟踪应用程序和在应用程序中插入检测点](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)
- [如何：使用跟踪和调试执行有条件编译](/dotnet/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug)
- [C#, F#, and Visual Basic Project Types](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)（C#、F# 和 Visual Basic 项目类型）
- [调试托管代码](../debugger/debugging-managed-code.md)
