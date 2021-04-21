---
title: 如何：以编程方式遍历在文档中找到的项
description: 了解如何使用 Visual Studio 以编程方式循环访问 Microsoft Word 文档中找到的项。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- loops, through found items in documents
- documents [Office development in Visual Studio], searching
- text [Office development in Visual Studio], searching in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ce3153eb4e2fd7fd44318097a6b76ef6e0346086
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827339"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>如何：以编程方式遍历在文档中找到的项
  <xref:Microsoft.Office.Interop.Word.Find>类具有一个 <xref:Microsoft.Office.Interop.Word.Find.Found%2A> 属性，该属性将在每次找到搜索项时返回 **true** 。 你可以使用 <xref:Microsoft.Office.Interop.Word.Range> 方法循环访问在 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 中找到的所有实例。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-loop-through-found-items"></a>循环访问找到的项

1. 声明 <xref:Microsoft.Office.Interop.Word.Range> 对象。

    下面的代码示例可用于文档级自定义项。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet79":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet79":::

    以下代码示例可用于 VSTO 外接程序。 本示例使用活动文档。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet79":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet79":::

2. 循环使用 <xref:Microsoft.Office.Interop.Word.Find.Found%2A> 属性来搜索文档中字符串的所有匹配项，每次找到该字符串时整数变量递增 1。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet80":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet80":::

3. 在消息框中显示找到字符串的次数。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet81":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet81":::

   以下示例显示了完整方法。

## <a name="document-level-customization-example"></a>文档级自定义项示例

### <a name="to-loop-through-items-in-a-document-level-customization"></a>循环访问文档级自定义项中的项

1. 下面的示例显示文档级自定项的完整代码。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet78":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet78":::

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="to-loop-through-items-in-a-vsto-add-in"></a>遍历 VSTO 外接程序中的项

1. 下面的示例显示 VSTO 外接程序的完整代码。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet78":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet78":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在文档中搜索和替换 uiresources.rext](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式在 Word 中设置搜索选项](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [如何：以编程方式在文档中定义和选择范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：以编程方式在搜索后还原选定内容](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
