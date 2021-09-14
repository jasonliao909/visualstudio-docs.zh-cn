---
title: 使用单选按钮更新工作表中的图表
description: 了解在工作表上使用单选Microsoft Excel的基础知识，让用户能够快速切换选项。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664685"
---
# <a name="walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons"></a>演练：使用单选按钮更新工作表中的图表
  本演练演示了在工作表Microsoft Office Excel单选按钮的基础知识，让用户能够快速切换选项。 在这种情况下，选项将更改图表的样式。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 若要将结果视为已完成的示例，请参阅 Excel 示例和Office[示例。](../vsto/office-development-samples-and-walkthroughs.md)

 本演练演示以下任务：

- 将一组单选按钮添加到工作表。

- 在选择了某个选项时更改图表样式。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="add-a-chart-to-a-worksheet"></a>将图表添加到工作表
 可以创建自定义Excel工作簿的工作簿项目。 在此演练中，你将向工作簿添加一个图表，然后在新的 Excel 解决方案中使用此工作簿。 本演练中的数据源是名为 Data for Chart **的工作表**。

### <a name="to-add-the-data"></a>添加数据

1. 打开 Microsoft Excel。

2. 右键单击 **"Sheet3"** 选项卡， **然后单击快捷菜单** 上的"重命名"。

3. 将工作表重命名为 **"图表的数据"。**

4. 将以下数据添加到"图表数据 **"，** 单元格 A4 位于左上角，E8 位于右下角。

   |区域/季度|Q1|Q2|Q3|Q4|
   |-|--------|--------|--------|--------|
   |West|500|550|550|600|
   |东部|600|625|675|700|
   |北部|450|470|490|510|
   |南部|800|750|775|790|

   接下来，将图表添加到第一个工作表以显示数据。

### <a name="to-add-a-chart-in-excel"></a>在图表中添加Excel

1. 在"**插入"** 选项卡上的"**图表"** 组中，单击"列 **"，然后单击**"**所有图表类型"。**

2. 在"**插入图表"** 对话框中，单击"确定 **"。**

3. 在"**设计"** 选项卡上的"**数据"** 组中，单击"**选择数据"。**

4. 在" **选择数据源"对话框中** ，单击 **"Chartdata 范围"框** 并清除任何默认选择。

5. 在" **图表数据"** 工作表中，选择包含数字的单元格块，其中包括右上角的 A4，右下角的 E8。

6. 在"**选择数据源"对话框中**，单击"确定 **"。**

7. 重新定位图表，使右上角与单元格 **E2 对齐**。

8. 将文件保存到驱动器 C，**并将其ExcelChart.xlsx。**

9. 退出 Excel。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，将基于 **ExcelChart** Excel创建一个工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一Excel工作簿项目，其名称为"我的Excel **图表"。** 在向导中，选择 **"复制现有文档"。**

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 单击" **浏览** "按钮，浏览到之前在此演练中创建的工作簿。

3. 单击“确定”。

     Visual Studio设计器中打开新的 Excel 工作簿，并将"我的 Excel **图表**"项目添加到 **解决方案资源管理器。**

## <a name="set-properties-of-the-chart"></a>设置图表的属性
 使用现有工作簿Excel工作簿项目时，会自动为工作簿中所有命名范围、列表对象和图表创建宿主控件。 可以使用"属性" <xref:Microsoft.Office.Tools.Excel.Chart> 窗口更改 **控件** 的名称。

### <a name="to-change-the-name-of-the-chart-control"></a>更改图表控件的名称

1. 在设计器 <xref:Microsoft.Office.Tools.Excel.Chart> 中选择控件，在"属性"窗口中更改 **以下** 属性。

    |Property|值|
    |--------------|-----------|
    |**名称**|**dataChart**|
    |**HasLegend**|**false**|

## <a name="add-controls"></a>添加控件
 此工作表使用单选按钮为用户提供快速更改图表样式的方法。 但是，单选按钮需要是排他按钮 - 选择一个按钮时，不能同时选择组中其他按钮。 向工作表添加多个单选按钮时，默认情况下不会发生此行为。

 添加此行为的一种方式是，对用户控件上的单选按钮进行分组，在用户控件后面编写代码，然后将用户控件添加到工作表。

### <a name="to-add-a-user-control"></a>要添加用户控件

1. 选择"**我的Excel图表**"**项目。解决方案资源管理器。**

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在"**添加新项"对话框中**，单击"**用户控件"，** 将控件命名 **ChartOptions，然后单击**"添加 **"。**

### <a name="to-add-radio-buttons-to-the-user-control"></a>向用户控件添加单选按钮

1. 如果用户控件在设计器中不可见，请在 中双击 **"ChartOptions"解决方案资源管理器。** 

2. 从" **工具箱"的** "公共控件" **选项卡中，** 将 **单** 选按钮控件拖到用户控件，并更改以下属性。

   | Property | 值 |
   |----------|------------------|
   | **名称** | **columnChart** |
   | **文本** | **柱形图** |

3. 向用户控件添加第二个单选按钮，并更改以下属性。

   | Property | 值 |
   |----------|---------------|
   | **名称** | **barChart** |
   | **文本** | **条形图** |

4. 将第三个单选按钮添加到用户控件，并更改以下属性。

   | Property | 值 |
   |----------|----------------|
   | **名称** | **lineChart** |
   | **文本** | **折线图** |

5. 将第四个单选按钮添加到用户控件，并更改以下属性。

   |Property|值|
   |--------------|-----------|
   |**名称**|**areaBlockChart**|
   |**文本**|**面积图**|

   接下来，在单击单选按钮时编写代码以更新图表。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>选中单选按钮时更改图表样式
 现在，您可以添加代码以更改图表样式。 为此，请在用户控件上创建一个公共事件，添加一个属性以设置选择类型，并为 `CheckedChanged` 每个单选按钮的事件创建一个事件处理程序。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>创建用户控件的事件和属性

1. 在 **解决方案资源管理器** 中，右键单击用户控件，然后单击 " **查看代码**"。

2. 向类添加代码 `ChartOptions` 以创建 `SelectionChanged` 事件和 `Selection` 属性。

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

5. 在 C# 中，必须为单选按钮添加事件处理程序。 可以将此代码添加到 `ChartOptions` 构造函数中 `InitializeComponent` 调用的下面。 有关如何创建事件处理程序的信息，请参阅[如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/ChartOptions.cs" id="Snippet18":::

## <a name="add-the-user-control-to-the-worksheet"></a>将用户控件添加到工作表
 生成解决方案时，新的用户控件将自动添加到 " **工具箱**"。 然后，可以将该控件从 " **工具箱** " 拖动到工作表中。

### <a name="to-add-the-user-control-your-worksheet"></a>向工作表添加用户控件

1. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

     将 **ChartOptions** 用户控件添加到 " **工具箱**"。

2. 在 **解决方案资源管理器** 中，右键单击 " **sheet1** " 或 " **sheet1**"，然后单击 " **视图设计器**"。

3. 将 **ChartOptions** 控件从 **工具箱** 拖到工作表中。

     名为的新控件 `my_Excel_Chart_ChartOptions1` 将添加到你的项目中。

4. 将控件的名称更改为 **ChartOptions1**。

## <a name="change-the-chart-type"></a>更改图表类型
 若要更改图表类型，请创建一个事件处理程序，该事件处理程序根据用户控件中选定的选项设置样式。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-worksheet"></a>更改工作表中显示的图表的类型

1. 将以下事件处理程序添加到 `Sheet1` 类。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet19":::

2. 在 c # 中，必须为用户控件添加事件处理程序，如下 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 所示。 有关如何创建事件处理程序的信息，请参阅[如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet20":::

## <a name="test-the-application"></a>测试应用程序
 你现在可以测试工作簿，以确保在你选择单选按钮时正确地设计图表的样式。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 选择不同的单选按钮。

3. 确认图表样式随所选选项发生了相应的更改。

## <a name="next-steps"></a>后续步骤
 本演练演示在工作表上使用单选按钮和图表样式的基础知识。 以下是接下来可能要执行的一些任务：

- 部署项目。 有关详细信息，请参阅[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)。

- 使用按钮填充文本框。 有关详细信息，请参阅 [演练：使用按钮在工作表的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)。

- 通过使用复选框更改工作表的格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改工作表格式](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>另请参阅
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
