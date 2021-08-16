---
title: 如何：以编程方式在 Word 中设置搜索选项
description: 了解如何使用 Visual Studio以编程方式设置搜索选项，以在 Microsoft Word。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- settings, Word search options
- documents [Office development in Visual Studio], search options
- Word, searching options
- searching, Word options
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c96533e9b6adf6367a8980f8315f84cc1c3ffe24cc8177ba799983e03bd9852e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394220"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>如何：以编程方式在 Word 中设置搜索选项
  有两种方法可以设置 Word 文档中Microsoft Office选项：

- 设置 对象的单个 <xref:Microsoft.Office.Interop.Word.Find> 属性。

- 使用 对象的 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 方法的参数 <xref:Microsoft.Office.Interop.Word.Find> 。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>使用 Find 对象的属性
 以下代码设置 对象的属性 <xref:Microsoft.Office.Interop.Word.Find> ，以在当前选定内容中搜索文本。 请注意，搜索条件（如向前搜索、换行和要搜索的文本）是 对象 <xref:Microsoft.Office.Interop.Word.Find> 的属性。

 编写 C# 代码时，设置 对象的每个属性都无用，因为必须在 方法中指定与参数 <xref:Microsoft.Office.Interop.Word.Find> 相同的 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 属性。 因此，此示例仅包含Visual Basic代码。

### <a name="to-set-search-options-using-a-find-object"></a>使用 Find 对象设置搜索选项

1. 设置 对象的属性 <xref:Microsoft.Office.Interop.Word.Find> ，以在所选文本中向前搜索"查找 **我"。**

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet76":::

## <a name="use-execute-method-arguments"></a>使用 Execute 方法参数
 以下代码使用 对象的 方法在当前选定 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> <xref:Microsoft.Office.Interop.Word.Find> 内容中搜索文本。 请注意，搜索条件（如向前搜索、换行和要搜索的文本）作为 方法 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 的参数传递。

### <a name="to-set-search-options-using-execute-method-arguments"></a>使用 Execute 方法参数设置搜索选项

1. 将搜索条件作为 方法的参数 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 传递，以通过所选文本向前搜索"查找 **我"。**

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet77":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet77":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式搜索和替换文档中的文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式循环访问文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [如何：在搜索后以编程方式还原选择](../vsto/how-to-programmatically-restore-selections-after-searches.md)
