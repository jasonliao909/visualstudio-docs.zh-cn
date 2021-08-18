---
title: 以编程&向 Word 表单元格添加文本格式设置
description: 了解如何以编程方式将文本和格式添加到 Word Microsoft Office单元格。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- cells, adding text and formatting
- text [Office development in Visual Studio], adding to Word tables
- formatting [Office development in Visual Studio]
- tables [Office development in Visual Studio], adding text and formatting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6cdb47e1db9893c128850407022eb95a358eb15e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046706"
---
# <a name="how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables"></a>如何：以编程方式向 Word 表中的单元格添加文本和格式设置
  每个表都包含一个单元格集合。 每个单独的 <xref:Microsoft.Office.Interop.Word.Cell> 对象都表示表中的一个单元格。 你可以通过表中每个单元格的位置对其进行引用。 此示例引用位于表中第一行和第一列的单元格；将文本添加到单元格；并应用格式设置。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-add-text-and-formatting-to-cells"></a>若要将文本和格式设置添加到单元格

1. 通过单元格在表中的位置对其进行引用，将文本添加到单元，并应用格式设置。

     下面的代码示例可用于文档级自定义项。 若要使用此示例，请从项目的 `ThisDocument` 类中运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet97":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet97":::

     以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet97":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet97":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式创建 Word 表](../vsto/how-to-programmatically-create-word-tables.md)
- [如何：以编程方式将行和列添加到 Word 表](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [如何：以编程方式使用文档属性填充 Word 表](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
