---
title: 如何：在受密码保护的文档中缓存数据
description: 了解如果在受密码保护的文档或工作簿中将数据添加到数据缓存中，则可以通过在项目中重写两种方法来保存对缓存数据所做的更改。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], protected documents
- datasets [Office development in Visual Studio], caching
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: db686d8b31f9a47fc68dc37f4844be60c46bf7a2812024c2385c147d6f604610
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440833"
---
# <a name="how-to-cache-data-in-a-password-protected-document"></a>如何：在受密码保护的文档中缓存数据
  如果将数据添加到受密码保护的文档或工作簿的数据缓存中，则不会自动保存对缓存数据所做的更改。 可以通过在项目中重写两种方法来保存对缓存数据所做的更改。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="caching-in-word-documents"></a>Caching Word 文档中显示

### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>在受密码保护的 Word 文档中缓存数据

1. 在 `ThisDocument` 类中，标记要缓存的公共字段或属性。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

2. 重写 <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> 类中的 `ThisDocument` 方法，并从文档中删除保护。

     保存文档时， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将调用此方法，让你有机会取消保护文档。 这样，可以保存对缓存数据所做的更改。

3. 重写 <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> 类中的 `ThisDocument` 方法，然后重新应用对文档的保护。

     保存文档后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将调用此方法，让你有机会重新应用对文档的保护。

### <a name="example"></a>示例
 下面的代码示例演示如何在受密码保护的 Word 文档中缓存数据。 在代码删除 方法中的保护之前，它会保存当前值，以便可以在 方法中重新 <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> <xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A> 应用相同类型的 <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> 保护。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb" id="Snippet1":::

### <a name="compile-the-code"></a>编译代码
 将此代码添加到 `ThisDocument` 项目中的 类。 此代码假定密码存储在名为 的字段中 `securelyStoredPassword` 。

## <a name="cache-in-excel-workbooks"></a>缓存在Excel工作簿中
 在Excel中，只有在使用 方法使用密码保护整个工作簿时，才需要 <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> 此过程。 如果仅使用 方法保护具有密码的特定工作表，则此过程 <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> 不是必需的。

### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>在受密码保护Excel工作簿中缓存数据

1. 在 `ThisWorkbook` 类或 n 个类 `Sheet` 之一中，标记要缓存的公共字段或属性。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

2. 重写 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> 类中的 `ThisWorkbook` 方法，并从工作簿中删除保护。

     保存工作簿后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将调用此方法，让你有机会取消保护工作簿。 这样，可以保存对缓存数据所做的更改。

3. 重写 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> 类中的 `ThisWorkbook` 方法，然后重新应用对文档的保护。

     保存工作簿后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将调用此方法，让你有机会重新应用对工作簿的保护。

### <a name="example"></a>示例
 下面的代码示例演示如何在受密码保护的 Excel工作簿中缓存数据。 在代码删除 方法中的保护之前，它会保存当前 和 值，以便可以在 方法中重新应用相同 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A> <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A> 类型的 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> 保护。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs" id="Snippet1":::

### <a name="compile-the-code"></a>编译代码
 将此代码添加到 `ThisWorkbook` 项目中的 类。 此代码假定密码存储在名为 的字段中 `securelyStoredPassword` 。

## <a name="see-also"></a>另请参阅
- [缓存数据](../vsto/caching-data.md)
- [如何：缓存数据以脱机或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：以编程方式将数据源缓存在Office文档中](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
