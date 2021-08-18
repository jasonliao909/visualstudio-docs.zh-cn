---
title: 如何：以编程方式关闭文档
description: 了解如何关闭活动文档，也可以指定要关闭的 Microsoft Office Word 文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing
- Word [Office development in Visual Studio], closing documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2b90af6301591f5f21c34d9f69e649e3ffa70097
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083266"
---
# <a name="how-to-programmatically-close-documents"></a>如何：以编程方式关闭文档
  可以关闭活动文档，也可以指定关闭某个文档。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="close-the-active-document"></a>关闭活动文档
 关闭活动文档有两个过程：一个用于文档级自定义项；另一个用于 VSTO 外接程序。

### <a name="to-close-the-active-document-in-a-document-level-customization"></a>关闭文档级自定义项中的活动文档

1. 调用项目中 <xref:Microsoft.Office.Tools.Word.Document.Close%2A> 类的 `ThisDocument` 方法，以关闭与自定义关联的文档。 若要使用以下代码示例，请从 `ThisDocument` 类中运行它。

    > [!NOTE]
    > 此示例将 <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> 值传递给要关闭的 *SaveChanges* 参数，而无需保存更改或提示用户。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet3":::

### <a name="to-close-the-active-document-in-a-vsto-add-in"></a>关闭 VSTO 外接程序中的活动文档

1. 调用 <xref:Microsoft.Office.Interop.Word._Document.Close%2A> 属性的 <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> 方法，以关闭活动文档。 若要使用下面的代码示例，请从项目的 `ThisAddIn` 类中运行它。

    > [!NOTE]
    > 此示例将 <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> 值传递给要关闭的 *SaveChanges* 参数，而无需保存更改或提示用户。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet3":::

## <a name="close-a-document-that-you-specify-by-name"></a>关闭按名称指定的文档
 对于 VSTO 外接程序和文档级自定义项来说，按名称指定的文档的关闭方式是相同的。

### <a name="to-close-a-document-that-you-specify-by-name"></a>关闭按名称指定的文档

1. 将文档名称指定为 <xref:Microsoft.Office.Interop.Word._Application.Documents%2A> 集合的参数，然后调用 <xref:Microsoft.Office.Interop.Word._Document.Close%2A> 方法。 以下代码示例假设在 Word 中打开了名为 **NewDocument** 的文档。

    > [!NOTE]
    > 此示例将 <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> 值传递给要关闭的 *SaveChanges* 参数，而无需保存更改或提示用户。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet4":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)
- [如何：以编程方式保存文档](../vsto/how-to-programmatically-save-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
