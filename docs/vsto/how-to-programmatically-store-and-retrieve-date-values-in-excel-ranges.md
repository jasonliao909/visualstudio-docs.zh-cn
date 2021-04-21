---
title: 以编程方式在 Excel 范围内存储 & 检索日期值
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Excel 范围内存储和检索日期值。
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
ms.workload:
- office
ms.openlocfilehash: 6e3115e00147a5dff850f6e0c051ffc3b6733218
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826234"
---
# <a name="how-to-programmatically-store-and-retrieve-date-values-in-excel-ranges"></a>如何：以编程方式在 Excel 范围内存储和检索日期值
  可以在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象中存储和检索值。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 如果你在 Visual Studio 中使用 Office 开发工具存储范围为1/1/1900 或之后的日期值，则它将以 OLE 自动化 (OA) 格式存储。 必须使用 <xref:System.DateTime.FromOADate%2A> 方法检索 (OA) 日期的 OLE 自动化的值。 如果日期早于1/1/1900，则将其存储为字符串。

> [!NOTE]
> 对于前两个月1900，Excel 日期不同于 OLE 自动化日期。 如果选中了 " **1904 日期系统** " 选项，则也有不同之处。 下面的代码示例不能解决这些差异。

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件

- 此示例适用于文档级自定义项。 下面的代码必须置于 sheet 类中，而不是在 `ThisWorkbook` 类中。

### <a name="to-store-a-date-value-in-a-named-range"></a>在命名范围中存储日期值

1. <xref:Microsoft.Office.Tools.Excel.NamedRange>在单元格 **A1** 中创建一个控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet50":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet50":::

2. 将今天的日期设置为的值 `NamedRange1` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet51":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet51":::

### <a name="to-retrieve-a-date-value-from-a-named-range"></a>检索命名范围中的日期值

1. 从中检索日期值 `NamedRange1` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet52":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet52":::

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围

### <a name="to-store-a-date-value-in-a-native-excel-range-object"></a>在本机 Excel 范围对象中存储日期值

1. 创建一个 <xref:Microsoft.Office.Interop.Excel.Range> 表示单元格 **A1** 的。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet25":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet25":::

2. 将今天的日期设置为的值 `rng` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet26":::

### <a name="to-retrieve-a-date-value-from-a-native-excel-range-object"></a>从本机 Excel 范围对象检索 date 值

1. 从中检索日期值 `rng` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet27":::

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：以编程方式在代码中引用工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：向工作表添加 NamedRange 控件](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
