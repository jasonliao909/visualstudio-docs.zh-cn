---
title: 如何：以编程方式将形状添加到 Visio 文档
description: 了解如何通过从模具中检索主控形状并将形状放置在活动页面上，将形状添加到 Microsoft Office Visio 文档。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], adding Visio shapes
- shapes [Office development in Visual Studio], adding Visio shapes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: abe165dc59aa5782bd555c7034e17924ac3d8015
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046693"
---
# <a name="how-to-programmatically-add-shapes-to-a-visio-document"></a>如何：以编程方式将形状添加到 Visio 文档
  可以通过从模具中检索主控形状并将形状放置在活动页面上，向 Microsoft Office Visio 文档添加形状。

 有关详细信息，请参阅 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) 方法、 [Microsoft.Office.Interop.Visio.Application.ActivePage](/office/vba/api/Visio.Application.ActivePage) 属性和 [Microsoft.Office.Interop.Visio.Page.Drop](/office/vba/api/Visio.Page.Drop) 方法的 VBA 参考文档。

## <a name="add-shapes-to-a-visio-document"></a>向 Visio 文档添加形状

### <a name="to-add-shapes-to-a-visio-document"></a>若要向 Visio 文档添加形状

- 在文档处于活动状态的情况下，从 Documents.Masters 集合中检索主控形状并将形状放置在活动文档上。 可以使用索引或主控形状名称来检索主控形状。

     下面的代码示例创建一个空白 Visio 文档，然后在“基本形状”  模具停靠的情况下打开它。 该代码随后检索多个形状并将它们放置在活动页面上。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet13":::

## <a name="see-also"></a>请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [使用 Visio 形状](../vsto/working-with-visio-shapes.md)
- [如何：以编程方式在 Visio 文档中复制和粘贴形状](../vsto/how-to-programmatically-copy-and-paste-shapes-in-a-visio-document.md)
