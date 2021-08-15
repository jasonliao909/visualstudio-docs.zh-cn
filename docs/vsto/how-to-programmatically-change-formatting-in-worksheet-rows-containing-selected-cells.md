---
title: 通过代码更改包含选定单元格的行中的格式
description: 了解如何更改包含选定单元格的整行的字体，使文本为粗体。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio]
- formatting [Office development in Visual Studio]
- worksheets, changing formatting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 641457a61f368db9ded75f27b335b345aab3019665c573d7589cea10beed5b3f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394571"
---
# <a name="how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells"></a>如何：以编程方式在包含选定单元格的工作表行中更改格式设置
  您可以更改包含选定单元格的整行的字体，使文本为粗体。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-make-the-current-row-bold-and-the-previously-bolded-row-normal"></a>将当前行设置为粗体，并使前面的粗体行成为普通行

1. 声明一个静态变量以跟踪之前所选的行。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet37":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet37":::

2. 使用属性检索对当前单元格的引用 <xref:Microsoft.Office.Interop.Excel._Application.ActiveCell%2A> 。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet38":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet38":::

3. 使用活动单元格的属性，将当前行的样式设为粗体 <xref:Microsoft.Office.Interop.Excel.Range.EntireRow%2A> 。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet39":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet39":::

4. 确保的当前值 `previousRow` 不是0。 0 (零) 指示这是第一次执行此代码。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet40":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet40":::

5. 确保当前行与上一行的行不同。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet41":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet41":::

6. 检索对表示以前选择的行的范围的引用，并将该行设置为不以粗体显示。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet42":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet42":::

7. 存储当前行，以使其成为下一个阶段的上一行。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet43":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet43":::

   以下示例显示完整的方法。

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet36":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet36":::

## <a name="see-also"></a>另请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式在工作表之间复制数据和格式设置](../vsto/how-to-programmatically-copy-data-and-formatting-across-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
