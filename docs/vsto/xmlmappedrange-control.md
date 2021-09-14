---
title: XmlMappedRange 控件
description: 了解 XmlMappedRange 控件是仅在非重复架构元素映射到该元素中的单元格时Microsoft Excel。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, data binding
- XMLMappedRange control
- XMLMappedRange control, events
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 173120009b6d295f04c467900e1918361cb5900e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664921"
---
# <a name="xmlmappedrange-control"></a>XmlMappedRange 控件
  控件是仅在非重复架构元素映射到非重复架构元素时创建的 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> Microsoft Office Excel。 例如，当 `maxOccurs` 架构元素的 属性等于 1 时。 创建Visual Studio XML 映射范围后，可以直接针对它进行编程，而无需遍历Excel模型。 只有在删除元素 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 映射Excel才能删除控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 控件 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 支持绑定到单个数据字段 (数据绑定) 。 控件可以支持复杂的数据绑定，在重复架构元素映射到单元格时 <xref:Microsoft.Office.Tools.Excel.ListObject> 自动创建。 有关详细信息，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件使用 属性绑定到 <xref:System.Windows.Forms.Control.DataBindings%2A> 数据源。 将 添加到工作表单元格时，Visual Studio从映射单元中的数据自动生成数据集，并将其 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 控件绑定到该数据集。 的默认数据绑定属性 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 为 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Value2%2A> 。

 如果绑定数据集中的数据通过任何机制进行更新，控件 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 将反映更改。

## <a name="formatting"></a>格式化
 可以将相同的格式应用于可应用于 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 的控件 <xref:Microsoft.Office.Interop.Excel.Range> 。 这包括边框、字体、数字格式和样式。

## <a name="events"></a>事件
 可用于 控件的事件 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 包括：

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.SelectionChange>

## <a name="see-also"></a>另请参阅
- [使用Excel对象自动执行自动执行](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：将 XMLMappedRange 控件添加到工作表](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：将架构映射到 Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
