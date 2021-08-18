---
title: 功能区对象模型概述
description: 了解 Visual Studio Tools for Office 运行时如何公开一个强类型对象模型，你可以使用该模型在运行时获取和设置功能区控件的属性。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], object model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f7d840db368f61c0e85b5b21d7ff1c0a32b4a472
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032207"
---
# <a name="ribbon-object-model-overview"></a>功能区对象模型概述
  [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]公开了一个强类型对象模型，可用于在运行时获取和设置功能区控件的属性。 例如，可以动态填充菜单控件，或显示和隐藏控件根据上下文。 你还可以将选项卡、组和控件添加到功能区，但在 Office 应用程序加载功能区之前。 有关信息，请参阅 [设置变成只读属性](#SettingReadOnlyProperties)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 此功能区对象模型主要包含 [功能区类](#RibbonClass)、 [功能区事件](#RibbonEvents)和 [功能区控件类](#RibbonControlClasses)。

## <a name="ribbon-class"></a><a name="RibbonClass"></a> 功能区类
 向项目中添加新的 **功能区 (可视化设计器)** 项时，Visual Studio 将 **功能区** 类添加到项目。 **功能区** 类从类继承 <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> 。

 此类显示为在功能区代码文件和功能区设计器代码文件之间拆分的分部类。

## <a name="ribbon-events"></a><a name="RibbonEvents"></a> 功能区事件
 **功能区** 类包含以下三个事件：

|事件|说明|
|-----------|-----------------|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|在 Office 应用程序加载功能区自定义项时引发。 此 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load> 事件处理程序将自动添加到功能区代码文件中。 此事件处理程序用于在功能区加载时运行自定义代码。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|使您能够在功能区加载时缓存功能区自定义项中的图像。 如果在此事件处理程序中编写代码来缓存功能区图像，则可以获得略微的性能提升。 有关详细信息，请参阅 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage>。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|在功能区实例关闭时引发。|

## <a name="ribbon-controls"></a><a name="RibbonControlClasses"></a> 功能区控件
 <xref:Microsoft.Office.Tools.Ribbon>命名空间包含你在 "**工具箱**" 的 " **Office 功能区控件**" 组中看到的每个控件的类型。

 下表显示每个控件的类型 `Ribbon` 。 有关每个控件的说明，请参阅 [功能区概述](../vsto/ribbon-overview.md)。

|控件名称|类名|
|------------------|----------------|
|**Box**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**Button**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|
|**ButtonGroup**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|
|**ComboBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|
|**DropDown**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|
|**"编辑框**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**图库**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**组**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**Label**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|
|**菜单**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**机**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|
|**SplitButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|Tab|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ToggleButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|

 <xref:Microsoft.Office.Tools.Ribbon>命名空间对这些类型使用 "功能区" 前缀，以避免名称与命名空间中的控件类的名称冲突 <xref:System.Windows.Forms> 。

 向功能区设计器添加控件时，功能区设计器会将该控件的类声明为功能区设计器代码文件中的字段。

### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>使用功能区控件的属性的常见任务
 每个 `Ribbon` 控件都包含可用于执行各种任务的属性，例如向控件分配标签或隐藏和显示控件。

 在某些情况下，属性将在功能区加载后或控件添加到动态菜单之后变为只读。 有关详细信息，请参阅 [设置变成只读属性](#SettingReadOnlyProperties)。

 下表介绍了一些可以通过使用控件属性执行的任务 `Ribbon` 。

|对于此任务：|执行此操作：|
|--------------------|--------------|
|隐藏或显示控件。|使用 Visible 属性。|
|启用或禁用控件。|使用 "已启用" 属性。|
|设置控件的大小。|使用 ControlSize 属性。|
|获取显示在控件上的图像。|使用 Image 属性。|
|更改控件的标签。|使用 "标签" 属性。|
|向控件添加用户定义数据。|使用 Tag 属性。|
|获取 <xref:Microsoft.Office.Tools.Ribbon.RibbonBox> 、、 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 或中的项<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> 控件.|使用 Items 属性。|
|向 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> 、 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 或控件添加项 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 。|使用 Items 属性。|
|向添加控件 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> 。|使用 Items 属性。<br /><br /> 若要在 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> 功能区加载到 Office 应用程序后将控件添加到中，则必须在 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> 功能区加载到 Office 应用程序中之前将属性设置为 **true** 。 有关信息，请参阅 [设置变成只读属性](#SettingReadOnlyProperties)。|
|获取的选定项 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> ，<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 或 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 中的一项。|使用 SelectedItem 属性。 对于 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> ，请使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A> 属性。|
|获取上的组 <xref:Microsoft.Office.Tools.Ribbon.RibbonTab> 。|使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A> 属性。|
|指定在中显示的行数和列数 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 。|使用 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> 和 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> 属性。|

## <a name="set-properties-that-become-read-only"></a><a name="SettingReadOnlyProperties"></a> 设置变成只读属性
 某些属性只能在功能区加载之前设置。 设置这些属性有三个位置：

- 在 "Visual Studio **属性**" 窗口中。

- 在 **功能区** 类的构造函数中。

- 在 `CreateRibbonExtensibilityObject` `ThisAddin` 项目的、 `ThisWorkbook` 或类的方法中 `ThisDocument` 。

  动态菜单提供一些例外。 你可以创建新的控件，设置其属性，然后在运行时将它们添加到动态菜单，即使在包含该菜单的功能区加载后也是如此。

  可随时设置添加到动态菜单的控件的属性。

  有关详细信息，请参阅 [变成只读属性](#ReadOnlyProperties)。

### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>在功能区的构造函数中设置属性
 可以 `Ribbon` 在 **功能区** 类的构造函数中设置控件的属性。 此代码必须在调用方法后出现 `InitializeComponent` 。 如果当前时间为17:00 太平洋时间 () 或更高版本，则下面的示例将向组中添加一个新按钮。

 添加以下代码。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb" id="Snippet1":::

 在从 Visual Studio 2008 升级的 Visual c # 项目中，该构造函数将显示在功能区代码文件中。

 在 Visual Basic 项目或在中创建的 Visual c # 项目中 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] ，构造函数显示在功能区设计器代码文件中。 此文件名为 *YourRibbonItem*。.Cs 或 *YourRibbonItem*。设计器 .vb。 若要在项目中Visual Basic此文件，必须先单击"显示所有文件"按钮解决方案资源管理器。 

### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>在 CreateRibbonExtensibilityObject 方法中设置属性
 重写项目的 、 或 类中的 方法时 `Ribbon` `CreateRibbonExtensibilityObject` ，可以设置 `ThisAddin` `ThisWorkbook` `ThisDocument` 控件的属性。 有关 方法详细信息 `CreateRibbonExtensibilityObject` ，请参阅功能 [区概述](../vsto/ribbon-overview.md)。

 以下示例在工作簿项目的 类的 方法中 `CreateRibbonExtensibilityObject` `ThisWorkbook` 设置功能Excel属性。

 添加以下代码。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs" id="Snippet2":::

### <a name="properties-that-become-read-only"></a><a name="ReadOnlyProperties"></a> 变为只读的属性
 下表显示了只能在功能区加载之前设置的属性。

> [!NOTE]
> 你随时都可以在动态菜单上设置控件的属性。 在这种情况下，此表不适用。

|属性|功能区控件类|
|--------------|--------------------------|
|**BoxStyle**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**ColumnCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ControlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**动态**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**全球**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**组**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**ItemSize**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**MaxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**名称**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|
|**位置**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**RibbonType**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**RowCount**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**SizeString**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**选项卡**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**标题**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|

### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>设置显示在检查器中的功能Outlook属性
 每次用户打开显示功能区的检查器时，将创建功能区的新实例。 但是，只能在创建功能区的第一个实例之前设置上表中所列的属性。 创建第一个实例后，这些属性变为只读，因为第一个实例定义了用于加载功能Outlook XML 文件。

 如果在创建功能区的其他实例时，条件逻辑将这些属性中的任意一个设置为不同的值，则此代码将不起作用。

> [!NOTE]
> 确保 **为添加到** 功能区的每个控件设置 Name Outlook属性。 如果运行时向 Outlook功能区添加控件，则必须在代码中设置此属性。 如果在设计时向功能区Outlook控件，则会自动设置 Name 属性。

## <a name="ribbon-control-events"></a>功能区控件事件
 每个控件类都包含一个或多个事件。 下表将描述这些事件。

|事件|说明|
|-----------|-----------------|
|单击|在单击控件时发生。|
|TextChanged|在更改编辑框或组合框的文本时发生。|
|ItemsLoading|在系统请求控件的 Items 集合时Office。 Office项集合，直到代码更改控件的属性，或者调用 <xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A> 方法。|
|ButtonClick|在单击 或 中的按钮 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 时发生。|
|SelectionChanged|在 或 中的选择更改 <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 时 <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 发生。|
|DialogLauncherClick|在单击组右下角的对话启动器图标时发生。|

 这些事件的事件处理程序具有以下两个参数。

|参数|说明|
|---------------|-----------------|
|*发送*|一个 <xref:System.Object>，表示引发事件的控件。|
|*e*|一个包含 <xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs> 的 <xref:Microsoft.Office.Core.IRibbonControl>。 使用此控件可以访问在 提供的功能区对象模型中不可用的任何属性 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。|

## <a name="see-also"></a>请参阅
- [运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：运行时更新功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [自定义用于自定义Outlook](../vsto/customizing-a-ribbon-for-outlook.md)
- [如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)
- [如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [如何：显示外接程序用户界面错误](../vsto/how-to-show-add-in-user-interface-errors.md)
