---
title: 准备调试控制台项目 | Microsoft Docs
description: 获取有关准备在 Visual Studio 中调试控制台项目（C#、C++、Visual Basic、F#）的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], console applications
- debugging console applications
- console applications, debugging
ms.assetid: 9641f1d9-2d5a-48b1-8731-6525e8f67892
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e627e88eb1dbfefe710233eb0136bbe650c782e8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122097410"
---
# <a name="debugging-preparation-console-projects-c-c-visual-basic-f"></a>调试准备：控制台项目（C#、C++、Visual Basic、F#）

准备调试控制台项目类似于准备调试 Windows 项目，但是有一些额外的注意事项，例如设置命令行参数以及如何暂停应用进行调试。 有关详细信息，请参阅 [Windows 窗体应用的调试准备工作](../debugger/debugging-preparation-windows-forms-applications.md)。 由于所有控制台应用程序的相似性，本主题介绍以下项目类型：

- C#、Visual Basic 和 F# 控制台应用程序

- C++ 控制台应用程序 (.NET)

- C++ 控制台应用程序 (Win32)

  控制台应用程序使用“控制台”窗口接受输入以及显示输出消息。 若要向“控制台”窗口写入内容，则应用程序必须使用 Console 对象而不是 Debug 对象 。 若要向“Visual Studio 输出”窗口写入内容，请照常使用 Debug 对象。 确保知道应用程序正在写入的位置，否则可能在错误的位置中查找消息。 有关详细信息，请参见 [Console 类](/dotnet/api/system.console)、[Debug 类](/dotnet/api/system.diagnostics.debug)和[输出窗口](../ide/reference/output-window.md)。

## <a name="set-command-line-arguments"></a>设置命令行参数

可能必须为控制台应用程序指定命令行自变量。 有关详细信息，请参阅 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)、[Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)或 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)。

同所有项目属性一样，这些参数将在调试会话之间和 Visual Studio 会话之间保留。 因此，如果控制台应用程序是以前调试过的，请记得在“\<Project> 属性页”对话框中可能输入了先前会话中的参数。

## <a name="start-the-application"></a>启动应用程序

 某些控制台应用程序在启动后将运行完成，然后退出。 此行为可能不会为您提供足够的时间来中断执行并调试。 若要能够调试应用程序，请使用下列过程之一来启动应用程序：

- 在代码中设置断点，然后启动应用程序。

- 使用 F10（“调试” > “单步跳过”）或 F11（“调试” > “单步进入”）启动应用程序，然后使用其他选项（如“运行到单击处”）在代码中导航      。

- 在代码编辑器中，右键单击一行，然后选择“运行到光标处”。

  调试控制台应用程序时，你可能希望从命令提示符处而不是从 Visual Studio 中启动该应用程序。 在这种情况下，可以从命令提示处启动应用程序并将 Visual Studio 调试器附加到该应用程序。 有关详细信息，请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

  当从 Visual Studio 中启动控制台应用程序时，“控制台”窗口有时会出现在 Visual Studio 窗口的后面。 如果尝试从 Visual Studio 中启动控制台应用程序但似乎未产生任何结果，请尝试移动 Visual Studio 窗口。

## <a name="see-also"></a>请参阅
- [调试本机代码](../debugger/debugging-native-code.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
- [准备调试 C++ 项目](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#, F#, and Visual Basic Project Types](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)（C#、F# 和 Visual Basic 项目类型）
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [调试器安全](../debugger/debugger-security.md)