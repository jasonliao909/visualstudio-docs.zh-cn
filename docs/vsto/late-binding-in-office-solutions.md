---
title: 解决方案中的Office绑定
description: 了解应用程序内对象模型中的Microsoft Office如何提供通过后期绑定功能提供的功能。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- objects [Office development in Visual Studio], casting
- types [Office development in Visual Studio], casting
- automation [Office development in Visual Studio], casting objects
- casting, object to specific type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0a68aafed5cc4bb42ba9b8d1c4b05d4167e32f68
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032610"
---
# <a name="late-binding-in-office-solutions"></a>解决方案中的Office绑定
  应用程序的对象模型中的Office提供通过后期绑定功能提供的功能。 例如，某些方法和属性可以返回不同类型的对象，具体取决于应用程序Office上下文，并且某些类型可以在不同的上下文中公开不同的方法或属性。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual Basic Option **Strict** 关闭，面向 或 的 Visual C# 项目可以直接处理使用这些后期绑定功能 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 的类型。

## <a name="implicit-and-explicit-casting-of-object-return-values"></a>隐式和显式强制转换对象返回值
 主互操作程序集中的Microsoft Office和属性 (PIA) 返回值，因为它们可以返回几种 <xref:System.Object> 不同类型的对象。 例如， 属性返回 ，因为它的返回值可以是 或 对象， <xref:Microsoft.Office.Tools.Excel.Workbook.ActiveSheet%2A> <xref:System.Object> <xref:Microsoft.Office.Interop.Excel.Worksheet> <xref:Microsoft.Office.Interop.Excel.Chart> 具体取决于活动工作表是什么。

 当方法或属性返回 时，必须将 (中的 Visual Basic) 显式转换为打开 <xref:System.Object> **Option Strict** Visual Basic项目中的正确类型。 在 Option Strict 关闭的项目中 <xref:System.Object> ，Visual Basic **显式** 转换返回值。

 在大多数情况下，参考文档列出了返回 的成员的可能返回值类型 <xref:System.Object> 。 转换或强制转换对象可在代码编辑器中为对象启用 IntelliSense。

 有关中转换的信息，Visual Basic隐式转换和显式&#40;Visual Basic&#41;[](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions)[和 CType 函数&#40;Visual Basic&#41;。 ](/dotnet/visual-basic/language-reference/functions/ctype-function)

### <a name="examples"></a>示例
 下面的代码示例演示如何在 Option **Strict** 为 on 的 Visual Basic项目中将对象强制转换到特定类型。 在此类型的项目中，必须将 属性显式 <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> 强制转换到 <xref:Microsoft.Office.Interop.Excel.Range> 。 此示例需要使用名为 的工作表Excel项目的文档级项目 `Sheet1` 。

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet9":::

 下面的代码示例演示如何将对象隐式强制转换到 Visual Basic项目中的一个特定类型，其中 Option **Strict** 已关闭，或在面向 的 Visual C# 项目中 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 在这些类型的项目中， <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> 属性隐式强制转换到 <xref:Microsoft.Office.Interop.Excel.Range> 。 此示例需要使用名为 的工作表Excel项目的文档级项目 `Sheet1` 。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet10":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="access-members-that-are-available-only-through-late-binding"></a>仅通过后期绑定可用的访问成员
 仅通过后期绑定Office PIA 中的某些属性和方法可用。 在Visual Basic Option **Strict** 关闭的项目或面向 或 的 Visual C# 项目中，可以使用这些语言中的后期绑定功能来访问后期 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 绑定成员。 在Visual Basic **Option Strict** 的项目中，必须使用反射来访问这些成员。

### <a name="examples"></a>示例
 下面的代码示例演示如何在 Option **Strict** Visual Basic或面向 的 Visual C# 项目中访问后期绑定成员 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 此示例访问 Word 中"文件打开"对话框的 **后期绑定的** Name 属性。 若要使用此示例，请从 Word 项目中 `ThisDocument` 的 或 `ThisAddIn` 类运行它。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet122":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet122":::

 下面的代码示例演示如何在 Option **Strict** 为 on 的 Visual Basic项目中使用反射来完成相同的任务。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet102":::

## <a name="see-also"></a>请参阅
- [在解决方案中Office代码](../vsto/writing-code-in-office-solutions.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
- [使用类型动态&#40;C&#35;编程指南&#41;](/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [Option Strict 语句](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [反射 (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [反射 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
