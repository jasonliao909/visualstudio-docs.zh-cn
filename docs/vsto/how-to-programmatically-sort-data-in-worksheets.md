---
title: 如何：以编程方式对工作表中的数据进行排序
description: 了解如何使用 Visual Studio运行时以编程方式对工作表范围和列表中包含的数据进行排序。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data sorting, worksheets
- data [Office development in Visual Studio], sorting in worksheets
- worksheets, sorting data
- sorting data, in worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 70d99cb76530f6f5b0452063c2d1d0aa21629e34
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083045"
---
# <a name="how-to-programmatically-sort-data-in-worksheets"></a>如何：以编程方式对工作表中的数据进行排序
  在运行时，可以对工作表区域和列表中所包含数据进行排序。 以下代码先按第一列中的数据对名为 `Fruits` 的多列区域进行排序，然后按第二列中的数据进行相同操作。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="sort-data-in-a-document-level-customization"></a>对文档级自定义项中的数据进行排序

### <a name="to-sort-data-in-a-namedrange-control"></a>若要对 NamedRange 控件中的数据进行排序

1. 调用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件的 <xref:Microsoft.Office.Tools.Excel.NamedRange.Sort%2A> 方法。 以下示例需要工作表上一个名为 `Fruits` 的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet78":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet78":::

   将以下代码放在 *Sheet1.vb* 或 *Sheet1.cs* 中，以在 控件中对数据 <xref:Microsoft.Office.Tools.Excel.ListObject> 进行排序。 该代码假定你在名为 `Sheet1` 的工作表中，具有名为 `fruitList` 的 <xref:Microsoft.Office.Tools.Excel.ListObject>控件。

### <a name="to-sort-data-in-a-listobject-control"></a>对 ListObject 控件中的数据进行排序

1. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject> 主机控件的 <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A> 属性的 <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet79":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet79":::

## <a name="sort-data-in-a-vsto-add-in"></a>对外接程序VSTO数据进行排序

### <a name="to-sort-data-in-a-native-range"></a>若要对本机范围内的数据进行排序

1. 调用本机 Excel <xref:Microsoft.Office.Interop.Excel.Range> 控件的 <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> 方法。 以下示例需要工作表上一个名为 `Fruits` 的本机 Excel 控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet23":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet23":::

### <a name="to-sort-data-in-a-listobject-control"></a>对 ListObject 控件中的数据进行排序

1. 调用本机 Excel <xref:Microsoft.Office.Interop.Excel.ListObject> 控件的 <xref:Microsoft.Office.Tools.Excel.ListObject.Range%2A>属性的 <xref:Microsoft.Office.Interop.Excel.Range.Sort%2A> 方法。 以下示例假定你在活动工作表中有名为 `fruitList` 的本机 Excel <xref:Microsoft.Office.Interop.Excel.ListObject> 控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet24":::

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式使用增量更改的数据自动填充范围](../vsto/how-to-programmatically-automatically-fill-ranges-with-incrementally-changing-data.md)
- [如何：以编程方式引用代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [ListObject 控件](../vsto/listobject-control.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
