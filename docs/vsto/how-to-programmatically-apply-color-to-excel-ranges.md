---
title: 如何：以编程方式将颜色应用到 Excel 范围
description: 了解，若要将颜色应用于单元范围内的文本，请使用 NamedRange 控件或本机 Excel 范围对象。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- color, Excel ranges
- ranges, applying color
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 3de687879a74c92c39331ca6668e29d7a3c77014a19cd3c7138eb396f2b52c78
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121384348"
---
# <a name="how-to-programmatically-apply-color-to-excel-ranges"></a>如何：以编程方式将颜色应用到 Excel 范围
  若要将颜色应用于单元范围内的文本，请使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 此示例适用于文档级自定义项。

### <a name="to-apply-color-to-a-namedrange-control"></a>将颜色应用于 NamedRange 控件

1. <xref:Microsoft.Office.Tools.Excel.NamedRange>在单元格 A1 中创建一个控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet65":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet65":::

2. 设置控件中文本的颜色 <xref:Microsoft.Office.Tools.Excel.NamedRange> 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet66":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet66":::

## <a name="use-native-excel-ranges"></a>使用本机 Excel 范围

### <a name="to-apply-color-to-a-native-excel-range-object"></a>将颜色应用于本机 Excel 范围对象

1. 在单元格 A1 中创建一个范围，然后设置文本的颜色。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet67":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet67":::

## <a name="see-also"></a>另请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式在代码中引用工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
