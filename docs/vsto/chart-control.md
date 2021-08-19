---
title: 图表控件
description: 请注意，当您向工作表添加图表时，Visual Studio 会创建可直接对其进行编程的图表对象。
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
ms.openlocfilehash: cd48c96ba1980a6c95207fae9674ad5480aa961f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122038195"
---
# <a name="chart-control"></a>图表控件
  <xref:Microsoft.Office.Tools.Excel.Chart> 控件是公开事件的图表对象。 当将图表添加到工作表时，Visual Studio 将创建 <xref:Microsoft.Office.Tools.Excel.Chart> 对象，你可以直接针对此对象编程而无需遍历 Microsoft Office Excel 对象模型。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>创建控件
 您可以在 <xref:Microsoft.Office.Tools.Excel.Chart> 设计时或在运行时将控件添加到 Microsoft Office Excel 工作表中的文档级项目。

 在 VSTO 外接程序中，你可以在运行时将 <xref:Microsoft.Office.Tools.Excel.Chart> 控件添加到工作表中。 有关详细信息，请参阅 [如何：向工作表添加图表控件](../vsto/how-to-add-chart-controls-to-worksheets.md)。

> [!NOTE]
> 工作表关闭时，动态创建的图表控件不作为主机控件保留在工作表中。 有关详细信息，请参阅[在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)。

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
- [Office 开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：向工作表添加图表控件](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [在 Office 解决方案中将数据绑定到控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
