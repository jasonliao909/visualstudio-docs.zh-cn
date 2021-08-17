---
title: 如何：以编程方式在 Word 中设置搜索选项
description: 了解如何使用 Visual Studio 以编程方式为 Microsoft Word 中的选择设置搜索选项。
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
  可以通过两种方式为 Microsoft Office Word 文档中的选择设置搜索选项：

- 设置对象的单个属性 <xref:Microsoft.Office.Interop.Word.Find> 。

- 使用对象的方法的参数 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> <xref:Microsoft.Office.Interop.Word.Find> 。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>使用查找对象的属性
 下面的代码设置对象的属性 <xref:Microsoft.Office.Interop.Word.Find> ，以在当前选定内容中搜索文本。 请注意，搜索条件（如向前搜索、换行和文本搜索）是对象的属性 <xref:Microsoft.Office.Interop.Word.Find> 。

 <xref:Microsoft.Office.Interop.Word.Find>当你编写 c # 代码时，设置对象的每个属性并不有用，因为你必须在方法中指定与参数相同的属性 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 。 因此，此示例仅包含 Visual Basic 代码。

### <a name="to-set-search-options-using-a-find-object"></a>使用 Find 对象设置搜索选项

1. 设置对象的属性 <xref:Microsoft.Office.Interop.Word.Find> ，以便通过文本 " **查找我**" 向前搜索所选内容。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet76":::

## <a name="use-execute-method-arguments"></a>使用 Execute 方法参数
 下面的代码使用 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 对象的方法在 <xref:Microsoft.Office.Interop.Word.Find> 当前选定内容中搜索文本。 请注意，搜索条件（如向前搜索、换行和文本搜索）作为方法的参数进行传递 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 。

### <a name="to-set-search-options-using-execute-method-arguments"></a>使用执行方法参数设置搜索选项

1. 将搜索条件作为方法的参数传递 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> ，以通过文本的选择向前搜索 " **查找我**"。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet77":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet77":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在文档中搜索和替换文本](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [如何：以编程方式遍历在文档中找到的项](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [如何：以编程方式在搜索后还原选定内容](../vsto/how-to-programmatically-restore-selections-after-searches.md)
