---
title: 以编程方式折叠文档中的范围或选定内容
description: 请注意，如果您使用的是范围或选择对象，则在插入文本之前，您可能需要将选定内容更改为插入点。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- selections, collapsing
- documents [Office development in Visual Studio], collapsing ranges
- collapsing selections
- ranges, collapsing
- collapsing ranges
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 18923a8db119540685ba2292c99082e00dabafd15e1888af13305f2b6c209588
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394478"
---
# <a name="how-to-programmatically-collapse-ranges-or-selections-in-documents"></a>如何：以编程方式折叠文档中的范围或选定内容
  如果你在使用 <xref:Microsoft.Office.Interop.Word.Range> 或 <xref:Microsoft.Office.Interop.Word.Selection> 对象，则可能要在插入文本之前更改对插入点的选择，以避免覆盖现有文本。 <xref:Microsoft.Office.Interop.Word.Range>和 <xref:Microsoft.Office.Interop.Word.Selection> 对象都有一个 Collapse 方法，该方法使用 <xref:Microsoft.Office.Interop.Word.WdCollapseDirection> 枚举值：

- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> 会将所选内容折叠到所选内容的开头。 如果未指定枚举值，则这是默认值。

- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> 会将所选内容折叠到所选内容的结尾。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-collapse-a-range-and-insert-new-text"></a>折叠范围并插入新文本

1. 创建一个包含文档中第一个段落的 <xref:Microsoft.Office.Interop.Word.Range> 对象。

    下面的代码示例可用于文档级自定义项。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet46":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet46":::

    以下代码示例可用于 VSTO 外接程序。 此代码运用了活动文档。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet46":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet46":::

2. 使用 <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> 枚举值折叠范围。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet47":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet47":::

3. 插入新文本。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet48":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet48":::

4. 选择 <xref:Microsoft.Office.Interop.Word.Range>。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet49":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet49":::

   如果使用 <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> 枚举值，则文本会在后续段落开头处插入。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet50":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet50":::

   你可能预计插入新句子是在段落标记之前插入它，但情况并非如此，因为原始范围包含段落标记。 有关详细信息，请参阅 [如何：以编程方式在创建范围时排除段落标记](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-collapse-a-range-in-a-document-level-customization"></a>在文档级自定义项中折叠范围

1. 下面的示例显示针对文档级自定项的完整方法。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet45":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet45":::

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="to-collapse-a-range-in-a-vsto-add-in"></a>折叠 VSTO 外接程序中的范围

1. 下面的示例演示 VSTO 外接程序的完整方法。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet45":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet45":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在 Word 文档中插入文本](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式检索范围中的开始字符和结束字符](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [如何：以编程方式在创建范围时排除段落标记](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [如何：以编程方式在文档中扩展范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
