---
title: 如何：以编程方式在隐藏模式下使用 Word 对话框
description: 了解如何在隐藏模式下Visual Studio以编程Microsoft Word对话框。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden dialog boxes
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, hidden mode in Word
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ca6d7f1e14904497ecb756936b996b64311a8423
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664707"
---
# <a name="how-to-programmatically-use-word-dialog-boxes-in-hidden-mode"></a>如何：以编程方式在隐藏模式下使用 Word 对话框
  可以通过调用 Microsoft Office Word 中的内置对话框，通过一个方法调用执行复杂操作，而无需向用户显示它们。 为此，可以使用 对象的 <xref:Microsoft.Office.Interop.Word.Dialog.Execute%2A> 方法 <xref:Microsoft.Office.Interop.Word.Dialog> ，而无需调用 <xref:Microsoft.Office.Interop.Word.Dialog.Display%2A> 方法。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="examples"></a>示例
 下面的代码示例演示如何在隐藏模式下使用"页面设置"对话框设置多个页面设置属性，无需用户输入。 这些示例使用 <xref:Microsoft.Office.Interop.Word.Dialog> 对象来配置自定义页面大小。 页面设置的特定设置（如上边距、下边距等）作为对象的后期绑定 <xref:Microsoft.Office.Interop.Word.Dialog> 属性提供。 这些属性在运行时由 Word 动态创建。

 以下示例演示如何在 Option **Strict** Visual Basic的 Visual C# 项目中执行此任务 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 在这些项目中，可以使用 visual C# 编译器中的Visual Basic绑定功能。 若要使用此示例，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet123":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet123":::

 以下示例演示如何在启用 Option **Strict** Visual Basic中执行此任务。 在这些项目中，必须使用反射来访问后期绑定属性。 若要使用此示例，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet104":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式使用 Word 中的内置对话框](../vsto/how-to-programmatically-use-built-in-dialog-boxes-in-word.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [解决方案中的Office绑定](../vsto/late-binding-in-office-solutions.md)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
