---
title: 以&方式在Excel中存储检索日期值
description: 了解如何使用 Visual Studio以编程方式存储和检索数据范围内Microsoft Excel值。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], retrieving date values from ranges
- ranges, retrieving data values
- dates, retrieving from Excel ranges
- Excel [Office development in Visual Studio], storing date values in ranges
- date values, storing in Excel ranges
- dates, storing in Excel ranges
- ranges, storing date values
- date values
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c9dbf0d63b13d6f7b66fc24c82a80e7fecea5d4c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025948"
---
# <a name="how-to-programmatically-store-and-retrieve-date-values-in-excel-ranges"></a>如何：以编程方式存储和检索数据范围内Excel值
  可以在控件或本机范围对象中存储和 <xref:Microsoft.Office.Tools.Excel.NamedRange> Excel值。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 如果使用 Visual Studio 中的 Office 开发工具将日期值存储在 1900/1/1/1 或之后，则该值以 OLE Automation (OA) 格式存储。 必须使用 方法 <xref:System.DateTime.FromOADate%2A> 检索 OLE Automation (OA) 日期。 如果日期早于 1900/1/1/1，则它存储为字符串。

> [!NOTE]
> Excel日期不同于 1900 年前两个月的 OLE 自动化日期。 如果选中 **"1904 日期系统"选项，则也** 存在差异。 下面的代码示例未解决这些差异。

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件

- 此示例适用于文档级自定义项。 以下代码必须放置在工作表类中，而不是类 `ThisWorkbook` 中。

### <a name="to-store-a-date-value-in-a-named-range"></a>在命名范围中存储日期值

1. 在单元格 <xref:Microsoft.Office.Tools.Excel.NamedRange> **A1 上创建控件**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet50":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet50":::

2. 将今天的日期设置为 的值 `NamedRange1` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet51":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet51":::

### <a name="to-retrieve-a-date-value-from-a-named-range"></a>从命名范围检索日期值

1. 从 检索日期值 `NamedRange1` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet52":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet52":::

## <a name="use-native-excel-ranges"></a>使用本机Excel范围

### <a name="to-store-a-date-value-in-a-native-excel-range-object"></a>在本机范围对象中存储Excel值

1. 创建一 <xref:Microsoft.Office.Interop.Excel.Range> 个表示单元 **A1 的**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet25":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet25":::

2. 将今天的日期设置为 的值 `rng` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet26":::

### <a name="to-retrieve-a-date-value-from-a-native-excel-range-object"></a>从本机范围对象中检索Excel值

1. 从 检索日期值 `rng` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet27":::

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [Excel对象模型概述](../vsto/excel-object-model-overview.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：以编程方式引用代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
