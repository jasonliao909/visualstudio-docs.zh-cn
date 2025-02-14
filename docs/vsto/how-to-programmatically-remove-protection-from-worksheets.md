---
title: 如何：以编程方式取消工作表保护
description: 了解如何使用 Visual Studio 以编程方式从 Microsoft Excel 工作表中移除保护。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, unprotecting
- documents [Office development in Visual Studio], document protection
- document protection, removing from worksheets
- Unprotect method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: af5fb0cab5501b6a5bbe19025be6f963728ee477
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664957"
---
# <a name="how-to-programmatically-remove-protection-from-worksheets"></a>如何：以编程方式取消工作表保护
  可以编程方式取消 Microsoft Office Excel 工作表保护。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 以下示例使用变量 `getPasswordFromUser`，该变量包含获取自用户的密码。

## <a name="to-unprotect-a-worksheet-in-a-document-level-customization"></a>若要在文档级自定义中取消工作表的保护

1. 调用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Unprotect%2A> 工作表的方法并传入密码（如果需要）。 此示例假定你正在使用名为 `Sheet1`的工作表。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet28":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet28":::

## <a name="to-unprotect-a-worksheet-in-a-vsto-add-in"></a>取消保护 VSTO 外接程序中的工作表

1. 调用 <xref:Microsoft.Office.Interop.Excel._Worksheet.Unprotect%2A> 活动工作表的方法并传入密码（如果需要）。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet18":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet18":::

## <a name="see-also"></a>另请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式保护工作表](../vsto/how-to-programmatically-protect-worksheets.md)
- [如何：以编程方式保护工作簿](../vsto/how-to-programmatically-protect-workbooks.md)
- [如何：以编程方式隐藏工作表](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)
