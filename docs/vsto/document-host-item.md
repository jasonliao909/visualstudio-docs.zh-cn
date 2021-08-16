---
title: 文档宿主项
description: 了解"文档宿主"项是一种从 Word 的主互操作程序集扩展文档类型的类型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio]
- documents [Office development in Visual Studio], document host items
- document host items
- Word [Office development in Visual Studio], Word documents
- Word [Office development in Visual Studio]
- Word documents
- host items [Office development in Visual Studio], Document
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4bfb1ce70bddec5a92c48dde6f67256f1a9b63e2391701a6e33ebeb1b5591276
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121268386"
---
# <a name="document-host-item"></a>文档宿主项
  <xref:Microsoft.Office.Tools.Word.Document> 宿主项这种类型从 Word 的主互操作程序集扩展类型 <xref:Microsoft.Office.Interop.Word.Document> 。 <xref:Microsoft.Office.Tools.Word.Document> 宿主项提供与 <xref:Microsoft.Office.Interop.Word.Document> 对象完全相同的属性、方法和事件，但它还公开其他事件并充当宿主控件和 Windows 窗体控件的容器。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 在文档级项目中，有代表你的项目中的文档的默认 <xref:Microsoft.Office.Tools.Word.Document> 宿主项。 在 VSTO 外接程序项目中，可以在运行时生成 <xref:Microsoft.Office.Tools.Word.Document> 主机项。

## <a name="understand-the-document-host-item-in-document-level-projects"></a>了解文档级项目中的文档宿主项
 若要访问你的项目中的文档，请使用 `ThisDocument` 类。 当你创建文档级项目时，Visual Studio 将生成 `ThisDocument` 类来充当 Word 和自定义代码之间的通信链接。 利用 `ThisDocument` 类，你可以访问 <xref:Microsoft.Office.Tools.Word.Document> 宿主项的成员，以在自定义项中执行基本任务，例如当文档打开或关闭时运行代码。 也可以使用该类将控件添加到文档。 通过组合不同的控件集并编写代码，可将控件绑定到数据、从用户处收集信息并响应用户操作。 有关详细信息，请参阅 [Program document-level customizations](../vsto/programming-document-level-customizations.md)。

 `ThisDocument` 类提供了一个位置，你可以在该位置开始编写项目中的代码。 因为该类提供与 Word 主互操作程序集中的 <xref:Microsoft.Office.Interop.Word.Document> 对象完全相同的属性、方法和事件，所以也可以使用 `ThisDocument` 访问 Word 的对象模型。 有关详细信息，请参阅 [Word 对象模型概述](../vsto/word-object-model-overview.md)。

### <a name="limitations-of-the-document-host-item-in-document-level-projects"></a>文档级项目中文档宿主项的限制
 文档级项目只能包含一个 <xref:Microsoft.Office.Tools.Word.Document> 宿主项（即 `ThisDocument` 类）。 不能在设计时将新的 <xref:Microsoft.Office.Tools.Word.Document> 宿主项添加到项目，也不能在运行时从文档级自定义项创建新的 <xref:Microsoft.Office.Tools.Word.Document> 宿主项。

 如果在运行时创建新的 Word 文档，则该文档为类型 <xref:Microsoft.Office.Interop.Word.Document>。 因为它不是宿主项，所以它不能包含任何宿主控件或 Windows 窗体控件。 有关运行时创建文档的信息，请参阅 [如何：以编程方式创建新文档](../vsto/how-to-programmatically-create-new-documents.md)。

## <a name="understand-document-host-items-in-application-level-projects"></a>了解应用程序级项目中的文档宿主项
 在 VSTO 外接程序项目中，可以在运行时为 Word 中打开的任何文档生成 <xref:Microsoft.Office.Tools.Word.Document> 宿主项。 可以使用 <xref:Microsoft.Office.Tools.Word.Document> 宿主项将控件添加到关联的文档中，或处理 <xref:Microsoft.Office.Interop.Word.Document> 对象中不可用的事件。

 若要生成 <xref:Microsoft.Office.Tools.Word.Document> 宿主项，请使用 `GetVstoObject` 方法。 有关详细信息，请参阅扩展[Word 文档和Excel运行时VSTO外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="see-also"></a>另请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [在外接程序Excel扩展 Word 文档VSTO工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
