---
title: 功能区概述
description: 了解功能区如何组织相关命令，使其更易于查找，以及如何在功能区上将命令显示为控件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, multiple Ribbons
- Ribbon [Office development in Visual Studio], about Ribbon
- toolbars [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], multiple Ribbons
- toolbars [Office development in Visual Studio]
- custom Ribbon, multiple Ribbons
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2f125edbf25c5a7732f3ce168bf96b90f4d94c11
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099511"
---
# <a name="ribbon-overview"></a>功能区概述
  功能区是组织相关命令的一种方法，以便更易于查找。 命令在功能区上显示为控件。 控件按照应用程序 *窗口* 上边缘的水平条带组织成组。 在选项卡上，相关组进行了整理。

 现在可以使用功能区访问在早期版本的 Microsoft Office 系统中使用菜单和工具栏访问的大多数功能。 有关详细信息，请参阅技术文章开发人员概述[2007](/previous-versions/office/developer/office-2007/aa338198(v=office.12))Microsoft Office 系统。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="customize-the-microsoft-office-ribbon"></a>自定义Microsoft Office功能区
 若要自定义功能区，将以下功能区项之一添加到Office项目：

- **功能区(可视化设计器)**

- **功能区 (XML)**

  例如，若要自定义 Excel 功能区，则将功能区项添加到 Excel VSTO 外接程序项目中。

### <a name="ribbon-visual-designer-item"></a>Visual Designer (功能区) 项
 Visual **Designer (功能区)** 提供了高级工具，方便你设计和开发自定义功能区。 使用 **Visual Designer (功能区)** 以下列方式自定义功能区：

- 将自定义或内置选项卡添加到功能区。

- 将自定义组添加到自定义或内置选项卡。

  > [!NOTE]
  > 内置选项卡或组是应用程序功能区上已存在的Microsoft Office组。 例如，"**数据"** 选项卡是"数据"选项卡中的Excel。 " **连接** "组是"数据"选项卡上的 **内置** 组。

- 将自定义控件添加到自定义组。

- 将自定义控件添加到 Backstage 视图。

  若要详细了解如何使用"功能区"和"可视化设计器" (**自定义) 功能** 区，请参阅功能 [区设计器](../vsto/ribbon-designer.md)。

### <a name="ribbon-xml-item"></a>功能 (XML) 项
 如果要 **以功能区 (Visual** Designer) 项不支持的方式自定义功能区，请使用功能区 (**XML)** 项。 使用 **功能 (XML)** 项，以下列方式自定义功能区：

- 将 *内置组* 添加到自定义选项卡或内置选项卡。

- 将内置控件添加到自定义组。

- 添加自定义代码，以替代内置控件的事件处理程序。

- 自定义“快速访问工具栏”。

- 通过使用限定 ID，在 VSTO 外接程序之间共享功能区自定义项。

  有关如何使用功能区自定义功能区的详细信息，请参阅功能区 [XML](../vsto/ribbon-xml.md) **(XML)** 项。

## <a name="export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>将功能区从功能区设计器导出到功能区 XML
 如果使用功能区设计器创建功能区，然后决定以功能区 **(可视化** 设计器) 项不支持的方式自定义功能区，可以将功能区导出为 XML。

 Visual Studio自动创建功能 **区 (XML)** 项，并使用功能区上每个控件的元素和属性填充功能区 XML 文件。

 并非功能区设计器的"属性 **"窗口中的所有** 属性都传输到功能区 XML 文件。  例如，Visual Studio不导出 **Image** 或 **Text 属性的值**。 这是因为你必须在导出项目的功能区代码文件中创建一个回调方法，以分配图像或设置控件的文本。 在导出过程中，Visual Studio 不会自动生成回调方法。

 此外，任何未更改的默认属性值都不会出现在生成的功能区 XML 文件中。

 若要详细了解如何将功能区导出为 XML，请参阅如何：将功能区从功能区设计器 [导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)。

### <a name="update-the-code"></a>更新代码
 新的功能区代码文件将添加到 **解决方案资源管理器。** 此文件包含功能区 XML 类。 必须在此类的 `Ribbon Callbacks` 区域中创建回调方法，以处理用户操作（例如单击某个按钮）。 将你的代码从事件处理程序移动到这些回调方法，并修改此代码以使用功能区扩展性 (RibbonX) 编程模型。 有关更多信息，请参见 [Ribbon XML](../vsto/ribbon-xml.md)。

 还必须将代码添加到替代 `CreateRibbonExtensibilityObject` 方法并将功能区 XML 类返回到 Office 应用程序的 `ThisAddIn`、`ThisWorkbook` 或 `ThisDocument` 类。

 有关更多信息，请参见 [Ribbon XML](../vsto/ribbon-xml.md)。

## <a name="add-multiple-ribbon-items-to-a-project"></a>向项目添加多个功能区项
 可以将多个功能区项添加到单个项目中。 如果想要执行以下两项任务之一，这会非常有用：

- 为检查器 Outlook *功能区*。 有关详细信息，请参阅[为自定义功能区Outlook。](../vsto/customizing-a-ribbon-for-outlook.md)

    > [!NOTE]
    > 检查器是当用户执行某些任务时（例如，创建一封电子邮件时）打开的窗口。

- 选择要运行时显示的功能区。

### <a name="select-which-ribbons-to-display-at-run-time"></a>选择要运行时显示的功能区
 由于项目可以包含多个功能区，因此可以选择要运行时显示的功能区。

 若要选择要运行时显示的功能区，请重写项目的 、 或 类中的 方法，并返回 `CreateRibbonExtensibilityObject` `ThisAddin` `ThisWorkbook` `ThisDocument` 要显示的功能区。 以下示例检查名为 的字段的值， `myCondition` 并返回相应的功能区。

> [!NOTE]
> 此示例中使用的语法返回使用"功能区"和"可视化设计器" (**创建)** 功能区。 用于返回使用功能区创建的功能区的语法 (**XML)** 略有不同。 有关返回功能区和 **XML (的详细信息) ，** 请参阅 [功能区 XML](../vsto/ribbon-xml.md)。

 添加以下代码：

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.cs" id="Snippet1":::

### <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)|演示如何自定义 Microsoft Office 应用程序的功能区，将功能区 **(可视化** 设计器) 或功能区 (XML **)** 项添加到 Office 项目。|
|[功能区设计器](../vsto/ribbon-designer.md)|介绍如何使用功能区设计器将自定义选项卡、组和控件添加到应用程序的功能Microsoft Office功能区。|
|[演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|显示如何通过使用功能区设计器创建自定义功能区选项卡。 可使用功能区设计器将控件添加和放置到自定义选项卡上。|
|[功能区对象模型概述](../vsto/ribbon-object-model-overview.md)|提供了强类型对象模型的概述，该模型可用于在运行时获取和设置功能区控件的属性。|
|[演练：运行时更新功能区上的控件](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|演示如何使用功能区对象模型在功能区加载到 Office 应用程序之后，更新该功能区上的控件。|
|[自定义用于自定义Outlook](../vsto/customizing-a-ribbon-for-outlook.md)|提供有关如何在 Microsoft Office Outlook 中自定义功能区的指南。|
|[自定义 InfoPath 的功能区](../vsto/customizing-a-ribbon-for-infopath.md)|提供有关在 InfoPath 中自定义功能Microsoft Office指南。|
|[运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)|演示如何显示、隐藏和修改功能区，以及使用户能够从自定义任务窗格、操作窗格或窗体Outlook控件运行代码。|
|[如何：更改功能区上选项卡的位置](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|演示如何更改功能区上的选项卡顺序。|
|[如何：自定义内置选项卡](../vsto/how-to-customize-a-built-in-tab.md)|显示如何将组和控件添加到内置选项卡。|
|[如何：向 Backstage 视图添加控件](../vsto/how-to-add-controls-to-the-backstage-view.md)|演示如何将控件添加到单击"文件"时打开 **的菜单**。|
|[如何：向功能区组添加对话框启动器](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|显示将对话框启动器添加到功能区上的任何组。|
|[如何：将功能区从功能区设计器导出到功能区 XML](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|演示如何通过从设计器将功能区导出到功能区 XML，以高级方式自定义功能区。|
|[Ribbon XML](../vsto/ribbon-xml.md)|说明如何使用功能区 XML 自定义功能区。|
|[演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|演示如何使用"功能区"和"XML"选项卡 **(创建自定义功能)** 选项卡。|
