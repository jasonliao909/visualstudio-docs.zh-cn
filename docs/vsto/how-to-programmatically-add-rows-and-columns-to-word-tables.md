---
title: 如何：以编程方式向 Word 表中添加行和列
description: 了解如何使用 Rows 对象的 Add 方法将行添加到表中。 你还可以使用 Columns 对象的 Add 方法来添加列。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio], adding to Word tables
- tables [Office development in Visual Studio], adding rows and columns
- columns [Office development in Visual Studio], adding to Word tables
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: cc4064677d35ada2a03baa1b4212a101bb6bd9a6df20f797596f9c31a961567e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424003"
---
# <a name="how-to-programmatically-add-rows-and-columns-to-word-tables"></a>如何：以编程方式向 Word 表中添加行和列
  在 Microsoft Office Word 表中，单元格组织为行和列。 你可以使用 <xref:Microsoft.Office.Interop.Word.Rows> 对象的 <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> 方法将行添加到表，并可以使用 <xref:Microsoft.Office.Interop.Word.Columns> 对象的 <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> 方法添加列。

 [!INCLUDE[appliesto_wdalldocapp](includes/appliesto-wdalldocapp-md.md)]

## <a name="document-level-customization-examples"></a>文档级自定义项示例
 可以在文档级自定义项中使用下列代码示例。 若要使用这些示例，请从项目中的 `ThisDocument` 类运行它们。 这些示例假定与你的自定义相关联的文档已具有至少一个表。

> [!IMPORTANT]
> 此代码仅在使用下列任意项目模板创建的项目中运行：
>
> - Word 2013 文档
> - Word 2013 模板
> - Word 2010 文档
> - Word 2010 模板
>
>   如果要在任何其他类型的项目中执行此任务，则必须添加对 Office 的引用 **。** 然后，必须使用程序集中的类来向表中添加行和列。 有关详细信息，请参阅[如何：通过主互操作程序集以 Office 应用程序为目标](how-to-target-office-applications-through-primary-interop-assemblies.md)，以及[Word 2010 主互操作程序集引用](office-primary-interop-assemblies.md)。

### <a name="to-add-a-row-to-a-table"></a>向表中添加行

1. 使用 <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> 方法向表中添加一行。

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet95":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet95":::

### <a name="to-add-a-column-to-a-table"></a>向表中添加列

1. 使用 <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> 方法，然后使用 <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> 方法使所有列具有相同的宽度。

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet96":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet96":::

## <a name="vsto-add-in-examples"></a>VSTO外接程序示例
 可以在 VSTO 外接程序中使用下列代码示例。 若要使用这些示例，请从项目中的 `ThisAddIn` 类运行它们。 这些示例假定活动文档已经具有至少一个表。

> [!IMPORTANT]
> 此代码仅在你使用 Word VSTO 外接程序模板创建的项目中运行。
>
> 如果要在任何其他类型的项目中执行此任务，则必须添加对 Office 的引用 **。** 然后，必须使用程序集中的类来向表中添加行和列。 有关详细信息，请参阅[如何：通过主互操作程序集以 Office 应用程序为目标](how-to-target-office-applications-through-primary-interop-assemblies.md)，以及[Word 2010 主互操作程序集引用](office-primary-interop-assemblies.md)。

### <a name="to-add-a-row-to-a-table"></a>向表中添加行

1. 使用 <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> 方法向表中添加一行。

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet95":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet95":::

### <a name="to-add-a-column-to-a-table"></a>向表中添加列

1. 使用 <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> 方法，然后使用 <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> 方法使所有列具有相同的宽度。

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet96":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet96":::

## <a name="see-also"></a>请参阅
- [如何：以编程方式创建 Word 表](how-to-programmatically-create-word-tables.md)
- [如何：以编程方式向 Word 表中的单元格添加文本和格式设置](how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [如何：以编程方式用文档属性填充 Word 表](how-to-programmatically-populate-word-tables-with-document-properties.md)
