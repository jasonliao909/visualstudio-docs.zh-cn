---
title: NamedRange 控件
description: 了解 NamedRange 控件如何是具有唯一名称、公开事件并可以绑定到数据的范围。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.Range
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, named
- NamedRange control, events
- NamedRange control, data binding
- NamedRange control
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 002fa5135eb99c671cd00eef76299858a3c8cba4ae1ea80cec46335486fb3d69
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121366012"
---
# <a name="namedrange-control"></a>NamedRange 控件
  <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件是一个具有唯一名称的范围，可用于公开事件且可以绑定到数据。 有关详细信息，请参阅对象[Excel概述](../vsto/excel-object-model-overview.md)。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>创建控件
 在文档级项目中，你可以在设计时或在运行时将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到 Microsoft Office Excel 工作表中。

 在 VSTO 外接程序中，你可以在运行时将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件添加到工作表中。 有关详细信息，请参阅 [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)。

> [!NOTE]
> 默认情况下，工作表关闭时，动态创建的命名范围不作为宿主控件保留在工作表中。 有关详细信息，请参阅[向Office添加控件。](../vsto/adding-controls-to-office-documents-at-run-time.md)

 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件可以仅包含特定的工作表上的范围。 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件不能具有适用于所有表的相对名称并且它们不能包含跨越工作簿中的两个或多个工作表的范围（3-D 范围）。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 命名的区域似乎很适合复杂的数据绑定，因为它可以有多个单元格；但是，范围仅仅是单元格的集合，无法轻易地从数据集映射到特定列。 因此， <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件仅支持简单数据绑定。 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件可用于复杂数据绑定。 有关详细信息，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

 可以使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 属性将 <xref:System.Windows.Forms.Control.DataBindings%2A> 控件绑定到数据源。 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件的默认数据绑定属性是 <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A>。

 如果绑定数据集中的数据通过任何机制进行了更新，那么 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件会反映这些变化。

## <a name="formatting"></a>格式设置
 可应用于 <xref:Microsoft.Office.Interop.Excel.Range> 的格式设置也可应用于 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。 这包括边框、字体、数字格式和样式。

## <a name="rename-the-control"></a>重命名控件
 当你将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件从“工具箱” 添加到工作表时，Visual Studio 会自动生成该控件的名称。 你可以在“属性”  窗口中更改名称。

## <a name="events"></a>事件
 以下事件可用于 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件：

- <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange>

## <a name="see-also"></a>请参阅
- [使用Excel对象自动执行自动执行](../vsto/automating-excel-by-using-extended-objects.md)
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [在外接程序Excel扩展 Word 文档VSTO工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [文档上的Office控件](../vsto/controls-on-office-documents.md)
- [运行时向Office添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [如何：调整 NamedRange 控件的大小](../vsto/how-to-resize-namedrange-controls.md)
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
