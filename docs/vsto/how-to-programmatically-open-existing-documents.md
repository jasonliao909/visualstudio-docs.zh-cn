---
title: 如何：以编程方式打开现有文档
description: 了解如何使用 Open 方法打开Microsoft Word完全限定的路径和文件名指定的现有文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening
- Word [Office development in Visual Studio], opening documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e1785053c4342144e56cb67e1f75adbef484058b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155845"
---
# <a name="how-to-programmatically-open-existing-documents"></a>如何：以编程方式打开现有文档
  方法 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 打开由完全Microsoft Office路径和文件名指定的现有 Word 文档。 此方法返回表示 <xref:Microsoft.Office.Interop.Word.Document> 打开的文档的 。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-open-a-document"></a>打开文档

- 调用 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 集合的 <xref:Microsoft.Office.Interop.Word.Documents> 方法，并提供文档的路径。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet5":::

## <a name="to-open-a-document-as-read-only"></a>以只读状态打开文档

- 调用 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 方法，提供文档的路径，在方法调用中将 *ReadOnly* 参数设置为 **True。**

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet6":::

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 名为 *NewDocument.doc的文档* 必须存在于驱动器 C 上名为 *Test* 的目录中。

## <a name="see-also"></a>请参阅
- [如何：以编程方式创建新文档](../vsto/how-to-programmatically-create-new-documents.md)
- [如何：以编程方式关闭文档](../vsto/how-to-programmatically-close-documents.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
