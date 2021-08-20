---
title: 如何：以编程方式打印 Visio 文档
description: 了解如何打印完整的 Microsoft Visio 文档，或者仅打印该文档中的特定页面。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], printing Visio documents
- documents [Office development in Visual Studio], printing Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: cb428567c5b6e58ec3832917da92e45f7b3ec605
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122105894"
---
# <a name="how-to-programmatically-print-visio-documents"></a>如何：以编程方式打印 Visio 文档
  你可以打印完整的 Microsoft Office Visio 文档或仅打印某一特定页。

 有关打印方法的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Document.Print](/office/vba/api/Visio.Document.Print) 方法和 [Microsoft.Office.Interop.Visio.Page.Print](/office/vba/api/Visio.Page.Print) 方法的 VBA 参考文档。

## <a name="print-a-visio-document"></a>打印 Visio 文档

### <a name="to-print-a-complete-document"></a>打印完整的文档

- 调用要打印的 `Microsoft.Office.Interop.Visio.Document.Print` 对象的 `Microsoft.Office.Interop.Visio.Document` 方法。

     下面的代码示例将打印活动文档。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet8":::

## <a name="print-a-page-of-a-visio-document"></a>打印 Visio 文档的页面

### <a name="to-print-a-page-of-a-document"></a>打印文档的某一页

- 调用要打印的 `Microsoft.Office.Interop.Visio.Pages.Print` 对象的 `Microsoft.Office.Interop.Visio.Pages` 方法。

     下面的代码示例打印活动文档的第一页。 若要使用此示例，请从项目的 `ThisAddIn` 类中运行代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet9":::

## <a name="see-also"></a>请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [如何：以编程方式创建新的 Visio 文档](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [如何：以编程方式打开 Visio 文档](../vsto/how-to-programmatically-open-visio-documents.md)
- [如何：以编程方式关闭 Visio 文档](../vsto/how-to-programmatically-close-visio-documents.md)
- [如何：以编程方式保存 Visio 文档](../vsto/how-to-programmatically-save-visio-documents.md)
