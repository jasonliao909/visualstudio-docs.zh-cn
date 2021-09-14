---
title: 如何：以编程方式打开 Visio 文档
description: 了解如何使用 Visual Studio 以编程方式使用 open 或 microsoft.office.interop.visio.documents.open 方法打开 Visio 文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening Visio documents
- Visio [Office development in Visual Studio], opening Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 1c3126f3f5ac73632996079a070c426afc20d656
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664718"
---
# <a name="how-to-programmatically-open-visio-documents"></a>如何：以编程方式打开 Visio 文档
  可以通过两种方法打开现有 Microsoft Office Visio 文档： Open 和 microsoft.office.interop.visio.documents.open。 Microsoft.office.interop.visio.documents.open 方法与 Open 方法相同，不同之处在于它提供调用方可以在其中指定文档打开方式的参数。

 有关对象模型的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Documents.Open](/office/vba/api/Visio.Documents.Open) 方法和 [Microsoft.Office.Interop.Visio.Documents.OpenEx](/office/vba/api/Visio.Documents.OpenEx) 方法的 VBA 参考文档。

## <a name="open-a-visio-document"></a>打开 Visio 文档

### <a name="to-open-a-visio-document"></a>若要打开 Visio 文档

- 调用 `Microsoft.Office.Interop.Visio.Documents.Open` 方法并提供 Visio 文档的完全限定路径。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet5":::

## <a name="open-a-visio-document-with-specified-arguments"></a>使用指定的参数打开 Visio 文档

### <a name="to-open-a-visio-document-as-read-only-and-docked"></a>如要以只读和停靠方式打开 Visio 文档

- 调用 `Microsoft.Office.Interop.Visio.Documents.OpenEx` 方法，提供 Visio 文档的完全限定路径，并包括想要使用的参数，在本例中为 Docked 和 Read-only。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet6":::

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 名为的 Visio 文档 `myDrawing.vsd` 必须位于 " `Test` *我的文档*" 文件夹中名为 "我的文档" 文件夹中的目录 (用于 Windows XP 和更早版本) 或 (Vista Windows 的 "*文档*" 文件夹) 。

## <a name="see-also"></a>另请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [如何：以编程方式创建新的 Visio 文档](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [如何：以编程方式关闭 Visio 文档](../vsto/how-to-programmatically-close-visio-documents.md)
- [如何：以编程方式保存 Visio 文档](../vsto/how-to-programmatically-save-visio-documents.md)
- [如何：以编程方式打印 Visio 文档](../vsto/how-to-programmatically-print-visio-documents.md)
