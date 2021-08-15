---
title: 如何：以编程方式在代码中引用工作表范围
description: 了解如何使用 Visual Studio 以编程方式引用 Microsoft Excel 工作表中的 NamedRange 控件或本机 Excel 范围对象的内容。
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
ms.openlocfilehash: e031876c4fb822f8f01b041bffecdc4ff6d6e5afec537610d296758b9779a05b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440716"
---
# <a name="how-to-programmatically-refer-to-worksheet-ranges-in-code"></a>如何：以编程方式在代码中引用工作表范围
  您可以使用类似的过程来引用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象的内容。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 下面的示例将添加 <xref:Microsoft.Office.Tools.Excel.NamedRange> 到工作表，然后向该范围中的单元格添加文本。

### <a name="to-refer-to-a-namedrange-control"></a>引用 NamedRange 控件

1. 将字符串分配给 <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> 控件的属性 <xref:Microsoft.Office.Tools.Excel.NamedRange> 。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet46":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet46":::

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围
 下面的示例将本机 Excel 范围添加到工作表，然后向该范围中的单元格添加文本。

### <a name="to-refer-to-a-native-range-object"></a>引用本机范围对象

1. 将字符串分配给 <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> 范围的属性。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet47":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet47":::

## <a name="see-also"></a>另请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式在工作表中检查拼写](../vsto/how-to-programmatically-check-spelling-in-worksheets.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式自动用递增变化的数据填充范围](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [如何：以编程方式在工作表范围内搜索文本](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
