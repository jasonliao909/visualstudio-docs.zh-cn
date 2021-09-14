---
title: 如何：调整 ListObject 控件的大小
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Excel 工作簿中调整 ListObject 控件的大小。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- ListObject control, resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0dedb2aad7598e1a9a3f97123260580de9a93f34
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664705"
---
# <a name="how-to-resize-listobject-controls"></a>如何：调整 ListObject 控件的大小
  将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到 Microsoft Office Excel 工作簿时，可以设置该控件的大小；但是，你可能需要在以后重设其大小。 例如，你可能希望将两列式列表更改为三列式列表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 在文档级项目中，可以在设计时或运行时重设 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件的大小。 可以在 <xref:Microsoft.Office.Tools.Excel.ListObject> 运行时在 VSTO 外接程序项目中调整控件的大小。

 本主题介绍了以下任务：

- [在设计时调整 ListObject 控件的大小](#designtime)

- [在运行时在文档级项目中调整 ListObject 控件的大小](#runtimedoclevel)

- [在运行时在 VSTO 外接程序项目中调整 ListObject 控件的大小](#runtimeaddin)

  有关控件的详细信息 <xref:Microsoft.Office.Tools.Excel.ListObject> ，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

## <a name="resize-a-listobject-control-at-design-time"></a><a name="designtime"></a> 在设计时调整 ListObject 控件的大小
 若要重设列表的大小，可以单击并拖动其中一个尺寸控点，或者在“重设列表大小”  对话框中重新定义其大小。

### <a name="to-resize-a-list-by-using-the-resize-list-dialog-box"></a>使用“重设列表大小”对话框重设列表的大小

1. 单击表中的任意位置  <xref:Microsoft.Office.Tools.Excel.ListObject> 。 功能区中的 "**表工具**  >  **设计**" 选项卡随即出现。

2. 在 "属性" 部分中，单击 " **调整大小" 表**。

    ![VSTO_ResizeTable](../vsto/media/vsto-resizetable.png)

3. 为表选择新的数据区域。

4. 单击“确定”。

## <a name="resize-a-listobject-control-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 在运行时在文档级项目中调整 ListObject 控件的大小
 在运行时，可以使用 <xref:Microsoft.Office.Tools.Excel.ListObject> 方法重设 <xref:Microsoft.Office.Tools.Excel.ListObject.Resize%2A> 控件的大小。 不能使用此方法将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件移动到工作表中的新位置。 标题必须保持在同一行中，且重设大小后的 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件必须与原列表对象重叠。 重设大小后的 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件必须包含一个标题行，而且至少有一行数据。

### <a name="to-resize-a-list-object-programmatically"></a>以编程方式重设列表对象的大小

1. 在 <xref:Microsoft.Office.Tools.Excel.ListObject> 上创建一个跨单元格“A1”  到“B3”  的 `Sheet1`控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet6":::

2. 重设该列表的大小，使其包含单元格“A1”  到“C5” 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet7":::

## <a name="resize-a-listobject-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>在运行时在 VSTO 外接程序项目中调整 ListObject 的大小
 你可以在运行时在任何打开的工作表中调整 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件的大小。 有关如何 <xref:Microsoft.Office.Tools.Excel.ListObject> 使用 VSTO 外接程序向工作表添加控件的详细信息，请参阅[如何：将 ListObject 控件添加到工作表](../vsto/how-to-add-listobject-controls-to-worksheets.md)。

### <a name="to-resize-a-list-object-programmatically"></a>以编程方式重设列表对象的大小

1. 在 <xref:Microsoft.Office.Tools.Excel.ListObject> 上创建一个跨单元格“A1”  到“B3”  的 `Sheet1`控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet12":::

2. 重设该列表的大小，使其包含单元格“A1”  到“C5” 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet13":::

## <a name="see-also"></a>另请参阅
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject 控件](../vsto/listobject-control.md)
- [如何：向工作表添加 ListObject 控件](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [如何：调整书签控件的大小](../vsto/how-to-resize-bookmark-controls.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
