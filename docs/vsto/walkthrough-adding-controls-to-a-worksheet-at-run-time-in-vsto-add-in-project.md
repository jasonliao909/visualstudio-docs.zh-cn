---
title: 在外接程序项目中VSTO控件添加到工作表
description: 了解如何使用功能区使用户能够向工作表添加 Button、NamedRange 和 ListObject。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], adding controls
- controls [Office development in Visual Studio], adding to worksheets at run time
- application-level add-ins [Office development in Visual Studio], adding controls
- worksheets, adding controls at run time
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d8706772526682c8856cedf5881ee0cd3f75dc76
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032142"
---
# <a name="walkthrough-add-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project"></a>演练：在外接程序项目中VSTO控件添加到工作表
  可通过使用 Excel VSTO 外接程序向任何打开的工作表添加控件。 本演练演示如何利用功能区使用户能够向工作表添加 <xref:Microsoft.Office.Tools.Excel.Controls.Button>、<xref:Microsoft.Office.Tools.Excel.NamedRange> 和 <xref:Microsoft.Office.Tools.Excel.ListObject>。 有关信息，请参阅[向Office添加控件。](../vsto/adding-controls-to-office-documents-at-run-time.md)

 **适用于：** 本主题中的信息适用于VSTO的外接程序Excel。 有关详细信息，请参阅[按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

 本演练演示以下任务：

- 提供用于将控件添加到工作表的用户界面 (UI)。

- 将控件添加到工作表。

- 从工作表中移除控件。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Excel

## <a name="create-a-new-excel-vsto-add-in-project"></a>新建Excel VSTO外接程序项目
 首先创建 Excel VSTO 外接程序项目。

### <a name="to-create-a-new-excel-vsto-add-in-project"></a>若要新建 Excel VSTO 外接程序项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，创建Excel VSTO **ExcelDynamicControls** 的外接程序项目。 有关详细信息，请参阅 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 添加对 **程序集Microsoft.Office.Tools.Excel.v4.0.Utilities.dll引用** 。 在本演练稍后内容中，需要此引用以编程方式将 Windows 窗体控件添加到工作表。

## <a name="provide-a-ui-to-add-controls-to-a-worksheet"></a>提供用于向工作表添加控件的 UI
 添加自定义选项卡到 Excel 功能区。 用户可以选中选项卡上的复选框，以向工作表添加控件。

#### <a name="to-provide-a-ui-to-add-controls-to-a-worksheet"></a>若要提供用于将控件添加到工作表的 UI

1. 在 **“项目”** 菜单上，单击 **“添加新项”**。

2. 在"**添加新项"对话框中**，选择"Visual Designer (**功能区) ，** 然后单击"添加 **"。**

     名为 **Ribbon1.cs** 或 **Ribbon1.vb** 的文件将在功能区设计器中打开并显示默认选项卡和组。

3. 从“工具箱”  的“Office 功能区控件” 选项卡中将“CheckBox”  控件拖到“group1” 上。

4. 单击 **CheckBox1** 以将其选中。

5. 在 **“属性”** 窗口中，更改下列属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**Button**|
    |**Label**|**Button**|

6. 将第二个复选框添加到 **group1**，然后更改下列属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**NamedRange**|
    |**Label**|**NamedRange**|

7. 向 **group1** 添加第三个复选框，然后更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**ListObject**|
    |**Label**|**ListObject**|

## <a name="add-controls-to-the-worksheet"></a>将控件添加到工作表
 托管的控件只能添加到主机项，充当容器。 因为 VSTO 外接程序项目使用任何打开的工作簿，所以 VSTO 外接程序会将工作表转换为主机项，或获取现有的主机项，然后才添加控件。 将代码添加到每个控件的单击事件处理程序中以生成基于打开的工作表的 <xref:Microsoft.Office.Tools.Excel.Worksheet> 主机项。 然后，在工作表当前所选内容中添加 <xref:Microsoft.Office.Tools.Excel.Controls.Button>、<xref:Microsoft.Office.Tools.Excel.NamedRange> 和 <xref:Microsoft.Office.Tools.Excel.ListObject>。

### <a name="to-add-controls-to-a-worksheet"></a>若要向工作表添加控件

1. 在功能区设计器中，双击"按钮 **"。**

     " <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click> 按钮"复选框 **的事件处理程序** 将在代码编辑器中打开。

2. 将 `Button_Click` 事件处理程序替换为以下代码。

     此代码使用 `GetVstoObject` 方法获取表示工作薄中第一个工作表的主机项，然后将 <xref:Microsoft.Office.Tools.Excel.Controls.Button> 控件添加到当前选定的单元格。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet2":::

3. 在 **解决方案资源管理器** 中，选择 *"Ribbon1.cs"* 或 *"Ribbon1.vb"。*

4. 在"视图 **"菜单** 上，单击"设计器 **"。**

5. 在功能区设计器中，双击 **NamedRange**。

6. 将 `NamedRange_Click` 事件处理程序替换为以下代码。

     此代码使用 `GetVstoObject` 方法获取表示工作簿中第一个工作表的主机项，然后为当前选定的单元格定义 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet3":::

7. 在功能区设计器中，双击 **"ListObject"。**

8. 将 `ListObject_Click` 事件处理程序替换为以下代码。

     此代码使用 `GetVstoObject` 方法获取表示工作薄中第一个工作表的主机项，然后为当前选定的单元格定义 <xref:Microsoft.Office.Tools.Excel.ListObject>。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet4":::

9. 将下面的语句添加到功能区代码文件的顶部。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/Ribbon1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/Ribbon1.vb" id="Snippet1":::

## <a name="remove-controls-from-the-worksheet"></a>从工作表中删除控件
 保存并关闭工作表时，不会保留控件。 保存工作表之前应以编程方式移除所有生成的 Windows 窗体控件，否则再次打开工作薄时，将仅出现控件的边框。 将代码添加到用于从生成的主机项的控件集合中移除 Windows 窗体控件的 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 事件中。 有关详细信息，请参阅在文档[文档中Office控件](../vsto/persisting-dynamic-controls-in-office-documents.md)。

### <a name="to-remove-controls-from-the-worksheet"></a>若要从工作表中移除控件

1. 在 **解决方案资源管理器** 中，选择 *"ThisAddIn.cs"* 或 *"ThisAddIn.vb"。*

2. 在 **“视图”** 菜单上，单击 **“代码”**。

3. 将以下方法添加到 `ThisAddIn` 类。 此代码会获取工作簿中的第一个工作表，然后使用 `HasVstoObject` 方法检查该工作表是否含有生成的工作表项目。 如果生成的工作表对象中含有控件，则该代码会获取工作表项目并循环访问控件集合，从而移除控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet6":::

4. 在 C# 中，必须为 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookBeforeSave> 事件创建一个事件处理程序。 你可以将此代码放置在 `ThisAddIn_Startup` 方法中。 有关创建事件处理程序的信息，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。 将 `ThisAddIn_Startup` 方法替换为以下代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet5":::

## <a name="test-the-solution"></a>测试解决方案
 通过从功能区上的自定义选项卡中选择控件，将控件添加到工作表。 保存该工作表时，这些控件也随之移除。

### <a name="to-test-the-solution"></a>若要测试解决方案。

1. 按 **F5** 运行项目。

2. 在 Sheet1 中选择任意单元格。

3. 单击 **“外接程序”** 选项卡。

4. 在 **group1 组中**，单击"按钮 **"。**

     选定的单元格中会出现一个按钮。

5. 在 Sheet1 中选择不同的单元格。

6. 在 **group1 组中**，单击 **"NamedRange"。**

     则会为选定的单元格定义命名范围。

7. 在 Sheet1 中选择一系列单元格。

8. 在 **group1 组中**，单击 **"ListObject"。**

     则会为选定的单元格添加列表对象。

9. 保存该工作表。

     添加到 Sheet1 的控件将不再出现。

## <a name="next-steps"></a>后续步骤
 你可以从此主题中了解关于 Excel VSTO 外接程序项目中控件的详细信息：

- 若要了解如何将控件保存到工作表，请参阅 Excel VSTO 开发示例和演练中的 Office 动态控件[示例](../vsto/office-development-samples-and-walkthroughs.md)。

## <a name="see-also"></a>请参阅
- [Excel解决方案](../vsto/excel-solutions.md)
- [Windows文档上的 Office 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [文档上的Office控件](../vsto/controls-on-office-documents.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [ListObject 控件](../vsto/listobject-control.md)
