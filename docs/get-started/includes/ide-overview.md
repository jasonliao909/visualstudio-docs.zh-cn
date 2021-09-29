---
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.custom: vs-get-started
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.topic: include
ms.openlocfilehash: d98812bdba2807038d23f43d07ea48f6d3d43bc0
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128430812"
---
集成开发环境 (IDE) 是一个功能丰富的程序，支持软件开发的许多方面。 Visual Studio IDE 是一种创新启动板，可用于编辑、调试并生成代码，然后发布应用。 除了大多数 IDE 提供的标准编辑器和调试器之外，Visual Studio 还包括编译器、代码完成工具、图形设计器和许多其他功能，以加强软件开发过程。

::: moniker range="vs-2017"

![显示 Visual Studio 2017 IDE 的屏幕截图。](../media/visual-studio-ide.png)

::: moniker-end

::: moniker range="vs-2019"

:::image type="content" source="../media/vs-2019/ide-overview.png" alt-text="Visual Studio 2019 IDE 的屏幕截图，其中包含指示关键特性和功能所在位置的标注。" lightbox="../media/vs-2019/ide-overview.png":::

::: moniker-end

::: moniker range=">=vs-2022"

[![显示 Visual Studio 2022 IDE 的屏幕截图，包含指示关键特性和功能所在位置的标注。](../media/vs-2022/ide-overview.png)](../media/vs-2022/ide-overview.png#lightbox)

::: moniker-end

上图显示了 Visual Studio 和一个打开的项目，其中显示了关键窗口及其功能：

- 在[“解决方案资源管理器”](../../ide/use-solution-explorer.md)右上角，可以查看、导航和管理代码文件。 解决方案资源管理器可将代码文件分组为[解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)，从而帮助整理代码  。

- 中心[编辑器窗口](../../ide/writing-code-in-the-code-and-text-editor.md)用于显示文件内容，你的大部分时间可能都是在此窗口中度过的。 在编辑窗口中，可以编辑代码或设计用户界面，例如带有按钮和文本框的窗口。

::: moniker range="vs-2017"

- [“输出”窗口](../../ide/reference/output-window.md)（底部中心）是 Visual Studio 发送通知（例如，调试和错误消息、编译器警告、发布状态消息等）的位置。 每个消息源都有自己的选项卡。

::: moniker-end

- 在 [Git 更改](/visualstudio/version-control/)右下方，可使用版本控制技术（如 [Git](https://git-scm.com/) 和 [GitHub](https://docs.github.com/github)）跟踪工作项并与他人共享代码。

## <a name="editions"></a>版本

Visual Studio 适用于 Windows 和 Mac。 [Visual Studio for Mac](/visualstudio/mac/) 的许多功能与 Visual Studio for Windows 相同，并针对开发跨平台应用和移动应用进行了优化。 本文重点介绍 Visual Studio 的 Windows 版本。

Visual Studio 有三个版本：社区版、专业版和企业版。 请参阅[比较 Visual Studio 版本](https://visualstudio.microsoft.com/vs/compare/)，了解各个版本支持的功能。

## <a name="popular-productivity-features"></a>高效性方面的常用功能

开发软件时，Visual Studio 可帮助提高工作效率的一些常用功能包括：

- 波形曲线和[快速操作](../../ide/quick-actions.md)

   波形曲线是波浪形下划线，它可以在键入时对代码中的错误或潜在问题发出警报。 这些视觉线索可帮助你立即解决问题，而无需等待在生成或运行时发现错误。 如果将鼠标悬停在波形曲线上，将看到关于此错误的更多信息。 灯泡也可能显示在左边距中，其中显示可采取以修复错误的快速操作。

   ::: moniker range="<=vs-2019"
   ![屏幕截图显示了 Visual Studio 中的波形曲线。](../media/squiggles-error.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![屏幕截图显示了 Visual Studio 中的波形曲线。](../media/vs-2022/squiggles-error.png)
   ::: moniker-end
  

::: moniker range="vs-2019"
- 代码清理

   通过单击一个按钮，可以设置代码格式并应用[代码样式设置](../../ide/reference/options-text-editor-csharp-formatting.md)、[.editorconfig 约定](../../ide/create-portable-custom-editor-options.md)和 [Roslyn 分析器](../../code-quality/roslyn-analyzers-overview.md)建议的任何代码修复程序。 代码清理（当前只适用于 C# 代码）有助于在代码进入代码评审之前解决代码中的问题。

   ![显示 Visual Studio 中的代码清理图标和菜单的屏幕截图。](../media/vs-2019/code-cleanup.png)
   ::: moniker-end

::: moniker range=">=vs-2022"
- 代码清理

   通过单击一个按钮，可以设置代码格式并应用[代码样式设置](../../ide/reference/options-text-editor-csharp-formatting.md)、[.editorconfig 约定](../../ide/create-portable-custom-editor-options.md)和 [Roslyn 分析器](../../code-quality/roslyn-analyzers-overview.md)建议的任何代码修复程序。 代码清理（当前只适用于 C# 代码）有助于在代码进入代码评审之前解决代码中的问题。

   ![显示 Visual Studio 中的代码清理图标和菜单的屏幕截图。](../media/vs-2022/code-cleanup.png)
   ::: moniker-end

- [重构](../../ide/refactoring-in-visual-studio.md)

   重构包括智能重命名变量、将一个或多个代码行提取到新方法中和更改方法参数的顺序。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中的重构的屏幕截图。](../media/refactoring-menu.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 Visual Studio 中的重构的屏幕截图。](../media/vs-2022/refactoring-menu.png)
   ::: moniker-end

- [IntelliSense](../../ide/using-intellisense.md)

   IntelliSense 是一组功能，可用于在编辑器中直接显示代码的信息，并且可在某些情况下编写小段代码。 如同在编辑器中拥有了基本文档内联，从而无需在其他位置查看类型信息。

   下图显示了 IntelliSense 如何显示类型的成员列表：

   ::: moniker range="<=vs-2019"
   ![显示 IntelliSense 成员列表的屏幕截图。](../media/intellisense-list-members.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 IntelliSense 成员列表的屏幕截图。](../media/vs-2022/intellisense-list-members.png)
   ::: moniker-end

   IntelliSense 功能因语言而异。 有关详细信息，请参阅 [C# IntelliSense](../../ide/visual-csharp-intellisense.md)、[Visual C++ IntelliSense](../../ide/visual-cpp-intellisense.md)、[JavaScript IntelliSense](../../ide/javascript-intellisense.md) 和 [Visual Basic IntelliSense](../../ide/visual-basic-specific-intellisense.md)。

- [Visual Studio 搜索](../../ide/visual-studio-search.md)

   Visual Studio 菜单、选项和属性有时可能会让人不知所措。 Visual Studio 搜索或 Ctrl+Q 是在同一位置快速查找 IDE 功能和代码的绝佳方法。

   ::: moniker range="vs-2017"

   ![显示 Visual Studio 2017 中“快速启动”搜索框的屏幕截图。](../media/quick-launch-nuget.png)

   有关详细信息，请参阅[快速启动](../../ide/reference/quick-launch-environment-options-dialog-box.md)。

   ::: moniker-end

   ::: moniker range="vs-2019"

   ![显示 Visual Studio 2019 中“快速启动”搜索框的屏幕截图。](../media/vs-2019/quick-launch-nuget.png)

    有关信息和工作效率提示，请参阅[如何使用 Visual Studio 搜索](../../ide/visual-studio-search.md)。

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   ![显示 Visual Studio 中“快速启动”搜索框的屏幕截图。](../media/vs-2022/quick-launch-nuget.png)

    有关信息和工作效率提示，请参阅[如何使用 Visual Studio 搜索](../../ide/visual-studio-search.md)。

   ::: moniker-end

- [Live Share](/visualstudio/liveshare/)

   与他人实时协作编辑和调试，无需考虑应用类型或编程语言。 可以立即安全地共享项目。 还可以共享调试会话、终端实例、localhost Web 应用、语音呼叫等等。

- [调用层次结构](../../ide/reference/call-hierarchy.md)

   “调用层次结构”窗口显示调用所选方法的方法。 考虑更改或删除方法时，或者尝试追踪 bug 时，这可能是有用的信息。

   ::: moniker range="<=vs-2019"
   ![显示“调用层次结构”窗口的屏幕截图。](../../ide/reference/media/call-hierarchy-csharp-expanded.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示“调用层次结构”窗口的屏幕截图。](../media/vs-2022/call-hierarchy-csharp-expanded.png)
   ::: moniker-end

- [CodeLens](../../ide/find-code-changes-and-other-history-with-codelens.md)

   CodeLens 可帮助查找代码引用、代码更改、链接错误、工作项、代码评审和单元测试，所有操作都在编辑器上进行。

   ::: moniker range="<=vs-2019"
   ![显示 CodeLens 的屏幕截图。](../media/codelens-overview.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 CodeLens 的屏幕截图。](../media/vs-2022/codelens-overview.png)
   ::: moniker-end

- [转到定义](../../ide/go-to-and-peek-definition.md)

   “转到定义”功能可将你直接带到函数或类型定义的位置。

   ::: moniker range="<=vs-2019"
   ![显示“转到定义”菜单项的屏幕截图。](../media/go-to-definition-menu.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示“转到定义”菜单项的屏幕截图。](../media/vs-2022/go-to-definition-menu.png)
   ::: moniker-end

- [查看定义](../../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)

   “速览定义”窗口显示方法或类型定义，而无需打开一个单独的文件。

   ::: moniker range="<=vs-2019"
   ![显示“速览定义”窗口的屏幕截图。](../media/peek-definition.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示“速览定义”窗口的屏幕截图。](../media/vs-2022/peek-definition.png)
   ::: moniker-end

## <a name="install-visual-studio"></a>安装 Visual Studio

在本部分中，你将创建一个简单的项目来尝试可在 Visual Studio 中执行的一些操作。 你将使用 [IntelliSense](../../ide/using-intellisense.md) 作为编码辅助，调试应用以便在应用执行期间查看变量值，并更改颜色主题。

::: moniker range="vs-2017"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 并将其安装到你的系统上。 通过模块化安装程序，可以选择和安装工作负荷。工作负荷是你习惯使用的编程语言或平台所需的一些功能。 若要执行[创建程序](#create-a-program)所需的步骤，请务必在安装过程中选择“.NET Core 跨平台开发”工作负载。

::: moniker-end

::: moniker range="vs-2019"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/downloads) 并将其安装到你的系统上。 通过模块化安装程序，可以选择和安装工作负载。工作负载是你希望使用的编程语言或平台所需的一些功能。 若要执行[创建程序](#create-a-program)所需的步骤，请务必在安装过程中选择“.NET Core 跨平台开发”工作负载。

![Visual Studio 安装程序中的“.NET Core 跨平台开发”工作负载的屏幕截图。](../media/dotnet-core-cross-platform-workload.png)

::: moniker-end

::: moniker range=">=vs-2022"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/downloads) 并将其安装到你的系统上。 在模块化安装程序中，可以选择和安装工作负载。工作负载是你希望使用的编程语言或平台所需的一些功能。 若要使用以下步骤[创建程序](#create-a-program)，请确保在安装过程中选择“.NET 桌面开发”工作负载。

![Visual Studio 安装程序中选择的 .NET 桌面开发工作负载的屏幕截图。](../media/vs-2022/dot-net-development-workload.png)

::: moniker-end

首次打开 Visual Studio 时，可使用 Microsoft 帐户或者单位或学校帐户[登录](../../ide/signing-in-to-visual-studio.md)。

## <a name="create-a-program"></a>创建程序

深入了解并创建一个简单的程序。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

1. 在菜单栏上，依次选择“文件”  >“新建”  >“项目”  。

   ![显示菜单栏上的“文件”>“新建项目”的屏幕截图。](../media/file-new-project-menu.png)

   “新建项目”对话框中会显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

1. 在“Visual C#”下选择“.NET Core”模板类别，然后选择“控制台应用(.NET Core)”模板。 在“名称”文本框中，键入“HelloWorld”，然后选择“确定”按钮。

   ![显示 .NET Core 应用模板的屏幕截图。](../media/overview-new-project-dialog.png)

   > [!NOTE]
   > 如果未看到“.NET Core”类别，则需要安装“.NET Core 跨平台开发”工作负载。 为此，选择“新建项目”对话框左下角的“打开 Visual Studio 安装程序”链接。 “Visual Studio 安装程序”打开后，向下滚动并选择“.NET Core 跨平台开发”工作负载，然后选择“修改”。

   Visual Studio 随即创建项目。 它是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。

   稍后可看到类似于以下屏幕的内容：

   ![显示 Visual Studio Code IDE 的屏幕截图。](../media/overview-ide-console-app.png)

   应用程序的 C# 代码显示于编辑器窗口中，会占用大部分空间。 请注意，文本已自动着色，用于指示代码的不同方面，如关键字或类型。 此外，代码中的垂直短虚线指示哪两个大括号相匹配，行号能够帮助你在以后查找代码。 可以通过选择带减号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要的代码，最大程度地减少屏幕混乱。 右侧名为“解决方案资源管理器”的窗口中列出了项目文件。

   ![显示带红色框的 Visual Studio IDE 的屏幕截图。](../media/overview-ide-console-app-red-boxes.png)

   还提供了一些其他的菜单和工具窗口，但是现在我们继续下一步操作。

1. 现在启动该应用。 可从菜单栏的“调试”菜单中选择“开始执行(不调试)”，以执行此操作。 还可按 Ctrl+F5 。

   ![显示“调试”>“启动时不调试”菜单的屏幕截图。](../media/overview-start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”。 现在你拥有了一个正在运行的应用！

   ![cmd.exe 控制台窗口的屏幕截图，其中显示输出“Hello World!” 以及“Press any key to continue”。](../media/overview-console-window.png)

1. 要关闭控制台窗口，请在键盘上按任意键。

1. 接下来，向应用添加更多代码。 在 `Console.WriteLine("Hello World!");` 行的前面添加以下 C# 代码：

   ```csharp
   Console.WriteLine("\nWhat is your name?");
   var name = Console.ReadLine();
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本并按 Enter 键。

1. 将显示 `Console.WriteLine("Hello World!");` 的行更改为以下代码：

   ```csharp
   Console.WriteLine($"\nHello {name}!");
   ```

1. 选择“调试”**“开始执行(不调试)”** > ，或按 Ctrl+F5，再次运行该应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中输入姓名，并按 Enter。

   ![显示控制台窗口输入的屏幕截图。](../media/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

   “启动”窗口中会显示有关克隆存储库、打开最近的项目或创建新项目的选项。

1. 选择“创建新项目”。

    :::image type="content" source="../media/vs-2019/start-window-create-new-project.png" alt-text="Visual Studio 2019 中“创建新项目”窗口的屏幕截图。":::

   随即打开“创建新项目”窗口，并显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

1. 若要查找所需的模板，请在搜索框中键入或输入“.Net Core 控制台”。 系统会自动根据输入的关键字筛选可用模板列表。 可以通过从“所有语言”下拉列表中选择“C#”、从“所有平台”列表中选择“Windows”以及从“所有项目类型”列表中选择“控制台”进一步筛选模板结果。

    选择“控制台应用程序”模板，然后单击“下一步” 。

    :::image type="content" source="../media/vs-2019/create-new-project.png" alt-text="Visual Studio 2019 中“创建新项目”窗口的屏幕截图，你可以在该窗口中选择所需的模板。":::

1. 在“配置新项目”窗口中，在“项目名称”框中输入“HelloWorld”，可以选择更改项目文件的目录位置（默认位置为 `C:\Users\<name>\source\repos`），然后单击“下一步”。

    :::image type="content" source="../media/vs-2019/configure-new-project.png" alt-text="Visual Studio 2019 中“配置新项目”窗口的屏幕截图，你可在该窗口中输入项目的名称。":::

1. 在“附加信息”窗口中，验证“目标框架”下拉菜单中是否显示“.NET Core 3.1”，然后单击“创建”。

    :::image type="content" source="../media/vs-2019/create-project-additional-info.png" alt-text="Visual Studio 2019 中“附加信息”窗口的屏幕截图，你可在该窗口中选择所需的 .NET Core Framework 版本。":::

   Visual Studio 随即创建项目。 它是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。

   稍后可看到类似于以下屏幕的内容：

   ![显示 Visual Studio Code IDE 的屏幕截图。](../media/vs-2019/overview-ide-console-app.png)

   应用程序的 C# 代码显示于编辑器窗口中，会占用大部分空间。 请注意，文本已自动着色，用于指示代码的不同方面，如关键字或类型。 此外，代码中的垂直短虚线指示哪两个大括号相匹配，行号能够帮助你在以后查找代码。 可以通过选择带减号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要的代码，最大程度地减少屏幕混乱。 右侧名为“解决方案资源管理器”的窗口中列出了项目文件。

   ![显示带红色框的 Visual Studio IDE 的屏幕截图。](../media/vs-2019/overview-ide-console-app-red-boxes.png)

   还提供了一些其他的菜单和工具窗口，但是现在我们继续下一步操作。

1. 现在启动该应用。 可从菜单栏的“调试”菜单中选择“开始执行(不调试)”，以执行此操作。 还可按 Ctrl+F5 。

   ![显示“调试”>“启动时不调试”菜单项的屏幕截图。](../media/overview-start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”。 现在你拥有了一个正在运行的应用！

   ![Microsoft Visual Studio 调试控制台窗口的屏幕截图，其中显示输出“Hello World!” 以及“Press any key to close this window”。](../media/vs-2019/overview-console-window.png)

1. 要关闭控制台窗口，请在键盘上按任意键。

1. 接下来，向应用添加更多代码。 在 `Console.WriteLine("Hello World!");` 行的前面添加以下 C# 代码：

   ```csharp
   Console.WriteLine("\nWhat is your name?");
   var name = Console.ReadLine();
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本并按 Enter 键。

1. 将显示 `Console.WriteLine("Hello World!");` 的行更改为以下代码：

   ```csharp
   Console.WriteLine($"\nHello {name}!");
   ```

1. 选择“调试”**“开始执行(不调试)”** > ，或按 Ctrl+F5，再次运行该应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中输入姓名，并按 Enter。

   ![Microsoft Visual Studio 调试控制台窗口的屏幕截图，其中显示输入姓名的提示、所输入的姓名以及输出“Hello Georgette!”。](../media/vs-2019/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end
::: moniker range=">=vs-2022"

1. 启动 Visual Studio。 “启动”窗口中会显示有关克隆存储库、打开最近的项目或创建新项目的选项。

1. 选择“创建新项目”。

   ![选择“创建新项目”的 Visual Studio 开始菜单的屏幕截图。](../media/vs-2022/create-new-project.png)

   随即打开“创建新项目”窗口，并显示几个项目模板。 模板包含给定项目类型所需的基本文件和设置。

1. 若要查找模板，可以在搜索框中键入或输入关键字。 系统会根据输入的关键字筛选可用模板列表。 可以通过从“所有语言”下拉列表中选择“C#”、从“所有平台”列表中选择“Windows”以及从“所有项目类型”列表中选择“控制台”进一步筛选模板结果。

    选择“控制台应用程序”模板，然后选择“下一步”。

   ![“创建新项目”窗口的屏幕截图，其中选择了“控制台应用程序”。](../media/vs-2022/start-window-create-new-project.png)

1. 在“配置新项目”窗口中，在“项目名称”框中输入“HelloWorld”。 （可选）更改项目目录的默认位置 C:\\Users\\\<name>\\source\\repos，然后选择“下一步”。

   ![“配置新项目”窗口的屏幕截图，其中输入了项目名称“HelloWorld”。](../media/vs-2022/configure-new-project.png)

1. 在“附加信息”窗口中，验证“目标框架”下拉菜单中是否显示“.NET 6.0”，然后选择“创建”。

   ![“附加信息”窗口的屏幕截图，其中选择了“.NET 6.0”。](../media/vs-2022/create-project-additional-info.png)

   Visual Studio 随即创建项目。 该程序是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中显示 字符串“Hello, World!”。

   项目文件显示在名为“解决方案资源管理器”的窗口中 Visual Studio IDE 的右侧。 在“解决方案资源管理器”窗口中，选择“Program.cs”文件。 应用的 C# 代码在编辑器窗口中打开，会占用大部分空间。

   ![显示编辑器中带有 Program.cs 代码的 Visual Studio IDE 的屏幕截图。](../media/vs-2022/overview-ide-console-app.png)

   代码已自动着色，用于指示不同方面，如关键字或类型。 行号可帮助你查找代码。

   代码中的小垂直虚线指示哪个大括号彼此匹配。 还可以通过选择带减号或加号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要显示的代码，最大程度地减少屏幕混乱。

   ![显示带红色框的 Visual Studio IDE 的屏幕截图。](../media/vs-2022/overview-ide-console-app-red-boxes.png)

   还提供了许多其他菜单和工具窗口。

1. 通过从 Visual Studio 顶部菜单中选择“调试” > “启动时不调用”来启动应用。 还可按 Ctrl+F5 。

   ![显示“调试”>“启动时不调试”菜单项的屏幕截图。](../media/vs-2022/overview-start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello, World!”。 现在你拥有了一个正在运行的应用！

   ![调试控制台窗口的屏幕截图，其中显示输出“Hello World!” 以及“Press any key to close this window”。](../media/vs-2022/overview-console-window.png)

1. 按任意键关闭控制台窗口。

1. 接下来，向应用添加更多代码。 在 `Console.WriteLine("Hello World!");` 行的前面添加以下 C# 代码：

   ```csharp
   Console.WriteLine("\nWhat is your name?");
   var name = Console.ReadLine();
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本。

1. 将显示 `Console.WriteLine("Hello World!");` 的行更改为以下行：

   ```csharp
   Console.WriteLine($"\nHello {name}!");
   ```

1. 通过选择“调试”>“启动但不调试”或通过按 Ctrl+F5 再次运行该应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中键入姓名，并按 Enter。

   ![调试控制台窗口的屏幕截图，其中显示输入姓名的提示、所输入的姓名以及输出“Hello Georgette!”。](../media/vs-2022/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

## <a name="use-refactoring-and-intellisense"></a>使用重构和 IntelliSense

让我们了解一下如何借助[重构](../../ide/refactoring-in-visual-studio.md)和[IntelliSense](../../ide/using-intellisense.md) 更有效地进行编码。

首先，重命名 `name` 变量：

1. 双击 `name` 变量，然后键入变量“username”的新名称。

   变量周围将出现一个框，且边距中会出现灯泡。

1. 选择灯泡图标，显示可用的[快速操作](../../ide/quick-actions.md)。 选择“将 'name' 重命名为 'username'”。

   ::: moniker range="vs-2017"
   ![显示 Visual Studio 中的“重命名”操作的屏幕截图。](../media/rename-quick-action.png)
   ::: moniker-end
   ::: moniker range="vs-2019"
   ![显示 Visual Studio 中的“重命名”操作的屏幕截图。](../media/vs-2019/rename-quick-action.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 Visual Studio 中的“重命名”操作的屏幕截图。](../media/vs-2022/rename-quick-action.png)
   ::: moniker-end

   该变量会在整个项目中进行重命名，本例中只有两处。

   ::: moniker range="vs-2017"
   ![显示 Visual Studio 中重命名重构的 gif 动图。](../media/rename-refactoring.gif)
   ::: moniker-end

1. 接下来了解下 IntelliSense。 在 `Console.WriteLine($"\nHello {username}!");` 行下方，键入 `DateTime now = DateTime.`。

   此时，框中显示 <xref:System.DateTime> 类的成员。 当前所选成员的说明还会显示在单独的框中。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中的 IntelliSense 列表成员的屏幕截图。](../media/intellisense-list-members.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 Visual Studio 中的 IntelliSense 列表成员的屏幕截图。](../media/vs-2022/intellisense-list-members.png)
   ::: moniker-end

1. 通过双击或按 Tab 键，选择名为“Now”的成员，它是类属性。通过在行末尾添加分号来完成代码行：`DateTime now = DateTime.Now;`。

1. 在该行下，输入以下代码行：

   ```csharp
   int dayOfYear = now.DayOfYear;

   Console.Write("Day of year: ");
   Console.WriteLine(dayOfYear);
   ```

   > [!TIP]
   > <xref:System.Console.Write%2A?displayProperty=nameWithType> 与 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 不同，它在打印后不会添加行终止符。 这意味着发送到输出的下一段文本将打印在同一行上。 将鼠标悬停在代码中的每个方法上，即可查看其说明。

1. 接下来，再次使用重构来使代码更加简洁。 在行 `DateTime now = DateTime.Now;` 中选择变量 `now`。 该行的边距中会显示一个小螺丝刀图标。

1. 选择小螺丝刀图标以查看 Visual Studio 中的可用建议。 本例显示[内联临时变量](../../ide/reference/inline-temporary-variable.md)重构，可在无需更改整体代码行为的情况下删除代码行。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中内联临时变量建议的屏幕截图。](../media/inline-temporary-variable-refactoring.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 Visual Studio 中内联临时变量建议的屏幕截图。](../media/vs-2022/inline-temporary-variable-refactoring.png)
   ::: moniker-end

1. 选择“内联临时变量”以重构代码。

1. 按 Ctrl+F5 重新运行程序 。 输出的内容与以下类似：

   ::: moniker range="<=vs-2019"
   ![调试控制台窗口的屏幕截图，其中显示输入姓名的提示、所输入的姓名以及输出“Hello Georgette! Day of year:43”。](../media/vs-2019/overview-console-final.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![调试控制台窗口的屏幕截图，其中显示输入姓名的提示、所输入的姓名以及输出“Hello Georgette! Day of year: 244”。](../media/vs-2022/overview-console-final.png)
   ::: moniker-end

## <a name="debug-code&quot;></a>调试代码

编写代码时，应运行并测试该代码是否存在 bug。 可通过 Visual Studio 的调试系统逐句执行代码，一次执行一条语句，逐步检查变量。 可以设置在特定行停止代码执行的断点，并观察变量值在代码运行时的变化方式。

通过设置断点，可查看程序运行时 `username` 变量的值。

1. 通过单击代码行旁边最左边距（或装订线），在代码行上设置一个断点，该断点表示 `Console.WriteLine($&quot;\nHello {username}!");`。 也可以选择代码行，然后按 F9。

   装订线中会出现一个红色圆圈，并突出显示该行。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 中代码行上的断点的屏幕截图。](../media/breakpoint.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 Visual Studio 中代码行上的断点的屏幕截图。](../media/vs-2022/breakpoint.png)
   ::: moniker-end

1. 选择“调试” > “启动调试”或按 F5，开始调试。

1. 控制台窗口出现并询问姓名时，请输入姓名。

   Visual Studio 代码编辑器重新获得焦点，有断点的代码行突出显示为黄色。 黄色突出显示表示将在下一步执行此代码行。 断点使应用在此行暂停执行。

1. 将鼠标悬停在 `username` 变量上，即可查看它的值。 也可以右键单击 `username` 并选择“添加监视”，将变量添加到“监视”窗口，这样也可查看它的值。

   ::: moniker range="<=vs-2019"
   ![在 Visual Studio 中调试过程中显示变量值的屏幕截图。](../media/debugging-variable-value.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![在 Visual Studio 中调试过程中显示变量值的屏幕截图。](../media/vs-2022/debugging-variable-value.png)
   ::: moniker-end

1. 再次按 F5 以结束应用运行。

有关 Visual Studio 中调试的详细信息，请参阅[调试器功能体验](../../debugger/debugger-feature-tour.md)。

## <a name="customize-visual-studio"></a>自定义 Visual Studio

可个性化设置 Visual Studio 用户界面，包括更改默认颜色主题。 若要更改颜色主题：

::: moniker range="vs-2017"

1. 在菜单栏中，选择“工具”>“选项”，打开“选项”对话框。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“深色”，然后选择“确定”    。

   此时，整个 IDE 的颜色主题更改为“深色”。

   ![显示深色主题 Visual Studio 的屏幕截图。](../media/dark-theme.png)
::: moniker-end

::: moniker range="vs-2019"

1. 在菜单栏中，选择“工具”>“选项”，打开“选项”对话框。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“深色”，然后选择“确定”    。

   此时，整个 IDE 的颜色主题更改为“深色”。

   ![显示深色主题 Visual Studio 的屏幕截图。](../media/vs-2019/dark-theme.png)
::: moniker-end

::: moniker range=">=vs-2022"
1. 在菜单栏中，选择“工具”>“选项”，打开“选项”对话框。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“蓝色”或“浅色”，然后选择“确定”。

   此时，整个 IDE 的颜色主题也会相应地更改。 以下屏幕截图显示“蓝色”主题：

   ![显示“蓝色”主题 Visual Studio 的屏幕截图。](../media/vs-2022/blue-theme.png)
::: moniker-end

若要了解有关 IDE 个性化设置的其他方法，请参阅[个性化设置 Visual Studio](../../ide/personalizing-the-visual-studio-ide.md)。