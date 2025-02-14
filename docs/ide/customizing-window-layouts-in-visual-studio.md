---
title: 自定义窗口布局
description: 了解如何在 Visual Studio中自定义窗口，以创建最适合开发工作流的布局。
ms.custom: SEO-VS-2020
ms.date: 02/22/2022
ms.topic: conceptual
f1_keywords:
- vs.windows
- vs.environment
helpviewer_keywords:
- windows [Visual Studio], managing
- custom window configurations
- layout [Visual Studio], window management
- document windows [Visual Studio]
- interface modes
- AutoHide windows
- MDI, window interface modes
- multiple monitors
- Tabbed Document mode
- debug mode
- custom layouts
ms.assetid: 7517ff13-76de-4ecf-9c1b-eb9b7ff4d718
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: d26afecee9cd0c7a9689bdd27fcd7a9c52865607
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139550088"
---
# <a name="customize-window-layouts-in-visual-studio"></a>在 Visual Studio 中自定义窗口布局

在 Visual Studio 中，可以自定义窗口的位置、大小和行为，为各种开发工作流创建最佳窗口布局。 自定义布局时，IDE 会记住它。 例如，如果更改了“解决方案资源管理器”的停靠位置，然后关闭 Visual Studio，则下次打开 Visual Studio 时，即使你在另一台计算机上工作，“解决方案资源管理器”也将停靠在相同的位置   。

还可以为自定义布局命名并将其保存，然后通过单个命令在各布局间切换。 例如，可以创建一个布局用于编辑，另一个布局用于调试，然后使用“窗口” > “应用窗口布局”菜单命令在二者之间切换   。

## <a name="tool-and-document-windows"></a>工具窗口和文档窗口

IDE 提供两种基本窗口类型，即 *“工具窗口”* 和 *“文档窗口”* 。 工具窗口包括“解决方案资源管理器”、“服务器资源管理器”、“输出窗口”、“错误列表”、设计器、调试程序窗口等   。 文档窗口包含源代码文件、任意文本文件、配置文件等。 可以在标题栏处对工具窗口进行重设大小和拖动。 可以在选项卡处拖动文档窗口。右键单击选项卡或标题栏，以设置窗口上的其他选项。

“窗口”菜单显示用于在 IDE 中停靠、浮动和隐藏窗口的选项。 右键单击窗口选项卡或标题栏，以了解该特定窗口的其他选项。 可以一次同时显示特定工具窗口的多个实例。 例如，可以显示多个 Web 浏览器窗口，还可以通过选择 **“窗口”** 菜单上的 **“新建窗口”** ，创建某些工具窗口的其他实例。

### <a name="split-windows"></a>拆分窗口

如果需要在文档中一次查看或编辑两个位置，可以拆分窗口。 若要将文档划分为两个独立滚动部分，请单击 **“窗口”** 菜单上的 **“拆分”** 。 单击 **“窗口”** 菜单上的 **“取消拆分”** 还原为单一视图。

### <a name="tabs"></a>制表符

可以使用选项卡以多种不同的方式排列布局。 例如，可以在不打开文件的情况下在编辑器中查看文件的预览，可以对选项卡进行分组等等。

#### <a name="preview-tab-document-windows"></a>“预览”选项卡（文档窗口）

在“预览”选项卡中，可以在不打开文件的情况下，在编辑器中查看它们。 在单步执行文件（通过“转到定义”）时进行调试的过程中以及在浏览搜索结果时，可以通过在 “解决方案资源管理器”中选择文件来预览文件 。 预览文档选项井右侧的选项卡中显示的文件。 如果修改了文件或选择了“打开”，文件将打开以便编辑。

::: moniker range=">=vs-2019"

#### <a name="vertical-document-tabs"></a>竖排文档选项卡

**[Visual Studio 2019 版本 16.4 及更高版本中的新增功能](/visualstudio/releases/2019/release-notes-v16.4/)** ：我们添加了一个热门的功能请求，即 [竖排文档选项卡](https://developercommunity.visualstudio.com/idea/467369/vertical-group-tab.html)。 现在，可以在位于编辑器左侧或右侧的垂直列表中管理文档选项卡。

可以通过以下方式应用竖排文档选项卡：

- 从菜单栏中选择“工具” > “选项” > “环境” > “选项卡和窗口”。 然后，从“设置选项卡布局”控件中，从下拉列表中选择“顶部”、“左侧”或“右侧”。

- 右键单击选项卡，选择“设置选项卡布局”，然后选择“左侧”或“右侧”。 （若要将选项卡返回到其默认位置，请选择“顶部”。）

    :::image type="content" source="./media/vs-2019/vertical-tabs.gif" alt-text="显示操作中的竖排文档选项卡的动画":::

::: moniker-end

::: moniker range="vs-2022"

#### <a name="color-document-tabs"></a>颜色文档选项卡

Visual Studio 2022 包括新的个性化设置选项，可用于帮助你更有效地编写代码。 我们添加了另一个顶级功能请求 [，即颜色文档选项卡](https://devblogs.microsoft.com/visualstudio/personalize-docs/)。 现在，按项目对文件选项卡进行着色，以便不必搜寻打开的文件。

> [!NOTE]
> 若要使用颜色选项卡，请导航 **到"工具** >  >  > ""选项""环境""选项卡 **Windows**，然后选择"按项目对 **文档选项卡着色"**。

以下是我们到目前为止的更新：

- **[2022 Visual Studio 17.0 及](/visualstudio/releases/2022/release-notes-v17.0)** 更高版本中的新增功能：现在可以在编辑器的垂直和水平视图中对选项卡进行着色。

    以下屏幕截图显示了垂直视图中的颜色选项卡示例：

    :::image type="content" source="media/vs-2022/color-tabs-vertical.png" alt-text="垂直视图中颜色选项卡的屏幕截图。":::

    以下屏幕截图显示了水平视图中的颜色选项卡示例：

    :::image type="content" source="media/vs-2022/color-tabs-horizontal.png" alt-text="水平视图中颜色选项卡的屏幕截图。":::

- **[2022 Visual Studio 17.1 及](/visualstudio/releases/2022/release-notes)** 更高版本中的新增功能：还可以选择自己的选项卡颜色。 为此，请右键单击选项卡，然后选择"设置 **选项卡颜色** "以从调色板中选择。

    以下屏幕截图显示了如何个性化设置选项卡的配色方案的示例：

    :::image type="content" source="media/vs-2022/color-tabs-personalize-schemes.png" alt-text="&quot;设置选项卡选项&quot;的屏幕截图，可用于个性化设置选项卡的颜色。":::

::: moniker-end

#### <a name="tab-groups"></a>选项卡组

在 IDE 中使用两个或更多个打开的文档时，选项卡组可扩展管理有限工作区的功能。 可以将多个文档窗口和工具窗口组织为垂直或水平选项卡组，并可以随机变换文档在不同选项卡组中的位置。

### <a name="toolbars"></a>工具栏

要排列工具栏，可以将工具栏拖动到所需位置，也可以使用“自定义”对话框。 有关如何定位和自定义工具栏的详细信息，请参阅[如何：自定义菜单和工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)。

## <a name="arrange-and-dock-windows"></a>排列和停靠窗口

文档窗口或工具窗口可以“停靠”，以便其在 IDE 窗口框架中具有位置和大小。 还可以将其作为独立于 IDE 的单独浮动窗口。

可以将工具窗口停靠在 IDE 框架内的任何位置。 也可以将一些工具窗口作为选项卡式窗口停靠在编辑器框架中。 另外，可以将文档窗口停靠在编辑器框架内，且可按选项卡顺序固定到其当前位置。

还可以停靠多个窗口，使其共同浮动在 IDE 上方或外部的同一个“筏”中。 也可以隐藏或最小化工具窗口。

可以通过以下方式排列窗口：

- 将文档窗口固定到选项卡井左侧。

- 将窗口以选项卡形式停靠到编辑框。

- 将工具窗口停靠到 IDE 中的框架边缘。

- 在 IDE 的上方或外部浮动文档窗口或工具窗口。

- 沿 IDE 的边缘隐藏工具窗口。

- 在不同监视器上显示窗口。

- 窗口位置重置为默认布局或已保存的自定义布局。

若要排列工具窗口和文档窗口，可以将光标放在窗口的标题栏上，然后将其拖动到所需的位置。 或者，可以右键单击窗口的标题栏以使用其上下文菜单，也可以使用“窗口”菜单上的命令。

### <a name="dock-windows"></a>停靠窗口

单击和拖动工具窗口的标题栏或文档窗口的选项卡时，将显示一个菱形引导标记。 进行拖动操作时，当鼠标光标悬停在菱形中的一个箭头之上时，将出现一个阴影区域，显示如果现在释放鼠标按钮，窗口将停靠的位置。

若要移动可停靠窗口而不将其对齐到位，请在拖动窗口时按住 Ctrl 键。

若要将工具窗口或文档窗口返回到最近停靠的位置，请在双击该窗口的标题栏或选项卡的同时按 Ctrl。

下图显示文档窗口（仅可停靠在编辑框内）的菱形引导标记：

![文档窗口菱形引导标记](../ide/media/documentwindowguidediamonds.png)

工具窗口可固定到 IDE 中框架的一侧或固定到编辑框内。 将工具窗口拖动到另一个位置时，会显示一个菱形引导标记，可帮助助你轻松地重新停靠窗口。

![工具窗口菱形引导标记](../ide/media/vs10guidediamond.png)

下图显示“解决方案资源管理器”停靠在蓝色阴影区域标定的新位置：

![新位置处的停靠解决方案资源管理器](../ide/media/vs2015_dock_diamond.png)

### <a name="close-and-auto-hide-tool-windows"></a>关闭和自动隐藏工具窗口

通过单击标题栏右上角的“X”可关闭工具窗口。 要重新打开窗口，请使用其键盘快捷键或菜单命令。 工具窗口支持一项名为“自动隐藏”的功能，这可导致窗口在使用其他窗口时滑开。 窗口自动隐藏时，其名称将显示在 IDE 边缘的选项卡上。 若要再次使用该窗口，请指向该选项卡，使该窗口滑回视野。

![自动隐藏](../ide/media/vs2015_auto_hide.png)

> [!NOTE]
> 若要设置“自动隐藏”是单独针对工具窗口执行还是作为停靠组执行，请选中或清除“选项”对话框中的“自动隐藏按钮仅影响活动工具窗口” 。 有关详细信息，请参阅[“选项”对话框->“环境”->“常规”](../ide/reference/general-environment-options-dialog-box.md)。

> [!NOTE]
> 窗口处于使用状态时，启用了自动隐藏的工具窗口可能会暂时滑入视野。 若要再次隐藏该窗口，请选择位于当前窗口之外的项。 当窗口不处于使用状态时，它将滑出视野。

### <a name="use-a-second-monitor"></a>使用其他监视器

如果你还有一个监视器，并且操作系统支持，你可以选择在任一监视器上显示窗口。 甚至可以将多个窗口组合到其他监视器上的“筏”中。

> [!TIP]
> 可以创建 **“解决方案资源管理器”** 的多个实例，并将它们移动到另一个监视器。 右键单击窗口，并选择 **“新建解决方案资源管理器视图”** 。 可以通过在选择 Ctrl 键的同时双击，使所有窗口返回到原监视器。

### <a name="reset-name-and-switch-between-window-layouts"></a>重置、命名窗口布局，以及在各布局间切换

使用 **“重置窗口布局”** 命令，可将 IDE 恢复到原窗口布局以用于设置集合。 运行此命令时，将出现以下操作：

- 所有 windows 都移动到其默认位置。

- 默认窗口布局中关闭的所有窗口都关闭。

- 默认窗口布局中打开的所有窗口都打开。

### <a name="create-and-save-custom-layouts"></a>创建和保存自定义布局

Visual Studio 使你可以保存最多 10 个自定义窗口布局，并在这些布局之间快速切换。 以下步骤展示如何创建、保存、调用和管理自定义布局，这些布局利用带有停靠工具窗口和浮动工具窗口的多个监视器。

首先，创建一个具有两个项目的测试解决方案，每个项目具有不同的最佳布局。

#### <a name="create-a-ui-project-and-customize-the-layout"></a>创建 UI 项目，自定义布局

::: moniker range="vs-2017"

1. 创建新的 C#“WPF 应用”项目。 假设在此项目中，你将开发一个用户界面。 你希望将设计器窗口的空间最大化，并将其他工具窗口移开。

::: moniker-end

::: moniker range=">=vs-2019"

1. 创建新的 C# WPF 应用程序项目。 假设在此项目中，你将开发一个用户界面。 你希望将设计器窗口的空间最大化，并将其他工具窗口移开。

::: moniker-end

2. 如果有多个监视器，可将“解决方案资源管理器”窗口和“属性”窗口拉到第二个监视器旁。 在单监视器系统中，尝试关闭除设计器以外的所有其他窗口。

3. 按 Ctrl+Alt+X，显示“工具箱”窗口   。 如果窗口停靠，则拖动该窗口，使它浮动在你想要安放的位置。

4. 按 F5，将 Visual Studio 设置为调试模式。 根据需要调整“自动”、“调用堆栈”和“输出”调试窗口的位置  。 即将创建的布局将应用于编辑模式和调试模式。

5. 如果调试模式和编辑模式中的布局满足需要，则选择“窗口” > “保存窗口布局” 。 将此布局命名为“设计器”。

     请注意：新布局分配了来自保留列表 Ctrl+Alt+1...0 的下一个键盘快捷方式  。

#### <a name="create-a-database-project-and-layout"></a>创建数据库项目和布局

1. 将新的 **“SQL Server 数据库”** 项目添加到解决方案。

2. 在“解决方案资源管理器”中右键单击新项目，然后选择“在对象资源管理器中查看” 。 这将显示 **“SQL Server 对象资源管理器”** 窗口，可在该窗口中访问你的数据库中的表格、视图和其他对象。 可使此窗口浮动或停靠。 根据需要调整其他工具窗口。 如果要增强真实性，可添加实际数据库，但本演练不必这样做。

3. 如果布局满足要求，请在主菜单中选择“窗口” > “保存窗口布局” 。 将此布局命名为“DB 项目”。 （此项目不涉及调试模式布局。）

#### <a name="switch-between-the-layouts"></a>在布局之间切换

要在布局之间切换，可使用键盘快捷键，或者在主菜单中选择“窗口” > “应用窗口布局” 。

![应用窗口布局菜单](../ide/media/vs2015_applywindowlayout.png)

应用 UI 布局后，请注意此布局在编辑模式和调试模式中的保存方式。

如果在工作地点设置了多个监视器，在家里设置了一个单监视器笔记本电脑，则可创建为每个计算机优化的布局。

> [!NOTE]
> 如果在单监视器系统上应用多监视器布局，放置在第二个监视器上的浮动窗口将隐藏在 Visual Studio 窗口后。 可按 Alt + Tab 将这些窗口前置。如果稍后打开带多个监视器的 Visual Studio，则可通过重新应用布局将这些窗口恢复到其指定的位置。

#### <a name="manage-and-roam-your-layouts"></a>管理和漫游你的布局

可通过选择“窗口” > “管理窗口布局”来删除、重命名或重新排列自定义布局 。 如果移动布局，则键绑定自动调整以反映列表中的新位置。 绑定不能以其他方式修改，因此一次可存储最多 10 个布局。

![管理窗口布局](../ide/media/managewindowlayouts.png)

要提醒自己哪个键盘快捷键分配给了哪个布局，可选择“窗口” > “应用窗口布局” 。

这些布局自动在 Visual Studio 版本之间、单独计算机上的 Blend 实例之间以及从 Express Edition 到其他 Express 组织漫游。 但布局不在 Visual Studio、Blend 和 Express 之间漫游。

## <a name="see-also"></a>请参阅

- [如何：在 IDE 中移动](../ide/how-to-move-around-in-the-visual-studio-ide.md)
