---
title: 以编程方式在工作表之间复制数据和格式设置
description: 了解如何使用 FillAcrossSheets 方法将数据从一个工作表中的一个范围复制到工作簿中的所有其他表。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying data
- formatting [Office development in Visual Studio]
- data [Office development in Visual Studio], copying across worksheets
- copying data, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0696c99e78ee1b6a7acd174e5463bbdc514fe160
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828561"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>如何：以编程方式在工作表之间复制数据和格式设置
  您可以使用方法将数据从一个工作表中的一个范围复制到工作簿中的所有其他表 <xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A> 。 指定一个范围，以及是要复制数据、设置格式还是同时复制两者。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet44":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet44":::

## <a name="compile-the-code"></a>编译代码
 此示例需要 `rangeData` 在工作表中指定一个范围。

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式向工作簿添加新工作表](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式在包含选定单元格的工作表行中更改格式设置](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
