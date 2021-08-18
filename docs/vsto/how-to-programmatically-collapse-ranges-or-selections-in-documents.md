---
title: 以编程方式折叠文档中的范围或选择
description: 了解如果使用 Range 或 Selection 对象，可能需要在插入文本之前将所选内容更改为插入点。
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
ms.openlocfilehash: 8d023c5f6a5373d14d6869bc9927975676e74fbc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099849"
---
# <a name="how-to-programmatically-collapse-ranges-or-selections-in-documents"></a>如何：以编程方式折叠文档中的范围或选择
  如果你在使用 <xref:Microsoft.Office.Interop.Word.Range> 或 <xref:Microsoft.Office.Interop.Word.Selection> 对象，则可能要在插入文本之前更改对插入点的选择，以避免覆盖现有文本。 和 <xref:Microsoft.Office.Interop.Word.Range> <xref:Microsoft.Office.Interop.Word.Selection> 对象都有 Collapse 方法，该方法利用 <xref:Microsoft.Office.Interop.Word.WdCollapseDirection> 枚举值：

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

   你可能预计插入新句子是在段落标记之前插入它，但情况并非如此，因为原始范围包含段落标记。 有关详细信息，请参阅如何：在创建范围 时以编程方式 [排除段落标记](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)。

## <a name="document-level-customization-example"></a>文档级自定义示例

### <a name="to-collapse-a-range-in-a-document-level-customization"></a>在文档级自定义项中折叠范围

1. 下面的示例显示针对文档级自定项的完整方法。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet45":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet45":::

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="to-collapse-a-range-in-a-vsto-add-in"></a>在外接程序中折叠VSTO范围

1. 以下示例演示外接程序的完整VSTO方法。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet45":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet45":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式将文本插入 Word 文档](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [如何：以编程方式定义和选择文档中的范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式检索范围中的开始字符和结束字符](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [如何：在创建范围时以编程方式排除段落标记](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)
- [如何：以编程方式扩展文档中的范围](../vsto/how-to-programmatically-extend-ranges-in-documents.md)
- [如何：以编程方式重置 Word 文档中的范围](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)
