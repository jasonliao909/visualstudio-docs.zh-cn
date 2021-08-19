---
title: 如何：以编程方式关闭工作簿
description: 了解如何关闭活动工作簿，也可以指定以编程方式关闭的工作簿。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, closing
- Excel [Office development in Visual Studio], closing workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 21b789a2a722e78d0a89f7db9b1eaeaf28d9db58
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099888"
---
# <a name="how-to-programmatically-close-workbooks"></a>如何：以编程方式关闭工作簿
  你可以关闭活动工作簿，也可以指定关闭某个工作簿。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="close-the-active-workbook"></a>关闭活动工作簿
 关闭活动工作薄有两个过程：一个用于文档级自定义项；另一个用于 VSTO 外接程序。

### <a name="to-close-the-active-workbook-in-a-document-level-customization"></a>若要关闭文档级自定义项的活动工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.Close%2A> 方法来关闭与自定义项关联的工作簿。 若要使用下面的代码示例，请在 Excel 文档级项目的 `Sheet1` 类中运行。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet3":::

### <a name="to-close-the-active-workbook-in-a-vsto-add-in"></a>若要关闭 VSTO 外接程序中的活动工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.Close%2A> 方法来关闭活动工作簿。 若要使用下面的代码示例，请在 Excel 的应用程序级项目内的 `ThisAddIn` 类中运行它。

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet1":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet1":::

## <a name="close-a-workbook-that-you-specify-by-name"></a>关闭按名称指定的工作簿
 关闭按名称指定的工作簿的方法与关闭 VSTO 外接程序和文档级自定义项的方法相同。

### <a name="to-close-a-workbook-that-you-specify-by-name"></a>若要关闭按名称指定的工作薄

1. 将工作薄名称作为自变量指定到 <xref:Microsoft.Office.Interop.Excel.Workbooks> 集合。 下面的代码示例假定名为 **NewWorkbook** 工作簿在 Excel 中打开。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet2":::

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
