---
title: 如何：以编程方式Excel计算
description: 了解如何使用 Visual Studio 以编程方式在工作簿中Microsoft Excel计算。
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
ms.openlocfilehash: 234457e235a78281858a45a202fdeff9ff781a849fef5a5757ad505f368cd023
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121384231"
---
# <a name="how-to-programmatically-run-excel-calculations"></a>如何：以编程方式Excel计算
  使用类似的过程在控件或本机范围对象中 <xref:Microsoft.Office.Tools.Excel.NamedRange> Excel计算。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="run-calculations-in-a-namedrange-control"></a>在 NamedRange 控件中运行计算
 以下示例在单元格 <xref:Microsoft.Office.Tools.Excel.NamedRange> A1 上创建 ，然后计算单元格。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

### <a name="to-run-calculations-in-a-namedrange-control"></a>在 NamedRange 控件中运行计算

1. 创建命名范围。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet75":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet75":::

2. 调用 <xref:Microsoft.Office.Tools.Excel.NamedRange.Calculate%2A> 指定范围的 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet76":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet76":::

## <a name="run-calculations-in-a-native-excel-range"></a>在本机范围中Excel计算

### <a name="to-run-calculations-in-a-native-excel-range"></a>在本机计算范围中Excel计算

1. 创建命名范围。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet30":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet30":::

2. 调用 <xref:Microsoft.Office.Interop.Excel.Range.Calculate%2A> 指定范围的 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet31":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet31":::

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
