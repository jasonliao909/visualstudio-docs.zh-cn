---
title: 使用功能区按钮同步自定义任务窗格
description: 了解如何创建自定义任务窗格，用户可以单击功能区上的切换按钮隐藏或显示该窗格。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom task panes [Office development in Visual Studio], showing and hiding
- showing custom task panes
- Ribbon [Office development in Visual Studio], custom task panes
- toggle buttons [Office development in Visual Studio]
- custom task panes [Office development in Visual Studio], synchronizing with Ribbon button
- user interfaces [Office development in Visual Studio], custom task panes
- synchronization [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], showing and hiding
- custom task panes [Office development in Visual Studio], creating
- hiding custom task panes
- task panes [Office development in Visual Studio], creating
- task panes [Office development in Visual Studio], synchronizing with Ribbon button
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ce9f00bf31013450c25dd3bac6325e7288be50a2b866989fd3b0b9d301b30410
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121225746"
---
# <a name="walkthrough-synchronize-a-custom-task-pane-with-a-ribbon-button"></a>演练：使用功能区按钮同步自定义任务窗格
  本演练演示如何创建自定义任务窗格，用户可以单击功能区上的切换按钮隐藏或显示该窗格。 应始终创建一个可供用户单击以显示或隐藏你的自定义任务窗格的用户界面 (UI) 元素，如按钮，因为 Microsoft Office 应用程序不提供用户用于显示或隐藏自定义任务窗格的默认方式。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 虽然本演练具体使用的是 Excel，但其中所阐释的概念同样适用于上面所列的应用程序。

 本演练演示以下任务：

- 设计自定义任务窗格的 UI。

- 向功能区添加切换按钮。

- 使用自定义任务窗格同步切换按钮。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel 或 Microsoft [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)]。

## <a name="create-the-add-in-project"></a>创建外接程序项目
 在此步骤中，将为 VSTO 创建一个外接程序Excel。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Excel 外接程序项目模板，创建一个名为 **SynchronizeTaskPaneAndRibbon** 的 Excel 外接程序项目。 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 打开 **ThisAddIn.cs** 或 **ThisAddIn.vb** 代码文件，并将 **SynchronizeTaskPaneAndRibbon** 项目添加到 **“解决方案资源管理器”**。

## <a name="add-a-toggle-button-to-the-ribbon"></a>向功能区添加切换按钮
 Office 应用程序的设计准则之一是：用户应始终能控制 Office 应用程序 UI。 若要让用户可以控制自定义任务窗格，可以添加一个可显示和隐藏任务窗格的功能区切换按钮。 若要创建一个切换按钮，则将 **“功能区(可视化设计器)”** 项添加到项目。 设计器可帮助你添加和放置控件、设置控件属性以及处理控件事件。 有关详细信息，请参阅功能 [区设计器](../vsto/ribbon-designer.md)。

### <a name="to-add-a-toggle-button-to-the-ribbon"></a>向功能区添加切换按钮

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在 **“添加新项”** 对话框中，选择 **“功能区(可视化设计器)”**。

3. 将新功能区更名为 **ManageTaskPaneRibbon**，然后单击“添加” 。

     **ManageTaskPaneRibbon.cs** 或 **ManageTaskPaneRibbon.vb** 文件将在功能区设计器中打开，并显示一个默认选项卡和组。

4. 在功能区设计器中，单击“Group1” 。

5. 在“属性”  窗口中，将“Label”属性  设置为 **Task Pane Manager**。

6. 从“工具箱”  的“Office 功能区控件” 选项卡中，将 **ToggleButton** 拖到“Task Pane Manager”  组。

7. 单击“toggleButton1” 。

8. 在“属性”  窗口中，将“Label”属性  设置为 **Show Task Pane**。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>设计自定义任务窗格的用户界面
 没有针对自定义任务窗格的可视化设计器，但可以设计具有所需布局的用户控件。 稍后在本演练中，你将向自定义任务窗格添加用户控件。

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>若要设计自定义任务窗格的用户界面

1. 在 **“项目”** 菜单上，单击 **“添加用户控件”**。

2. 在“添加新项”  对话框中，将用户控件的名称更改为 **TaskPaneControl**，然后单击“添加” 。

     用户控件将在设计器中打开。

3. 从“工具箱”  的“公共控件” 选项卡中，将 **TextBox** 控件拖到用户控件中。

## <a name="create-the-custom-task-pane"></a>创建自定义任务窗格
 若要在 VSTO 外接程序启动时创建自定义任务窗格，请将用户控件添加到 VSTO 外接程序的 <xref:Microsoft.Office.Tools.AddIn.Startup> 事件处理程序中的任务窗格中。 默认情况下，自定义任务窗格将不可见。 本演练稍后将添加代码，当用户单击添加到功能区的切换按钮时，该代码将显示或隐藏任务窗格。

### <a name="to-create-the-custom-task-pane"></a>若要创建自定义任务窗格

1. 在 **“解决方案资源管理器”** 中，展开 **“Excel”**。

2. 右键单击 **ThisAddIn.cs** 或 **ThisAddIn.vb** ，然后单击“查看代码” 。

3. 将以下代码添加到 `ThisAddIn` 类。 此代码将 `TaskPaneControl` 的实例声明为 `ThisAddIn`的成员。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet1":::

4. 将 `ThisAddIn_Startup` 事件处理程序替换为以下代码。 此代码向 `TaskPaneControl` 字段添加 `CustomTaskPanes` 对象，但它不显示自定义任务窗格（默认情况下， <xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> 类的 <xref:Microsoft.Office.Tools.CustomTaskPane> 属性是 **false**）。 Visual C# 代码还会将一个事件处理程序附加到 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> 事件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet2":::

5. 将以下方法添加到 `ThisAddIn` 类。 此方法处理 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> 事件。 当用户通过单击 **“关闭”** 按钮 (X) 来关闭任务窗格时，此方法将更新功能区上切换按钮的状态。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet3":::

6. 向 `ThisAddIn` 类添加以下属性。 此属性对其他类公开私有 `myCustomTaskPane1` 对象。 稍后在本演练中，你将向使用此属性的 `MyRibbon` 类添加代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb" id="Snippet4":::

## <a name="hide-and-show-the-custom-task-pane-by-using-the-toggle-button"></a>使用切换按钮隐藏和显示自定义任务窗格
 最后一步是添加可在用户单击功能区上的切换按钮时显示或隐藏自定义任务窗格的代码。

### <a name="to-display-and-hide-the-custom-task-pane-by-using-the-toggle-button"></a>通过使用切换按钮显示和隐藏自定义任务窗格

1. 在功能区设计器中，双击“显示任务窗格”  切换按钮。

     Visual Studio 会自动生成名为 `toggleButton1_Click`的事件处理程序，它将处理切换按钮的 <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> 事件。 Visual Studio 还会打开代码编辑器中的 *MyRibbon.cs* 或 *MyRibbon.vb* 文件。

2. 将 `toggleButton1_Click` 事件处理程序替换为以下代码。 当用户单击切换按钮时，此代码显示或隐藏自定义任务窗格，具体取决于是按下还是未按下切换按钮。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.cs" id="Snippet5":::

## <a name="test-the-add-in"></a>测试外接程序
 运行项目时，Excel 会打开，但不显示自定义任务窗格。 单击功能区上的切换按钮以测试代码。

### <a name="to-test-your-vsto-add-in"></a>测试 VSTO 外接程序

1. 按 **F5** 运行项目。

     确认Excel打开，功能 **区** 上会显示"外接程序"选项卡。

2. 单击功能 **区上的"** 外接程序"选项卡。

3. 在 **“任务窗格管理器”** 组中，单击 **“显示任务窗格”** 切换按钮。

     验证当点击切换按钮时，任务窗格交替显示和隐藏。

4. 当任务窗格可见时，单击任务窗格一角的 **“关闭”** 按钮 (X)。

     验证切换按钮显示为未按下。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何创建自定义任务窗格的详细信息：

- 在外接程序中为VSTO创建自定义任务窗格。 有关支持自定义任务窗格的应用程序的详细信息，请参阅 [自定义任务窗格](../vsto/custom-task-panes.md)。

- 从自定义任务窗格自动化应用程序。 有关详细信息，请参阅 [演练：从自定义任务窗格 自动执行应用程序](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)。

- 为 Outlook 中打开的每封电子邮件创建自定义任务窗格。 有关详细信息，请参阅演练：在 中显示包含电子邮件的自定义[Outlook。](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)

## <a name="see-also"></a>请参阅
- [自定义任务窗格](../vsto/custom-task-panes.md)
- [如何：向应用程序添加自定义任务窗格](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [演练：从自定义任务窗格自动执行应用程序](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [演练：显示包含电子邮件的自定义任务Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
- [功能区概述](../vsto/ribbon-overview.md)
