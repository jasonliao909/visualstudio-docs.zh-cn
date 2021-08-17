---
title: 如何：以编程方式在工作表单元格中显示字符串
description: 了解如何通过使用 NamedRange 控件或本机 Excel 范围对象，以编程方式在 Microsoft Excel 工作表单元格中显示字符串。
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
ms.openlocfilehash: 4e6e7b1159101319d41e86b8bc4a81c70c8e2035872166a2f739e31dde64268c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121423860"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>如何：以编程方式在工作表单元格中显示字符串
  此示例演示如何以编程方式在单元中显示文本。 若要在单元格中显示文本，请使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机 Excel 范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 此示例使用一个 <xref:Microsoft.Office.Tools.Excel.NamedRange> 名为的控件 `message` 。 必须在设计时将控件添加到文档级自定义项。 下面的代码必须置于 sheet 类中，而不是在 `ThisWorkbook` 类中。

### <a name="to-display-text-in-a-namedrange-control"></a>在 NamedRange 控件中显示文本

1. 将控件的值设置 <xref:Microsoft.Office.Tools.Excel.NamedRange> 为 **Hello World**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet68":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet68":::

## <a name="use-a-native-excel-range"></a>使用本机 Excel 范围
 下面的代码以编程方式创建一个新范围，然后为其赋值。

### <a name="to-display-text-in-an-excel-range"></a>显示 Excel 范围内的文本

1. 检索上单元格 **A1** 的范围 `Sheet1` ，并将值设置为 **Hello World**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet69":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet69":::

## <a name="see-also"></a>请参阅
- [演练：使用 Windows 窗体收集数据](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [解决 Office 解决方案问题](../vsto/troubleshooting-office-solutions.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
