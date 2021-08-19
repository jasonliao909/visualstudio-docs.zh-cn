---
title: 使用单选按钮更新工作表中的图表
description: 了解在 Microsoft Excel 工作表上使用单选按钮的基础知识，使用户能够在两个选项之间快速切换。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, updating using managed controls
- controls [Office development in Visual Studio], updating worksheets
- worksheets, using radio buttons
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4edf0813fcbcd9b7013b85bcf251da9a47beb78a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155377"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>演练：使用单选按钮更新工作表中的图表
  本演练演示了在 Microsoft Office Excel 工作表上使用单选按钮的基础知识，使用户能够在两个选项之间快速切换。 在这种情况下，选项更改图表的样式。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 若要查看已完成示例的结果，请参阅[Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)中的 Excel 控件示例。

 本演练演示以下任务：

- 向工作表添加一组单选按钮。

- 在选择了某个选项时更改图表样式。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="add-a-chart-to-a-worksheet"></a>向工作表添加图表
 您可以创建一个自定义现有工作簿的 Excel 工作簿项目。 在本演练中，您将向工作簿添加一个图表，然后在新的 Excel 解决方案中使用此工作簿。 此演练中的数据源是一个名为 " **图表" 的数据** 工作表。

### <a name="to-add-the-data"></a>添加数据

1. 打开 Microsoft Excel。

2. 右键单击 " **Sheet3** " 选项卡，然后单击快捷菜单上的 " **重命名** "。

3. 将工作表重命名为 " **图表数据**"。

4. 将以下数据添加到单元格 A4 为左上角的 **图表** ，并 E8 右下角。

   |区域/季度|Q1|Q2|Q3|Q4|
   |-|--------|--------|--------|--------|
   |West|500|550|550|600|
   |东部|600|625|675|700|
   |北部|450|470|490|510|
   |南部|800|750|775|790|

   接下来，将图表添加到第一个工作表以显示数据。

### <a name="to-add-a-chart-in-excel"></a>在 Excel 中添加图表

1. 在 " **插入** " 选项卡上的 " **图表** " 组中，单击 " **列**"，然后单击 " **所有图表类型**"。

2. 在 " **插入图表** " 对话框中，单击 **"确定"**。

3. 在 " **设计** " 选项卡上的 " **数据** " 组中，单击 " **选择数据**"。

4. 在 " **选择数据源** " 对话框中，单击 " **chartdata.zip" 范围** 框，并清除任何默认选择。

5. 在 " **图表数据** " 工作表中，选择包含数字的单元格块，其中包含从左上角到右下角 E8 的 A4。

6. 在 " **选择数据源** " 对话框中，单击 **"确定"**。

7. 重新定位图表，使右上角与单元格 **E2** 对齐。

8. 将文件保存到驱动器 C，并将其命名 **ExcelChart.xlsx**。

9. 退出 Excel。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，你将基于 **ExcelChart** 工作簿创建 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 "**我的 Excel" 图表** 创建 Excel 工作簿项目。 在向导中，选择 " **复制现有文档**"。

     有关详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 单击 " **浏览** " 按钮，浏览到本演练前面部分创建的工作簿。

3. 单击“确定”。

     Visual Studio 在设计器中打开新的 Excel 工作簿，并将 **我的 Excel 图表** 项目添加到 **解决方案资源管理器**。

## <a name="set-properties-of-the-chart"></a>设置图表的属性
 当您创建使用现有工作簿的新 Excel 工作簿项目时，将自动为该工作簿中的所有命名范围、列表对象和图表创建宿主控件。 您可以 <xref:Microsoft.Office.Tools.Excel.Chart> 使用 " **属性** " 窗口更改控件的名称。

### <a name="to-change-the-name-of-the-chart-control"></a>更改图表控件的名称

1. <xref:Microsoft.Office.Tools.Excel.Chart>在设计器中选择控件，并在 "**属性**" 窗口中更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**dataChart**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>添加控件
 此工作表使用单选按钮，以使用户能够快速更改图表样式。 但是，单选按钮需要是专用的-当选择一个按钮时，不能同时选择组中的其他按钮。 在将多个单选按钮添加到工作表时，默认情况下不会发生此行为。

 添加此行为的一种方法是将单选按钮分组到用户控件上，在用户控件后面编写代码，然后将用户控件添加到工作表。

### <a name="to-add-a-user-control"></a>要添加用户控件

1. 选择 **解决方案资源管理器** 中的 **"我的 Excel 图表** 项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在 " **添加新项** " 对话框中，单击 " **用户控件**"，将控件命名为 " **ChartOptions"，** 然后单击 " **添加**"。

### <a name="to-add-radio-buttons-to-the-user-control"></a>向用户控件添加单选按钮

1. 如果用户控件在设计器中不可见，请在 **解决方案资源管理器** 中双击 " **ChartOptions** "。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 **单选按钮** 控件拖到用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|------------------|
   | **名称** | **columnChart** |
   | **文本** | **柱形图** |

3. 将第二个单选按钮添加到用户控件，并更改以下属性。

   | 属性 | 值 |
   |----------|---------------|
   | **名称** | **barChart** |
   | **文本** | **条形图** |

4. 向用户控件添加第三个单选按钮，并更改以下属性。

   | 属性 | 值 |
   |----------|----------------|
   | **名称** | **lineChart** |
   | **文本** | **线条图** |

5. 向用户控件添加第四个单选按钮，并更改以下属性。

   |属性|值|
   |--------------|-----------|
   |**名称**|**areaBlockChart**|
   |**文本**|**面积图**|

   接下来，编写代码以在单击单选按钮时更新图表。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>选择单选按钮时更改图表样式
 现在，可以添加代码来更改图表样式。 为此，请针对用户控件创建公共事件，添加属性以设置选择类型，并为每个单选按钮的 事件创建 `CheckedChanged` 事件处理程序。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>创建用户控件的事件和属性

1. 在 **解决方案资源管理器** 中，右键单击用户控件，然后单击"**查看代码"。**

2. 将代码添加到 `ChartOptions` 类以创建 `SelectionChanged` 事件和 `Selection` 属性。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet13":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet13":::

### <a name="to-handle-the-checkedchanged-event-of-the-radio-buttons"></a>处理单选按钮的 CheckedChanged 事件

1. 设置 `CheckedChanged` 单选按钮的 `areaBlockChart` 事件处理程序中的图表类型，然后引发事件。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet14":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet14":::

2. 设置 `CheckedChanged` 单选按钮的 `barChart` 事件处理程序中的图表类型。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet15":::

3. 设置 `CheckedChanged` 单选按钮的 `columnChart` 事件处理程序中的图表类型。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet16":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet16":::

4. 设置 `CheckedChanged` 单选按钮的 `lineChart` 事件处理程序中的图表类型。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/ChartOptions.vb" id="Snippet17":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet17":::

5. 在 C# 中，必须为单选按钮添加事件处理程序。 可以将此代码添加到 `ChartOptions` 构造函数中 `InitializeComponent` 调用的下面。 若要了解如何创建事件处理程序，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet18":::

## <a name="add-the-user-control-to-the-worksheet"></a>将用户控件添加到工作表
 生成解决方案时，新用户控件会自动添加到"工具箱 **"中**。 然后，可以将控件从"工具箱 **"** 拖动到工作表。

### <a name="to-add-the-user-control-your-worksheet"></a>将用户控件添加到工作表

1. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

     **ChartOptions** 用户控件将 **添加到工具箱**。

2. 在 **解决方案资源管理器** 中，右键单击 **Sheet1.vb** 或 **Sheet1.cs，** 然后单击视图设计器 **。**

3. 将 **ChartOptions** 控件从" **工具箱"** 拖动到工作表。

     名为 的新 `my_Excel_Chart_ChartOptions1` 控件将添加到项目中。

4. 将控件的名称更改为 **ChartOptions1**。

## <a name="change-the-chart-type"></a>更改图表类型
 若要更改图表类型，请创建一个事件处理程序，用于根据用户控件中所选的选项设置样式。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>更改工作表中显示的图表类型

1. 将以下事件处理程序添加到 `Sheet1` 类。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet19":::

2. 在 C# 中，必须将用户控件的事件处理程序添加到 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 事件，如下所示。 若要了解如何创建事件处理程序，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet20":::

## <a name="test-the-application"></a>测试应用程序
 现在，可以在选择单选按钮时测试工作簿，以验证图表的样式是否正确。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 选择不同的单选按钮。

3. 确认图表样式随所选选项发生了相应的更改。

## <a name="next-steps"></a>后续步骤
 本演练演示了在工作表上使用单选按钮和图表样式的基础知识。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅[部署Office解决方案](../vsto/deploying-an-office-solution.md)。

- 使用按钮填充文本框。 有关详细信息，请参阅演练：使用按钮 在工作表的文本框 [中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)。

- 使用复选框更改工作表上的格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改工作表格式](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>请参阅
- [使用 Excel](../vsto/walkthroughs-using-excel.md)
