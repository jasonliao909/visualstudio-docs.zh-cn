---
title: 如何：以编程方式关闭Visio文档
description: 了解如何使用 Microsoft Office Visio ument 关闭活动Microsoft.Office.Interop.Visio.Doc文档。Close 方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing Visio documents
- Visio [Office development in Visual Studio], closing Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c48b814629e01e370696bb30f8ee15af60098ec3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046641"
---
# <a name="how-to-programmatically-close-visio-documents"></a>如何：以编程方式关闭Visio文档
  可以使用 `Microsoft.Office.Interop.Visio.Document.Close` 方法关闭活动 Microsoft Office Visio 文档。

 有关此方法的详细信息，请参阅 [Microsoft.Office.Interop.Visio.Document.Close](/office/vba/api/Visio.Document.Close) 方法的 VBA 参考文档。

## <a name="close-the-active-document"></a>关闭活动文档

### <a name="to-close-the-active-document"></a>关闭活动文档

- 调用 `Microsoft.Office.Interop.Visio.Document.Close` 方法关闭活动文档。

     若要使用以下代码示例，请将其运行在 VSTO `ThisAddIn` 外接程序项目中的 类中，Visio。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet7":::

## <a name="see-also"></a>请参阅
- [Visio解决方案](../vsto/visio-solutions.md)
- [Visio对象模型概述](../vsto/visio-object-model-overview.md)
- [如何：以编程方式创建新的Visio文档](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [如何：以编程方式打开Visio文档](../vsto/how-to-programmatically-open-visio-documents.md)
- [如何：以编程方式保存Visio文档](../vsto/how-to-programmatically-save-visio-documents.md)
- [如何：以编程方式打印Visio文档](../vsto/how-to-programmatically-print-visio-documents.md)
