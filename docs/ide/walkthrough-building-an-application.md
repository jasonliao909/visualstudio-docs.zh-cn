---
title: 教程：生成应用程序
description: 更熟悉使用 Visual Studio 生成应用程序时可配置的多个选项。
ms.custom: SEO-VS-2020
ms.date: 05/10/2022
ms.technology: vs-ide-compile
ms.topic: tutorial
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ee02fd71c3df50fcfdd96e91b58f21d589e7c8d3
ms.sourcegitcommit: 8e829a5358a0ce32a81a0f97060237be3c9ab074
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2022
ms.locfileid: "145045263"
---
# <a name="tutorial-build-an-application"></a>教程：生成应用程序

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]
在本文中，你会更熟悉使用 Visual Studio 生成应用程序时可配置的多个选项。 将为示例应用程序创建自定义生成配置、隐藏特定警告消息以及增加生成输出信息。

## <a name="install-the-sample-application"></a>安装示例应用程序

:::moniker range="vs-2017"
本教程中使用的示例代码位于 [WPF 示例](https://github.com/microsoft/wpf-samples)。 若要克隆存储库，请使用GitHub的绿色 **“克隆**”按钮，然后选择存储库的本地硬盘驱动器上的位置。 在Visual Studio中，选择 **“打开”项目**，然后浏览到选择克隆存储库的位置，在该位置下，查找 *GettingStarted/WalkthroughFirstWPFApp/csharp/ExpenseItIntro.sln* 以在 C# 中工作，或 *使用 GettingStarted/WalkthroughFirstWPFApp/vb/ExpenseItIntro2.sln* 以在 Visual Basic 工作。
:::moniker-end

:::moniker range=">=vs-2019"
 本教程中使用的示例代码位于 [WPF 示例](https://github.com/microsoft/wpf-samples)。 若要克隆存储库，请使用GitHub的绿色 **“克隆**”按钮，然后在 **Visual Studio中选择“克隆**”。 可以选择本地硬盘驱动器上的位置，以创建存储库内容的副本。 存储库包含许多解决方案。 如果Visual Studio打开其中一个解决方案，请关闭该解决方案，然后选择 **“打开项目或解决方案**”，然后浏览到克隆存储库的位置，然后在其中查找 *GettingStarted/WalkthroughFirstWPFApp/csharp/ExpenseItIntro.sln* 以在 C# 中工作，或者 *使用 GettingStarted/WalkthroughFirstWPFApp/vb/ExpenseItIntro2.sln* 以在 Visual Basic 工作。
:::moniker-end

## <a name="create-a-custom-build-configuration"></a>创建自定义生成配置

创建解决方案时，会自动为解决方案定义调试和发布生成配置及其默认平台目标。 然后，可以自定义这些配置，或创建自己的配置。 生成配置指定生成类型。 生成平台指定应用程序为该配置定向的操作系统。 有关详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)、[了解生成平台](../ide/understanding-build-platforms.md)，以及[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。

可以使用“配置管理器”  对话框更改或创建配置和平台设置。 在此过程中将创建用于测试的生成配置。

### <a name="create-a-build-configuration"></a>创建生成配置

1. 打开“配置管理器”  对话框。

   :::moniker range="<=vs-2019"
   ![“生成”菜单的屏幕截图，Configuration Manager命令。](../ide/media/buildwalk_configurationmanagerdialogbox.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![“生成”菜单Configuration Manager命令的屏幕截图。](media/vs-2022/build-tutorial-configuration-manager-menu.png)
   :::moniker-end

1. 在“活动解决方案配置”列表中，选择 \<New...\>。

1. 在“新建解决方案配置”对话框中，命名新配置 `Test`，复制现有“调试”配置中的设置，然后选择“确定”按钮。

   :::moniker range="<=vs-2019"
   ![“新建解决方案配置”对话框的屏幕截图](../ide/media/buildwalk_newsolutionconfigdlgbox.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![显示“新建解决方案配置”对话框中创建测试配置的屏幕截图。](media/vs-2022/build-tutorial-create-test-configuration.png)
   :::moniker-end

1. 在“活动解决方案平台”列表中，选择 \<New...\> 。

1. 在“新建解决方案平台”对话框中，选择“x64”，且不要复制 x86 平台中的设置   。

   :::moniker range="<=vs-2019"
   ![“新建解决方案平台”对话框的屏幕截图。](../ide/media/buildwalk_newsolutionplatform.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![“新建解决方案平台”对话框的屏幕截图。](media/vs-2022/build-tutorial-new-solution-platform.png)
   :::moniker-end

1. 选择 **“确定”** 按钮。

   “活动解决方案配置”已更改为“测试”，且“活动解决方案平台”设置为“x64”  。

   :::moniker range="<=vs-2019"
   ![包含测试配置的Configuration Manager的屏幕截图。](../ide/media/buildwalk_configmanagertestconfig.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![包含测试配置的Configuration Manager的屏幕截图。](media/vs-2022/build-tutorial-configuration-manager.png)
   :::moniker-end

1. 选择“关闭”  。

使用“标准”工具栏上的“解决方案配置”列表，可快速验证或更改“活动解决方案配置”。

:::moniker range="<=vs-2019"
![标准工具栏上“解决方案配置”下拉列表的屏幕截图。](../ide/media/buildwalk_standardtoolbarsolutioncongfig.png)
:::moniker-end
:::moniker range=">=vs-2022"
![标准工具栏上“解决方案配置”下拉列表的屏幕截图。](media/vs-2022/build-tutorial-configuration-dropdown.png)
:::moniker-end

## <a name="build-the-application"></a>生成应用程序

接下来将生成具有自定义生成配置的解决方案。

### <a name="build-the-solution"></a>生成解决方案

- 在菜单栏上，依次选择“生成” > “生成解决方案”，或按 Ctrl+Shift+B。

    “输出”  窗口将显示生成的结果。 成功生成。

## <a name="hide-compiler-warnings"></a>隐藏编译器警告

接下来将介绍一些会导致编译器生成警告的代码。

1. 在 C# 项目中，打开 ExpenseReportPage.xaml.cs  文件。 在 ExpenseReportPage  方法中，添加以下代码：`int i;`。

    或

    在 Visual Basic 项目中，打开 ExpenseReportPage.xaml.vb  文件。 在自定义的构造函数“Public Sub New...”  中，添加以下代码：`Dim i`。

1. 生成解决方案。

“输出”  窗口将显示生成的结果。 成功生成，但生成了警告：

:::moniker range="<=vs-2019"
![Visual Basic的输出窗口中生成警告的屏幕截图。](../ide/media/buildwalk_vbbuildoutputwnd.png)

![C# 的输出窗口中生成警告的屏幕截图。](../ide/media/buildwalk_csharpbuildoutputwnd.png)
:::moniker-end
:::moniker range=">=vs-2022"
![C# 的“输出”窗口中生成警告的屏幕截图。](media/vs-2022/build-tutorial-build-warning-csharp.png)

![Visual Basic的“输出”窗口中生成警告的屏幕截图。](media/vs-2022/build-tutorial-build-warning-vb.png)
:::Moniker-end

可在生成期间暂时隐藏某些警告消息，而不是使其扰乱生成输出。

### <a name="hide-a-specific-c-warning"></a>隐藏特定的 C# 警告

1. 在“解决方案资源管理器”  中，选择顶级项目节点。

1. 在菜单栏上，选择“ **查看** > **属性页**”。

     将打开“项目设计器”  。

1. 选择“ **生成** ”选项卡或部分，然后在“ **禁止显示警告** ”框中指定警告号 **0168**。 如果已列出其他警告，请使用分号作为分隔符。

    :::moniker range="<=vs-2019"
    ![“生成”页的屏幕截图，Project设计器。](../ide/media/buildwalk_csharpsuppresswarnings.png)
    :::moniker-end
    :::moniker range=">=vs-2022"
    ![Project属性中的“生成”部分的屏幕截图。](media/vs-2022/build-tutorial-disable-warning-0168.png)
    :::moniker-end

    有关详细信息，请参阅 [“项目设计器”->“生成”页 (C#)](../ide/reference/build-page-project-designer-csharp.md)。

1. 使用 **生成>重新生成解决方案生成解决方案**。

    “ **输出** ”窗口仅显示生成摘要信息 (没有警告) 。

    :::moniker range="<=vs-2019"
    ![C# 的“输出窗口”的屏幕截图，其中没有生成警告](../ide/media/buildwalk_visualcsharpbuildwarnings.png)
    :::moniker-end
    :::moniker range=">=vs-2022"
    ![C# 的“输出”窗口的屏幕截图，其中没有生成警告](media/vs-2022/build-tutorial-output-csharp-no-warning.png)
    :::moniker-end

### <a name="suppress-all-visual-basic-build-warnings"></a>禁止显示所有 Visual Basic 生成警告

1. 在“解决方案资源管理器”  中，选择顶级项目节点。

2. 在菜单栏上，依次选择“查看”   > “属性页”  。

     将打开“项目设计器”  。

3. 在“编译”  页上，选择“禁用所有警告”  复选框。

     :::moniker range="<=vs-2019"
     ![“编译”页，“项目设计器”](../ide/media/buildwalk_vbsuppresswarnings.png)
     :::moniker-end
     :::moniker range=">=vs-2022"
     ![在Project设计器的“编译”选项卡中禁用警告的屏幕截图](media/vs-2022/build-tutorial-disable-warnings-vb.png)
     :::moniker-end

     有关详细信息，请参阅[在 Visual Basic 中配置警告](../ide/configuring-warnings-in-visual-basic.md)。

4. 生成解决方案。 如果未重新生成，请使用 **生成>重新生成解决方案生成解决方案**。

   “ **输出** ”窗口仅显示生成摘要信息 (没有警告) 。

   :::moniker range="<=vs-2019"
   ![没有生成警告的Visual Basic的“输出窗口”屏幕截图](../ide/media/buildwalk_visualbasicbuildwarnings.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![没有生成警告的Visual Basic的“输出”窗口的屏幕截图](media/vs-2022/build-tutorial-build-output-vb-no-warning.png)
   :::moniker-end

   有关详细信息，请参阅[如何：禁止显示编译器警告](../ide/how-to-suppress-compiler-warnings.md)。

## <a name="display-additional-build-details-in-the-output-window"></a>在“输出”窗口中显示其他生成详细信息

你可以更改“输出”  窗口中显示的关于生成过程的信息量。 生成详细程度通常设置为“最小”，这意味着，“输出”窗口仅显示生成过程的摘要以及任何高优先级的警告或错误   。 使用[“选项”对话框->“项目和解决方案”->“生成和运行”](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)，可显示有关生成的详细信息。

> [!IMPORTANT]
> 如果显示详细信息，生成将花费更长时间才能完成。

### <a name="change-the-amount-of-information-in-the-output-window"></a>更改“输出”窗口中的信息量

1. 打开“选项”  对话框。

     :::moniker range="<=vs-2019"
     ![“工具”菜单上的“选项”命令的屏幕截图。](../ide/media/exploreide-toolsoptionsmenu.png)
     :::moniker-end
     :::moniker range=">=vs-2022"
     ![“工具”、“选项”菜单项的屏幕截图。](media/vs-2022/build-tutorial-tools-options-menu-item.png)
     :::moniker-end

1. 选择“项目和解决方案”  类别，然后选择“生成和运行”  页。

1. 在“MSBuild 项目生成输出详细信息”  列表中，选择“常规”  ，然后选择“确定”  按钮。

1. 在菜单栏上，依次选择“生成” > “清理解决方案”。

1. 生成解决方案，然后查看“输出”  窗口中的信息。

     生成信息包括生成开始的时间（位于开头）和处理文件的顺序。 此信息还包括生成期间 Visual Studio 运行的实际的编译器语法。

     例如，在 C# 生成中，[/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) 选项列出了本主题前面部分随其他三个警告一起指定的警告代码 0168  。

     在 Visual Basic 生成中，[/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) 不包括要排除的特定警告，因此不会出现任何警告。

    > [!TIP]
    > 如果通过选择 Ctrl+F 键，显示“查找”对话框，则可以搜索“输出”窗口的内容。

有关详细信息，请参阅[如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)。

## <a name="create-a-release-build"></a>创建版本生成

可以生成针对交付进行了优化的示例应用程序版本。 对于版本生成，需指定在启动生成前，将可执行文件复制到网络共享。

有关详细信息，请参阅[如何：更改生成输出目录](../ide/how-to-change-the-build-output-directory.md)和[在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)。

### <a name="specify-a-release-build-for-visual-basic"></a>指定 Visual Basic 的版本生成

1. 若要打开 **Project设计器**，请在 **解决方案资源管理器** 中右键单击并选择 **“属性**” (或按 **AltEnter** +) ，或在 **“视图**”菜单上选择 **“属性页**” ：

    :::moniker range="<=vs-2019"
    ![视图的屏幕截图，“属性页”菜单项。](../ide/media/buildwalk_viewpropertypages.png)
    :::moniker-end
    :::moniker range=">=vs-2022"
    ![视图的屏幕截图，“属性页”菜单项。](media/vs-2022/build-tutorial-property-pages-menu-item.png)
    :::moniker-end

1. 选择“编译”  页。

1. 在“配置”  列表中，选择“版本”  。

1. 在“平台”  列表中，选择“x86”  。

1. 在“生成输出路径”  框中，指定网络路径。

     例如，你可以指定 `\\myserver\builds`。

    > [!IMPORTANT]
    > 可能会出现一个消息框，警告指定的网络共享位置可能不受信任。 如果信任指定的位置，请在消息框中选择“确定”按钮  。

1. 构建应用程序。

    :::moniker range="<=vs-2019"
    ![“生成”菜单上的“生成解决方案”命令](../ide/media/exploreide-buildsolution.png)
    :::moniker-end
    :::moniker range=">=vs-2022"
    ![“生成”菜单上“生成解决方案”命令的屏幕截图](media/vs-2022/build-tutorial-build-menu.png)
    :::moniker-end

### <a name="specify-a-release-build-for-c"></a>指定 C\# 的版本生成

1. 打开“项目设计器”  。

    :::moniker range="<=vs-2019"
    ![视图的屏幕截图，“属性页”菜单项。](../ide/media/buildwalk_viewpropertypages.png)
    :::moniker-end
    :::moniker range=">=vs-2022"
    ![视图的屏幕截图，“属性页”菜单项。](media/vs-2022/build-tutorial-property-pages-menu-item.png)
    :::moniker-end

1. 选择“生成”页。 

1. 在“配置”  列表中，选择“版本”  。

1. 在“平台”  列表中，选择“x86”  。

1. 在“输出路径”  框中，指定网络路径。

     例如，可指定 `\\myserver\builds`。

    > [!IMPORTANT]
    > 可能会出现一个消息框，警告指定的网络共享位置可能不受信任。 如果信任指定的位置，请在消息框中选择“确定”按钮  。

1. 在“标准工具栏”  上，将解决方案配置设置为“发布”  ，将解决方案平台设置为“x86”  。

1. 构建应用程序。

    :::moniker range="<=vs-2019"
    ![“生成”菜单上的“生成解决方案”命令](../ide/media/exploreide-buildsolution.png)
    :::moniker-end
    :::moniker range=">=vs-2022"
    ![“生成”菜单上“生成解决方案”命令的屏幕截图](media/vs-2022/build-tutorial-build-menu.png)
    :::moniker-end

   可执行文件已复制到指定的网络路径。 其路径将为 `\\myserver\builds\\FileName.exe`。

祝贺你！ 你已成功完成本教程。

## <a name="see-also"></a>另请参阅

- [演练：生成项目 (C++)](/cpp/ide/walkthrough-building-a-project-cpp)
- [ASP.NET Web 应用程序项目预编译概述](/previous-versions/aspnet/aa983464\(v\=vs.110\))
- [演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md)
