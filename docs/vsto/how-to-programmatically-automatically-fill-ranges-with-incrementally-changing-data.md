---
title: 以编程方式自动填充增量更改数据范围
description: 了解 Range 对象的 AutoFill 方法如何使你在工作表中自动填充值的范围。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Autofill method [Excel]
- filling ranges automatically
- ranges, automatically filling
- workbooks, filling ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9a4dfe4ad526d811d0252816cd0544913328cb9f21e290ae40d653e211cd9e2e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121384335"
---
# <a name="how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data"></a>如何：以编程方式使用增量更改的数据自动填充范围
  <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A>对象的 方法 <xref:Microsoft.Office.Interop.Excel.Range> 允许自动用值填充工作表中的范围。 大多数情况下， <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 方法用于以增量方式存储范围中递增或递减的值。 可以通过从 枚举提供可选常量来指定 <xref:Microsoft.Office.Interop.Excel.XlAutoFillType> 行为。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 使用 时，必须指定两个范围 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> ：

- 调用 方法的范围 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> ，该方法指定填充的起点并包含初始值。

- 要填充的范围，作为参数传递给 <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> 方法。 此目标范围必须包含包含初始值的范围。

    > [!NOTE]
    > 不能传递 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件来表示 <xref:Microsoft.Office.Interop.Excel.Range> 。 有关详细信息，请参阅主机 [项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet49":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet49":::

## <a name="compile-the-code"></a>编译代码
 要填充的范围的第一个单元格必须包含初始值。

 该示例要求填充三个区域：

- 列 B 包含五个工作日。 对于初始值，在单元格 B1 中键入 **Monday。**

- 列 C 包含五个月。 对于初始值，在单元格 C1 中键入 **"January"。**

- 列 D 包括一系列数字，每行递增两个。 对于初始值，在单元格 D1 中键入 **4，** 在单元格 D2 **中键入 6。**

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式引用代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式Excel计算](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
