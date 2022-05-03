---
title: Visual Studio for Mac IDE 教程
description: Visual Studio for Mac提供集成开发环境 (IDE) ，用于在 macOS 上生成 .NET 应用程序，包括适用于 iOS、Android、Mac 和 Xamarin.Forms 的 ASP.NET Core 网站和 Xamarin 项目。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 3/20/2022
ms.assetid: 7DC64A52-AA41-4F3A-A8A1-8A20BCD81CC7
ms.custom: video, devdivchpfy22
ms.topic: overview
ms.openlocfilehash: 584501e37fb9026ba5a787f20774c4ffa1ee47d9
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144505466"
---
# <a name="visual-studio-for-mac-ide-tour"></a>Visual Studio for Mac IDE 教程

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

::: moniker range="vsmac-2022"

本介绍Visual Studio for Mac _集成开发环境_ (IDE) ，我们将介绍一些窗口、菜单和其他 UI 功能。

Visual Studio for Mac 是 Mac 上的 .NET 集成开发环境，可用于编辑、调试和生成代码，然后发布应用。 除了代码编辑器和调试程序外，Visual Studio for Mac 还包括编译器、代码完成工具、图形设计器和源代码管理功能，以简化软件开发过程。

如果尚未安装 Visual Studio，请转到 Visual Studio 下载页免费安装。

## <a name="start-window"></a>启动窗口

打开Visual Studio for Mac后会看到的第一件事是 _开始窗口_。 它显示最近打开现有项目或创建新项目的选项的列表。

![从最近的项目中选择，或创建新项目](media/vsmac-2022/ide-tour-start-window.png)

如果首次使用 Visual Studio，最近的项目列表将为空。

## <a name="create-a-project"></a>创建一个项目

若要继续探索功能，让我们创建一个新项目。

1. 在“开始”窗口中，选择“ **新建** ”以创建新项目。

   ![创建新项目](media/vsmac-2022/ide-tour-new-project.png)

1. **选择新项目窗口的模板** 将打开并显示多个项目模板。 如果 **选择“** 最近使用”，它还会显示最近使用的项目模板的列表。 模板包含给定项目类型所需的基本文件和设置。 

   在 **“Web 和控制台**”部分中从 **“应用**”中选择“**控制台应用程序**”，然后选择“**继续**”。

   ![选择模板](media/vsmac-2022/ide-tour-select-template.png)

1. 在 **“配置新的控制台应用程序** ”窗口中，确保 **.NET 6.0** 显示在 **“目标框架** ”下拉列表中，然后选择“ **下一步**”。

   ![目标 Framework](media/vsmac-2022/ide-tour-target-framework.png)

1. 在 **“配置新的控制台应用程序**”窗口中，添加 **Project名称**、**解决方案名称和****位置**，然后选择“**创建**”。

   ![配置新的控制台应用程序](media/vsmac-2022/ide-tour-create-new-project.png)

1. 项目已创建。 在 **解决方案** 窗口中选择 *代码文件 Program.cs*，该窗口位于Visual Studio for Mac左侧。

   ![控制台应用程序项目](media/vsmac-2022/ide-tour-console-application-project.png)

文件 Program.cs 将在 **编辑器** 窗口中打开。 编辑器显示文件的内容，可在其中执行大部分编码工作。

## <a name="solution-window"></a>解决方案窗口

**解决方案** 显示项目、解决方案或代码文件夹中文件和文件夹层次结构的图形表示形式。 你可以浏览层次结构并选择要在“编辑器”中打开的文件。

![解决方案窗口](media/vsmac-2022/ide-tour-solution-window.png)

## <a name="menus"></a>菜单

Visual Studio for Mac命令顶部的菜单栏分为类别。 例如，“项目”菜单包含与你正在处理的项目相关的命令。 在 **“工具”** 菜单上，可以通过选择 **“首选项**”来自定义Visual Studio的行为方式。

![菜单](media/vsmac-2022/ide-tour-menus.png)

## <a name="errors-window"></a>“错误”窗口

“ **错误** ”窗口显示有关代码当前状态的错误、警告和消息。 如果文件中或项目的任何地方出现错误（例如缺少括号或分号），则会在此处列出。

若要打开 **“错误** ”窗口，请选择 **“视图** ”菜单，然后选择“ **错误**”。

![“错误”窗口](media/vsmac-2022/ide-tour-errors-window.png)

## <a name="build-output-window"></a>“生成输出”窗口

“ **生成输出** ”窗口显示生成项目的消息。

让我们生成该项目来查看一些生成输出。 从 **“生成”** 菜单中选择 **“生成解决方案”** 。 “生成输出”窗口会自动获取焦点，并显示成功的生成消息。

![“生成输出”窗口](media/vsmac-2022/ide-tour-build-output-window.png)

## <a name="run-your-console-application"></a>运行控制台应用程序

让我们通过选择播放图标来运行控制台应用程序。 你将在 **终端** 中看到输出。

![运行控制台应用程序](media/vsmac-2022/ide-tour-run-console-application.png)

## <a name="send-feedback"></a>发送反馈
如果在使用Visual Studio for Mac时遇到问题，或者有有关如何改进产品的建议，可以告知我们。 为此，请从 **“帮助**”菜单中选择“**报告问题**”或 **“提供建议**”。

## <a name="learn-more"></a>了解更多

我们只了解了一些Visual Studio功能来熟悉用户界面。 
进一步探索：

- Visual Studio for Mac中的[源编辑器](./source-editor.md)
- [重构](./refactoring.md)
- 调试时[的数据可视化效果](./data-visualizations.md)
- [版本控制](./version-control.md)

::: moniker-end

::: moniker range="vsmac-2019"

Visual Studio for Mac是 Mac 上的 .NET _集成开发环境_。 它可用于编辑、调试和生成代码，然后发布应用。 除了代码编辑器和调试程序外，Visual Studio for Mac 还包括编译器、代码完成工具、图形设计器和源代码管理功能，以简化软件开发过程。

Visual Studio for Mac 支持许多与其 Windows 对应的文件类型相同的文件类型（例如 `.csproj`、`.fsproj` 或 `.sln`文件），并且支持 EditorConfig 等功能，这意味着可以使用最适合自己的 IDE。
对于以前在Windows上使用过Visual Studio的用户，创建、打开和开发应用是一种熟悉的体验。 此外，Visual Studio for Mac采用许多功能强大的工具，使其Windows对应如此强大的 IDE。 Roslyn 编译器平台用于重构和 IntelliSense。 它的项目系统和生成引擎使用 MSBuild，它的源编辑器使用与 Windows 上的 Visual Studio 相同的基础。 对于 Xamarin 和 .NET Core 应用，使用的是相同的调试器引擎，对于 Xamarin.iOS 和 Xamarin.Android 使用的是相同的设计器。

## <a name="what-can-i-do-in-visual-studio-for-mac"></a>可以在 Visual Studio for Mac 中执行的操作

Visual Studio for Mac 支持以下类型的开发：

- 使用 C#、F# 的 ASP.NET Core Web 应用程序，以及对 Razor 页面、JavaScript 和 TypeScript 的支持
- 使用 C# 或 F# 的 .NET Core 控制台应用程序
- 使用 C# 的跨平台 Unity 游戏和应用程序
- 使用 C# 或 F# 和 XAML 的 Xamarin 中的 Android、iOS、tvOS 和 watchOS 应用程序
- 使用 C# 或 F# 的 Cocoa 桌面应用

本文探讨Visual Studio for Mac的不同部分，提供一些功能，使其成为创建这些应用程序的强大工具。

## <a name="ide-tour"></a>IDE 导览

Visual Studio for Mac 分为多个部分，用于管理应用程序文件和设置、创建应用程序代码以及进行调试。

## <a name="getting-started"></a>入门

首次启动 Visual Studio 2019 for Mac 后，新用户可看到登录窗口。 如果拥有一个) 或链接到 Azure 订阅，请使用 Microsoft 帐户激活付费许可证 (。 可以按下“我稍后再执行此操作”，然后通过“Visual Studio”>“登录”菜单项登录：

![登录 Microsoft 帐户](media/ide-tour-2019-start-signin.png)

然后，可以通过选择自己喜欢的键盘快捷方式来自定义 IDE：Visual Studio for Mac、Visual Studio、Visual Studio Code 或 Xcode：

![选择你最喜爱的键盘快捷方式](media/ide-tour-2019-keyboard-shortcut.png)

完成此初始设置体验后，每当打开 Visual Studio 2019 for Mac 时，都会看到 _启动窗口_。 它显示最近项目和按钮的列表，用于打开现有项目或创建新项目：

![从最近的项目中选择，或创建新项目](media/ide-tour-2019-start-projects.png)

## <a name="solutions-and-projects"></a>解决方案和项目

下图显示加载了应用程序的 Visual Studio for Mac：

![加载了应用程序的 Visual Studio for Mac](media/ide-tour-image17.png)

以下部分概述了 Visual Studio for Mac 中的主要区域。

## <a name="solution-window"></a>解决方案窗口

解决方案窗口在解决方案中组织项目：

![在解决方案窗口中组织的项目](media/ide-tour-image18.png)

解决方案窗口是将源代码、资源、用户界面和依赖项的文件组织到特定于平台的项目的位置。

有关在 Visual Studio for Mac 中使用项目和解决方案的详细信息，请参阅[项目和解决方案](./projects-and-solutions.md)一文。

## <a name="assembly-references"></a>程序集引用

“引用”文件夹中提供每个项目的程序集引用：

![解决方案窗口中的“引用”文件夹](media/ide-tour-image19.png)

使用 **“编辑引用** ”对话框添加更多引用，该对话框通过双击“引用”文件夹或在其上下文菜单操作上选择 **“编辑引用** ”来显示：

![“编辑引用”对话框](media/ide-tour-image20.png)

有关在 Visual Studio for Mac 中使用引用的详细信息，请参阅[管理项目中的引用](./managing-references-in-a-project.md)一文。

## <a name="dependencies--packages"></a>依赖项/包

在应用中使用的所有外部依赖关系存储在“依赖关系”或“包”文件夹中，具体取决于所在的项目是 .NET Core 还是 Xamarin.iOS/Xamarin.Android 项目。 这些内容以NuGet的形式提供。

NuGet 是 .NET 开发最常用的程序包管理器。 通过 Visual Studio 的 NuGet 支持，可以轻松地搜索包并将其添加到项目，再添加到应用程序。

若要将依赖关系添加到应用程序，请右键单击“依赖关系”/“包”文件夹，然后选择“添加包”：

![添加 NuGet 包](media/ide-tour-image21.png)

可在[在项目中包括 NuGet 包](./nuget-walkthrough.md)一文中找到在应用程序中使用 NuGet 包的相关信息。

## <a name="source-editor"></a>源编辑器

无论使用 C#、XAML 或 JavaScript 编写，代码编辑器都会与 Windows 上的 Visual Studio 共享相同的核心组件，并具有完全本机用户界面。

源编辑器提供以下一些功能：

* 本机 macOS（基于 Cocoa）用户界面（工具提示、编辑器外观、边距修饰、文本渲染、IntelliSense）
* IntelliSense 类型筛选以及“显示导入项”
* 支持本机文本输入
* RTL/BiDi 语言支持
* Roslyn 3
* 多个插入点支持
* 自动换行
* 更新后的 IntelliSense UI
* 改进了“查找/替换”
* 代码片段支持 
* 设置选定内容的格式
* 内联灯泡

有关在 Visual Studio for Mac 中使用源编辑器的详细信息，请参阅[源编辑器](./source-editor.md)文档。

若要使选项卡始终可见，可以利用固定选项卡。 这可确保每次启动项目时，都将始终显示需要的选项卡。 若要固定选项卡，请将鼠标悬停在选项卡上，然后选择 _固定_ 图标：

![固定选项卡](media/ide-tour-tabpin.png)

## <a name="refactoring"></a>重构

Visual Studio for Mac 提供用于重构代码的两种有用途径：上下文操作和源分析。 可在[重构](./refactoring.md)一文中阅读更多相关信息。

## <a name="debugging"></a>调试

Visual Studio for Mac 提供支持 .Net Core、.NET Framework、Unity 和 Xamarin 项目的调试器。 Visual Studio for Mac 使用 .NET Core 调试器和 Mono 软调试器，以便 IDE 跨所有平台调试托管代码。 有关调试的详细信息，请访问 [调试](./debugging.md) 文章。

调试器包含用于特殊类型的丰富可视化工具，例如字符串、颜色、URL、大小、坐标和 bézier 曲线。

有关调试器的数据可视化效果的详细信息，请访问[数据可视化效果](./data-visualizations.md)一文。

## <a name="version-control"></a>版本控制

Visual Studio for Mac 与 Git 和 Subversion 源控件系统集成。 源控件下的项目用解决方案名称旁列出的分支表示：

![分支名称用来表示源控件下的项目](media/ide-tour-image22.png)

未提交的更改的文件在解决方案窗口中的图标上有注释，如下图所示：

![解决方案窗口中的未提交文件](media/ide-tour-image23.png)

有关在 Visual Studio 中使用版本控制的详细信息，请参阅[版本控制](./version-control.md)一文。

::: moniker-end

## <a name="next-steps"></a>后续步骤

- [安装 Visual Studio for Mac](installation.md)
- [查看可用工作负载](workloads.md)

## <a name="related-video"></a>相关视频

> [!Video https://docs.microsoft.com/shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Overview/player]

## <a name="see-also"></a>请参阅

- [Visual Studio IDE (Windows)](/visualstudio/ide/visual-studio-ide)