---
title: 如何：以编程方式统计文档中的字符数
description: 了解如何使用字符集合的 Count 属性来确定文档中的字符数。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- characters, counting in documents
- counting characters in documents
- documents [Office development in Visual Studio], counting characters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ba77fd6d68ba3c11f1ef4fe81b664ef27da2eaa9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046563"
---
# <a name="how-to-programmatically-count-characters-in-documents"></a>如何：以编程方式统计文档中的字符数
  文档中的第一个字符位于字符位置 0，它表示插入点。 末尾字符位置值与文档中的字符总数相同。 可以使用 <xref:Microsoft.Office.Interop.Word.Characters.Count%2A> 集合的 <xref:Microsoft.Office.Interop.Word.Characters> 属性确定文档中的字符数。

 文档中的所有字符都被计算在内，包括空格、段落标记及通常是隐藏的其他字符。 甚至一个新的空文档的计数结果都返回一个字符，因为它包含一个段落标记。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-display-the-number-of-characters-in-a-document-level-customization"></a>显示文档级自定义项中的字符数

1. 选择整个文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet98":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet98":::

2. 在一个消息框中显示文档中的字符数。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet99":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet99":::

## <a name="to-display-the-number-of-characters-in-a-vsto-add-in"></a>显示 VSTO 外接程序中的字符数

1. 选择整个文档。 下面的示例将选择活动文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet98":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet98":::

2. 在一个消息框中显示文档中的字符数。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet99":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet99":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式检索范围中的开始字符和结束字符](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
