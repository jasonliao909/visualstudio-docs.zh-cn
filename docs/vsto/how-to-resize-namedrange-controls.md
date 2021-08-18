---
title: 如何：调整 NamedRange 控件的大小
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Excel 工作簿中调整 NamedRange 控件的大小。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- NamedRange control, resizing
- ranges, resizing in Excel
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6f30671c883c06834e9c00fadd81760b123ae9f4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115221"
---
# <a name="how-to-resize-namedrange-controls"></a>如何：调整 NamedRange 控件的大小
  将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到 Microsoft Office Excel 文档时，可以设置该控件的大小；但是，你可能需要在以后调整其大小。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 在文档级项目中，可以在设计时或运行时调整命名范围的大小。 还可以在运行时在应用程序级 VSTO 外接程序中调整命名范围的大小。

 本主题介绍了以下任务：

- [在设计时调整 NamedRange 控件的大小](#designtime)

- [在运行时在文档级项目中调整 NamedRange 控件的大小](#runtimedoclevel)

- [在运行时在 VSTO 外接程序项目中调整 NamedRange 控件的大小](#runtimeaddin)

## <a name="resize-namedrange-controls-at-design-time"></a><a name="designtime"></a> 在设计时调整 NamedRange 控件的大小
 可以通过在“定义名称”  对话框中重新定义其大小来调整命名范围的大小。

### <a name="to-resize-a-named-range-by-using-the-define-name-dialog-box"></a>使用“定义名称”对话框来调整命名范围的大小

1. 右击 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。

2. 在快捷菜单上单击“管理命名范围”  。

     “定义名称”  对话框随即出现。

3. 选择要调整大小的命名范围。

4. 清除 **引用** 框。

5. 选择要用来定义命名范围大小的单元格。

6. 单击“确定”。

## <a name="resize-namedrange-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 在运行时在文档级项目中调整 NamedRange 控件的大小
 可以通过编程的方式，使用 <xref:Microsoft.Office.Tools.Excel.NamedRange.RefersTo%2A> 属性调整命名范围的大小。

> [!NOTE]
> 在“属性”  窗口中， <xref:Microsoft.Office.Tools.Excel.NamedRange.RefersTo%2A> 属性标记为“只读”。

### <a name="to-resize-a-named-range-programmatically"></a>以编程方式调整命名范围大小

1. 在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 的单元格 **A1** 中创建一个 `Sheet1`控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet4":::

2. 调整命名范围的大小，使其包含单元格 **B1**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet5":::

## <a name="resize-namedrange-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>在运行时在 VSTO 外接程序项目中调整 NamedRange 控件的大小
 你可以在运行时在任何打开的工作表中调整 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件的大小。 有关如何 <xref:Microsoft.Office.Tools.Excel.NamedRange> 使用 VSTO 外接程序向工作表添加控件的详细信息，请参阅[如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)。

### <a name="to-resize-a-named-range-programmatically"></a>以编程方式调整命名范围大小

1. 在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 的单元格 **A1** 中创建一个 `Sheet1`控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet10":::

2. 调整命名范围的大小，使其包含单元格 **B1**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet11":::

## <a name="see-also"></a>请参阅
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [如何：调整书签控件的大小](../vsto/how-to-resize-bookmark-controls.md)
- [如何：调整 ListObject 控件的大小](../vsto/how-to-resize-listobject-controls.md)
