---
title: 如何：以编程方式从文档中删除所有注释
description: 了解如何使用 Visual Studio 以编程方式从 Microsoft Word 文档中删除所有注释。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], removing comments
- comments, removing from documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 3ba39c17b5c00ec78af0b4ba89aedb528cb6a322ca22aaa8b44bab2d21f732ef
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121366194"
---
# <a name="how-to-programmatically-remove-all-comments-from-documents"></a>如何：以编程方式从文档中删除所有注释
  使用 `DeleteAllComments` 方法可以删除 Microsoft Office Word 文档中的所有注释。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-remove-all-comments-from-a-document-that-is-part-of-a-document-level-customization"></a>从属于文档级自定义项的文档中删除所有注释

1. 调用项目中 <xref:Microsoft.Office.Tools.Word.Document.DeleteAllComments%2A> 类的 `ThisDocument` 方法。 若要使用此代码示例，请从 `ThisDocument` 类中运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet119":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet119":::

## <a name="to-remove-all-comments-from-a-document-by-using-a-vsto-add-in"></a>使用 VSTO 外接程序从文档中删除所有注释

1. 调用要从中删除注释的 <xref:Microsoft.Office.Interop.Word._Document.DeleteAllComments%2A> 的 <xref:Microsoft.Office.Interop.Word.Document> 方法。

     下面的代码示例从活动文档中删除所有注释。 若要使用此代码示例，请从项目中的 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet119":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet119":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式向文档中的文本添加注释](../vsto/how-to-programmatically-add-comments-to-text-in-documents.md)
- [文档宿主项](../vsto/document-host-item.md)
