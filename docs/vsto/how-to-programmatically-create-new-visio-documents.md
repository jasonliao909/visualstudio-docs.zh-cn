---
title: 如何：以编程方式创建新的 Visio 文档
description: 了解如何以编程方式创建新的 Microsoft Visio 绘图文档并将其添加到打开 Visio 文档的文档集合中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], creating Visio documents
- documents [Office development in Visual Studio], creating Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a195996684334cbc658d75f82a5f81f1d69109af45174b3ce6b2f6c996c38ae8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121384322"
---
# <a name="how-to-programmatically-create-new-visio-documents"></a>如何：以编程方式创建新的 Visio 文档
  创建新的 Microsoft Office Visio 绘图文档时，会将其添加到所打开 Visio 文档的 `Microsoft.Office.Interop.Visio.Documents` 集合中。 随后，`Microsoft.Office.Interop.Visio.Documents.Add` 方法会创建一个新的 Visio 绘图文档。 有关详细信息，请参阅 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) 方法的 VBA 参考文档。

## <a name="create-new-blank-documents"></a>创建新的空白文档

### <a name="to-create-a-new-document"></a>创建新文档

- 使用 `Microsoft.Office.Interop.Visio.Documents.Add` 方法创建一个不基于模板的新空白文档。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet1":::

## <a name="create-documents-copied-from-existing-documents"></a>创建从现有文档复制的文档
 `Microsoft.Office.Interop.Visio.Documents.Add` 方法可创建从现有 Visio 文档复制而来的新文档。 你必须提供相应关系图的文件名和完全限定路径。

### <a name="to-create-a-new-document-that-is-copied-from-an-existing-document"></a>创建从现有文档复制而来的新文档

- 调用 `Microsoft.Office.Interop.Visio.Documents.Add` 方法并指定 Visio 关系图的路径。

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet2":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet2":::

## <a name="create-stencils-copied-from-existing-stencils"></a>创建从现有模具复制的模具
 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) 方法可创建从现有 Visio 模具复制而来的新模具。 你必须提供相应模具的文件名和完全限定路径。

### <a name="to-create-a-new-stencil-that-is-copied-from-an-existing-stencil"></a>创建从现有模具复制而来的新模具

- 调用 `Microsoft.Office.Interop.Visio.Documents.Add` 方法并指定相应模具的路径。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet3":::

## <a name="create-documents-based-on-existing-templates"></a>基于现有模板创建文档
 `Microsoft.Office.Interop.Visio.Documents.Add`方法可以 (基于) 的现有 Visio (模板的一个 *.vsd* 文件创建新文档) 。  此方法会复制作为模板工作区一部分的模具、样式和设置。 你必须提供模板的文件名称和完全限定路径。

### <a name="to-create-a-new-document-that-is-based-on-an-existing-template"></a>创建基于现有模板的新文档

- 调用 `Microsoft.Office.Interop.Visio.Documents.Add` 方法并指定相应模板的路径。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet4":::

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 名为的 Visio 文档 `myDrawing.vsd` 必须位于 " `Test` *我的文档*" 文件夹中名为 "我的文档" 文件夹中的目录 (用于 Windows XP 和更早版本) 或 (Vista Windows 的 "*文档*" 文件夹) 。

- 名为的 Visio 文档 `myStencil.vss` 必须位于 " `Test` *我的文档*" 文件夹中名为 "我的文档" 文件夹中的目录 (用于 Windows XP 和更早版本) 或 (Vista Windows 的 "*文档*" 文件夹) 。

- 名为的 Visio 文档 `myTemplate.vst` 必须位于 " `Test` *我的文档*" 文件夹中名为 "我的文档" 文件夹中的目录 (用于 Windows XP 和更早版本) 或 (Vista Windows 的 "*文档*" 文件夹) 。

## <a name="see-also"></a>请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [如何：以编程方式打开 Visio 文档](../vsto/how-to-programmatically-open-visio-documents.md)
- [如何：以编程方式关闭 Visio 文档](../vsto/how-to-programmatically-close-visio-documents.md)
- [如何：以编程方式保存 Visio 文档](../vsto/how-to-programmatically-save-visio-documents.md)
- [如何：以编程方式打印 Visio 文档](../vsto/how-to-programmatically-print-visio-documents.md)
