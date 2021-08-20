---
title: 如何：以编程方式使用 Word 中的内置对话框
description: 了解如何使用Visual Studio以编程方式使用 Microsoft Word。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, Word
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 66b35e6a46ba42f64dddf54427d43bba74f10ae0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147981"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>如何：以编程方式使用 Word 中的内置对话框
  使用 Microsoft Office Word 时，有时需要显示用于用户输入的对话框。 尽管你可以创建自己的对话框，但你可能还希望采用在 Word 中使用内置对话框的方法，该对话框在 对象集合中 <xref:Microsoft.Office.Interop.Word.Dialogs> <xref:Microsoft.Office.Interop.Word.Application> 公开。 这使你可以访问 200 多个内置对话框，这些对话框表示为枚举。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="display-dialog-boxes"></a>显示对话框
 若要显示对话框，请使用 枚举的值之一创建一个 对象，该对象表示 <xref:Microsoft.Office.Interop.Word.WdWordDialog> <xref:Microsoft.Office.Interop.Word.Dialog> 要显示的对话框。 然后，调用 <xref:Microsoft.Office.Interop.Word.Dialog.Show%2A> 对象的 <xref:Microsoft.Office.Interop.Word.Dialog> 方法。

 下面的代码示例演示如何显示"文件 **打开"** 对话框。 若要使用此示例，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet100":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet100":::

### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>通过后期绑定提供的"访问"对话框成员
 Word 中对话框的一些属性和方法仅通过后期绑定可用。 在Visual Basic **Option Strict** 的项目中，必须使用反射来访问这些成员。 有关详细信息，请参阅解决方案[中的Office绑定](../vsto/late-binding-in-office-solutions.md)。

 下面的代码示例演示如何使用 Visual Basic 项目中"文件打开"对话框的 Name 属性，其中 Option **Strict** 已关闭，或在面向 或 的 Visual C# 项目中 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 。 若要使用此示例，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet122":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet122":::

 下面的代码示例演示如何使用反射访问 Option Strict Visual Basic中"文件打开"对话框的 **Name** 属性。 若要使用此示例，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet102":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式在隐藏模式下使用 Word 对话框](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
- [Option strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
