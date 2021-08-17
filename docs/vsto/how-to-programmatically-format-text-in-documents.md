---
title: 如何：以编程方式在文档中设置文本格式
description: 了解如何使用 Range 对象以编程方式设置 Microsoft Word 文档中文本的格式。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- documents [Office development in Visual Studio], formatting text
- text [Office development in Visual Studio], formatting in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 130469ddd084a1a044e4af458164f15c82412eef
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122704"
---
# <a name="how-to-programmatically-format-text-in-documents"></a>如何：以编程方式在文档中设置文本格式
  你可以使用 <xref:Microsoft.Office.Interop.Word.Range> 对象来格式化 Microsoft Office Word 文档中的文本。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 下面的示例选择文档中的第一个段落并更改字号、字体名称和对齐方式。 然后，它会选择范围并显示一个消息框，以在执行下一段代码前暂停。 下一节将 <xref:Microsoft.Office.Tools.Word.Document> 为文档级自定义项调用宿主项 (的 Undo 方法) 或 <xref:Microsoft.Office.Interop.Word.Document> VSTO 外接程序的类 () 三次。 它应用“正文缩进”样式，并显示一个消息框以暂停代码。 然后，该代码调用 <xref:Microsoft.Office.Tools.Word.Document.Undo%2A> 方法一次，并显示一个消息框。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-format-text-using-a-document-level-customization"></a>使用文档级自定义项格式化文本

1. 可以在文档级自定义项中使用下面的示例。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet62":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet62":::

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="to-format-text-using-a-vsto-add-in"></a>使用 VSTO 外接程序格式化文本

1. 可以在 VSTO 外接程序中使用下面的示例。 本示例使用活动文档。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet62":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet62":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式在 Word 文档中插入文本](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [如何：以编程方式在文档中搜索和替换文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
