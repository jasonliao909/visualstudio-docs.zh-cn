---
title: 如何：向工作表添加图表控件
description: 了解如何在设计时和运行时在文档级自定义项中将图表控件添加到 Microsoft Office Excel 工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2e714f486ebfb83f6cf5b6374e722b7d83cd3de3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664754"
---
# <a name="how-to-add-chart-controls-to-worksheets"></a>如何：向工作表添加图表控件
  您可以在 <xref:Microsoft.Office.Tools.Excel.Chart> 设计时和运行时在文档级自定义项中将控件添加到 Microsoft Office Excel 工作表。 你还可以在 <xref:Microsoft.Office.Tools.Excel.Chart> 运行时 VSTO 外接程序中添加控件。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 本主题介绍了以下任务：

- [在设计时添加图表控件](#designtime)

- [在运行时在文档级项目中添加图表控件](#runtimedoclevel)

- [在运行时在 VSTO 外接程序项目中添加图表控件](#runtimeaddin)

  有关控件的详细信息 <xref:Microsoft.Office.Tools.Excel.Chart> ，请参阅 [图表控件](../vsto/chart-control.md)。

## <a name="add-chart-controls-at-design-time"></a><a name="designtime"></a> 在设计时添加图表控件
 可按照与从应用程序添加图表相同的方式，将 <xref:Microsoft.Office.Tools.Excel.Chart> 控件添加到工作表中。

> [!NOTE]
> 控件在 " <xref:Microsoft.Office.Tools.Excel.Chart> **工具箱** " 或 " **数据源** " 窗口中不可用。

### <a name="to-add-a-chart-host-control-to-a-worksheet-in-excel"></a>将图表主机控件添加到 Excel 的工作表中

1. 在 " **插入** " 选项卡上的 " **图表** " 组中，单击 " **列**"，单击 "图表" 类别，然后单击所需的图表类型。

2. 在 " **插入图表** " 对话框中，单击 **"确定"**。

3. 在 " **设计** " 选项卡上的 " **数据** " 组中，单击 " **选择数据**"。

4. 在 "**选择数据源**" 对话框中，在 "**图表****数据区域**" 框中单击，并清除任何默认选择。

5. 在 " **图表数据** " 工作表中，选择包含图表数据的单元格范围 (单元格 **A5** 到 **D8**) 。

6. 在 " **选择数据源** " 对话框中，单击 **"确定"**。

## <a name="add-chart-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 在运行时在文档级项目中添加图表控件
 可以在运行时动态添加 <xref:Microsoft.Office.Tools.Excel.Chart> 控件。 文档关闭时，动态创建的图表不会作为主机控件保留在文档中。 有关详细信息，请参阅[在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)。

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>以编程方式将图表控件添加到工作表中

1. 在 `Sheet1` 的 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 事件处理程序中，插入下列代码以添加 <xref:Microsoft.Office.Tools.Excel.Chart> 控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet1":::

## <a name="add-chart-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>在运行时在 VSTO 外接程序项目中添加图表控件
 可以按编程方式将 <xref:Microsoft.Office.Tools.Excel.Chart> 控件添加到 VSTO 外接程序项目中任何打开的工作表中。 有关详细信息，请参阅在[运行时 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

 工作表关闭时，动态创建的图表控件不会作为主机控件保留在工作表中。 有关详细信息，请参阅[在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)。

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>以编程方式将图表控件添加到工作表中

1. 下面的代码将生成基于打开工作表的工作表主机项，然后添加 <xref:Microsoft.Office.Tools.Excel.Chart> 控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet9":::

## <a name="compile-the-code"></a>编译代码
 此示例具有下列要求：

- 制成图表并存储在工作表中 A5 到 D8 范围内的数据。

## <a name="see-also"></a>另请参阅
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [图表控件](../vsto/chart-control.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [在 Office 解决方案中将数据绑定到控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
