---
title: 演练：针对 NamedRange 控件的事件进行编程
description: 了解如何通过使用 Visual Studio 中的开发工具Microsoft Excel NamedRange 控件，并针对其事件Office NamedRange Visual Studio。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, programming against events
- worksheets, changing cell values
- NamedRange control, events
- worksheets, events
- worksheets, automating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8a6b5ca7d884fbece6795f63d668aa04a8ba6f80
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664931"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>演练：针对 NamedRange 控件的事件进行编程
  本演练演示如何通过使用 Visual Studio Office 开发工具，将控件添加到 Microsoft Office Excel 工作表并针对其 <xref:Microsoft.Office.Tools.Excel.NamedRange> 事件进行Visual Studio。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 在本演练中，你将学会如何执行以下任务：

- 将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到工作表。

- 针对控制 <xref:Microsoft.Office.Tools.Excel.NamedRange> 事件进行编程。

- 测试项目。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 在此步骤中，你将使用 Excel 创建一个Visual Studio。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一Excel名为 **"我的命名范围事件"的工作簿项目**。 确保已 **选择"创建新** 文档"。 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio设计器中打开新的 Excel 工作簿，并将"我的命名范围 **事件**"项目添加到 **解决方案资源管理器。**

## <a name="add-text-and-named-ranges-to-the-worksheet"></a>将文本和命名范围添加到工作表
 由于宿主控件是Office对象扩展的，因此可以以与添加本机对象相同的方式将它们添加到文档中。 例如，可以通过打开"插入Excel，指向"名称"，并选择"定义"，将一个控件 <xref:Microsoft.Office.Tools.Excel.NamedRange> 添加到 **工作表**。  还可以将控件 <xref:Microsoft.Office.Tools.Excel.NamedRange> 从"工具箱"拖动到工作表 **上来** 添加控件。

 在此步骤中，你将使用工具箱 将两个命名范围控件添加到工作表 **，然后将** 文本添加到工作表。

### <a name="to-add-a-range-to-your-worksheet"></a>向工作表添加范围

1. 验证"*我的命名范围"Events.xlsx* 工作簿是否已打开，Visual Studio设计器中显示 `Sheet1` 。

2. 从 **"Excel"** 的"控件"选项卡中，将控件拖动 <xref:Microsoft.Office.Tools.Excel.NamedRange> 到 **中的单元格 A1。** `Sheet1`

     将出现 **"添加 NamedRange 控件** "对话框。

3. 验证 **$A"文本框** 中是否显示"$1"，并选中单元格 **A1。** 如果不是，请单击单元格 **A1** 将其选中。

4. 单击“确定”。

     单元格 **A1** 成为名为 的范围 `namedRange1` 。 工作表上没有可见的指示，但在选择单元格 A1 (位于左侧工作表上方的"名称"框中) `namedRange1` **显示**。 

5. 将另 <xref:Microsoft.Office.Tools.Excel.NamedRange> 一个控件添加到 **单元格 B3**。

6. 验证 **$B"文本框中是否显示"$3"，** 并选中单元格 **B3。** 如果不是，请单击单元格 **B3** 将其选中。

7. 单击“确定”。

     单元格 **B3** 成为名为 的范围 `namedRange2` 。

### <a name="to-add-text-to-your-worksheet"></a>向工作表添加文本

1. 在单元格 **A1** 中，键入以下文本：

    **这是 NamedRange 控件的示例。**

2. 在 **单元格 A3** (左侧 `namedRange2`) ，键入以下文本：

    **事件：**

   在下列部分中，将编写代码，以将文本插入到 控件中并修改 控件的属性，以响应 的 、 和 `namedRange2` `namedRange2` <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 事件 `namedRange1` 。

## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>添加代码以响应 BeforeDoubleClick 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>基于 BeforeDoubleClick 事件将文本插入 NamedRange2

1. 在 **解决方案资源管理器** 中，右键单击 **"Sheet1.vb"** 或 **"Sheet1.cs"，然后选择**"**查看代码"。**

2. 添加代码， `namedRange1_BeforeDoubleClick` 使事件处理程序如下所示：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet24":::

3. 在 C# 中，必须为命名范围添加事件处理程序，如下事件 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 所示。 有关创建事件处理程序的信息，请参阅[如何：](../vsto/how-to-create-event-handlers-in-office-projects.md)在项目中Office处理程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet25":::

## <a name="add-code-to-respond-to-the-change-event"></a>添加代码以响应 Change 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>根据 Change 事件将文本插入 namedRange2

1. 添加代码， `NamedRange1_Change` 使事件处理程序如下所示：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet26":::

    > [!NOTE]
    > 由于双击某个范围中的Excel进入编辑模式，因此，即使未对文本进行更改，当所选内容移动到范围外时，也 <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> 会出现事件。

## <a name="add-code-to-respond-to-the-selectionchange-event"></a>添加代码以响应 SelectionChange 事件

### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>根据 SelectionChange 事件将文本插入 namedRange2

1. 添加代码 **，NamedRange1_SelectionChange** 事件处理程序如下所示：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet27":::

    > [!NOTE]
    > 由于双击某个范围中的Excel会导致所选内容移动到该范围内，因此在事件发生 <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> 之前会发生事件。

## <a name="test-the-application"></a>测试应用程序
 现在，可以测试工作簿，验证在引发事件时，描述控件事件的文本是否插入到另一 <xref:Microsoft.Office.Tools.Excel.NamedRange> 个命名范围中。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 将光标置于 中，并验证是否插入了有关事件的文本，以及是否向工作表插入 `namedRange1` <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> 了注释。

3. 在 中双击 ，并验证有关事件的文本是否插入了中红色 `namedRange1` <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> italicized 文本 `namedRange2` 。

4. 单击 外部并注意，退出编辑模式时会发生更改事件，即使未更改 `namedRange1` 文本。

5. 更改 中的文本 `namedRange1` 。

6. 单击 外部 `namedRange1` ，验证有关 事件的文本是否插入 <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> 了蓝色文本 `namedRange2` 。

## <a name="next-steps"></a>后续步骤
 本演练演示了针对 控件的事件编程的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 基础知识。 下面是下一步可能完成的任务：

- 部署项目。 有关详细信息，请参阅[部署Office解决方案](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>另请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用Excel对象自动执行自动执行](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [如何：在项目中创建Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)
