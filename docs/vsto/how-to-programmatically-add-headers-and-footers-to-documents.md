---
title: 如何：以编程方式将页眉和页脚添加到文档
description: 了解如何使用 节的"页眉"属性和"页脚"属性向文档中的页眉和页脚添加文本。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- headers, adding to Office documents
- documents [Office development in Visual Studio], adding headers
- documents [Office development in Visual Studio], adding footers
- footers, adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: b2ddbc24bcd567ce56326a4b96d9c97f1e50061c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664734"
---
# <a name="how-to-programmatically-add-headers-and-footers-to-documents"></a>如何：以编程方式将页眉和页脚添加到文档
  可以通过使用 <xref:Microsoft.Office.Interop.Word.Section> 的 <xref:Microsoft.Office.Interop.Word.Section.Headers%2A> 属性和 <xref:Microsoft.Office.Interop.Word.Section.Footers%2A> 属性将文本添加到文档中的页眉和页脚。 文档各部分均包含三个页眉和页脚：

- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterPrimary>

- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterEvenPages>

- <xref:Microsoft.Office.Interop.Word.WdHeaderFooterIndex.wdHeaderFooterFirstPage>

  对于文档级自定义项和 VSTO 外接程序，此过程有所不同。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="document-level-customizations"></a>文档级自定义项
 若要使用以下代码示例，请从项目中的 `ThisDocument` 类运行它们。

### <a name="to-add-text-to-footers-in-the-document"></a>将文本添加到文档的页脚

1. 以下代码示例设置要插入到文档各部分主页脚的文本字体，然后再将文本插入页脚。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet114":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet114":::

### <a name="to-add-text-to-headers-in-the-document"></a>将文本添加到文档的页眉

1. 以下代码示例将添加一个字段，以在文档各个页眉中显示页码，然后设置段落对齐方式，使文本对齐到页眉的右侧。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet116":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet116":::

## <a name="vsto-add-ins"></a>VSTO 外接程序
 若要使用以下代码示例，请从项目中的 `ThisAddIn` 类运行它们。

### <a name="to-add-text-to-footers-in-a-document"></a>将文本添加到文档的页脚

1. 以下代码示例设置要插入到文档各部分主页脚的文本字体，然后再将文本插入页脚。 此代码示例使用活动文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet114":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet114":::

### <a name="to-add-text-to-headers-in-the-document"></a>将文本添加到文档的页眉

1. 以下代码示例将添加一个字段，以在文档各个页眉中显示页码，然后设置段落对齐方式，使文本对齐到页眉的右侧。 此代码示例使用活动文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet116":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet116":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式创建新文档](../vsto/how-to-programmatically-create-new-documents.md)
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式循环访问文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
