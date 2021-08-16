---
title: 如何：以编程方式定义和选择文档中的范围
description: 了解如何使用 Range 对象以编程方式在文档中Microsoft Word范围。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], selecting sentences
- documents [Office development in Visual Studio], ranges
- sentences, selecting in documents
- ranges, selecting in documents
- ranges, defining in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 98b7e6aa0d95322fb3a69263d487ba0ce21e5d9f5c7c8b4606c12cbdd489655d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394454"
---
# <a name="how-to-programmatically-define-and-select-ranges-in-documents"></a>如何：以编程方式定义和选择文档中的范围
  你也可以通过使用 <xref:Microsoft.Office.Interop.Word.Range> 对象在 Microsoft Office Word 文档中定义一个范围。 可以通过多种方式选择整个文档，例如，通过使用 对象的 方法，或者通过使用文档级自定义项) 或 VSTO 外接程序) 中的类 (的 Content 属性或 <xref:Microsoft.Office.Interop.Word.Range.Select%2A> <xref:Microsoft.Office.Interop.Word.Range> 类 <xref:Microsoft.Office.Tools.Word.Document> <xref:Microsoft.Office.Interop.Word.Document> (。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="define-a-range"></a>定义范围
 下面的示例演示如何创建一个新的 <xref:Microsoft.Office.Interop.Word.Range> 对象，该对象包括活动文档中的前七个字符，其中包括非打印字符。 然后，它选择范围内的文本。

### <a name="to-define-a-range-in-a-document-level-customization"></a>在文档级自定义项中定义范围

1. 通过将开始和结束字符传递到 <xref:Microsoft.Office.Tools.Word.Document> 类的 <xref:Microsoft.Office.Tools.Word.Document.Range%2A> 方法来将范围添加到文档中。 若要使用此代码示例，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet18":::

### <a name="to-define-a-range-by-using-a-vsto-add-in"></a>通过使用 VSTO 外接程序定义范围

1. 通过将开始和结束字符传递到 <xref:Microsoft.Office.Interop.Word.Document> 类的 <xref:Microsoft.Office.Interop.Word._Document.Range%2A> 方法来将范围添加到文档中。 下面的代码示例将一个范围添加到活动文档。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet18":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet18":::

## <a name="select-a-range-in-a-document-level-customization"></a>在文档级自定义项中选择范围
 下面的示例演示如何通过使用 <xref:Microsoft.Office.Interop.Word.Range> 对象的 <xref:Microsoft.Office.Interop.Word.Range.Select%2A> 方法，或者通过使用 <xref:Microsoft.Office.Tools.Word.Document> 类的 <xref:Microsoft.Office.Tools.Word.Document.Content%2A> 属性来选择整个文档。

### <a name="to-select-the-entire-document-as-a-range-by-using-the-select-method"></a>通过使用 Select 方法来选择整个文档作为范围

1. 使用包含整个文档的 <xref:Microsoft.Office.Interop.Word.Range> 的 <xref:Microsoft.Office.Interop.Word.Range.Select%2A> 方法。 若要使用下面的代码示例，请从项目的 `ThisDocument` 类中运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet19":::

### <a name="to-select-the-entire-document-as-a-range-by-using-the-content-property"></a>通过使用 Content 属性来选择整个文档作为范围

1. 使用 <xref:Microsoft.Office.Tools.Word.Document.Content%2A> 属性定义包含整个文档的范围。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet20":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet20":::

   你还可以使用其他对象的方法和属性来定义范围。

### <a name="to-select-a-sentence-in-the-active-document"></a>在活动文档中选择一个句子

1. 通过使用 <xref:Microsoft.Office.Interop.Word.Sentences> 集合设置范围。 使用你要选择的句子的索引。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet21":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet21":::

   选择句子的另一种方法是手动设置范围的开始和结束值。

### <a name="to-select-a-sentence-by-manually-setting-the-start-and-end-values"></a>通过手动设置开始和结束值来选择一个句子

1. 创建一个范围变量。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet23":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet23":::

2. 检查文档中是否至少有两个句子，设置范围的 *Start* 和 *End* 参数，然后选择范围。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet24":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet24":::

## <a name="select-a-range-by-using-a-vsto-add-in"></a>使用外接程序选择VSTO范围
 下面的示例演示如何通过使用 <xref:Microsoft.Office.Interop.Word.Range> 对象的 <xref:Microsoft.Office.Interop.Word.Range.Select%2A> 方法，或者通过使用 <xref:Microsoft.Office.Interop.Word.Document> 类的 <xref:Microsoft.Office.Interop.Word._Document.Content%2A> 属性来选择整个文档。

### <a name="to-select-the-entire-document-as-a-range-by-using-the-select-method"></a>通过使用 Select 方法来选择整个文档作为范围

1. 使用包含整个文档的 <xref:Microsoft.Office.Interop.Word.Range> 的 <xref:Microsoft.Office.Interop.Word.Range.Select%2A> 方法。 下面的代码示例选择活动文档的内容。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet19":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet19":::

### <a name="to-select-the-entire-document-as-a-range-by-using-the-content-property"></a>通过使用 Content 属性来选择整个文档作为范围

1. 使用 <xref:Microsoft.Office.Interop.Word._Document.Content%2A> 属性定义包含整个文档的范围。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet20":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet20":::

   你还可以使用其他对象的方法和属性来定义范围。

### <a name="to-select-a-sentence-in-the-active-document"></a>在活动文档中选择一个句子

1. 通过使用 <xref:Microsoft.Office.Interop.Word.Sentences> 集合设置范围。 使用你要选择的句子的索引。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet21":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet21":::

   选择句子的另一种方法是手动设置范围的开始和结束值。

### <a name="to-select-a-sentence-by-manually-setting-the-start-and-end-values"></a>通过手动设置开始和结束值来选择一个句子

1. 创建一个范围变量。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet23":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet23":::

2. 检查文档中是否至少有两个句子，设置范围的 *Start* 和 *End* 参数，然后选择范围。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet24":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet24":::

## <a name="see-also"></a>另请参阅
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式检索范围中的开始字符和结束字符](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
- [如何：以编程方式折叠文档中的范围或选择](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)
- [如何：在创建范围时以编程方式排除段落标记](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
