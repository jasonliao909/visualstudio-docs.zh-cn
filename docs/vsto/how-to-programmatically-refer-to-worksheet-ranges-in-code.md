---
title: 如何：以编程方式引用代码中的工作表范围
description: 了解如何使用 Visual Studio 以编程方式引用 NamedRange 控件或本机 Excel范围对象的内容，Microsoft Excel工作表。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, referring to
- worksheets, referring to ranges
- referring to worksheet ranges
- Excel [Office development in Visual Studio], referring to worksheet ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: be0052005ecc7af763aa1f4f934ef529afa4d4c0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032766"
---
# <a name="how-to-programmatically-refer-to-worksheet-ranges-in-code"></a>如何：以编程方式引用代码中的工作表范围
  使用类似的过程来引用控件或本机范围对象Excel <xref:Microsoft.Office.Tools.Excel.NamedRange> 内容。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 以下示例将 添加到 <xref:Microsoft.Office.Tools.Excel.NamedRange> 工作表，然后将文本添加到 范围中的单元格。

### <a name="to-refer-to-a-namedrange-control"></a>引用 NamedRange 控件

1. 将字符串分配给 <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> 控件的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 属性。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet46":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet46":::

## <a name="use-native-excel-ranges"></a>使用本机Excel范围
 以下示例将本机Excel添加到工作表，然后将文本添加到该范围的单元格。

### <a name="to-refer-to-a-native-range-object"></a>引用本机范围对象

1. 将字符串分配给范围的 <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> 属性。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet47":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet47":::

## <a name="see-also"></a>请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式检查工作表中的拼写](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式使用增量更改的数据自动填充范围](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [如何：以编程方式搜索工作表范围中的文本](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
