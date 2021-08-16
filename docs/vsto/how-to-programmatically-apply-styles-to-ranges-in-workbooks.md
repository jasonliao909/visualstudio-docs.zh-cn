---
title: 如何：以编程方式将样式应用于工作簿中的范围
description: 了解如何将命名样式应用于工作簿中的区域。 Excel 提供了大量预定义样式。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, styles
- styles, workbook ranges
- workbooks, styles
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 25ae70edc79c648fd908b8d357469cc1ebe2af95050cf14292eb4ebc5deaa465
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121268113"
---
# <a name="how-to-programmatically-apply-styles-to-ranges-in-workbooks"></a>如何：以编程方式将样式应用于工作簿中的范围
  可以将已命名的样式应用到工作簿中的区域。 Excel 提供了大量预定义样式。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 **“设置单元格格式”** 对话框显示了可用于设置单元格格式的所有选项，且其中每个选项都可从你的代码获取。 若要在 Excel 中显示此对话框，请单击 **“格式”** 菜单上的 **“单元格”** 。

## <a name="to-apply-a-style-to-a-named-range-in-a-document-level-customization"></a>将样式应用到文档级自定义项中的命名区域

1. 创建一个新样式并设置其属性。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet53":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet53":::

2. 创建一个 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件，向其分配文本，然后应用新样式。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet54":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet54":::

## <a name="to-clear-a-style-from-a-named-range-in-a-document-level-customization"></a>从文档级自定义项的命名区域中清除样式

1. 将正文样式应用到该区域中。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet55":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet55":::

## <a name="to-apply-a-style-to-a-named-range-in-a-vsto-add-in"></a>将样式应用到 VSTO 外接程序中的命名区域

1. 创建一个新样式并设置其属性。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet28":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet28":::

2. 创建一个 <xref:Microsoft.Office.Interop.Excel.Range>，对其分配文本，然后应用新样式。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet29":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet29":::

## <a name="to-clear-a-style-from-a-named-range-in-a-vsto-add-in"></a>从外接程序中的命名范围中清除VSTO样式

1. 将正文样式应用到该区域中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet56":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet56":::

## <a name="see-also"></a>另请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [对项目中对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
