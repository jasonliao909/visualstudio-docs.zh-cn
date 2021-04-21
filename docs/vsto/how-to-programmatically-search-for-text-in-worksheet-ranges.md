---
title: 如何：以编程方式在工作表范围内搜索文本
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Excel 工作表范围内搜索文本。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, searching
- text [Office development in Visual Studio], searching in worksheets
- text searches, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 762cb3fc35b43bfd3ad15aea669adff2d370b632
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827937"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>如何：以编程方式在工作表范围内搜索文本
  <xref:Microsoft.Office.Interop.Excel.Range.Find%2A>对象的方法 <xref:Microsoft.Office.Interop.Excel.Range> 使您能够在范围内搜索文本。 此文本还可以是工作表单元格（如或）中可能出现的任何错误字符串 `#NULL!` `#VALUE!` 。 有关错误字符串的详细信息，请参阅 [单元错误值](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values)。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 下面的示例在名为的范围内搜索 `Fruits` ，并修改包含 "苹果" 一词的单元的字体。 此过程还使用 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 方法，该方法使用以前设置的搜索设置来重复搜索。 指定要搜索的单元格，并且该方法将 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 处理其余内容。

> [!NOTE]
> 此 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 方法的搜索在到达范围末尾后将向后返回到搜索范围的开头。 你的代码必须确保搜索不会绕过无限循环。 示例过程演示了使用属性处理此情况的一种方法 <xref:Microsoft.Office.Interop.Excel.Range.Address%2A> 。

## <a name="to-search-for-text-in-a-worksheet-range"></a>在工作表范围内搜索文本

1. 声明用于跟踪整个范围、找到的第一个范围和当前找到的范围的变量。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet58":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet58":::

2. 搜索第一个匹配项，同时指定除后要搜索的单元格以外的所有参数。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet59":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet59":::

3. 继续搜索，只要有匹配项。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet60":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet60":::

4. 将)  (第一个找到的范围与 " `firstFind` **无**" 比较。 如果 `firstFind` 不包含值，则代码会将找到的范围存储 (`currentFind`) 。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet61":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet61":::

5. 如果找到范围的地址与第一个找到范围的地址匹配，则退出循环。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet62":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet62":::

6. 设置所找到范围的外观。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet63":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet63":::

7. 执行其他搜索。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet64":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet64":::

   以下示例显示完整的方法。

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet57":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet57":::

## <a name="see-also"></a>另请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式在代码中引用工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
