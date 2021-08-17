---
title: 图表控件
description: 了解将图表添加到工作表时，Visual Studio创建可直接编程的图表对象。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.ExcelChart
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], events
- Chart control [Office development in Visual Studio]
- Chart control [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 957f9a8a1959879f32e3eb4ee9b75645308d7ea6b57358ec37e04e9ea433f42c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121226404"
---
# <a name="chart-control"></a>图表控件
  <xref:Microsoft.Office.Tools.Excel.Chart> 控件是公开事件的图表对象。 当将图表添加到工作表时，Visual Studio 将创建 <xref:Microsoft.Office.Tools.Excel.Chart> 对象，你可以直接针对此对象编程而无需遍历 Microsoft Office Excel 对象模型。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>创建控件
 可以在设计时或Microsoft Office Excel向文档级项目中的工作表 <xref:Microsoft.Office.Tools.Excel.Chart> 添加控件。

 在 VSTO 外接程序中，你可以在运行时将 <xref:Microsoft.Office.Tools.Excel.Chart> 控件添加到工作表中。 有关详细信息，请参阅 [如何：向工作表添加图表控件](../vsto/how-to-add-chart-controls-to-worksheets.md)。

> [!NOTE]
> 工作表关闭时，动态创建的图表控件不作为主机控件保留在工作表中。 有关详细信息，请参阅[向Office添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

## <a name="formatting"></a>格式设置
 可应用于 <xref:Microsoft.Office.Interop.Excel.Chart> 的所有格式设置也可应用于 <xref:Microsoft.Office.Tools.Excel.Chart> 控件。 这包括边框、字体、图表类型、网格线、图例和数据标签。

## <a name="events"></a>事件
 以下事件可用于 <xref:Microsoft.Office.Tools.Excel.Chart> 控件：

- <xref:Microsoft.Office.Tools.Excel.Chart.ActivateEvent>

- <xref:Microsoft.Office.Tools.Excel.Chart.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.Chart.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.Chart.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.Chart.Calculate>

- <xref:Microsoft.Office.Tools.Excel.Chart.Deactivate>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.Chart.DragOver>

- <xref:Microsoft.Office.Tools.Excel.Chart.DragPlot>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseDown>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseMove>

- <xref:Microsoft.Office.Tools.Excel.Chart.MouseUp>

- <xref:Microsoft.Office.Tools.Excel.Chart.Resize>

- <xref:Microsoft.Office.Tools.Excel.Chart.SelectEvent>

- <xref:Microsoft.Office.Tools.Excel.Chart.SeriesChange>

## <a name="see-also"></a>请参阅
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [在外接程序Excel扩展 Word 文档VSTO工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [文档上的Office控件](../vsto/controls-on-office-documents.md)
- [运行时向Office文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [使用Excel对象自动执行自动执行](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：向工作表添加图表控件](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
