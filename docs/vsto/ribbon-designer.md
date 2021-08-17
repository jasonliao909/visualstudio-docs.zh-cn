---
title: 功能区设计器
description: 了解如何使用功能区设计器向应用程序的功能区添加自定义选项卡、组Microsoft Office控件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- Designer_Microsoft.VisualStudio.Tools.Office.Ribbon.Design.RibbonDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, about Ribbon Designer
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- customizing the Ribbon, about Ribbon Designer
- Ribbon [Office development in Visual Studio], visual designer
- customizing the Ribbon
- custom Ribbon
- designers [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon [Office development in Visual Studio], common tasks
- Ribbon Designer [Office development in Visual Studio]
- read-only properties
- Ribbon [Office development in Visual Studio], shortcut keys
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 5bef09e7b808b4473f15b2d103bac7a55ce1eef8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025766"
---
# <a name="ribbon-designer"></a>功能区设计器
  功能区设计器是可视化设计画布。 使用功能区设计器将自定义选项卡、组和控件添加到应用程序的功能Microsoft Office功能区。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 若要打开功能区设计器，请为项目 (**Visual Designer)** 功能区。 然后，可以使用设计工具执行以下任务：

- [设计功能区布局](#DesigningRibbonLayout)

- [处理事件并设置控件属性](#HandleEventsSetProperties)

- [将控件添加到 Backstage 视图](#CustomizingMicrosoftOfficeButton)

> [!NOTE]
> 使用功能区设计器无法完成某些任务。 有关这些任务以及如何完成这些任务的信息，请参阅功能 [区概述](../vsto/ribbon-overview.md)。

## <a name="add-a-ribbon-visual-designer-item-to-a-project"></a>向项目 (Visual Designer) 功能区
 若要使用功能区设计器，请向项目 (**Visual Designer)** 功能区。 有关详细信息，请参阅 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

 在 Visual Designer 项目 **(功能区) ，Visual Studio** 自动将以下文件添加到项目：

- 功能区代码文件。 此文件具有你在"添加新项"对话框中 (**Visual Designer**) 功能区 **项目** 的名称。 添加代码以处理此文件的功能区事件。

- 功能区设计器代码文件。 此文件包含功能区设计器生成的代码，不应直接编辑。

- 资源文件。 此文件包含功能区上每个控件的属性值。

  如果已有来自另一 **(项目** 的功能区) ，可以使用"添加现有项"对话框在当前 **项目中重复使用** 它。

## <a name="design-a-ribbon"></a><a name="DesigningRibbonLayout"></a> 设计功能区
 有三种方法可以打开功能区设计器：

- 在 **解决方案资源管理器** 中，双击功能区代码文件。

- 在 **解决方案资源管理器** 中，右键单击功能区代码文件，然后单击 **视图设计器。**

- 在 **解决方案资源管理器** 中，选择功能区代码文件，然后单击 **"视图"** 菜单上的 **"设计器** "。

  功能区设计器包含默认选项卡和组。 可以从功能区设计器中删除默认选项卡和组。 若要删除默认组，请右键单击 **"Group1"，** 然后单击"删除 **"。** 若要删除默认选项卡，请右键单击设计图面的空白区域，然后单击"**删除功能区选项卡"。**

  还可以将自定义选项卡、组和控件添加到功能区设计器。 可以在"工具箱"的"功能 **区控件"** 组中Office **控件**。 有三种方法可以将控件从"功能区控件Office **添加到** 功能区设计器：

- 将控件拖到功能区设计器上的相应区域。

- 单击控件，然后在功能区设计器中单击相应的区域。

- 在设计器中选择适当的区域，然后双击"工具箱"中的 **控件**。

### <a name="ribbon-design-workflow"></a>功能区设计工作流
 按照以下基本步骤设计功能区布局：

1. [将自定义选项卡添加到功能区](#AddTabToRibbon)。

2. [将组添加到选项卡](#AddGroupsToTab)。

3. [将控件添加到组](#AddControlsToGroups)。

   只能在组上删除控件;不能将控件直接拖动到选项卡或功能区。 只能在选项卡上删除组;不能将组直接拖动到功能区。

   将控件拖动到正确的位置来排列控件。 可以使用"属性"窗口设置 **控件** 的属性。

   不能在功能区上将控件从一个选项卡拖动到另一个选项卡。 如果要将控件移动到另一个选项卡，则必须使用 **Cut** 命令从一个选项卡中删除该控件，然后将该控件粘贴到另一个选项卡上。如果剪切并粘贴控件，事件处理程序将停止工作。 可以在"属性"窗口中重新连接 **事件** 处理程序。 有关详细信息，请参阅[属性窗口。](../ide/reference/properties-window.md)

### <a name="add-custom-tabs-to-the-ribbon"></a><a name="AddTabToRibbon"></a> 将自定义选项卡添加到功能区
 有三种方法可以将自定义选项卡添加到功能区：

- 从"工具箱"添加 **选项卡**。

- 右键单击功能区设计器，然后单击"**添加功能区选项卡"。**

- 打开选项卡 **集合编辑器**，然后单击"添加 **"。**

   若要打开选项卡集合 **编辑器**，请在"属性"窗口中选择"选项卡"属性，然后单击移动设计器省略号 ASP.NET ![省略号按钮](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")。

  添加选项卡后，可以添加组以包含控件。

#### <a name="remove-custom-tabs-from-the-ribbon"></a>从功能区中删除自定义选项卡
 有三种方法可以删除功能区中的自定义选项卡：

- 右键单击设计器，然后单击"删除 **功能区选项卡"。**

- 在"**属性"窗口** 的"**命令"窗格中**，单击"**删除功能区选项卡"。**

- 打开"**选项卡集合编辑器"，** 选择选项卡，然后单击"删除 **"。**

#### <a name="change-the-position-of-a-tab-on-the-ribbon"></a>更改功能区上选项卡的位置
 可以更改功能区上自定义选项卡的顺序。 还可以在功能区上的内置选项卡之前或之后放置自定义选项卡。 有关详细信息，请参阅 [如何：更改功能区 上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)。

#### <a name="customize-built-in-tabs-on-the-ribbon"></a>自定义功能区上的内置选项卡
 内置选项卡是已位于应用程序功能区上的选项卡Microsoft Office选项卡。 例如，"**数据"** 选项卡是"数据"选项卡中的Excel。

 可以将组和控件添加到内置选项卡。默认情况下，自定义组在内置选项卡上显示为最后一个组，但可以在选项卡上的任何内置组之前或之后移动它。

 不能删除内置组。

 若要详细了解如何自定义内置选项卡，请参阅 [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)。

### <a name="add-groups-to-a-tab"></a><a name="AddGroupsToTab"></a> 将组添加到选项卡
 组以逻辑方式组织功能区上的控件。 将组添加到选项卡。 将所有其他控件添加到组。

### <a name="add-controls-to-groups"></a><a name="AddControlsToGroups"></a> 向组添加控件
 向组添加一个或多个控件。 下表描述了每个控件。

|控件|说明|
|-------------|-----------------|
|**Box**|用于组织组中控件的容器。 可以将除分隔符、组或选项卡以外的任何控件添加到框中。框可以是水平或垂直的。|
|**Button**|启动操作按钮。 可以将按钮添加到组、按钮组、下拉列表、库、菜单或拆分按钮。|
|**ButtonGroup**|包含一个或多个按钮、切换按钮、菜单、拆分按钮和库的组。 可以将按钮组添加到组或菜单。|
|**CheckBox**|选中或清除以打开或关闭选项的框。|
|**ComboBox**|附加了列表框的编辑框。 用户可以键入或选择其选择。 此框显示当前选定内容。 使用 属性在功能区加载到应用程序之前或之后Office <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Items%2A> 项。|
|**拉**|用户可以选择的项的列表。 用户不能在下拉列表中键入新项。<br /><br /> 使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Items%2A> 属性可向列表中添加项。 您可以在运行时添加和移除项。<br /><br /> 使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Buttons%2A> 属性可向列表中添加按钮。 但是，在功能区加载到 Office 应用程序中之后，不能在运行时添加和删除按钮。|
|**"编辑框**|一个框，用户可以在其中键入文本。|
|**图库**|一个菜单，该菜单显示用户可从中选择的可视化选项的数组或网格。 可以在菜单中控制选择的布局。 使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> 和 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> 属性来指定将显示库的项和按钮的行数和列数。|
|**Label**|可以用来标识功能区上控件的文本。|
|**菜单**|一个下拉列表，其中可以包含以下任何控件：<br /><br /> -按钮<br />-复选框<br />-库<br />-菜单<br />-拆分按钮<br />-切换按钮<br />-分隔符<br /><br /> 若要将控件添加到功能区设计器中的菜单，请单击菜单中的向下箭头以显示菜单设计图面。 然后，您可以将功能区控件从 **工具箱** 拖至菜单上。 若要排列控件，请将其拖到所需的位置。<br /><br /> 若要在 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> 功能区加载到 Office 应用程序后将控件添加到中，则必须在 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> 加载功能区之前将属性设置为 **true** 。 有关如何执行此操作的信息，请参阅 [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。|
|**机**|用于分隔列表中的项的窄条。 添加到组时，条形是垂直的。 添加到菜单时，条形是水平的。|
|**SplitButton**|附加了菜单的按钮。 拆分按钮可以包含以下任何控件：<br /><br /> -按钮<br />-复选框<br />-库<br />-菜单<br />-拆分按钮<br />-切换按钮<br />-分隔符<br /><br /> 与菜单类似，"拆分" 按钮具有其自己的设计图面。 但是，与菜单不同，在功能区加载到 Office 应用程序中之前，只能更新拆分按钮中的项。 有关如何更新拆分按钮中的项的信息，请参阅 [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。|
|**ToggleButton**|显示为按下或未按下的按钮。|

## <a name="handle-events-and-setting-properties"></a><a name="HandleEventsSetProperties"></a> 处理事件和设置属性
 功能区设计器使您能够通过使用 " **属性** " 窗口在设计时设置控件属性。 此外，功能区公开了一个强类型对象模型，可用于在运行时获取和设置功能区控件的属性。

 您可以双击设计器上的任何控件，打开控件的默认事件的事件处理程序。 您可以使用 " **属性** " 窗口为所有其他控件事件创建事件处理程序。

 功能区事件和属性位于 <xref:Microsoft.Office.Tools.Ribbon> 命名空间中。 **功能区 (可视化设计器)** 项会自动在项目中添加对此程序集的引用，并在功能区代码文件的顶部插入适当的 **using** 或 **Imports** 语句。

 有关处理功能区事件和在运行时设置功能区控件的属性的信息，请参阅 [功能区对象模型概述](../vsto/ribbon-object-model-overview.md)。

## <a name="customize-backstage-view"></a><a name="CustomizingMicrosoftOfficeButton"></a> 自定义 Backstage 视图
 您可以使用功能区设计器将控件添加到单击 " **文件** " 选项卡时打开的菜单。此菜单称为 Backstage 视图。

 不能使用功能区设计器在内置控件之前或之后放置控件。 内置控件是已在 Backstage 视图中显示的控件。 如果要将控件放置在内置控件之前或之后，必须使用功能区 XML。 有关 **功能区 (XML)** 的详细信息，请参阅 [功能区 XML](../vsto/ribbon-xml.md)。 有关自定义 Backstage 视图的详细信息，请参阅面向[开发人员的 Office 2010 backstage 视图的简介](/previous-versions/office/developer/office-2010/ee691833(v=office.14))，并[为开发人员自定义 Office 2010 backstage 视图](/previous-versions/office/developer/office-2010/ee815851(v=office.14))。

 [!INCLUDE[appliesto_ribbon_2010](../vsto/includes/appliesto-ribbon-2010-md.md)]

 有关如何向 Backstage 视图添加控件的信息，请参阅 [如何：向 backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)。

## <a name="accessibility-in-the-ribbon-designer"></a><a name="Accessibility"></a> 功能区设计器中的辅助功能
 您可以使用键盘快捷方式在功能区设计器中移动控件。 某些键盘快捷方式适用于所有控件，有些快捷方式仅适用于具有菜单的控件。

 下表显示了适用于所有控件的键盘快捷方式。

|操作|键盘快捷键|
|------------|-----------------------|
|将控件移动到列表中上一个控件之前。|**Ctrl** +**向上**<br /><br /> **Ctrl** +**左**|
|将控件移动到列表中的下一个控件之后。|**Ctrl** +**下**<br /><br /> **Ctrl** +**向右**|
|将所选内容从一个控件移到同一个组中的另一个控件。 对于下拉面板，请在父控件和下拉面板中的控件之间移动。|**Up**<br /><br /> **向下**|
|向前循环访问所有控件。|Tab|
|循环访问所有控件。|**Shift**+**Tab**|
|删除所选的一个或一组控件。|**删除**|
|复制选定的控件。|**Ctrl** +**C**|
|剪切选定的控件。|**Ctrl** +**X**|
|从剪贴板粘贴控件。|**Ctrl** +**V**|
|选择 " **工具箱**"。|**Ctrl** +**Alt** +**X**|
|选择父组件。|**Esc**|

 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>下表显示了仅适用于 Microsoft Office 菜单、和的键盘快捷方式 <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> 。

|操作|键盘快捷键|
|------------|-----------------------|
|如果下拉面板已打开，并且在下拉面板上选择了控件，则选择父控件。|**Left**|
|如果下拉面板已打开且已选择父控件，请关闭下拉面板。|**Left**|
|打开下拉面板。|**Right**|
|如果下拉列表面板已打开，请选择下拉面板上的第一个控件。|**Right**|
|关闭下拉面板。|**Esc**|

## <a name="see-also"></a>请参阅

- [功能区概述](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
