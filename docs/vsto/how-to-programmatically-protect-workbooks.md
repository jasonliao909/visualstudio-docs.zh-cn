---
title: 如何：以编程方式保护工作簿
description: 了解如何保护 Microsoft Excel 工作簿，使用户不能添加或删除工作表，还可以通过编程方式取消保护工作簿。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, passwords
- documents [Office development in Visual Studio], document protection
- workbooks, unprotecting
- document protection, removing from workbooks
- document protection, adding to workbooks
- workbooks, protecting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 41875cb3be9ee49d696991c1eb4bc33605123cd2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122092210"
---
# <a name="how-to-programmatically-protect-workbooks"></a>如何：以编程方式保护工作簿
  您可以保护 Microsoft Office Excel 工作簿，使用户不能添加或删除工作表，还可以通过编程方式取消保护工作簿。 您可以选择指定一个密码，指出您是否希望 (受保护的结构，以使用户不能在) 周围移动工作表，并指示是否要保护工作簿的 windows。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 保护工作簿不会阻止用户编辑单元格。 若要保护数据，必须保护工作表。 有关详细信息，请参阅 [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)。

 下面的代码示例使用变量来包含从用户获取的密码。

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>保护属于文档级自定义项的工作簿

### <a name="to-protect-a-workbook"></a>保护工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> 工作簿的方法并包含密码。 若要使用下面的代码示例，请在类中运行它 `ThisWorkbook` ，而不是在 sheet 类中运行。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet10":::

### <a name="to-unprotect-a-workbook"></a>取消保护工作簿

1. 调用 <xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A> 方法，并在需要时传递密码。 若要使用下面的代码示例，请在类中运行它 `ThisWorkbook` ，而不是在 sheet 类中运行。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet11":::

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>使用应用程序级外接程序保护工作簿

### <a name="to-protect-a-workbook"></a>保护工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A> 工作簿的方法并包含密码。 此代码示例使用活动工作簿。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet6":::

### <a name="to-unprotect-a-workbook"></a>取消保护工作簿

1. 调用 <xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A> 活动工作簿的方法，并在需要时传递密码。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet7":::

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
