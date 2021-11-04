---
title: 常见问题解答 - 查找调试功能
description: 常见问题解答有助于你识别可帮助你调试应用的调试器功能
ms.custom: ''
ms.date: 10/01/2019
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], find your feature
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3c215b232c64b97c57285618056ee4675587b48e
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800535"
---
# <a name="faq---find-the-debugging-feature-you-need-in-visual-studio"></a>常见问题解答 - 在 Visual Studio 中查找所需的调试功能

如果需要帮助你将调试任务映射到相关 Visual Studio 调试器的正确功能，请使用本文中提供的链接。 此处的任务列表包括常见任务，如暂停代码调试、检查变量以及将消息发送到“输出”窗口  。 如果需要大致了解调试器功能，请改为参阅[初探调试器](debugger-feature-tour.md)。

## <a name="fix-an-exception"></a>修复异常

- 请参阅[修复异常](write-better-code-with-visual-studio.md#fix-an-exception)。

## <a name="pause-running-code"></a>暂停代码运行

- **暂停代码运行以检查可能包含 bug 的代码行**

  设置断点。 有关详细信息，请参阅[使用断点](using-breakpoints.md)。

- **当应用达到特定状态时暂停并检查应用**

  尝试设置条件断点以通过使用条件逻辑来控制断点的激活位置和激活时间。 有关详细信息，请参阅[断点条件](using-breakpoints.md#breakpoint-conditions)。

- **仅当特定对象的属性或值更改时暂停代码**

  对于 C++，请设置[数据断点](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)。 
  ::: moniker range=">= vs-2019"
  对于使用 .NET Core 3 的应用，还可以[设置数据断点](using-breakpoints.md#BKMK_set_a_data_breakpoint_managed)。
  ::: moniker-end

  此外，还可以[使用条件断点跟踪对象 ID](using-breakpoints.md#using-object-ids-in-breakpoint-conditions-c-and-f)，但仅适用于 C# 和 F#。

- **在循环内的某个迭代位置暂停代码**

  使用“命中次数”作为条件设置断点  。 有关详细信息，请参阅[命中次数](using-breakpoints.md#set-a-hit-count-condition)。

- **当知道函数名称但不知道其位置时在函数开头暂停代码**

  你可以使用函数断点实现此操作。 有关详细信息，请参阅[设置函数断点](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)。

- **在同名的多个函数的开头暂停代码**

  如果有多个同名的函数（重载的函数或不同项目中的多个函数），则可以使用[函数断点](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)。

- **管理和跟踪断点**

  使用“断点”窗口  。 有关详细信息，请参阅[管理断点](using-breakpoints.md#BKMK_Specify_advanced_properties_of_a_breakpoint_)。

- **引发特定的已处理或未处理异常时暂停代码和调试**

  尽管异常器向你显示了发生错误的位置，但如果想要暂停和调试特定的错误，则可以[告知调试器在引发异常时中断](managing-exceptions-with-the-debugger.md#tell-the-debugger-to-break-when-an-exception-is-thrown)。

- **在“调用堆栈”窗口中设置断点**

  如果希望暂停和调试代码，同时在“调用堆栈”窗口中检查执行流或查看函数，请参阅[在“调用堆栈”窗口中设置断点](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)  。

- **在特定程序集指令处暂停代码**

  你可以通过[在“反汇编”窗口中设置断点](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)来实现此操作。

## <a name="execute-code"></a>执行代码

- **了解在调试时逐行执行代码的命令**

  有关详细信息，请参阅[使用调试器逐行执行代码](navigating-through-code-with-the-debugger.md)。

## <a name="inspect-data"></a>检查数据

- **在运行应用时检查变量的值**

  按照[数据提示](view-data-values-in-data-tips-in-the-code-editor.md)将鼠标悬停在变量上，或[在“自动和本地”窗口中检查变量](autos-and-locals-windows.md)。

- **观察特定变量的变化值**

  对变量设置监视。 有关详细信息，请参阅[对变量设置监视](watch-and-quickwatch-windows.md)。

- **查看调试器窗口无法完全显示的字符串**

  调试时打开内置的[字符串可视化工具](view-strings-visualizer.md)。

## <a name="debug-an-app-that-is-already-running"></a>调试已运行的应用

- 请参阅[附加到正在运行的进程](attach-to-running-processes-with-the-visual-studio-debugger.md)。

## <a name="debug-multithreaded-applications"></a>调试多线程应用程序

- 请参阅[调试多线程应用程序](debug-multithreaded-applications-in-visual-studio.md)。

## <a name="configure-debugging"></a>配置调试

- **自定义调试器设置**

  要配置调试器选项和调试器项目设置，请参阅[调试器设置和准备](debugger-settings-and-preparation.md)。

- **自定义调试器中显示的信息**

  你可能希望在其他调试器窗口中将非对象类型信息显示为值。 对于 C#、Visual Basic、F# 和 C++/CLI 代码，请使用 [DebuggerDisplay](using-the-debuggerdisplay-attribute.md) 属性。 对于更高级的选项，还可以通过创建[自定义可视化工具](create-custom-visualizers-of-data.md)来自定义 UI。

  对于本机 C++，请使用 [NatVis 框架](create-custom-views-of-native-objects.md)。

## <a name="additional-tasks"></a>其他任务

- **在调试会话期间编辑代码**

  使用[编辑并继续](edit-and-continue.md)。 对于 XAML，请使用 [XAML 热重载](../xaml-tools/xaml-hot-reload.md)。

- **将消息发送到“输出”窗口而不修改代码**

  设置跟踪点。 有关详细信息，请参阅[使用跟踪点](using-tracepoints.md)。

- **查看函数的调用顺序**

  请参阅[如何查看调用堆栈](how-to-use-the-call-stack-window.md)。

- **在远程计算机上调试**

  请参阅[远程调试](remote-debugging.md)。

- **修复性能问题**

  请参阅[初探分析工具](../profiling/profiling-feature-tour.md)
