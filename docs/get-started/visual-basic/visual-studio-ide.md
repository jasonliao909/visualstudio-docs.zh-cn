---
title: 面向 Visual Basic 开发人员的概述
description: 了解 Visual Basic 开发人员如何使用 Visual Basic 编辑、调试和生成代码以及如何发布应用。
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: conceptual
author: anandmeg
ms.author: meghaanand
manager: jmartens
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: f2868a4a86f1ce70fbaf9f94bf1c5f3971b45c59
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429791"
---
# <a name="welcome-to-the-visual-studio-ide--visual-basic"></a>欢迎使用 Visual Studio IDE | Visual Basic

集成开发环境 (IDE) 是一个功能丰富的程序，支持软件开发的许多方面。 Visual Studio IDE 是一种创新启动板，可用于编辑、调试并生成代码，然后发布应用。 除了大多数 IDE 提供的标准编辑器和调试器之外，Visual Studio 还包括编译器、代码完成工具、图形设计器和许多其他功能，以加强软件开发过程。

::: moniker range="vs-2017"

![包含 Visual Basic 代码的 Visual Studio 2017 IDE 的屏幕截图。](../media/visual-studio-ide.png)

::: moniker-end

::: moniker range="vs-2019"

[![包含 Visual Basic 代码的 Visual Studio 2019 IDE 的屏幕截图。](media/vs-2019/ide-overview.png)](media/vs-2019/ide-overview.png#lightbox)

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/ide-overview.png" alt-text="包含 Visual Basic 代码和关键功能的 Visual Studio IDE 的屏幕截图。" lightbox="media/vs-2022/ide-overview.png" border="false":::

::: moniker-end

上图显示了 Visual Studio 和一个打开的 Visual Basic 项目，其中显示了关键窗口及其功能：

- 在[“解决方案资源管理器”](../../ide/solutions-and-projects-in-visual-studio.md)右上角，可以查看、导航和管理代码文件。 解决方案资源管理器可将代码文件分组为[解决方案和项目](tutorial-projects-solutions.md)，从而帮助整理代码  。

- 中心[编辑器窗口](../../ide/writing-code-in-the-code-and-text-editor.md)用于显示文件内容，你的大部分时间可能都是在此窗口中度过的。 在编辑窗口中，可以编辑代码或设计用户界面，例如带有按钮和文本框的窗口。

::: moniker range="vs-2017"

- [“输出”窗口](../../ide/reference/output-window.md)（底部中心）是 Visual Studio 发送通知（例如，调试和错误消息、编译器警告、发布状态消息等）的位置。 每个消息源都有自己的选项卡。

::: moniker-end

::: moniker range="<=vs-2019"
- 在右下方的[团队资源管理器](/azure/devops/user-guide/work-team-explorer?view=vsts&preserve-view=true)中，可以使用 [Git](https://git-scm.com/) 和 [Team Foundation 版本控制 (TFVC)](/azure/devops/repos/tfvc/overview?view=vsts&preserve-view=true) 等版本控制技术来跟踪工作项和共享代码。
::: moniker-end

::: moniker range=">=vs-2022"
- 在 [Git 更改](/visualstudio/version-control/)右下方，可使用版本控制技术（如 [Git](https://git-scm.com/) 和 [GitHub](https://docs.github.com/github)）跟踪工作项并与他人共享代码。
::: moniker-end

## <a name="editions"></a>版本

Visual Studio 适用于 Windows 和 Mac。 [Visual Studio for Mac](/visualstudio/mac/) 的许多功能与 Visual Studio for Windows 相同，并针对开发跨平台应用和移动应用进行了优化。 本文重点介绍 Visual Studio 的 Windows 版本。

Visual Studio 有三个版本：社区版、专业版和企业版。 请参阅[比较 Visual Studio 版本](https://visualstudio.microsoft.com/vs/compare/)，了解各个版本支持的功能。

## <a name="popular-productivity-features"></a>高效性方面的常用功能

开发软件时，Visual Studio 可帮助提高工作效率的一些常用功能包括：

- 波形曲线和[快速操作](../../ide/quick-actions.md)

  波形曲线是波浪形下划线，它可以在键入时对代码中的错误或潜在问题发出警报。 这些视觉线索可帮助你立即解决问题，而无需等待在生成或运行时发现错误。 如果将鼠标悬停在波形曲线上，将看到关于此错误的更多信息。 灯泡也可能显示在左边距中，其中显示可采取以修复错误的快速操作。

   ::: moniker range="vs-2017"

   ![Visual Studio 中的波形下划线的屏幕截图。](media/squiggles-error.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![Visual Studio 中的波形下划线的屏幕截图。](media/vs-2019/squiggles-error.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/squiggles-error.png" alt-text="Visual Studio 中的波形下划线的屏幕截图。" border="false":::

   ::: moniker-end

- [重构](../../ide/refactoring-in-visual-studio.md)

   重构包括智能重命名变量、将一个或多个代码行提取到新方法中和更改方法参数的顺序。

   ::: moniker range="vs-2017"

   ![Visual Studio 中的“重构”菜单的屏幕截图。](media/refactoring-menu.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![Visual Studio 中的“重构”菜单的屏幕截图。](media/vs-2019/refactorings-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/refactoring-menu.png" alt-text="Visual Studio 中的“重构”菜单的屏幕截图。" border="false":::

   ::: moniker-end

- [IntelliSense](../../ide/using-intellisense.md)

   IntelliSense 是一组功能，可用于在编辑器中直接显示代码的信息，并且可在某些情况下编写小段代码。 如同在编辑器中拥有了基本文档内联，从而无需在其他位置查看类型信息。

   下图显示了 IntelliSense 如何显示类型的成员列表：

   ::: moniker range="vs-2017"

   ![IntelliSense 成员列表的屏幕截图。](media/intellisense-list-members.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![IntelliSense 成员列表的屏幕截图。](media/vs-2019/intellisense-list-members.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/intellisense.png" alt-text="IntelliSense 成员列表的屏幕截图。" border="false":::

   ::: moniker-end

   IntelliSense 功能因语言而异。 有关详细信息，请参阅 [C# IntelliSense](../../ide/visual-csharp-intellisense.md)、[Visual C++ IntelliSense](../../ide/visual-cpp-intellisense.md)、[JavaScript IntelliSense](../../ide/javascript-intellisense.md) 和 [Visual Basic IntelliSense](../../ide/visual-basic-specific-intellisense.md)。

- [Visual Studio 搜索](../../ide/visual-studio-search.md)

   Visual Studio 菜单、选项和属性有时可能会让人不知所措。 Visual Studio 搜索或 Ctrl+Q 是在同一位置快速查找 IDE 功能和代码的绝佳方法。

   开始键入要查找内容的名称时，Visual Studio 会列出结果，这些结果可将你转到所需的位置。 如果需要添加功能（例如，添加另一种编程语言），可以从搜索框结果中打开 Visual Studio 安装程序以安装工作负载或组件。

   ::: moniker range="vs-2017"

   ![显示 Visual Studio 2017 中“快速启动”搜索框的屏幕截图。](../media/quick-launch-nuget.png)

   有关详细信息，请参阅[快速启动](../../ide/reference/quick-launch-environment-options-dialog-box.md)。

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![显示 Visual Studio 2019 中“快速启动”搜索框的屏幕截图。](../media/vs-2019/quick-launch-nuget.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/quick-launch-nuget.png" alt-text="显示 Visual Studio 中“快速启动”搜索框的屏幕截图。" border="false":::

   ::: moniker-end

- [Live Share](/visualstudio/liveshare/)

   与他人实时协作编辑和调试，无需考虑应用类型或编程语言。 可以立即安全地共享项目。 还可以共享调试会话、终端实例、localhost Web 应用、语音呼叫等等。

- [调用层次结构](../../ide/reference/call-hierarchy.md)

   “调用层次结构”窗口显示调用所选方法的方法。 考虑更改或删除方法时，或者尝试追踪 bug 时，这可能是有用的信息。

   ::: moniker range="vs-2017"

   ![显示 Visual Studio中“调用层次结构”窗口的屏幕截图。](media/call-hierarchy.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![显示 Visual Studio中“调用层次结构”窗口的屏幕截图。](media/vs-2019/call-hierarchy.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/call-hierarchy.png" alt-text="显示 Visual Studio中“调用层次结构”窗口的屏幕截图。" border="false":::

   ::: moniker-end

- [CodeLens](../../ide/find-code-changes-and-other-history-with-codelens.md)

   CodeLens 可帮助查找代码引用、代码更改、链接错误、工作项、代码评审和单元测试，所有操作都在编辑器上进行。

   ::: moniker range="vs-2017"

   ![显示 Visual Studio 中的 CodeLens 的屏幕截图。](media/codelens.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![显示 Visual Studio 中的 CodeLens 的屏幕截图。](media/vs-2019/codelens.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/codelens.png" alt-text="显示 Visual Studio 中的 CodeLens 的屏幕截图。" border="false":::

   ::: moniker-end

- [转到定义](../../ide/go-to-and-peek-definition.md)

   “转到定义”功能可将你直接带到函数或类型定义的位置。

   ::: moniker range="vs-2017"

   ![显示 Visual Studio 2017 中“转到定义”的屏幕截图。](media/go-to-definition-menu.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![显示 Visual Studio 2019 中“转到定义”的屏幕截图。](media/vs-2019/go-to-definition-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/go-to-definition-menu.png" alt-text="显示 Visual Studio 中“转到定义”的屏幕截图。" border="false":::

   ::: moniker-end

- [查看定义](../../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)

   “速览定义”窗口显示方法或类型定义，而无需打开一个单独的文件。

   ::: moniker range="vs-2017"

   ![显示 Visual Studio 中“速览定义”的屏幕截图。](media/peek-definition.png)

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![显示 Visual Studio 中“速览定义”的屏幕截图。](media/vs-2019/peek-definition.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/peek-definition.png" alt-text="显示 Visual Studio 中“速览定义”的屏幕截图。" border="false":::

   ::: moniker-end

## <a name="install-visual-studio"></a>安装 Visual Studio

在本部分中，你将创建一个简单的项目来尝试可在 Visual Studio 中执行的一些操作。 你将了解如何更改颜色主题，使用 [IntelliSense](../../ide/using-intellisense.md) 作为编码助手，以及调试应用以便在应用执行期间查看变量值。

::: moniker range="vs-2017"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 并将其安装到你的系统上。 通过模块化安装程序，可以选择和安装工作负荷。工作负荷是你习惯使用的编程语言或平台所需的一些功能。 若要执行[创建程序](#create-a-program)所需的步骤，请务必在安装过程中选择“.NET Core 跨平台开发”工作负载。

![Visual Studio 安装程序中的“.NET Core 跨平台开发”工作负载的屏幕截图。](../media/dotnet-core-cross-platform-workload.png)

::: moniker-end

::: moniker range="vs-2019"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/downloads) 并将其安装到你的系统上。 通过模块化安装程序，可以选择和安装工作负载。工作负载是你习惯使用的编程语言或平台所需的一些功能。 若要执行[创建程序](#create-a-program)所需的步骤，请务必在安装过程中选择“.NET Core 跨平台开发”工作负载。

![Visual Studio 安装程序中的“.NET Core 跨平台开发”工作负载的屏幕截图。](../media/dotnet-core-cross-platform-workload.png)

::: moniker-end

::: moniker range=">=vs-2022"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/downloads) 并将其安装到你的系统上。 在模块化安装程序中，可以选择和安装工作负载。工作负载是你希望使用的编程语言或平台所需的一些功能。 若要使用以下步骤[创建程序](#create-a-program)，请确保在安装过程中选择“.NET 桌面开发”工作负载。

:::image type="content" source="media/vs-2022/dot-net-development-workload.png" alt-text="在 Visual Studio 安装程序中选择的“.NET 桌面开发”工作负载的屏幕截图。" border="false":::

::: moniker-end

首次打开 Visual Studio 时，可使用 Microsoft 帐户或者单位或学校帐户[登录](../../ide/signing-in-to-visual-studio.md)。

## <a name="customize-visual-studio"></a>自定义 Visual Studio

可个性化设置 Visual Studio 用户界面，包括更改默认颜色主题。

### <a name="change-the-color-theme"></a>更改颜色主题

若要更改颜色主题：

::: moniker range="vs-2017"

1. 打开 Visual Studio。

1. 在菜单栏中，选择“工具”>“选项”，打开“选项”对话框。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“深色”，然后单击“确定”    。

   ![显示在 Visual Studio 中将颜色主题更改为“深色”的屏幕截图。](media/change-color-theme.png)

   此时，整个 IDE 的颜色主题更改为“深色”。

   ![显示深色主题 Visual Studio 的屏幕截图。](../../ide/media/quickstart-personalize-dark-theme.png)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。 在“开始”窗口中，选择“继续但无需代码”。

   :::image type="content" source="media/vs-2019/continue-without-code.png" alt-text="Visual Studio 2019 中“开始”窗口的屏幕截图，突出显示了“继续但无需代码”链接。":::

   IDE 将随即打开。

1. 在 Visual Studio 菜单栏中，选择“工具”>“选项”打开“选项”对话框  。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“深色”，然后选择“确定”    。

   ![显示在 Visual Studio 中将颜色主题更改为“深色”的屏幕截图。](media/change-color-theme.png)

   此时，整个 IDE 的颜色主题更改为“深色”。

   ![显示深色主题 Visual Studio 的屏幕截图。](../media/vs-2019/dark-theme.png)

::: moniker-end

::: moniker range=">=vs-2022"
1. 打开 Visual Studio。 在“开始”窗口中，选择“继续但无需代码”。

   :::image type="content" source="media/vs-2022/continue-without-code.png" alt-text="Visual Studio“开始”屏幕的屏幕截图，其中突出显示了“继续但无需代码”链接。" border="false":::

1. 在 Visual Studio 菜单栏中，选择“工具”>“选项”打开“选项”对话框  。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“蓝色”或“浅色”，然后选择“确定”。

   :::image type="content" source="media/vs-2022//change-color-theme.png" alt-text="显示在 Visual Studio 中将颜色主题更改为“蓝色”的屏幕截图。":::

   此时，整个 IDE 的颜色主题也会相应地更改。 以下屏幕截图显示“蓝色”主题：

   :::image type="content" source="media/vs-2022/blue-theme.png" alt-text="显示“蓝色”主题 Visual Studio 的屏幕截图。":::
::: moniker-end

### <a name="select-environment-settings"></a>选择环境设置

可将 Visual Studio 配置为使用专为 Visual Basic 开发人员定制的环境设置。

1. 在菜单栏上，选择“工具” > “导入和导出设置” 。

1. 在“导入和导出设置向导”中，选择“重置所有设置”，然后选择“下一步”。

1. 在“保存当前设置”页上，选择是否在重置之前保存当前设置。 如果尚未自定义任何设置，请选择“不，只重置设置，同时覆盖我的当前设置”。 然后，选择“下一步”  。

1. 在“选择一个默认设置集合”页上，依次选择“Visual Basic”和“完成”  。

1. 在“重置完成”页上，选择“关闭”。

若要了解有关 IDE 个性化设置的其他方法，请参阅[个性化设置 Visual Studio](../../ide/personalizing-the-visual-studio-ide.md)。

## <a name="create-a-program"></a>创建程序

深入了解并创建一个简单的程序。

::: moniker range="vs-2017"

1. 在 Visual Studio 菜单栏上，依次选择“文件”“新建项目” > 。

   ![显示菜单栏上的“文件”>“新建项目”的屏幕截图。](media/file-new-project-menu.png)

   “新建项目”对话框中会显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

1. 依次选择“Visual Basic”下的“.NET Core”类别和“控制台应用(.NET Core)”模板。 在“名称”文本框中，键入“HelloWorld”，然后选择“确定”按钮。

   ![显示 .NET Core 应用模板的屏幕截图。](media/overview-npd.png)

   > [!NOTE]
   > 如果未看到“.NET Core”类别，则需要安装“.NET Core 跨平台开发”工作负载。 为此，选择“新建项目”对话框左下角的“打开 Visual Studio 安装程序”链接。 “Visual Studio 安装程序”打开后，向下滚动并选择“.NET Core 跨平台开发”工作负载，然后选择“修改”。

   Visual Studio 随即创建项目。 它是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。

   稍后，将看到类似于以下的内容：

   ![显示 Visual Studio Code IDE 的屏幕截图。](media/overview-ide-console-app.png)

   应用的 Visual Basic 代码会显示在编辑窗口中，占据大部分空间。 请注意，文本已自动着色，用于指示代码的不同方面，如关键字或类型。 此外，代码中的垂直短虚线指示哪两个大括号相匹配，行号能够帮助你在以后查找代码。 可以通过选择带减号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要的代码，最大程度地减少屏幕混乱。 右侧名为“解决方案资源管理器”的窗口中列出了项目文件。

   ![显示带红色框的 Visual Studio IDE 的屏幕截图。](media/overview-ide-console-app-red-boxes.png)

   还提供了一些其他的菜单和工具窗口，但是现在我们继续下一步操作。

1. 现在启动该应用。 可从菜单栏的“调试”菜单中选择“开始执行(不调试)”，以执行此操作。 还可按 Ctrl+F5 。

   ![显示“调试”>“开始执行(不调试)”的屏幕截图。](../media/overview-start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”。 现在你拥有了一个正在运行的应用！

   ![显示控制台窗口的屏幕截图。](../media/overview-console-window.png)

1. 要关闭控制台窗口，请在键盘上按任意键。

1. 接下来，向应用添加一些附加代码。 在 `Console.WriteLine("Hello World!")` 行前面添加以下 Visual Basic 代码：

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本并按 Enter 键。

1. 将显示 `Console.WriteLine("Hello World!")` 的行更改为以下代码：

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. 按“Ctrl+F5”，以重新运行应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中输入姓名，并按 Enter。

   ![显示控制台窗口输入的屏幕截图。](../media/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

::: moniker range="vs-2019"

1. 在 Visual Studio 菜单栏上，选择“文件” > “新建” > “项目”。 （或者，按 Ctrl+**Shift**+N。）

    :::image type="content" source="media/vs-2019/file-new-project.png" alt-text="Visual Studio 2019 菜单栏中“文件”>“新建”>“项目选择”的屏幕截图。":::

   随即打开“创建新项目”窗口，并显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

1. 若要查找所需的模板，请在搜索框中键入或输入“.Net Core 控制台”。 系统会自动根据输入的关键字筛选可用模板列表。 可以通过从“所有语言”下拉列表中选择“Visual Basic”、从“所有平台”列表中选择“Windows”以及从“所有项目类型”列表中选择“控制台”进一步筛选模板结果     。

   选择“控制台应用程序”模板，然后单击“下一步” 。

    :::image type="content" source="media/vs-2019/create-new-project.png" alt-text="Visual Studio 2019 中“创建新项目”窗口的屏幕截图，你可以在该窗口中选择所需的模板。":::

1. 在“配置新项目”窗口中，在“项目名称”框中输入“HelloWorld”，可以选择更改项目文件的目录位置（默认位置为 `C:\Users\<name>\source\repos`），然后单击“下一步”。

    :::image type="content" source="media/vs-2019/configure-new-project.png" alt-text="Visual Studio 2019 中“配置新项目”窗口的屏幕截图，你可在该窗口中输入项目的名称。":::

1. 在“附加信息”窗口中，验证“目标框架”下拉菜单中是否显示“.NET Core 3.1”，然后单击“创建”。

    :::image type="content" source="media/vs-2019/create-project-additional-info.png" alt-text="Visual Studio 2019 中“附加信息”窗口的屏幕截图，你可在该窗口中选择所需的 .NET Core Framework 版本。":::

   Visual Studio 随即创建项目。 它是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。

   稍后，将看到类似于以下的内容：

   ![显示 Visual Studio Code IDE 的屏幕截图。](media/overview-ide-console-app.png)

   应用的 Visual Basic 代码会显示在编辑窗口中，占据大部分空间。 请注意，文本已自动着色，用于指示代码的不同方面，如关键字或类型。 此外，代码中的垂直短虚线指示哪两个大括号相匹配，行号能够帮助你在以后查找代码。 可以通过选择带减号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要的代码，最大程度地减少屏幕混乱。 右侧名为“解决方案资源管理器”的窗口中列出了项目文件。

   ![显示带红色框的 Visual Studio IDE 的屏幕截图。](media/overview-ide-console-app-red-boxes.png)

   还提供了一些其他的菜单和工具窗口，但是现在我们继续下一步操作。

1. 现在启动该应用。 可从菜单栏的“调试”菜单中选择“开始执行(不调试)”，以执行此操作。 还可按 Ctrl+F5 。

   ![显示“调试”>“开始执行(不调试)”的屏幕截图。](media/vs-2019/start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”。 现在你拥有了一个正在运行的应用！

   ![控制台窗口的屏幕截图，其中显示 Hello World 消息。](../media/vs-2019/overview-console-window.png)

1. 要关闭控制台窗口，请在键盘上按任意键。

1. 接下来，向应用添加一些附加代码。 在 `Console.WriteLine("Hello World!")` 行前面添加以下 Visual Basic 代码：

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本并按 Enter 键。

1. 将显示 `Console.WriteLine("Hello World!")` 的行更改为以下代码：

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. 按“Ctrl+F5”，以重新运行应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中输入姓名，并按 Enter。

   ![控制台窗口的屏幕截图，其中显示问题“你的名字是什么”以及应用的回复。](../media/vs-2019/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在 Visual Studio 菜单栏上，选择“文件” > “新建” > “项目”。 也可以按 Ctrl+Shift+N  。

   :::image type="content" source="media/vs-2022/file-new-project.png" alt-text="Visual Studio 菜单栏中“文件”>“新建”>“项目选择”的屏幕截图。" border="false":::

   随即打开“创建新项目”窗口，并显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

1. 若要查找模板，可以在搜索框中键入或输入关键字。 系统会根据输入的关键字筛选可用模板列表。 可以通过从“所有语言”下拉列表中选择“Visual Basic”、从“所有平台”列表中选择“Windows”以及从“所有项目类型”列表中选择“控制台”进一步筛选模板结果     。

   选择 Visual Basic 的“控制台应用程序”模板，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/create-project.png" alt-text="“创建新项目”窗口的屏幕截图，其中选择了 Visual Basic 的“控制台应用程序”。" border="false":::

1. 在“配置新项目”窗口中，在“项目名称”框中输入“HelloWorld”。 （可选）更改项目目录的默认位置 C:\\Users\\\<name>\\source\\repos，然后选择“下一步”。

   :::image type="content" source="media/vs-2022/configure.png" alt-text="“配置新项目”窗口的屏幕截图，其中输入了项目名称“HelloWorld”。" border="false":::

1. 在“附加信息”窗口中，验证“目标框架”下拉菜单中是否显示“.NET 6.0”，然后选择“创建”。

   :::image type="content" source="media/vs-2022/additional-information.png" alt-text="“其他信息”窗口的屏幕截图，其中选择了“.NET 6.0”。" border="false":::

   Visual Studio 随即创建项目。 该程序是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中显示 字符串“Hello, World!”。

   项目文件显示在名为“解决方案资源管理器”的窗口中 Visual Studio IDE 的右侧。 在“解决方案资源管理器”窗口中，选择“Program.vb”文件 。 应用的 Visual Basic 代码将在中心编辑器窗口中打开，占据大部分空间。

   :::image type="content" source="media/vs-2022/open-program.png" alt-text="显示 Visual Studio IDE 以及编辑器中的 Program.vb 代码的屏幕截图。" border="false":::

   代码已自动着色，用于指示不同方面，如关键字或类型。 行号可帮助你查找代码。

   代码中的垂直小虚线指示代码结构或可共存的代码块。 还可以通过选择带框的小减号或小加号来折叠或展开代码块。 此代码大纲功能可以隐藏不需要显示的代码，最大程度地减少屏幕混乱。

   :::image type="content" source="media/vs-2022/editor-features.png" alt-text="显示带红色框的 Visual Studio IDE 的屏幕截图。" border="false":::

   还提供了许多其他菜单和工具窗口。

1. 通过从 Visual Studio 顶部菜单中选择“调试” > “启动时不调用”来启动应用。 还可按 Ctrl+F5 。

   :::image type="content" source="media/vs-2022/start-without-debugging.png" alt-text="显示“调试”>“开始执行(不调试)”菜单项的屏幕截图。" border="false":::

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”。 现在你拥有了一个正在运行的应用！

   :::image type="content" source="../media/vs-2019/overview-console-window.png" alt-text="调试控制台窗口的屏幕截图，其中显示了“Hello World!”输出和“Press any key to close this window”。" border="false":::

1. 按任意键关闭控制台窗口。

1. 向应用添加一些代码。 在 `Console.WriteLine("Hello World!")` 行前面添加以下 Visual Basic 代码：

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本。

1. 将显示 `Console.WriteLine("Hello World!")` 的行更改为以下行：

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. 通过选择“调试”>“启动但不调试”或通过按 Ctrl+F5 再次运行该应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中键入姓名，并按 Enter。

   :::image type="content" source="../media/vs-2022/overview-console-input.png" alt-text="调试控制台窗口的屏幕截图，其中显示输入姓名的提示、所输入的姓名以及输出“Hello Georgette!”。" border="false":::

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

## <a name="use-refactoring-and-intellisense"></a>使用重构和 IntelliSense

让我们了解一下如何借助[重构](../../ide/refactoring-in-visual-studio.md)和[IntelliSense](../../ide/using-intellisense.md) 更有效地进行编码。

首先，重命名 `name` 变量：

1. 双击 `name` 变量，然后键入变量“username”的新名称。

   变量周围将出现一个框，且边距中会出现灯泡。

1. 选择灯泡图标，显示可用的[快速操作](../../ide/quick-actions.md)。 选择“将 'name' 重命名为 'username'”。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中的“重命名”操作的屏幕截图。](media/rename-quick-action.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022&quot;
   :::image type=&quot;content&quot; source=&quot;media/vs-2022/rename.png&quot; alt-text=&quot;显示 Visual Studio 中的“重命名”操作的屏幕截图。&quot; border=&quot;false&quot;:::
   ::: moniker-end

   该变量会在整个项目中进行重命名，本例中只有两处。

接下来了解下 IntelliSense。

1. 在 `Console.WriteLine(&quot;Hello &quot; + username + &quot;!")` 行下方，键入以下代码：

   ```vb
   Dim now = Date.
   ```
   
   此时，框中显示 <xref:System.DateTime> 类的成员。 当前所选成员的说明还会显示在单独的框中。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中的 IntelliSense 列表成员的屏幕截图。](media/intellisense-list-members.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022&quot;
   :::image type=&quot;content&quot; source=&quot;media/vs-2022/intellisense-list-members.png&quot; alt-text=&quot;显示 Visual Studio 中的 IntelliSense 列表成员的屏幕截图。&quot; border=&quot;false&quot;:::
   ::: moniker-end

1. 选择名为“Now”的成员，它是类的属性。 双击“Now”，或将其选中并按 Tab 键 。

1. 在该行下，输入以下代码行：

   ```vb
   Dim dayOfYear = now.DayOfYear
   Console.Write(&quot;Day of year: ")
   Console.WriteLine(dayOfYear)
   ```

   > [!TIP]
   > <xref:System.Console.Write%2A?displayProperty=nameWithType> 与 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 不同，它在打印后不会添加行终止符。 这意味着发送到输出的下一段文本将打印在同一行上。 将鼠标悬停在代码中的每个方法上，即可查看其说明。

接下来，再次使用重构来使代码更加简洁。

::: moniker range="<=vs-2019"
1. 在行 `Dim now = Date.Now` 中选择变量 `now`。 该行的边距中会显示一个小螺丝刀图标。

1. 选择小螺丝刀图标以查看 Visual Studio 中的可用建议。 本例显示[内联临时变量](../../ide/reference/inline-temporary-variable.md)重构，可在无需更改整体代码行为的情况下删除代码行。

   ![显示 Visual Studio 中内联临时变量建议的屏幕截图。](media/inline-temporary-variable-refactoring.png)

1. 选择“内联临时变量”以重构代码。

1. 按 Ctrl+F5 重新运行程序 。 输出的内容与以下类似：

   ![调试控制台窗口的屏幕截图，其中显示了输入姓名的提示、输入内容和输出。](../media/vs-2019/overview-console-final.png)
   ::: moniker-end

::: moniker range=">=vs-2022"
1. 在行 `Dim now = Date.Now` 中选择变量 `now`。 该行的边缘中会显示一个灯泡图标。

1. 选择灯泡图标以查看 Visual Studio 中的可用建议。 本例显示[内联临时变量](../../ide/reference/inline-temporary-variable.md)重构，可在无需更改整体代码行为的情况下删除代码行。

   :::image type="content" source="media/vs-2022/inline-temporary-variable.png" alt-text="显示 Visual Studio 中内联临时变量建议的屏幕截图。" border="false":::

1. 选择“内联临时变量”以重构代码。

1. 按 Ctrl+F5 重新运行程序 。 输出的内容与以下类似：

   :::image type="content" source="../media/vs-2022/overview-console-final.png" alt-text="调试控制台窗口的屏幕截图，其中显示了输入姓名的提示、输入内容和输出。" border="false":::
::: moniker-end

## <a name="debug-code"></a>调试代码

编写代码时，应运行并测试该代码是否存在 bug。 可通过 Visual Studio 的调试系统逐句执行代码，一次执行一条语句，逐步检查变量。 可以设置在特定行停止代码执行的断点，并观察变量值在代码运行时的变化方式。

通过设置断点，可查看程序运行时 `username` 变量的值。

1. 通过单击代码行旁边最左边距（或装订线），在代码行上设置一个断点，该断点表示 `Console.WriteLine("Hello " + username + "!")`。 也可以选择代码行，然后按 F9。

   装订线中会出现一个红色圆圈，并突出显示该行。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中代码行上的断点的屏幕截图。](media/breakpoint.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   :::image type="content" source="media/vs-2022/breakpoint.png" alt-text="显示 Visual Studio 中代码行上的断点的屏幕截图。" border="false":::
   ::: moniker-end

1. 选择“调试” > “启动调试”或按 F5，开始调试。

1. 控制台窗口出现并询问姓名时，请输入姓名。

   Visual Studio 代码编辑器重新获得焦点，有断点的代码行突出显示为黄色。 黄色突出显示表示将在下一步执行此代码行。 断点使应用在此行暂停执行。

1. 将鼠标悬停在 `username` 变量上，即可查看它的值。 也可以右键单击 `username` 并选择“添加监视”，将变量添加到“监视”窗口，这样也可查看它的值。

   ::: moniker range="<=vs-2019"
   ![在 Visual Studio 中调试过程中显示变量值的屏幕截图。](media/debugging-variable-value.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   :::image type="content" source="media/vs-2022/inspect-variable.png" alt-text="在 Visual Studio 中调试过程中显示变量值的屏幕截图。" border="false":::
   ::: moniker-end

1. 再次按 F5 以结束应用运行。

有关 Visual Studio 中调试的详细信息，请参阅[调试器功能体验](../../debugger/debugger-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

查看下述一篇介绍性的文章，进一步了解 Visual Studio：

> [!div class="nextstepaction"]
> [了解如何使用代码编辑器](tutorial-editor.md)

> [!div class="nextstepaction"]
> [了解项目和解决方案](tutorial-projects-solutions.md)

## <a name="see-also"></a>请参阅

- 发现[更多 Visual Studio 功能](../../ide/advanced-feature-overview.md)。
- 访问 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/)。
- 阅读 [Visual Studio 博客](https://devblogs.microsoft.com/visualstudio/)。
