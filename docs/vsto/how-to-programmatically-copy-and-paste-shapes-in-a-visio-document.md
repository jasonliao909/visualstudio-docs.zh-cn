---
title: 以编程方式在文档中Visio形状
description: 了解如何以编程方式在文档的一页上复制形状，并将其粘贴到同一文档中的新页面中。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- shapes [Office development in Visual Studio], copying and pasting Visio shapes
- Visio [Office development in Visual Studio], copying and pasting Visio shapes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: fb913dc14437f9593a656a5ae4eb02368b82493b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046602"
---
# <a name="how-to-programmatically-copy-and-paste-shapes-in-a-visio-document"></a>如何：以编程方式将形状复制和粘贴到Visio文档中
  你可以以编程方式复制文档中某一页上的形状，并将其粘贴到同一文档中新的一页。 你可以选择将其粘贴到默认位置（活动窗口的中央），或将其粘贴到与在其原始页相同的坐标位置。

## <a name="copy-and-paste-shapes"></a>复制和粘贴形状
 有关对象模型的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle)、 [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval)、 [Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy)和 [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) 方法以及 [Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNormal](/office/vba/api/Visio.viscutcopypastecodes) 标志的 VBA 参考文档。

### <a name="to-copy-shapes-to-the-center-of-another-page"></a>将形状复制到另一页的中央

- 下面的示例演示如何复制第一页中的形状并将其粘贴到第二页的中央。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet14":::

## <a name="copy-and-paste-shapes-with-the-same-positions"></a>复制并粘贴相同位置的形状
 有关对象模型的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle)、 [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval)、 [Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy)和 [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) 方法以及 [Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNoTranslate](/office/vba/api/Visio.viscutcopypastecodes) 标志的 VBA 参考文档。

 如果需要控制粘贴信息的格式， (（可选) 建立指向源文件的链接 (例如 Microsoft Office Word 文档) ，请使用 PasteSpecial 方法。

### <a name="to-copy-shapes-and-shape-locations-to-another-page"></a>将形状和形状位置复制到另一页

- 下面的示例演示如何复制第一页中的形状并将其粘贴到第二页中与其原始坐标相同的位置。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet15":::

## <a name="see-also"></a>请参阅
- [Visio解决方案](../vsto/visio-solutions.md)
- [Visio对象模型概述](../vsto/visio-object-model-overview.md)
- [使用Visio形状](../vsto/working-with-visio-shapes.md)
- [如何：以编程方式将形状添加到Visio文档](../vsto/how-to-programmatically-add-shapes-to-a-visio-document.md)
