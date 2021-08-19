---
title: 如何：以编程方式运行 Excel 计算
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Excel 工作簿中运行计算。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, running calculations
- calculations, running in Excel
- Excel [Office development in Visual Studio], running calculations programmatically
- workbooks, running calculations
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ab15a81c0ddb03dd30a865b1a11b191bc9c7f5f9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083123"
---
# <a name="how-to-programmatically-run-excel-calculations"></a>如何：以编程方式运行 Excel 计算
  您可以使用类似的过程在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象中运行计算。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="run-calculations-in-a-namedrange-control"></a>在 NamedRange 控件中运行计算
 下面的示例 <xref:Microsoft.Office.Tools.Excel.NamedRange> 在单元格 A1 中创建一个，然后计算单元。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

### <a name="to-run-calculations-in-a-namedrange-control"></a>在 NamedRange 控件中运行计算

1. 创建命名范围。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet75":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet75":::

2. 调用 <xref:Microsoft.Office.Tools.Excel.NamedRange.Calculate%2A> 指定范围的方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet76":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet76":::

## <a name="run-calculations-in-a-native-excel-range"></a>在本机 Excel 范围内运行计算

### <a name="to-run-calculations-in-a-native-excel-range"></a>在本机 Excel 范围中运行计算

1. 创建命名范围。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet30":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet30":::

2. 调用 <xref:Microsoft.Office.Interop.Excel.Range.Calculate%2A> 指定范围的方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet31":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet31":::

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
