---
title: 如何：以编程方式循环访问文档中找到的项
description: 了解如何使用 Visual Studio 以编程方式循环访问文档中Microsoft Word项。
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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8a9333efec2886ba4ed7d8d33a99e2de85bd1733f10837299643cae0c19a9f30
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440742"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>如何：以编程方式循环访问文档中找到的项
  类具有 属性，只要找到已搜索的项， <xref:Microsoft.Office.Interop.Word.Find> <xref:Microsoft.Office.Interop.Word.Find.Found%2A> 该属性就会返回true。 你可以使用 <xref:Microsoft.Office.Interop.Word.Range> 方法循环访问在 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 中找到的所有实例。

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

## <a name="document-level-customization-example"></a>文档级自定义示例

### <a name="to-loop-through-items-in-a-document-level-customization"></a>循环访问文档级自定义项中的项

1. 下面的示例显示文档级自定项的完整代码。 若要使用此代码，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet78":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet78":::

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="to-loop-through-items-in-a-vsto-add-in"></a>循环访问外接程序VSTO项

1. 下面的示例显示 VSTO 外接程序的完整代码。 若要使用此代码，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet78":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet78":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式搜索和替换文档中的 rext](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式在 Word 中设置搜索选项](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [如何：以编程方式定义和选择文档中的范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [如何：在搜索后以编程方式还原选择](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
