---
title: 从 DLL 项目调试 | Microsoft Docs
description: 可以通过在项目属性中指定调用应用，从项目本身开始调试 DLL 项目。 请参阅本文以获取详细信息。
ms.custom: SEO-VS-2020
ms.date: 4/18/2022
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DLL projects, debugging
- debugging DLLs
- DLLs, debugging projects
- debugging [Visual Studio], DLLs
ms.assetid: 40a94339-d3f7-4ab9-b8a1-b8cf82942f44
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b3ba9ddf7b42637e3765f00c9114c81e51684d88
ms.sourcegitcommit: 35045c249e619401c19dff14b966caf1d7907e6c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2022
ms.locfileid: "143612537"
---
# <a name="how-to-debug-from-a-dll-project-in-visual-studio-c-c-visual-basic-f"></a>如何：在 Visual Studio 中从 DLL 项目调试（C#、C++、Visual Basic、F#）

调试 DLL 项目的一种方法是在 DLL 项目属性中指定调用应用。 随后可以从 DLL 项目本身开始调试。 若要使此方法有效，应用必须调用与配置相同的位置处的相同 DLL。 如果应用找到并加载了不同版本的 DLL，则该版本不包含断点。 有关调试 DLL 的其他方法，请参阅[调试 DLL 项目](../debugger/debugging-dll-projects.md)。

如果托管应用调用本机 DLL，或本机应用调用托管 DLL，则可以同时调试 DLL 和调用应用。 有关详细信息，请参阅[如何：在混合模式下调试](../debugger/how-to-debug-in-mixed-mode.md)。

本机和托管 DLL 项目具有不同的设置来指定调用应用。

## <a name="specify-a-calling-app-in-a-native-dll-project"></a>在本机 DLL 项目中指定调用应用

1. 在解决方案资源管理器中选择 C++ DLL 项目。 选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”。

1. 在“\<Project> 属性页”对话框中，确保窗口顶部的“配置”字段设置为“调试”  。

1. 选择“配置属性” > “调试”。

1. 在“要启动的调试器”列表中，选择“本地 Windows 调试器”或“远程 Windows 调试器”。

1. 在“命令”或“远程命令”框中，添加调用应用的完全限定路径和文件名，如 .exe 文件。

   ![调试属性窗口](../debugger/media/dbg-debugging-properties-dll.png "调试属性窗口")

1. 向“命令参数”框添加任何必要的程序参数。

1. 选择“确定”。

::: moniker range=">= vs-2022"
## <a name="specify-a-calling-app-in-a-c-dll-project-net-core-net-5"></a>在 C# DLL 项目中指定调用应用 (.NET Core， .NET 5+) 

1. 在解决方案资源管理器中选择 C# 或 Visual Basic DLL 项目。 选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”。

1. 在“调试”选项卡中，选择“ **打开调试启动配置文件”UI**。

1. 在“启动配置文件”对话框中，选择“ **创建新配置文件** ”图标，然后选择“ **可执行文件**”。

   :::image type="content" source="../debugger/media/vs-2022/dbg-profile-create-new.png" alt-text="用于创建新调试配置文件的 UI 的屏幕截图。":::

1. 在新配置文件的 **“可执行文件**”下，浏览到可执行文件的位置 (*.exe* 文件) 并选择它。

1. 在“启动配置文件”对话框中，记下默认配置文件的名称，然后选择它并将其删除。

1. 将新配置文件重命名为与默认配置文件相同的名称。

   或者，可以手动编辑 *launchSettings.json* 以获取相同的结果。 希望 *launchSettings.json* 中的第一个配置文件与类库的名称匹配，并且希望它首先列在文件中。

::: moniker-end

## <a name="specify-a-calling-app-in-a-managed-dll-project"></a>在托管 DLL 项目中指定调用应用

1. 在解决方案资源管理器中选择 C# 或 Visual Basic DLL 项目。 选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”。

1. 确保窗口顶部的“配置”字段设置为“调试” 。

1. 在“启动操作”下：

   - 对于 .NET Framework DLL。选择“启动外部程序”，并添加调用应用的完全限定路径和名称。

   - 或者，选择“使用 URL 启动浏览器”并填写本地 ASP.NET 应用的 URL。

   ::: moniker range=">= vs-2022"
   - 对于Visual Basic中的 .NET Core DLL，**“调试** 属性”页是不同的。 从“启动”下拉列表中选择“可执行文件”，然后在“可执行文件”字段中添加调用应用的完全限定路径和名称。
   ::: moniker-end
   ::: moniker range="<= vs-2019"
   - 对于 .NET Core DLL，“调试”属性页不同。 从“启动”下拉列表中选择“可执行文件”，然后在“可执行文件”字段中添加调用应用的完全限定路径和名称。
   ::: moniker-end

1. 在“命令行参数”或“应用程序参数”字段中添加任何所需的命令行参数。

   ![C# 调试属性窗口](../debugger/media/dbg-debugging-properties-dll-csharp.png "C# 调试属性窗口")

1. 使用“文件” > “保存选定项”或 Ctrl+S 来保存更改。

## <a name="debug-from-the-dll-project"></a>从 DLL 项目调试

1. 在 DLL 项目中设置断点。

1. 右键单击 DLL 项目，然后选择“设为启动项目”。

1. 确保“解决方案配置”设置为“调试” 。 按 F5，然后单击绿色“启动”箭头，或选择“调试” > “启动调试”。

其他提示：

- 如果调试未命中断点，请确保 DLL 输出（默认情况为 \<project>\Debug 文件夹）是调用应用进行调用的位置。

- 如果要从本机 DLL 中断托管调用应用中的代码，或进行相反的转换，请启用[混合模式调试](../debugger/how-to-debug-in-mixed-mode.md)。

- 在某些情况下，可能需要告诉调试器在何处查找源代码。 有关详细信息，请参阅[使用“未加载符号/未加载源”页面](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#use-the-no-symbols-loadedno-source-loaded-pages)。

## <a name="see-also"></a>请参阅
- [调试 DLL 项目](../debugger/debugging-dll-projects.md)
- [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
