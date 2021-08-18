---
title: 以编程方式跨工作表复制数据和格式设置
description: 了解如何使用 FillAcrossSheets 方法将数据从一个工作表上的范围复制到工作簿中的所有其他工作表。
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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 5640984c0de325f1b2e699a3658f914f627b87a1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083253"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>如何：以编程方式跨工作表复制数据和格式设置
  可以使用 方法将数据从一个工作表上的范围复制到工作簿中的所有其他 <xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A> 工作表。 指定范围，以及是否要复制数据、格式设置或同时复制两者。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet44":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet44":::

## <a name="compile-the-code"></a>编译代码
 此示例需要工作表中名为 `rangeData` 的范围。

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式将新工作表添加到工作簿](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [如何：以编程方式更改包含所选单元格的工作表行中的格式设置](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
