---
title: 适用于开发人员的命令行 shell 和提示
description: 从“工具”>“命令行”菜单开始。 通过使用 Visual Studio 开发人员命令提示、开发人员 PowerShell 和终端，可以更轻松地使用 .NET 和 C++ 工具。
author: TerryGLee
ms.author: tglee
ms.date: 06/11/2021
ms.topic: reference
ms.custom: contperf-fy21q4
helpviewer_keywords:
- Visual Studio command prompt
- command prompt, Visual Studio
- Developer Command Prompt
- Developer PowerShell
- Visual Studio terminal
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
no-loc: cmdlet
ms.openlocfilehash: 858845ca5629f64e282e3864daa0201935316062
ms.sourcegitcommit: b4cc3dee59421f7089112becf128a369acadaf61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2021
ms.locfileid: "112990514"
---
# <a name="visual-studio-developer-command-prompt-and-developer-powershell"></a>Visual Studio 开发人员命令提示和开发人员 PowerShell

Visual Studio 2019 包含两个开发人员命令行 shell：

- **Visual Studio 开发人员命令提示** - 一种设置了某些环境变量的标准命令提示，可以让使用命令行开发人员工具变得更容易。 自 Visual Studio 2015 起可用。

- **Visual Studio 开发人员 PowerShell** - 比命令提示符更强大。 例如，你可以将一个命令的输出（称为 *cmdlet* ）传递给另一个 cmdlet。 此 shell 的环境变量集与开发人员命令提示的相同。 自 Visual Studio 2019 起可用。


:::image type="content" source="media/developer-command-prompt-for-vs/command-prompt.png" alt-text="显示 clrver 工具的 Visual Studio 开发人员命令提示":::

从 Visual Studio 2019 版本 16.5 开始，Visual Studio 包含一个集成终端，此终端可以托管这些 shell（开发人员命令提示和开发人员 PowerShell）中的任何一个。 你还可以打开每个 shell 的多个选项卡。 Visual Studio 终端是在 [Windows 终端](/windows/terminal/)的基础上生成的。 若要在 Visual Studio 中打开此终端，请选择“查看” > 终端。

:::image type="content" source="media/developer-command-prompt-for-vs/vs-terminal.png" alt-text="显示多个选项卡的 Visual Studio 终端":::

从 Visual Studio 作为一个单独的应用程序打开其中一个开发人员 shell，或者在终端窗口中打开其中一个开发人员 shell 时，它会打开转到当前解决方案的目录（如果已加载解决方案）。 通过此行为，你可以便捷地针对解决方案或其项目运行命令。

这两个 shell 都具有特定的环境变量集，使你可以更轻松地使用命令行开发人员工具。 打开其中一个 shell 后，可以输入针对不同实用程序的命令，而无需知道它们的位置。 

|常用命令|说明|
|--|--|
|[`MSBuild`](../../msbuild/msbuild-command-line-reference.md)|生成项目或解决方案|
|[`clrver`](/dotnet/framework/tools/clrver-exe-clr-version-tool)| 用于 CLR 的 [.NET Framework 工具](/dotnet/framework/tools/index)。|
|[`ildasm`](/dotnet/framework/tools/ildasm-exe-il-disassembler)|用于反汇编程序的 [.NET Framework 工具](/dotnet/framework/tools/index)。|
|[`dotnet`](/dotnet/core/tools/dotnet)|[.NET CLI 命令](/dotnet/core/tools/index)|
|[`dotnet run`](/dotnet/core/tools/dotnet-run)|[.NET CLI 命令](/dotnet/core/tools/index)|
|[`CL`](/cpp/build/reference/compiler-command-line-syntax)|C/C++ 编译工具|
|[`NMAKE`](/cpp/build/reference/running-nmake)|C/C++ 编译工具|
|[`LIB`](/cpp/build/reference/lib-reference)| C/C++ 生成工具|
|[`DUMPBIN`](/cpp/build/reference/dumpbin-reference)| C/C++ 生成工具|


## <a name="start-in-visual-studio"></a>在 Visual Studio 中启动

按照以下步骤从 Visual Studio 内部打开“开发人员命令提示”或“开发人员 PowerShell”：

1. 打开 Visual Studio。

1. 在菜单栏上，依次选择“工具” > 命令行 > 开发人员命令提示或“开发人员 PowerShell”。

   ![Visual Studio 中的命令提示符菜单项](./media/developer-command-prompt-for-vs/vs-menu.png)

## <a name="start-from-windows-menu"></a>从 Windows 菜单中启动

启动 shell 的另一种方法是从“开始”菜单启动。 你可能会有多个命令提示符，具体取决于你安装的 Visual Studio 的版本及其他任何 SDK 和工作负载。 

### <a name="windows-10"></a>Windows 10

1. 选择“开始”![键盘上的 Windows 徽标键。](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) 并滚动到字母“V”。

1. 展开“Visual Studio 2019”文件夹。

1. 选择“VS 2019 开发人员命令提示”或“VS 2019 开发人员 PowerShell”。

   或者，你可以首先在任务栏的搜索框中键入 shell 的名称，然后在结果列表开始显示搜索匹配项时选择所需的结果。

   ![在 Windows 10 上显示搜索行为的动画 gif](./media/developer-command-prompt-for-vs/windows-10-search.gif)

### <a name="windows-81"></a>Windows 8.1

1. 按 Windows 徽标键![键盘上的 Windows 徽标键](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png)，转到“开始”屏幕。 例如，在键盘上。

1. 在“开始”屏幕上，按 Ctrl+Tab 打开“应用程序”列表，然后按 V。然后显示一个列表，其中包含所有已安装的 Visual Studio 命令提示。

1. 选择“VS 2019 开发人员命令提示”或“VS 2019 开发人员 PowerShell”。

### <a name="windows-7"></a>Windows 7

1. 选择“开始”，然后展开“所有程序”。

1. 依次选择“Visual Studio 2019” > “Visual Studio Tools” > “VS 2019 开发人员命令提示”或“VS 2019 开发人员 PowerShell”。

   ![突出显示命令提示符的 Windows 7“开始”菜单](./media/developer-command-prompt-for-vs/windows-7-menu.png)

如果安装了其他 SDK，例如 [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 或[之前的版本](https://developer.microsoft.com/windows/downloads/sdk-archive)，则可能看到其他命令提示符。 查看单个工具的文档，以确定应使用哪个版本的命令提示。

## <a name="start-from-file-browser"></a>从文件浏览器启动 

已安装的 shell 的快捷方式通常放在 Visual Studio 的“开始菜单”文件夹中，例如 %ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2019\Visual Studio Tools。 但是如果搜索命令提示未产生预期的效果，你可以尝试在计算机中手动查找文件。

### <a name="developer-command-prompt"></a>开发人员命令提示

搜索命令提示符文件的名称，即 VsDevCmd.bat，或者转到 Visual Studio 的“工具”文件夹，例如 %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools（该路径根据你的 Visual Studio 版本和安装位置而变化）。

找到命令提示符文件后，在常规的命令提示符窗口中输入以下命令以将其打开：

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

或者在 Windows“运行”对话框中输入以下命令：

```cmd
%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

> [!TIP]
> 你需要编辑路径才能匹配 Visual Studio 安装。

### <a name="developer-powershell"></a>开发人员 PowerShell

搜索名为 Launch-VsDevShell.ps1 的 PowerShell 脚本文件，或转到 Visual Studio 的“工具”文件夹，例如 %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools。 （该路径根据你的 Visual Studio 版本和安装位置而变化。）找到 PowerShell 文件后，在 Windows PowerShell 或 PowerShell 6 提示符处输入以下命令以运行：

```powershell
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\Launch-VsDevShell.ps1'
```

默认情况下，已为 Visual Studio 安装配置了启动的开发人员 PowerShell，而 Launch-VsDevShell.ps1 文件就位于 Visual Studio 的安装路径中。

> [!TIP]
> 必须设置[执行策略](/powershell/module/microsoft.powershell.core/about/about_execution_policies)才能运行 cmdlet。

## <a name="see-also"></a>另请参阅

- [开发人员 PowerShell](https://devblogs.microsoft.com/visualstudio/the-powershell-you-know-and-love-now-with-a-side-of-visual-studio/)
- [认识全新的 Visual Studio 终端](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/)
- [Windows 终端](/windows/terminal/)
- [.NET Framework 工具](/dotnet/framework/tools/index)
- [管理外部工具](../managing-external-tools.md)
- [通过命令行使用 Microsoft C++ 工具集](/cpp/build/building-on-the-command-line)
