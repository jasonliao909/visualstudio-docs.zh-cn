---
title: 如何：以编程方式保存 Visio 文档
description: 了解如何使用 Visual Studio 以编程方式保存 Microsoft Visio 现有文档和尚未保存的新文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving Visio documents
- Visio [Office development in Visual Studio], saving Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 676281c289d565e4e8ffc07e68c6ced0199b10d0c3f5270e60b43fea222de025
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121351676"
---
# <a name="how-to-programmatically-save-visio-documents"></a>如何：以编程方式保存 Visio 文档
  可通过几种方法来保存 Microsoft Office Visio 文档：

- 将更改保存在现有文档中。

- 保存新文档，或使用新名称保存文档。

- 使用指定参数保存文档。

  有关详细信息，请参阅 [Microsoft.Office.Interop.Visio.Document.Save](/office/vba/api/Visio.Document.Save) 方法、 [Microsoft.Office.Interop.Visio.Document.SaveAs](/office/vba/api/Visio.Document.SaveAs) 方法和 [Microsoft.Office.Interop.Visio.Document.SaveAsEx](/office/vba/api/Visio.Document.SaveAsEx) 方法的 VBA 参考文档。

## <a name="save-an-existing-document"></a>保存现有文档

### <a name="to-save-a-document"></a>保存文档

- 调用以前保存的文档的 `Microsoft.Office.Tools.Visio.Document` 类的 `Microsoft.Office.Interop.Visio.Document.Save` 方法。

     若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

    > [!NOTE]
    > 如果尚未保存新 Visio 文档，则 `Microsoft.Office.Interop.Visio.Document.Save` 方法会引发异常。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet11":::

## <a name="save-a-document-with-a-new-name"></a>使用新名称保存文档
 使用 `Microsoft.Office.Interop.Visio.Document.SaveAs` 方法可保存新文档或具有新名称的文档。 此方法要求指定新文件名。

### <a name="to-save-the-active-visio-document-with-a-new-name"></a>使用新名称保存活动 Visio 文档

- 使用包括文件名的完全限定路径来调用要保存的 `Microsoft.Office.Tools.Visio.Document` 的 `Microsoft.Office.Interop.Visio.Document.SaveAs` 方法。 如果该文件夹中已存在具有该名称的文件，则以无提示方式覆盖它。

     若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet10":::

## <a name="save-a-document-with-a-new-name-and-specified-arguments"></a>使用新名称和指定参数保存文档
 使用 `Microsoft.Office.Interop.Visio.Document.SaveAsEx` 方法可使用新名称保存文档，并指定要应用于该文档的任何适用自变量。

### <a name="to-save-document-with-a-new-name-and-specified-arguments"></a>若要使用新名称和指定参数保存文档

- 使用包括文件名的完全限定路径来调用要保存的 `Microsoft.Office.Tools.Visio.Document` 的 `Microsoft.Office.Interop.Visio.Document.SaveAsEx` 方法。 如果该文件夹中已存在具有该名称的文件，则引发异常。

     下面的代码示例使用新名称保存活动文档，将文档标记为只读，并在“最近使用过的”文档列表中显示文档。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet12":::

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 若要保存具有新名称的文档，名为的目录 `Test` 必须位于 "我的 *文档*" 文件夹中 (Windows XP 及更早版本) 或 "*文档*" 文件夹 (用于 Windows Vista) 。

## <a name="see-also"></a>另请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [如何：以编程方式创建新的 Visio 文档](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [如何：以编程方式打开 Visio 文档](../vsto/how-to-programmatically-open-visio-documents.md)
- [如何：以编程方式关闭 Visio 文档](../vsto/how-to-programmatically-close-visio-documents.md)
- [如何：以编程方式打印 Visio 文档](../vsto/how-to-programmatically-print-visio-documents.md)
