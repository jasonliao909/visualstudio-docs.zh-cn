---
title: 如何：以编程方式列出最近使用的工作簿文件
description: 了解如何使用 Microsoft Excel 以编程方式列出最近使用的工作簿Visual Studio。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, listing recently used
- RecentFiles property
- Excel [Office development in Visual Studio], recently used files listing
- recent file list, Excel
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 738340efbdc7f266ae8da5ed10363858df970f7175507ddf73e4c5ec5097a4ec
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121351832"
---
# <a name="how-to-programmatically-list-recently-used-workbook-files"></a>如何：以编程方式列出最近使用的工作簿文件
  <xref:Microsoft.Office.Interop.Excel._Application.RecentFiles%2A>属性返回一个集合，其中包含最近使用的文件的列表Microsoft Office Excel显示的所有文件的名称。 列表的长度因用户选择保留的文件数而异。 可以在一个范围中显示结果。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-list-recently-used-workbooks-in-a-range-object"></a>列出范围对象中最近使用的工作簿

1. 循环访问最近文件的列表，并显示相对于 对象的单元格 <xref:Microsoft.Office.Interop.Excel.Range> 中的名称。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet9":::

## <a name="see-also"></a>另请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
