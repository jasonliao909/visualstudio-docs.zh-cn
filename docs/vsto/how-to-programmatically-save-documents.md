---
title: 如何：以编程方式保存文档
description: 了解如何使用 Visual Studio以编程方式保存文档，而无需更改文档的名称或新名称。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving
- Word [Office development in Visual Studio], saving documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2b1e00d60709d506ae0d3ee2d4bd6842be43be19
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046459"
---
# <a name="how-to-programmatically-save-documents"></a>如何：以编程方式保存文档

有几种方法可以保存 word Microsoft Office文档。 可以在不更改文档名称的情况下保存文档，也可以保存具有新名称的文档。

[!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="save-a-document-without-changing-the-name"></a>保存文档而不更改名称

### <a name="to-save-the-document-associated-with-a-document-level-customization"></a>保存与文档级自定义项关联的文档

1. 调用 <xref:Microsoft.Office.Tools.Word.Document.Save%2A> 类的 <xref:Microsoft.Office.Tools.Word.Document> 方法。 若要使用此代码示例，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet7":::

### <a name="to-save-the-active-document"></a>保存活动文档

1. 为 <xref:Microsoft.Office.Interop.Word._Document.Save%2A> 活动文档调用 方法。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet8":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet8":::

   如果不确定要保存的文档是否是活动文档，可以按其名称引用它。

### <a name="to-save-a-document-specified-by-name"></a>保存按名称指定的文档

1. 使用文档名称作为集合的参数 <xref:Microsoft.Office.Interop.Word.Documents> 。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet9":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet9":::

## <a name="save-a-document-with-a-new-name"></a>使用新名称保存文档

使用 `SaveAs` 方法保存具有新名称的文档。 可以在文档级 Word 项目中对宿主项使用此方法，或者在任何 Word 项目中对本机对象 <xref:Microsoft.Office.Tools.Word.Document> <xref:Microsoft.Office.Interop.Word.Document> 使用此方法。 此方法要求指定新文件名，但其他参数是可选的。

> [!NOTE]
> 如果在 的事件处理程序内显示 **"SaveAs"** 对话框，并且将 Cancel 参数设置为 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> `ThisDocument` **false，** 则应用程序可能会意外退出。  如果将 Cancel *参数设置为* **true，** 则会显示一条错误消息，指示已禁用自动保存。

### <a name="to-save-the-document-associated-with-a-document-level-customization-with-a-new-name"></a>使用新名称保存与文档级自定义项关联的文档

1. 使用 `SaveAs` 完全限定的路径和文件名调用项目中 `ThisDocument` 类的 方法。 如果该文件夹中已存在具有该名称的文件，则以无提示方式覆盖它。 若要使用此代码示例，请从 `ThisDocument` 类中运行它。

    > [!NOTE]
    > 如果目标目录不存在或者保存文件时存在其他问题，则 方法 `SaveAs` 将引发异常。 在 方法周围或在调用方法内使用 块 `try...catch` `SaveAs` 是一种很好的做法。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet10":::

### <a name="to-save-a-native-document-with-a-new-name"></a>使用新名称保存本机文档

1. 使用完全限定的路径和文件名调用要保存的 <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> <xref:Microsoft.Office.Interop.Word.Document> 的 方法。 如果该文件夹中已存在具有该名称的文件，则以无提示方式覆盖它。

     下面的代码示例使用新名称保存活动文档。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

    > [!NOTE]
    > 如果目标目录不存在或者保存文件时存在其他问题，则 方法 <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> 将引发异常。 使用...是一种 **很好的做法。在** 方法周围 <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> 或调用方法内捕获 块。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet10":::

## <a name="compile-the-code"></a>编译代码

此代码示例要求满足以下条件：

- 若要按名称保存文档，名为 *NewDocument.doc* 的文档必须存在于驱动器 C 上名为 *Test* 的目录中。

- 若要保存具有新名称的文档，驱动器 C 上必须存在名为 *Test* 的目录。

## <a name="see-also"></a>请参阅

- [如何：以编程方式关闭文档](../vsto/how-to-programmatically-close-documents.md)
- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)
- [文档宿主项](../vsto/document-host-item.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
