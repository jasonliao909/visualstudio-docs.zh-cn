---
title: 如何：以编程方式在 Word 文档中插入文本
description: 了解如何使用 Visual Studio 以编程方式将文本插入 Microsoft Word 文档中。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, inserting text in documents
- text [Office development in Visual Studio], inserting in documents
- ranges, replacing text in documents
- documents [Office development in Visual Studio], inserting text
- text [Office development in Visual Studio], replacing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f17828b4617f84cb104761918787b4bbb79f7afc
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827352"
---
# <a name="how-to-programmatically-insert-text-into-word-documents"></a>如何：以编程方式在 Word 文档中插入文本
  向 Microsoft Office Word 文档中插入文本主要有三种方式：

- 在范围中插入文本。

- 将范围中的文本替换为新文本。

- 使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Selection> 方法在光标或所选位置处插入文本。

> [!NOTE]
> 你还可以将文本插入到内容控件和书签中。 有关详细信息，请参阅 [内容控件](../vsto/content-controls.md) 和 [书签控件](../vsto/bookmark-control.md)。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="insert-text-in-a-range"></a>在范围中插入文本
 使用 <xref:Microsoft.Office.Interop.Word.Range.Text%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Range> 属性在文档中插入文本。

### <a name="to-insert-text-in-a-range"></a>若要在范围中插入文本

1. 在文档开头指定一个范围，并插入文本 **New Text**。

     下面的代码示例可用于文档级自定义项。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet51":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet51":::

     以下代码示例可用于 VSTO 外接程序。 此代码运用了活动文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet51":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet51":::

2. 选择 <xref:Microsoft.Office.Interop.Word.Range> 对象，该对象已从一个字符长度扩展到了插入文本的长度。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet52":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet52":::

## <a name="replace-text-in-a-range"></a>替换范围中的文本
 如果指定的范围包含文本，则该范围中的所有文本将被插入的文本替换。

### <a name="to-replace-text-in-a-range"></a>若要替换范围中的文本

1. 创建一个 <xref:Microsoft.Office.Interop.Word.Range> 对象，该对象包含文档中的前 12 个字符。

     下面的代码示例可用于文档级自定义项。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet53":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet53":::

     以下代码示例可用于 VSTO 外接程序。 此代码运用了活动文档。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet53":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet53":::

2. 将这些字符替换为字符串 **New Text**。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet54":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet54":::

3. 选择范围。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet55":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet55":::

## <a name="insert-text-using-typetext"></a>使用 TypeText 插入文本
 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> 方法可在所选位置处插入文本。 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> 的行为有所不同，具体取决于用户计算机上设置的选项。 以下过程中的代码声明了一个 <xref:Microsoft.Office.Interop.Word.Selection> 对象变量，如果 **Overtype** 选项已打开，则会将其关闭。 如果 **Overtype** 选项已激活，则关闭旁的任何文本将被覆盖。

### <a name="to-insert-text-using-the-typetext-method"></a>若要使用 TypeText 方法插入文本

1. 声明一个 <xref:Microsoft.Office.Interop.Word.Selection> 对象变量。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet57":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet57":::

2. 如果 **Overtype** 选项已打开，请将其关闭。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet58":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet58":::

3. 测试当前选择项是否未插入点。

    如果是，此代码将使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A>插入一个句子，然后使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeParagraph%2A> 方法插入段落标记。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet59":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet59":::

4. **ElseIf** 块中的代码用于测试选择项是否为正常选择项。 如果是，则另一个 **If** 块将测试 **ReplaceSelection** 选项是否已打开。 如果是，该代码将使用选择项的 <xref:Microsoft.Office.Interop.Word.Selection.Collapse%2A> 方法将选择项折叠为文本所选块起始处的插入点。 插入文本和段落标记。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet60":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet60":::

5. 如果选择项不是所选文本的插入点或块，则 **Else** 块中的代码将不会执行任何操作。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet61":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet61":::

   你还可以使用 <xref:Microsoft.Office.Interop.Word.Selection.TypeBackspace%2A> 对象的方法 <xref:Microsoft.Office.Interop.Word.Selection> ，该方法模仿键盘上 **Backspace** 键的功能。 但是，当涉及到插入和操作文本时，<xref:Microsoft.Office.Interop.Word.Range> 对象将提供更多控件。

   以下示例显示了完整的代码。 若要使用此示例，请运行项目中的 `ThisDocument` 或 `ThisAddIn` 类的代码。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet56":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet56":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在文档中设置文本格式](../vsto/how-to-programmatically-format-text-in-documents.md)
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式在文档中扩展范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
