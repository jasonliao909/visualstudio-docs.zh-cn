---
title: 如何：以编程方式保存文档
description: 了解如何使用 Visual Studio 以编程方式保存文档，而无需更改文档名称或使用新名称。
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
ms.openlocfilehash: 7571ca0d16bdd1fc8ebb9f8552d6b55618ffa746dc505bf8bdc81ee2e9452306
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121351702"
---
# <a name="how-to-programmatically-save-documents"></a>如何：以编程方式保存文档

有多种方法可保存 Microsoft Office Word 文档。 你可以在不更改文档名称的情况下保存文档，也可以使用新名称保存文档。

[!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="save-a-document-without-changing-the-name"></a>保存文档但不更改名称

### <a name="to-save-the-document-associated-with-a-document-level-customization"></a>保存与文档级自定义项关联的文档

1. 调用 <xref:Microsoft.Office.Tools.Word.Document.Save%2A> 类的 <xref:Microsoft.Office.Tools.Word.Document> 方法。 若要使用此代码示例，请从项目中的 `ThisDocument` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet7":::

### <a name="to-save-the-active-document"></a>保存活动文档

1. 调用 <xref:Microsoft.Office.Interop.Word._Document.Save%2A> 活动文档的方法。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet8":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet8":::

   如果不确定要保存的文档是否为活动文档，可以通过名称来引用它。

### <a name="to-save-a-document-specified-by-name"></a>保存按名称指定的文档的方法

1. 将文档名称用作集合的参数 <xref:Microsoft.Office.Interop.Word.Documents> 。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet9":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet9":::

## <a name="save-a-document-with-a-new-name"></a>使用新名称保存文档

使用 `SaveAs` 方法可使用新名称保存文档。 你可以在 <xref:Microsoft.Office.Tools.Word.Document> 文档级 word 项目中使用宿主项的此方法，或者 <xref:Microsoft.Office.Interop.Word.Document> 在任意 Word 项目中使用本机对象的此方法。 此方法要求指定新文件名，但其他参数是可选的。

> [!NOTE]
> 如果在的事件处理程序中显示 " **另存** 为" 对话框， <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> `ThisDocument` 并将 *Cancel* 参数设置为 **false**，则应用程序可能会意外退出。 如果将 " *取消* " 参数设置为 " **true**"，则会出现一条错误消息，指示已禁用自动保存。

### <a name="to-save-the-document-associated-with-a-document-level-customization-with-a-new-name"></a>使用新名称保存与文档级自定义项关联的文档

1. `SaveAs` `ThisDocument` 使用完全限定的路径和文件名调用项目中类的方法。 如果该文件夹中已存在具有该名称的文件，则以无提示方式覆盖它。 若要使用此代码示例，请从 `ThisDocument` 类中运行它。

    > [!NOTE]
    > `SaveAs`如果目标目录不存在，或者保存文件时存在其他问题，则该方法将引发异常。 最好在 `try...catch` `SaveAs` 方法或调用方法内部使用块。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet10":::

### <a name="to-save-a-native-document-with-a-new-name"></a>使用新名称保存本机文档

1. <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> <xref:Microsoft.Office.Interop.Word.Document> 使用完全限定的路径和文件名调用要保存的的方法。 如果该文件夹中已存在具有该名称的文件，则以无提示方式覆盖它。

     下面的代码示例使用新名称保存活动文档。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

    > [!NOTE]
    > <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A>如果目标目录不存在，或者保存文件时存在其他问题，则该方法将引发异常。 最佳做法是使用 **try .。。** 围绕 <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> 方法或调用方法内部的 catch 块。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet10":::

## <a name="compile-the-code"></a>编译代码

此代码示例要求满足以下条件：

- 若要按名称保存文档，名为 *NewDocument.doc* 的文档必须存在于驱动器 C 上名为 *Test* 的目录中。

- 若要保存具有新名称的文档，驱动器 C 上必须存在一个名为 " *Test* " 的目录。

## <a name="see-also"></a>请参阅

- [如何：以编程方式关闭文档](../vsto/how-to-programmatically-close-documents.md)
- [如何：以编程方式打开现有文档](../vsto/how-to-programmatically-open-existing-documents.md)
- [文档宿主项](../vsto/document-host-item.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
