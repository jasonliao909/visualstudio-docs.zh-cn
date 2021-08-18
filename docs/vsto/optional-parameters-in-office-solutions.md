---
title: Office 解决方案中的可选参数
description: 了解如何不需要为可选参数传递值，因为默认值会自动用于每个缺少的参数。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], optional parameters
- Visual C# [Office development in Visual Studio], optional parameters
- Visual Basic [Office development in Visual Studio], optional parameters
- application development [Office development in Visual Studio], optional parameters
- missing field [Office development in Visual Studio]
- optional parameters [Office development in Visual Studio]
- parameters [Office development in Visual Studio], optional
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ab02913bb165f6f3ca7c240a27ee838fa5cf8e3b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032337"
---
# <a name="optional-parameters-in-office-solutions"></a>Office 解决方案中的可选参数
  Microsoft Office 应用程序的对象模型中的许多方法都接受可选参数。 如果使用 Visual Basic 在 Visual Studio 中开发 Office 解决方案，你不必为可选参数传递值，因为系统会为每个缺少的参数自动使用默认值。 在大多数情况下，你还可以在 Visual C# 项目中省略可选参数。 但是，在 `ThisDocument` 文档级 Word 项目中，不能省略类的可选 ref 参数。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 有关使用 Visual c # 和 Visual Basic 项目中的可选参数的详细信息，请参阅[&#41;的命名参数和可选参数 &#40;C&#35; 编程指南](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)和[可选参数 &#40;](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters)Visual Basic&#41;。

> [!NOTE]
> 在 Visual Studio 的早期版本中，必须为 Visual C# 项目中的每个可选参数传递一个值。 为了方便起见，这些项目包括一个名为 `missing` 的全局变量，当你想要使用某个可选参数的默认值时，可以将该变量传递给该可选参数。 Visual Studio 中 Office 的 Visual c # 项目仍包含 `missing` 变量，但在中开发 Office 解决方案时，通常不需要使用它，但在 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] Word 的 `ThisDocument` 文档级项目的类中调用方法时除外。

## <a name="example-in-excel"></a>Excel 中的示例
 <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> 方法具有多个可选参数。 可以为某些参数指定值，并接受其他参数的默认值，如下面的代码示例所示。 此示例需要一个具有名为 `Sheet1` 的工作表类的文档级项目。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb" id="Snippet1":::

## <a name="example-in-word"></a>Word 中的示例
 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 方法具有多个可选参数。 可以为某些参数指定值，并接受其他参数的默认值，如下面的代码示例所示。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet1":::

## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>在 Word 的 Visual c # 文档级项目中，使用 ThisDocument 类中方法的可选参数
 Word 对象模型包含许多具有可选的 **ref** 参数的方法，这些方法接受 <xref:System.Object> 值。 但是，  `ThisDocument` 在 Word 的 Visual c # 文档级项目中，不能省略生成类的方法的可选 ref 参数。 Visual c # 使你能够仅对接口的方法（而不是类）省略可选的 **ref** 参数。 例如，下面的代码示例不会进行编译，因为您不能省略类的方法的可选 **ref** 参数 <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> `ThisDocument` 。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet3":::

 调用 `ThisDocument` 类的方法时，请遵循以下准则：

- 若要接受可选 **ref** 参数的默认值，请将 `missing` 变量传递给参数。 在 Visual C# Office 项目中自动定义 `missing` 变量，并分配给生成的项目代码中的值 <xref:System.Type.Missing>。

- 若要为可选的 **ref** 参数指定你自己的值，请声明一个分配给你要指定的值的对象，然后将该对象传递给该参数。

  下面的代码示例演示如何 <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> 通过指定 *ignoreUppercase* 参数的值并接受其他参数的默认值来调用方法。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet4":::

  如果要编写在类中省略方法的可选 **ref** 参数的代码， `ThisDocument` 可以在属性返回的对象上调用相同的方法 <xref:Microsoft.Office.Interop.Word.Document> <xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A> ，并从该方法中省略这些参数。 可以这样做是因为 <xref:Microsoft.Office.Interop.Word.Document> 是接口而不是类。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet5":::

  有关值和引用类型参数的详细信息，请参阅[按值和按引用传递参数 &#40;Visual Basic](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) Visual Basic) 的&#41;(和将[参数传递 &#40;C&#35; 编程指南&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters)。

## <a name="see-also"></a>请参阅
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
