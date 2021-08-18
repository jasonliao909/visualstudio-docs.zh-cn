---
title: 如何：以编程方式在工作表单元格中显示字符串
description: 了解如何通过使用 NamedRange 控件或本机范围Microsoft Excel在工作表单元格中以编程方式Excel字符串。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], adding to worksheets
- worksheets, displaying text in cells
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 5058a41a40ed834dc715a09de3b28c0e28cf594a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099797"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>如何：以编程方式在工作表单元格中显示字符串
  此示例演示如何以编程方式显示单元格中的文本。 若要在单元格中显示文本，请使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机Excel范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 此示例使用名为 <xref:Microsoft.Office.Tools.Excel.NamedRange> 的控件 `message` 。 必须在设计时将 控件添加到文档级自定义项。 以下代码必须放置在工作表类中，而不是类 `ThisWorkbook` 中。

### <a name="to-display-text-in-a-namedrange-control"></a>在 NamedRange 控件中显示文本

1. 将 控件的值 <xref:Microsoft.Office.Tools.Excel.NamedRange> 设置为 Hello World。 

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet68":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet68":::

## <a name="use-a-native-excel-range"></a>使用本机Excel范围
 以下代码以编程方式创建新范围，然后为其赋值。

### <a name="to-display-text-in-an-excel-range"></a>显示文本范围Excel文本

1. 检索上 **单元格 A1** 的范围 `Sheet1` ，将值设置为Hello World。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet69":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet69":::

## <a name="see-also"></a>请参阅
- [演练：使用表单Windows数据收集](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [解决方案Office疑难解答](../vsto/troubleshooting-office-solutions.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [对项目中对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
