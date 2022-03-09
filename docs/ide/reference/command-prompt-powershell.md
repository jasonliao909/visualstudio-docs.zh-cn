---
title: 适用于开发人员的命令行 shell 和提示
description: 从"工具">"命令行"菜单开始。 选择Visual Studio 开发人员命令提示、开发人员 PowerShell 或终端，以更轻松地使用 .NET 和 C++ 工具。
author: TerryGLee
ms.author: tglee
ms.date: 02/28/2022
ms.topic: conceptual
ms.custom: contperf-fy21q4
helpviewer_keywords:
- Visual Studio command prompt
- command prompt, Visual Studio
- Developer Command Prompt
- Developer PowerShell
- Visual Studio terminal
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
no-loc: cmdlet
monikerRange: '>=vs-2019'
ms.openlocfilehash: 5f4349ad09814afcb88c06b7a7ea75234f72e686
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139549979"
---
# <a name="visual-studio-developer-command-prompt-and-developer-powershell"></a>Visual Studio 开发人员命令提示和开发人员 PowerShell

Visual Studio开发人员的两个命令行 shell、一个命令提示符和一个 PowerShell 实例，如下所示：

- **Visual Studio 开发人员命令提示** - 一种设置了某些环境变量的标准命令提示，可以让使用命令行开发人员工具变得更容易。 自 Visual Studio 2015 起可用。

    ::: moniker range="vs-2019"
    :::image type="content" source="media/developer-command-prompt-for-vs/command-prompt.png" alt-text="2019 开发人员命令提示 2019 Visual Studio的屏幕截图，其中显示了 clrver 工具。":::
    ::: moniker-end

    ::: moniker range="vs-2022"
    :::image type="content" source="media/developer-command-prompt-for-vs/developer-command-prompt-visual-studio-2022.png" alt-text="2022 开发人员命令提示 2022 Visual Studio的屏幕截图，其中显示了 clrver 工具。":::
    ::: moniker-end

- **Visual Studio 开发人员 PowerShell** - 比命令提示符更强大。 例如，你可以将一个命令的输出（称为 *cmdlet* ）传递给另一个 cmdlet。 此 shell 的环境变量集与开发人员命令提示的相同。 自 Visual Studio 2019 起可用。

    ::: moniker range="vs-2022"
    :::image type="content" source="media/developer-command-prompt-for-vs/developer-powershell-visual-studio-2022.png" alt-text="Visual Studio 2022 中的开发人员 PowerShell 工具的屏幕截图。":::
    ::: moniker-end

从 [Visual Studio 2019 版本 16.5](/visualstudio/releases/2019/release-notes-v16.5) 开始，Visual Studio 包含一个集成终端，该终端可以托管这些 shell  (开发人员命令提示 和开发人员 PowerShell) 。 你还可以打开每个 shell 的多个选项卡。 Visual Studio 终端是在 [Windows 终端](/windows/terminal/)的基础上生成的。 若要在终端中打开Visual Studio，请选择 **"视图** > ""**终端"**。

::: moniker range="vs-2022"
:::image type="content" source="media/developer-command-prompt-for-vs/visual-studio-2022-terminal-window.png" alt-text="显示多个选项卡Visual Studio终端窗格的屏幕截图。":::
::: moniker-end

::: moniker range="vs-2019"
:::image type="content" source="media/developer-command-prompt-for-vs/vs-terminal.png" alt-text="显示多个选项卡Visual Studio终端的屏幕截图。":::
::: moniker-end

从 Visual Studio 作为一个单独的应用程序打开其中一个开发人员 shell，或者在终端窗口中打开其中一个开发人员 shell 时，它会打开转到当前解决方案的目录（如果已加载解决方案）。 通过此行为，你可以便捷地针对解决方案或其项目运行命令。

这两个 shell 都具有特定的环境变量集，使你可以更轻松地使用命令行开发人员工具。 打开其中一个 shell 后，可以输入针对不同实用程序的命令，而无需知道它们的位置。

|常用命令|说明|
|--|--|
|[`MSBuild`](../../msbuild/msbuild-command-line-reference.md)|生成项目或解决方案|
|[`clrver`](/dotnet/framework/tools/clrver-exe-clr-version-tool)| 用于 CLR 的 [.NET Framework 工具](/dotnet/framework/tools/index)|
|[`ildasm`](/dotnet/framework/tools/ildasm-exe-il-disassembler)|用于反汇编程序的 [.NET Framework 工具](/dotnet/framework/tools/index)|
|[`dotnet`](/dotnet/core/tools/dotnet)|[.NET CLI 命令](/dotnet/core/tools/index)|
|[`dotnet run`](/dotnet/core/tools/dotnet-run)|[.NET CLI 命令](/dotnet/core/tools/index)|
|[`CL`](/cpp/build/reference/compiler-command-line-syntax)|C/C++ 编译工具|
|[`NMAKE`](/cpp/build/reference/running-nmake)|C/C++ 编译工具|
|[`LIB`](/cpp/build/reference/lib-reference)| C/C++ 生成工具|
|[`DUMPBIN`](/cpp/build/reference/dumpbin-reference)| C/C++ 生成工具|

## <a name="start-in-visual-studio"></a>在 Visual Studio 中启动

按照以下步骤从 Visual Studio 内部打开“开发人员命令提示”或“开发人员 PowerShell”：

1. 打开 Visual Studio。

1. 在菜单栏上，选择"**工具** > **"** > "**命令行开发人员命令提示** 开发人员 **PowerShell"**。

    ::: moniker range="vs-2022"
    :::image type="content" source="media/developer-command-prompt-for-vs/visual-studio-2022-command-line-menu.png" alt-text="2022 年 1 月中&quot;命令行&quot;Visual Studio屏幕截图。":::
    ::: moniker-end

    ::: moniker range="vs-2019"
   ![2019 年 1 月中"命令行"Visual Studio屏幕截图。](./media/developer-command-prompt-for-vs/vs-menu.png)
    ::: moniker-end

## <a name="start-from-windows-menu"></a>从 Windows 菜单中启动

启动 shell 的另一种方法是从“开始”菜单启动。 你可能会有多个命令提示符，具体取决于你安装的 Visual Studio 的版本及其他任何 SDK 和工作负载。

### <a name="windows-11"></a>Windows 11

1. 选择 **"**:::image type="content" source="media/developer-command-prompt-for-vs/windows-11-logo-button.png" alt-text="开始&quot;“开始”按钮屏幕截图。Windows 11，":::然后在"在此处键入 **搜索**"对话框中，输入 或 `developer command prompt` `developer powershell`。

1. 选择与搜索文本关联的应用结果。

### <a name="windows-10"></a>Windows 10

1. 选择 **"开始**!["“开始”按钮屏幕截图Windows 10。](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png)"，然后滚动到字母 **"V"**。

1. 展开"**Visual Studio 2019**"或"**Visual Studio 2022"** 文件夹。

1. 如果运行的是 2019 Visual Studio，请选择"**适用于 VS 2019** 开发人员命令提示开发人员 **PowerShell for VS 2019"**。 如果运行的是 2022 Visual Studio，请选择适用于 **VS 2022** 开发人员命令提示开发人员 **PowerShell for VS 2022。**

   或者，可以在任务栏上的搜索框中开始键入 shell 的名称，并选择想要的结果，因为结果列表开始显示搜索匹配项。

   ![一个动画，该动画显示搜索Windows 10。](./media/developer-command-prompt-for-vs/windows-10-search.gif)

### <a name="windows-81"></a>Windows 8.1

1. 通过按键盘 **上的** Windows徽标键转到"开始"屏幕Windows![徽标键的屏幕截图。](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) 例如，在键盘上。

1. 在“开始”屏幕上，按 Ctrl+Tab 打开“应用程序”列表，然后按 V。然后显示一个列表，其中包含所有已安装的 Visual Studio 命令提示。

1. 如果运行的是 2019 Visual Studio，请选择"**适用于 VS 2019** 开发人员命令提示开发人员 **PowerShell for VS 2019"**。 如果运行的是 2022 Visual Studio，请选择"**适用于 VS 2022** 开发人员命令提示开发人员 **PowerShell for VS 2022"**。

### <a name="windows-7"></a>Windows 7

1. 选择 **"开始** "，然后展开" **所有程序"**。

1. 选择 **Visual Studio 2019** >  **Visual Studio Tools** > **开发人员命令提示 VS 2019 或 VS 2019** 开发人员 **PowerShell**。  (如果运行的是 2022 Visual Studio，请查找包含"2022"而不是"2019"的相同) 

   ![第 7 Windows个"开始"菜单屏幕截图，其中突出显示了命令提示符。](./media/developer-command-prompt-for-vs/windows-7-menu.png)

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
> 请确保编辑路径以匹配Visual Studio的版本。

### <a name="developer-powershell"></a>开发人员 PowerShell

搜索名为 Launch-VsDevShell.ps1 的 PowerShell 脚本文件，或转到 Visual Studio 的“工具”文件夹，例如 %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools。 （该路径根据你的 Visual Studio 版本和安装位置而变化。）找到 PowerShell 文件后，在 Windows PowerShell 或 PowerShell 6 提示符处输入以下命令以运行：

```powershell
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\Launch-VsDevShell.ps1'
```

默认情况下，已为 Visual Studio 安装配置了启动的开发人员 PowerShell，而 Launch-VsDevShell.ps1 文件就位于 Visual Studio 的安装路径中。

> [!TIP]
> 必须设置[执行策略](/powershell/module/microsoft.powershell.core/about/about_execution_policies)才能运行 cmdlet。

该`Launch-VsDevShell.ps1`脚本的工作方式是：在安装路径`Microsoft.VisualStudio.DevShell.dll`中Visual Studio PowerShell 模块，加载该模块，然后调用 `Enter-VsDevShell` cmdlet。 已安装的快捷方式（如 "开始"菜单中的快捷方式）加载模块并直接cmdlet调用 。 `Launch-VsDevShell.ps1` 是交互式初始化开发人员 PowerShell 或编写生成自动化脚本的建议方法。

## <a name="command-line-arguments"></a>命令行参数

可以将命令行参数用于 shell、开发人员命令提示开发人员 PowerShell。

### <a name="target-architecture-and-host-architecture"></a>目标体系结构和主机体系结构

对于创建面向特定 CPU 体系结构的输出的生成工具（如 C++ 编译器），可以使用相应的命令行参数配置开发人员 shell。 也可使用命令行参数配置生成工具二进制文件的体系结构。 当生成计算机与目标体系结构不同时，这很有用。

> [!TIP]
> 从 Visual Studio 2022 开始， `msbuild` 默认为 64 msbuild.exe二进制文件，而不考虑主机体系结构。

|Shell|参数|
|--|--|
|开发人员命令提示|-arch=&lt;目标体系结构&gt;|
|开发人员命令提示|-host_arch=&lt;主机体系结构&gt;|
|开发人员 PowerShell|-Arch &lt;目标体系结构&gt;|
|开发人员 PowerShell|-HostArch &lt;主机体系结构&gt;|

> [!IMPORTANT]
> 开发人员 PowerShell 参数 -Arch 和 -HostArch 仅在 [2022 Visual Studio 17.1](/visualstudio/releases/2022/release-notes#1710--visual-studio-2022-version-171-newreleasebutton) 版开始可用。

下表列出了支持哪些体系结构，以及这些体系结构是否可用于目标体系结构或主机体系结构参数。

|体系结构|目标体系结构|主机体系结构|
|--|--|--|
|x86|默认|默认|
|amd64|是|是|
|arm|是|否|
|arm64|是|否|

> [!TIP]
> 如果仅设置目标体系结构，shell 会尝试使主机体系结构匹配。 当仅目标体系结构设置为主机体系结构也不支持的值时，这可能会导致错误。

#### <a name="examples"></a>示例

在 64 开发人员命令提示启动 Visual Studio 2019 Community Edition 版本，创建面向 64 位的生成输出：
```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat" -arch=amd64
```

在 64 开发人员命令提示启动 Visual Studio 2019 Community Edition 版本，并创建面向 arm 的生成输出：
```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat" -arch=arm -host_arch=amd64
```

在 64 位计算机上启动 [Community 版本 Visual Studio 2022 版本 17.1](/visualstudio/releases/2022/release-notes#1710--visual-studio-2022-version-171-newreleasebutton) 或更高版本的开发人员 PowerShell，并创建面向 arm64 的生成输出：
```powershell
& 'C:\Program Files (x86)\Microsoft Visual Studio\2022\Community\Common7\Tools\Launch-VsDevShell.ps1' -Arch arm64 -HostArch amd64
```

### <a name="skipautomaticlocation"></a>SkipAutomaticLocation

对于开发人员 PowerShell，shell 的起始目录是Visual Studio Project位置。 此默认区域设置将替代任何其他路径，例如工作目录。 可以使用命令行参数 关闭此行为 `-SkipAutomaticLocation`。 如果希望 shell 在初始化后停留在当前目录中，这非常有用。

可以在Project选项 > **&amp;** >  > ""项目解决方案""位置"中调整 **Project位置**。

> [!TIP]
> 脚本和 `-Arch`都cmdlet`-HostArch``-SkipAutomaticLocation` `Launch-VsDevShell.ps1` `Enter-VsDevShell`支持命令行参数 、 和 。

## <a name="see-also"></a>另请参阅

- [Windows 终端](/windows/terminal/)
- [.NET Framework 工具](/dotnet/framework/tools/index)
- [通过命令行使用 Microsoft C++ 工具集](/cpp/build/building-on-the-command-line)
- [Visual Studio Code 用户](https://code.visualstudio.com/docs/cpp/config-msvc#:~:text=To%20open%20the%20Developer%20Command,item%20to%20open%20the%20prompt.)
