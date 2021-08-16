---
title: 如何：调整工作表单元格中的控件大小
description: 了解如何在设计时和运行时使用 Visual Studio 在 Microsoft Excel 工作表单元格中调整控件的大小。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], resizing
- managed controls, resizing
- worksheets, resizing
- Windows Forms controls [Office development in Visual Studio], resizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4df6ea34f13e26ef24b32169a8f3db30298895bf05fc00ef8f4e88438910c817
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121366116"
---
# <a name="how-to-resize-controls-within-worksheet-cells"></a>如何：调整工作表单元格中的控件大小
  当调整工作表中的列或行的大小时，单元中的所有主机控件都将自动调整大小，以调整调整后的单元格的高度或宽度。 Windows默认情况下，窗体控件不会自动调整大小。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 如果在设计时添加控件，则必须设置每个控件的定位选项。

 如果以编程方式添加 Windows 窗体控件并提供 range 参数，则当调整范围内的单元格大小时，控件会自动调整大小。 有关详细信息，请参阅[在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="resize-controls-at-design-time"></a>在设计时调整控件大小

### <a name="to-make-controls-resize-with-cells-at-design-time"></a>在设计时使控件调整单元格大小

1. 从 "**工具箱**" 中，将 Windows 窗体控件拖到工作表。

2. 右键单击控件，然后单击 " **设置控件格式**"。

3. 在 " **设置控件格式** " 对话框中，单击 " **属性** " 选项卡。

4. 在 " **对象定位**" 下，选择 " **移动单元大小** " 选项，然后单击 **"确定"**。

     当调整包含控件的单元格的大小时，控件调整大小以适合单元格。

## <a name="resize-controls-at-run-time"></a>在运行时调整控件大小
 如果在运行时添加 Windows 窗体控件并传入 <xref:Microsoft.Office.Interop.Excel.Range> 作为控件的位置，则当调整包含该范围的工作表单元格的大小时，控件将自动调整大小。

### <a name="to-make-controls-resize-with-cells-at-run-time"></a>在运行时使控件调整单元格大小

1. 将控件添加到 A1 范围。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet5":::

     当调整包含控件的单元格的大小时，控件调整大小以适合单元格。

## <a name="reset-control-placement"></a>重置控件位置
 可以通过将 `Placement` 属性设置为以下值之一来重置控件的位置和大小调整 <xref:Microsoft.Office.Interop.Excel.XlPlacement> ：

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMove>

- <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlMoveAndSize>

### <a name="to-change-the-behavior-of-a-control-so-that-it-does-not-resize-or-move-with-the-cell"></a>更改控件的行为，使其不会调整单元格的大小或移动

1. 调用控件的 "位置" 属性，并将值设置为 <xref:Microsoft.Office.Interop.Excel.XlPlacement.xlFreeFloating> 。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet6":::

## <a name="see-also"></a>另请参阅
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [如何：在打印时隐藏工作表上的控件](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Office 文档上 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
