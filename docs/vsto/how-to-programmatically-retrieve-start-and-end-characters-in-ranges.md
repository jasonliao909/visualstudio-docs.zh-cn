---
title: 以编程方式获取范围内的开始 & 结束字符
description: 此示例演示如何检索范围开始和结束位置的字符位置。
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, retrieving start and end characters
- end characters
- start characters
- documents [Office development in Visual Studio], retrieving ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 76b5c367223731518a9f09899259d7d7534a76a4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122105881"
---
# <a name="how-to-programmatically-retrieve-start-and-end-characters-in-ranges"></a>如何：以编程方式检索范围中的开始字符和结束字符
  此示例演示如何检索范围开始和结束位置的字符位置。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-retrieve-start-and-end-characters-of-a-range-in-a-document-level-customization"></a>检索文档级自定义项中范围的开始和结束字符

1. 获取 <xref:Microsoft.Office.Interop.Word.Range.Start%2A> 的值和 <xref:Microsoft.Office.Interop.Word.Range.End%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 属性。 下面的代码示例获取了文档中第二个语句的开始和结束位置。 若要使用此代码示例，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet25":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet25":::

## <a name="to-retrieve-start-and-end-characters-of-a-range-by-using-a-vsto-add-in"></a>使用 VSTO 外接程序检索范围的开始和结束字符

1. 获取 <xref:Microsoft.Office.Interop.Word.Range.Start%2A> 的值和 <xref:Microsoft.Office.Interop.Word.Range.End%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 属性。 下面的代码示例获取了活动文档中第二个语句的开始和结束位置。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet25":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet25":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式在文档中扩展范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [如何：以编程方式折叠文档中的范围或选定内容](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [如何：以编程方式在创建范围时排除段落标记](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [如何：以编程方式统计文档中的字符数](../vsto/how-to-programmatically-count-characters-in-documents.md)
