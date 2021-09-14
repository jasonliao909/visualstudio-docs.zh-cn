---
title: 如何：以编程方式搜索工作表范围中的文本
description: 了解如何使用 Visual Studio以编程方式搜索工作表Microsoft Excel文本。
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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: dd001c197f9c64c5d0fa5c89a3920a40f427cf58
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602243"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>如何：以编程方式搜索工作表范围中的文本
  <xref:Microsoft.Office.Interop.Excel.Range.Find%2A>对象的 方法 <xref:Microsoft.Office.Interop.Excel.Range> 可用于搜索范围内的文本。 此文本还可以是工作表单元格（如 或 ）中可能显示的任何错误 `#NULL!` 字符串 `#VALUE!` 。 有关错误字符串的详细信息，请参阅 [单元格错误值](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values)。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 以下示例搜索名为 的范围，并修改包含单词"服务"的 `Fruits` 单元格的字体。 此过程还使用 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 方法，该方法使用以前设置的搜索设置来重复搜索。 指定要搜索的单元格，方法 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 将处理其余单元格。

> [!NOTE]
> 方法的搜索在到达范围的末尾后包装回搜索 <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> 范围的开头。 代码必须确保搜索不会以无限循环结束。 示例过程演示了一种使用 属性处理这种情况 <xref:Microsoft.Office.Interop.Excel.Range.Address%2A> 的方法。

## <a name="to-search-for-text-in-a-worksheet-range"></a>搜索工作表范围中的文本

1. 声明变量用于跟踪整个范围、第一个找到的范围和当前找到的范围。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet58":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet58":::

2. 搜索第一个匹配项，指定除要搜索的单元格之外的所有参数。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet59":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet59":::

3. 只要有匹配项，就继续搜索。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet60":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet60":::

4. 将找到的第一个 () 与 `firstFind` **Nothing 进行比较**。 如果 `firstFind` 不包含任何值，则代码将存储找到 `currentFind` () 。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet61":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet61":::

5. 如果找到的范围的地址与找到的第一个范围的地址匹配，则退出循环。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet62":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet62":::

6. 设置找到的范围的外观。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet63":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet63":::

7. 执行另一个搜索。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet64":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet64":::

   以下示例显示完整的方法。

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet57":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet57":::

## <a name="see-also"></a>另请参阅
- [使用范围](../vsto/working-with-ranges.md)
- [如何：以编程方式将样式应用于工作簿中的范围](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [如何：以编程方式引用代码中的工作表范围](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
