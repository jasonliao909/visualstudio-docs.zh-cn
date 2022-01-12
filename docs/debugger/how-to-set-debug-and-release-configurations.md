---
title: 设置调试和发布配置 | Microsoft Docs
description: 在 Visual Studio 中设置调试和发布配置。 生成调试版本的目的是用于调试，而生成发布版本的目的是用于最终发布分发。
ms.custom: SEO-VS-2020
ms.date: 12/21/2021
ms.topic: how-to
f1_keywords:
- vs.debug.builds
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- configurations, release
- build configurations, release
- projects [Visual Studio], release configurations
- debugging [Visual Studio], release configurations
- release builds, changing settings
- debug builds
- debug builds, switching to release build
- debug builds, changing configuration settings
- debugging [Visual Studio], debug configurations
- projects [Visual Studio], debug configurations
- build configurations, debug
- debug configurations
- release builds, switching to debug build
- Visual Basic projects, debug and release builds
ms.assetid: 57b6bbb7-f2af-48f7-8773-127d75034ed2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c08015b138f273d0708bc897b8d719282115efc1
ms.sourcegitcommit: 52a425b5a541034cda26db8df9cd43281c007e80
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2021
ms.locfileid: "135540562"
---
# <a name="set-debug-and-release-configurations-in-visual-studio"></a>在 Visual Studio 中设置调试和发布配置

Visual Studio 项目具有针对你的程序的单独发布和调试配置。 生成调试版本的目的是用于调试，而生成发布版本的目的是用于最终发布分发。

在调用配置中，程序使用完整符号调用信息编译，且不进行优化。 优化会使调试复杂化，因为源代码和生成的指令之间的关系更加复杂。

程序的发布配置进行了完全优化，且不包含任何符号调试信息。 对于托管代码和 C++ 代码，[根据使用的编译器选项](#BKMK_symbols_release)，可在 .pdb 文件中生成调试信息。 如果以后还必须调试发布版本，创建 .pdb 文件就非常有用。

有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

可以从“生成”菜单、从工具栏或在项目的属性页中更改生成配置。 项目属性页是特定于语言的。 下面的过程演示如何从菜单和工具栏更改生成配置。 有关如何在使用不同语言的项目中更改生成配置的详细信息，请参阅下面的[另请参阅](#see-also)一节。

## <a name="change-the-build-configuration"></a>更改生成配置

要更改生成配置，请执行以下操作之一：

* 在工具栏上，从“解决方案配置”列表选择“调试”或“发布”  。

  ![工具栏生成配置](../debugger/media/toolbar-build-configuration.png "ToolbarBuildConfiguration")

  或

* 从“生成”菜单，选择“Configuration Manager”，然后选择“调试”或“发布”   。

## <a name="generate-symbol-pdb-files-for-a-build-c-c-visual-basic-f"></a><a name="BKMK_symbols_release"></a>为版本生成符号 (.pdb) 文件（C#、C++、Visual Basic、F#）

可以选择生成符号 (.pdb) 文件以及要包括的调试信息。 对于大多数项目类型，编译器默认为调试和发布版本生成符号文件，而其他默认设置因项目类型和 Visual Studio 版本而异。

> [!IMPORTANT]
> 调试器只会为可执行文件加载与该可执行文件生成之时所创建的 .pdb 文件完全匹配的 .pdb 文件（即该 .pdb 文件必须是原始 .pdb 文件或其副本）。 有关详细信息，请参阅 [为什么 Visual Studio 要求调试器符号文件必须与同时生成的二进制文件完全匹配？](/archive/blogs/jimgries/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with)。

每个项目类型可能有不同的设置这些选项的方法。

::: moniker range=">=vs-2022"
### <a name="generate-symbol-files-for-a-c-or-aspnet-core-project-net-only"></a>为 C# 或 ASP.NET Core 项目生成符号文件 A0.NET 仅) 

有关 C# 中调试配置的项目设置的详细信息，请参阅Project [C# 调试配置 的一些设置](../debugger/project-settings-for-csharp-debug-configurations.md)。  (对于 Visual Basic 中的 .NET 项目，符号文件的配置方式与 .NET Framework.) 

1. 在“解决方案资源管理器”中，右键单击项目，然后选择“属性”。

2. 在侧窗格中，选择"生成 **常规** > **"。**

3. 在"**优化代码"部分中**，选择"**调试"或**"**发布"。**

4. 在"**调试符号"** 列表中，选择 **"PDB** 文件"、当前平台 **、PBD 文件、可移植** 或"嵌入 **"。**

   可移植格式是 .NET Core 的最新跨平台格式。 如需详细了解各个选项，请参阅[“高级生成设置”对话框 (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md)。

   ![为 .NET 中的生成生成 PDB](../debugger/media/vs-2022/dbg-project-properties-pdb-dotnet.png "GeneratePDBsForDotNet")

5. 生成你的项目。

   编译器将在与可执行文件或主输出文件相同的文件夹中创建符号文件。
::: moniker-end

### <a name="generate-symbol-files-for-a-c-aspnet-or-visual-basic-project-net-framework"></a>生成 C#、ASP.NET 或 Visual Basic 项目的符号 (.NET Framework) 

如需详细了解用 C# 或 Visual Basic 的调试配置的项目设置，请参阅 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)或 [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)。

1. 在“解决方案资源管理器”中，右键单击项目，然后选择“属性”。

2. 在侧窗格中，选择“生成”（或 Visual Basic 中的“编译”） 。

3. 在顶部的 **"配置**"列表中，选择"**调试"或**"**发布"。**

4. 选择“高级”按钮（或 Visual Studio 中的“高级编译选项”按钮） 。

5. 在“调试信息”（或 Visual Basic 中的“生成调用信息”列表）中，选择“完整”、“仅 Pdb”或“可移植”    。

   可移植格式是 .NET Core 的最新跨平台格式。 如需详细了解各个选项，请参阅[“高级生成设置”对话框 (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md)。

   ![使用 C# 为版本生成 PDB](../debugger/media/dbg-project-properties-pdb-csharp.png "GeneratePDBsForCSharp")

6. 生成你的项目。

   编译器将在与可执行文件或主输出文件相同的文件夹中创建符号文件。

### <a name="generate-symbol-files-for-a-c-project"></a>为 C++ 项目生成符号文件

1. 在“解决方案资源管理器”中，右键单击项目，然后选择“属性”。

2. 在“配置”列表中，选择“调试”或“发布”  。

3. 在侧窗中，选择“链接器”>“调试”，然后选择“生成调用信息”的选项 。

   在大多数 C++ 项目中，默认值为 "使用 **/DEBUG (生成调试) 。**

   如需详细了解 C++ 调试配置的项目设置，请参阅 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

4. 配置“生成程序数据库文件”的选项。

   在大多数 C++ 项目中，默认值为 `$(OutDir)$(TargetName).pdb`，用于在输出文件夹中生成 .pdb 文件。

   ![使用 C++ 为版本生成 PDB](../debugger/media/dbg-project-properties-pdb-cplusplus.png "GeneratePDBsforCPlusPlus")

5. 生成你的项目。

   编译器将在与可执行文件或主输出文件相同的文件夹中创建符号文件。

## <a name="see-also"></a><a name="see-also"></a>另请参阅

- [在 Visual Studio 调试器中指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)<br/>
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)<br/>
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)<br/>
- [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)<br/>
- [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)<br/>
- [如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)