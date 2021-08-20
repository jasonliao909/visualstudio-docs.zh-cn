---
title: 如何：向工作表添加 NamedRange 控件
description: 了解如何在设计时和运行时在文档级项目中将 NamedRange 控件添加到 Microsoft Office Excel 工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, adding to worksheets
- NamedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e6192a4fcd8a10f2152fc26602e52e3f9ec44f58
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122899"
---
# <a name="how-to-add-namedrange-controls-to-worksheets"></a>如何：向工作表添加 NamedRange 控件
  在文档级项目中，你可以在设计时和运行时将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到 Microsoft Office Excel 工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 你也可以在 VSTO 外接程序项目中，在运行时添加 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。

 本主题介绍了以下任务：

- [在设计时添加 NamedRange 控件](#designtime)

- [在运行时在文档级项目中添加 NamedRange 控件](#runtimedoclevel)

- [在运行时在 VSTO 外接程序项目中添加 NamedRange 控件](#runtimeaddin)

  有关控件的详细信息 <xref:Microsoft.Office.Tools.Excel.NamedRange> ，请参阅 [NamedRange 控件](../vsto/namedrange-control.md)。

## <a name="add-namedrange-controls-at-design-time"></a><a name="designtime"></a> 在设计时添加 NamedRange 控件
 有多种方法可在设计时在文档级项目中将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到工作表：从 Excel、从 Visual Studio“工具箱” ，以及从“数据源”  窗口。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-name-box-in-excel"></a>若要使用 Excel 中的“名称框”向工作表添加 NamedRange 控件

1. 选择要包含在命名范围中的一个或多个单元格。

2. 在 " **名称" 框** 中，键入范围名称并按 **enter**。

     **“名称框”** 位于公式栏旁边，也即工作表 **A** 列的正上方。

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-toolbox"></a>若要使用“工具箱”向工作表添加 NamedRange 控件

1. 打开 **“工具箱”** 并单击 **“Excel 控件”** 选项卡。

2. 单击 <xref:Microsoft.Office.Tools.Excel.NamedRange> 并将其拖到工作表。

     **“添加命名范围”** 对话框随即出现。

3. 选择要包含在命名范围中的一个或多个单元格。

4. 单击“确定”。

     如果不需要提供给控件的默认名称，可以在 **“属性”** 窗口中更改名称。

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-data-sources-window"></a>若要使用“数据源”窗口向工作表添加 NamedRange 控件

1. 打开“数据源”  窗口并为项目创建数据源。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

2. 将单个字段从 **“数据源”** 窗口拖到工作表中。

     数据绑定 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件将添加到工作表中。 有关详细信息，请参阅[数据绑定和 Windows 窗体](/dotnet/framework/winforms/data-binding-and-windows-forms)。

## <a name="add-namedrange-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 在运行时在文档级项目中添加 NamedRange 控件
 可以在运行时以编程方式将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到工作表。 这使得你可以创建宿主控件以响应事件。 工作表关闭时，动态创建的命名范围不作为宿主控件保留在工作表中。 有关详细信息，请参阅[在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)。

### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>以编程方式将 NamedRange 控件添加到工作表中

1. 在 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 的 `Sheet1`事件处理程序中，插入下列代码以将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到单元格 **A1** 并将其 <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> 属性设置为 `Hello world!`

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet3":::

## <a name="add-namedrange-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>在运行时在 VSTO 外接程序项目中添加 NamedRange 控件
 可以按编程方式将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到 VSTO 外接程序项目中任何打开的工作表中。 工作表关闭时，动态创建的命名范围不作为宿主控件保留在工作表中。 有关详细信息，请参阅在[运行时 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>以编程方式将 NamedRange 控件添加到工作表中

1. 下面的代码将生成基于打开工作表的工作表宿主项，然后将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到 **A1** 单元格并将其 <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> 属性设置为 `Hello world`。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet7":::

## <a name="see-also"></a>请参阅
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
