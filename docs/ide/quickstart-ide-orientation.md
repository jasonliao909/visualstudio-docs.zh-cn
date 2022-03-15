---
title: 教程：IDE Visual Studio教程
description: 了解 Visual Studio 集成开发环境 (IDE) 的一些窗口、菜单和其他 UI 功能。
ms.custom: vs-acquisition
titleSuffix: ''
ms.date: 09/14/2021
ms.topic: quickstart
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: cbc802600be4a528ca10bf3bcfa95a0bd6d9bae1
ms.sourcegitcommit: 5b2c3a2c5f22e0cd6d35aab6049c1f61c4916e74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2022
ms.locfileid: "139852662"
---
# <a name="tutorial-first-look-at-the-visual-studio-ide"></a>教程：首先查看 Visual Studio IDE

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，我们将介绍一些窗口、菜单和其他 UI 功能。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

::: moniker range="vs-2017"

## <a name="start-page"></a>起始页

打开 Visual Studio 之后你最先看到的很可能就是起始页  。 起始页设计成一个“中心”，可帮助你更快地找到所需的命令和项目文件  。 “最新动态”部分显示你最近处理的项目和文件夹。 在“新建项目”下，可以单击链接转到“新建项目”对话框中，或在“打开”下，可以打开现有代码项目或文件夹  。 右侧是最新的开发人员新闻源。

![Visual Studio 2017 中“起始页”的屏幕截图。](media/start-page.png)

如果关闭“起始页”并希望再次查看，则可以从“文件”菜单重新打开它 。

![Visual Studio 2017 中“文件”菜单的屏幕截图。](media/quickstart-IDE-file-menu-large.png)

::: moniker-end

::: moniker range="vs-2019"

## <a name="start-window"></a>启动窗口

打开 Visual Studio 之后你最先看到的是“启动”窗口。 启动窗口旨在帮助你更快地“编码”。 它具有以下选项：克隆或签出代码、打开现有项目或解决方案、创建新项目或只打开包含一些代码文件的文件夹。

[![Visual Studio 2019 中“启动”窗口的屏幕截图。](media/vs-2019/start-window-labeled.png)](media/vs-2019/start-window-labeled.png#lightbox)

如果首次使用 Visual Studio，最近的项目列表将为空。

如果使用基于非 MSBuild 的代码库，则将使用“打开本地文件夹”选项在 Visual Studio 中打开代码。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](develop-code-in-visual-studio-without-projects-or-solutions.md)。 否则，可以从源提供程序（如 GitHub 或 Azure DevOps）创建新项目或克隆项目。

“无需代码，即可继续”选项仅打开 Visual Studio 开发环境，而不加载任何特定项目或代码。 可以选择此选项，加入 [Live Share](/visualstudio/liveshare/) 会话或附加到进程以进行调试。 此外可以按“Esc”关闭启动窗口，然后打开 IDE  。

::: moniker-end

::: moniker range=">=vs-2022"

## <a name="start-window"></a>启动窗口

打开 Visual Studio 之后你最先看到的是“启动”窗口。 启动窗口旨在帮助你更快地“编码”。 它具有以下选项：克隆或签出代码、打开现有项目或解决方案、创建新项目或只打开具有一些代码文件的文件夹。

:::image type="content" source="media/vs-2022/quickstart-start-window-labeled.png" border="true" alt-text="带批注的屏幕截图，其中显示了 Visual Studio 2022 中的“启动”窗口。" lightbox="media/vs-2022/quickstart-start-window-labeled.png":::

如果首次使用 Visual Studio，最近的项目列表将为空。

如果处理不使用 MSBuild 的代码库，则将使用“打开本地文件夹”选项在 Visual Studio 中打开代码。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](develop-code-in-visual-studio-without-projects-or-solutions.md)。 否则，可以从源提供程序（如 GitHub 或 Azure DevOps）创建新项目或克隆项目。

“继续但无需代码”选项打开 Visual Studio 开发环境，而不加载任何特定项目或代码。 可以选择此选项，加入 [Live Share](/visualstudio/liveshare/) 会话或附加到进程以进行调试。 此外可以按“Esc”关闭启动窗口，然后打开 IDE  。

::: moniker-end

## <a name="create-a-project"></a>创建项目

为继续了解 Visual Studio 的功能，我们将创建一个新项目。

::: moniker range="vs-2017"

1. 在“起始页”上“新建项目”下的搜索框中，键入 console ，以筛选项目类型列表，仅显示名称中包含“console”的项目类型    。

   ![显示 Visual Studio 2017 中的“起始页”上项目模板列表的屏幕截图。](media/start-page-search-templates.png)

   Visual Studio 提供了各种类型的项目模板，帮助你快速开始编写代码。 选择 C#“控制台应用(.NET Core)”项目模板  。 （或者，如果你是 Visual Basic、C++、JavaScript 或其他语言开发人员，请随意使用其中一种语言创建项目。 对于所有编程语言而言，我们将查看的 UI 都是相似的。）

1. 在显示的“新建项目”对话框中，接受默认的项目名称并选择“确定”   。

创建项目，并在“编辑器”窗口中打开名为 Program.cs 的文件   。 “编辑器”可显示文件的内容，是你在 Visual Studio 中完成大部分编码工作的地方  。

![显示 Visual Studio 2017 中的编辑器的屏幕截图。](media/editor.png)

::: moniker-end

::: moniker range="vs-2019"

1. 在“开始”窗口上，选择“创建新项目”  。

    :::image type="content" source="../get-started/media/vs-2019/start-window-create-new-project.png" alt-text="Visual Studio 2019 中“创建新项目”窗口的屏幕截图。":::

   随即打开“创建新项目”窗口，并显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

   通过此对话框，可搜索、筛选和选择项目模板。 它还会显示最近使用的项目模板的列表。

1. 在顶部的搜索框中，键入“console”，以筛选项目类型列表，仅显示名称中包含“console”的项目类型  。 通过从“所有语言”下拉列表中选取“C#”（或你选择的其他语言）来进一步细化搜索结果。

    :::image type="content" source="media/vs-2019/create-new-project.png" alt-text="Visual Studio 2019 中“创建新项目”窗口的屏幕截图，你可以在该窗口中选择所需的模板。":::

1. 如果已选择 C#、Visual Basic 或 F# 作为你的语言，请选择“控制台应用程序”模板，然后选择“下一步” 。 （如果已选择其他语言，只需选择任意模板。 对于所有编程语言而言，我们将查看的 UI 都是相似的。）

1. 在“配置新项目”窗口上，接受默认的项目名称和位置，然后选择“下一步”。

    :::image type="content" source="media/vs-2019/configure-new-project-console.png" alt-text="Visual Studio 2019 中“配置新项目”窗口的屏幕截图，你可在该窗口中输入项目的名称。":::

1. 在“附加信息”窗口中，验证“目标框架”下拉菜单中是否显示“.NET Core 3.1”，然后单击“创建”。

    :::image type="content" source="../get-started/media/vs-2019/create-project-additional-info.png" alt-text="Visual Studio 2019 中“附加信息”窗口的屏幕截图，你可在该窗口中选择所需的 .NET Core Framework 版本。":::

创建项目，并在“编辑器”窗口中打开名为 Program.cs 的文件   。 “编辑器”可显示文件的内容，是你在 Visual Studio 中完成大部分编码工作的地方  。

![显示 Visual Studio 2019 中的“编辑器”窗口的屏幕截图。](media/editor.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“开始”窗口上，选择“创建新项目”  。

    :::image type="content" source="media/vs-2022/start-window-create-new-project.png" alt-text="Visual Studio 2022 中“创建新项目”窗口的屏幕截图。":::

   随即打开“创建新项目”窗口，并显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

   通过此对话框，可搜索、筛选和选择项目模板。 “创建新项目”窗口还会显示最近使用的项目模板的列表。

1. 在顶部的搜索框中，键入“console”，以筛选项目类型列表，仅显示名称中包含“console”的项目类型  。 通过从“所有语言”下拉列表中选取“C#”（或你选择的其他语言）来进一步细化搜索结果。

    :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="Visual Studio 2022 中“创建新项目”窗口的屏幕截图，你可以在该窗口中选择所需的模板。":::

1. 如果已选择 C#、Visual Basic 或 F# 作为你的语言，请选择“控制台应用程序”模板，然后选择“下一步” 。 如果已选择其他语言，只需选择任意模板。

1. 在“配置新项目”窗口上，接受默认的项目名称和位置，然后选择“下一步”。

    :::image type="content" source="media/vs-2022/quickstart-configure-new-project-console.png" alt-text="Visual Studio 2022 中“配置新项目”窗口的屏幕截图，你可在该窗口中输入项目的名称。":::

1. 在“其他信息”窗口中，确保“框架”下拉菜单中显示“.NET 6.0”，然后选择“创建”   。

    :::image type="content" source="media/vs-2022/create-project-additional-info.png" alt-text="Visual Studio 2022 中“附加信息”窗口的屏幕截图，你可在该窗口中选择所需的 .NET 版本。":::

1. 项目已创建。 在“解决方案资源管理器”窗口中选择代码文件“Program.cs”，该窗口通常位于 Visual Studio 的右侧。

    :::image type="content" source="media/vs-2022/quickstart-opened-new-project.png" alt-text="Visual Studio 2022 中新 C# 控制台项目的屏幕截图。":::

“编辑器”窗口中的文件“Program.cs”打开。 “编辑器”可显示文件的内容，是你在 Visual Studio 中完成大部分编码工作的地方  。

:::image type="content" source="media/vs-2022/editor.png" alt-text="Visual Studio 2022 中“编辑器”的屏幕截图。":::

::: moniker-end

## <a name="solution-explorer"></a>“解决方案资源管理器”

::: moniker range="<=vs-2019"

“解决方案资源管理器”（通常位于 Visual Studio 的右侧）可以显示项目、解决方案或代码文件夹中文件和文件夹层次结构的图形表示形式。 你可以浏览层次结构，并导航到“解决方案资源管理器”中的某个文件。

![显示 Visual Studio 中的解决方案资源管理器的屏幕截图。](media/quickstart-IDE-solution-explorer.png)

::: moniker-end

::: moniker range=">=vs-2022"

“解决方案资源管理器”可以显示项目、解决方案或代码文件夹中的文件和文件夹层次结构的图形表示。 你可以浏览层次结构并选择要在“编辑器”中打开的文件。

:::image type="content" source="media/vs-2022/quickstart-ide-solution-explorer.png" alt-text="Visual Studio 2022 中“解决方案资源管理器”的屏幕截图。":::

::: moniker-end

## <a name="menus"></a>菜单

Visual Studio 顶部的菜单栏将命令分组成不同的类别。 例如，“项目”菜单包含与你正在处理的项目相关的命令。 在“工具”菜单上，可通过选择“选项”自定义 Visual Studio 的行为方式，或选择“获取工具和功能”向安装程序添加功能    。

::: moniker range="vs-2017"

![显示 Visual Studio 2017 中的“菜单”栏的屏幕截图。](media/quickstart-IDE-menu-bar.png)

::: moniker-end

::: moniker range="vs-2019"

![显示 Visual Studio 2019 中的“菜单”栏的屏幕截图。](media/vs-2019/menu-bar.png)

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/menu-bar.png" alt-text="Visual Studio 2022 中“菜单”栏的屏幕截图。":::

::: moniker-end

## <a name="error-list"></a>错误列表

“错误列表”显示错误、警告以及有关当前代码状态的消息。 如果文件中或项目的任何地方出现错误（例如缺少括号或分号），则会在此处列出。

要打开“错误列表”窗口，请依次选择“视图”菜单和“错误列表”  。

::: moniker range="<=vs-2019"

:::image type="content" source="media/quickstart-IDE-error-list.png" alt-text="Visual Studio 2019 中“错误列表”的屏幕截图。":::

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/quickstart-ide-error-list.png" alt-text="Visual Studio 2022 中“错误列表”的屏幕截图。":::

::: moniker-end

## <a name="output-window"></a>“输出”窗口

“输出”窗口显示生成项目和源代码管理提供程序中的输出消息。

让我们生成该项目来查看一些生成输出。 从 **“生成”** 菜单中选择 **“生成解决方案”** 。 “输出”窗口自动获得焦点并显示成功生成的消息。

::: moniker range="<=vs-2019"

![Visual Studio 中“输出”窗口的屏幕截图。](media/build-output-minimal.png)

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/quickstart-build-output-minimal.png" alt-text="Visual Studio 2022 中“输出”窗口的屏幕截图。":::

::: moniker-end

## <a name="search-box"></a>搜索框

搜索框是在 Visual Studio 中查找几乎所有内容的快捷方式。 你可以输入一些与你想要执行的操作相关的文本，它会为你显示一个与文本相关的选项列表。 例如，假设要增加生成输出的详细程度，以显示有关生成内容的更多详细信息。 具体操作如下：

::: moniker range="vs-2017"

1. 找到 IDE 右上方的“快速启动”  搜索框。 （或者，通过按 Ctrl+Q 访问该搜索框。）

1. 在搜索框中键入“详细信息”  。 从显示的结果中，选择“选项”类别下的“项目和解决方案”->“生成并运行”   。

   ![Visual Studio 2017 中“快速启动”搜索框的屏幕截图。](media/quickstart-IDE-quick-launch.png)

   “选项”对话框打开，会显示“生成并运行”选项页。  

1. 在“MSBuild 项目生成输出详细信息”下，选择“常规”，然后单击“确定”。   

1. 通过右键单击“解决方案资源管理器”中的“ConsoleApp1”项目，然后从上下文菜单中选择“重新生成”，重新生成项目    。

   这次“输出”窗口显示了生成过程中更详细的日志记录，包括在哪里复制哪些文件  。

   ![Visual Studio 2017 中“输出”窗口内更详细生成日志的屏幕截图。](media/build-output-verbose.png)

::: moniker-end

::: moniker range="vs-2019"

1. 按 Ctrl+Q 激活 IDE 上半部分中的搜索框。

1. 在搜索框中键入“详细信息”  。 从显示的结果中，选择“更改 MSBuild 详细信息”  。

   ![Visual Studio 2019 中“搜索”框的屏幕截图。](media/vs-2019/quick-launch-verbosity.png)

   “选项”对话框打开，会显示“生成并运行”选项页。  

1. 在“MSBuild 项目生成输出详细信息”下，选择“常规”，然后单击“确定”。   

1. 通过右键单击“解决方案资源管理器”中的“ConsoleApp1”项目，然后从上下文菜单中选择“重新生成”，重新生成项目    。

   这次“输出”窗口显示了生成过程中更详细的日志记录，包括在哪里复制哪些文件  。

   ![Visual Studio 2019 中“输出”窗口内更详细生成日志的屏幕截图。](media/build-output-verbose.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 按 Ctrl+Q 激活 IDE 上半部分中的搜索框。

1. 在搜索框中键入“详细信息”  。 从显示的结果中，选择“更改 MSBuild 详细信息”  。

   :::image type="content" source="media/vs-2022/quickstart-search-verbosity.png" alt-text="Visual Studio 2022 中“搜索”框的屏幕截图。":::

   “选项”对话框打开，会显示“生成并运行”选项页。  

1. 在“MSBuild 项目生成输出详细信息”下，选择“常规”，然后选择“确定”。  

1. 通过右键单击“解决方案资源管理器”中的“ConsoleApp1”项目，然后从上下文菜单中选择“重新生成”，重新生成项目    。

   这次“输出”窗口显示了生成过程中更详细的日志记录，包括在哪里复制哪些文件  。

   :::image type="content" source="media/vs-2022/quickstart-build-output-verbose.png" alt-text="Visual Studio 2022 中“输出”窗口内更详细生成日志的屏幕截图。":::

::: moniker-end

## <a name="send-feedback-menu"></a>“发送反馈”菜单

::: moniker range="vs-2017"

如果在使用 Visual Studio 时遇到任何问题，或者有关于如何改进产品的建议，请使用 Visual Studio 窗口顶部附近的“发送反馈”  菜单。

![Visual Studio 2017 中“发送反馈”菜单的屏幕截图。](media/quickstart-IDE-send-feedback.png)

::: moniker-end

::: moniker range="vs-2019"

如果在使用 Visual Studio 时遇到任何问题，或者有关于如何改进产品的建议，请使用 Visual Studio 窗口顶部附近的“发送反馈”  菜单。

![Visual Studio 2019 中“发送反馈”菜单的屏幕截图。](media/vs-2019/send-feedback-menu.png)

::: moniker-end

::: moniker range=">=vs-2022"

如果在使用 Visual Studio 时遇到任何问题，或者有关于如何改进产品的建议，请告知我们。 为此，请选择 IDE 右上角附近的“发送反馈”按钮，并使用“发送反馈”菜单中的反馈选项之一。

:::image type="content" source="media/vs-2022/quickstart-ide-send-feedback.png" alt-text="Visual Studio 2022 中“发送反馈”按钮和菜单的屏幕截图。":::

::: moniker-end

## <a name="next-steps"></a>后续步骤

我们只介绍了 Visual Studio 的一些功能以便熟悉用户界面。 若要进一步了解，请继续：

> [!div class="nextstepaction"]
> [了解代码编辑器](../get-started/tutorial-editor.md)

> [!div class="nextstepaction"]
> [了解项目和解决方案](../get-started/tutorial-projects-solutions.md)

## <a name="see-also"></a>另请参阅

- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)
- [Visual Studio 的更多功能](../ide/advanced-feature-overview.md)
- [更改主题和字体颜色](../ide/quickstart-personalize-the-ide.md)
