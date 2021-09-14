---
title: 如何：以编程方式更新书签文本
description: 了解如何使用文本Visual Studio以编程方式将文本插入到文档中的占位符Microsoft Word书签。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- bookmarks, updating text
- text [Office development in Visual Studio], updating in bookmarks
- Bookmark control, updating contents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2e1c944b00f2581e62f49c56d946d78daefff935
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602235"
---
# <a name="how-to-programmatically-update-bookmark-text"></a>如何：以编程方式更新书签文本
  你可以将文本插入 Microsoft Office Word 文档中的占位符书签，以便稍后能够检索到该文本，或替换书签中的文本。 如果你正在开发文档级自定义项，则还可以更新绑定到数据的 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件中的文本。 有关详细信息，请参阅将数据绑定到解决方案 中的[Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 书签对象可为以下两种类型之一：

- <xref:Microsoft.Office.Tools.Word.Bookmark> 主机控件。

   <xref:Microsoft.Office.Tools.Word.Bookmark> 控件会通过启用数据绑定和公开事件来扩展本机 <xref:Microsoft.Office.Interop.Word.Bookmark> 对象。 有关主机控件详细信息，请参阅 [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

- 一个本机 <xref:Microsoft.Office.Interop.Word.Bookmark> 对象。

   <xref:Microsoft.Office.Interop.Word.Bookmark> 对象没有事件或数据绑定功能。

  将文本分配到书签时，<xref:Microsoft.Office.Interop.Word.Bookmark> 和 <xref:Microsoft.Office.Tools.Word.Bookmark> 的行为有所不同。 有关详细信息，请参阅书签 [控件](../vsto/bookmark-control.md)。

## <a name="use-host-controls"></a>使用主机控件

### <a name="to-update-bookmark-contents-using-a-bookmark-control"></a>使用书签控件更新书签内容

1. 创建一个过程，它将 `bookmark` 自变量用作书签的名称，并将 `newText` 自变量用作要分配给 <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> 属性的字符串。

    > [!NOTE]
    > 将文本分配给 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件的 <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> 或 <xref:Microsoft.Office.Tools.Word.Bookmark.FormattedText%2A> 属性不会删除书签。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet63":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet63":::

2. 将 *newText* 字符串 <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> 分配给 的 <xref:Microsoft.Office.Tools.Word.Bookmark> 属性。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet64":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet64":::

## <a name="use-word-objects"></a>使用 Word 对象

### <a name="to-update-bookmark-contents-using-a-word-bookmark-object"></a>使用 Word 书签对象更新书签内容

1. 创建一个过程，它将 `bookmark` 自变量用作 <xref:Microsoft.Office.Interop.Word.Bookmark> 的名称，并将 `newText` 自变量用作要分配给书签的 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 属性的字符串。

    > [!NOTE]
    > 将文本分配给本机 Word <xref:Microsoft.Office.Interop.Word.Bookmark> 对象会造成书签被删除。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet65":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet65":::

2. 将 *newText* 字符串分配给 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 书签的 属性，该属性会自动删除书签。 然后将书签重新添加到 <xref:Microsoft.Office.Interop.Word.Bookmarks> 集合。

     下面的代码示例可用于文档级自定义项。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet66":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet66":::

     以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet66":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet66":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式将文本插入 Word 文档](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [书签控件](../vsto/bookmark-control.md)
