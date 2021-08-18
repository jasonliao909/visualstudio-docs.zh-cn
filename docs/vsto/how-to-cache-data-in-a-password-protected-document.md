---
title: 如何：在受密码保护的文档中缓存数据
description: 了解，如果您将数据添加到用密码保护的文档或工作簿中的数据缓存，则可以通过重写项目中的两个方法来保存对缓存数据所做的更改。
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
  如果将数据添加到受密码保护的文档或工作簿中的数据缓存，则不会自动保存对缓存数据所做的更改。 可以通过重写项目中的两个方法来保存对缓存数据所做的更改。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="caching-in-word-documents"></a>Word 文档中的 Caching

### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>在受密码保护的 Word 文档中缓存数据

1. 在 `ThisDocument` 类中，将要缓存的公共字段或属性标记为。 有关详细信息，请参阅 [缓存数据](../vsto/caching-data.md)。

2. 重写 <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> 类中的方法 `ThisDocument` ，并从文档中移除保护。

     保存文档后，将 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 调用此方法以使您有机会取消对文档的保护。 这样，就可以保存对缓存数据所做的更改。

3. 重写 <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> 类中的方法 `ThisDocument` ，并对文档重新应用保护。

     保存文档后，将 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 调用此方法以使你有机会对文档重新应用保护。

### <a name="example"></a>示例
 下面的代码示例演示如何在受密码保护的 Word 文档中缓存数据。 在代码删除方法中的保护之前 <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> ，它会保存当前 <xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A> 值，以便可以在方法中重新应用相同类型的保护 <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> 。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb" id="Snippet1":::

### <a name="compile-the-code"></a>编译代码
 将此代码添加到 `ThisDocument` 项目中的类。 此代码假定密码存储在名为的字段中 `securelyStoredPassword` 。

## <a name="cache-in-excel-workbooks"></a>Excel 工作簿中的缓存
 在 Excel 项目中，仅当使用方法通过密码保护整个工作簿时，此过程才是必需的 <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> 。 如果使用方法仅通过密码保护特定工作表，则不需要执行此过程 <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> 。

### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>在使用密码保护的 Excel 工作簿中缓存数据

1. 在 `ThisWorkbook` 类或 `Sheet` *n* 类中，将要缓存的公共字段或属性标记为。 有关详细信息，请参阅 [缓存数据](../vsto/caching-data.md)。

2. 重写 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> 类中的方法 `ThisWorkbook` ，并从工作簿中移除保护。

     保存工作簿时，将 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 调用此方法以使你有机会取消对工作簿的保护。 这样，就可以保存对缓存数据所做的更改。

3. 重写 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> 类中的方法 `ThisWorkbook` ，并对文档重新应用保护。

     保存工作簿后，将 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 调用此方法以使你有机会对工作簿重新应用保护。

### <a name="example"></a>示例
 下面的代码示例演示如何在使用密码保护的 Excel 工作簿中缓存数据。 在代码删除方法中的保护之前 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> ，它将保存当前的 <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A> 和 <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A> 值，以便可以在方法中重新应用相同类型的保护 <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> 。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs" id="Snippet1":::

### <a name="compile-the-code"></a>编译代码
 将此代码添加到 `ThisWorkbook` 项目中的类。 此代码假定密码存储在名为的字段中 `securelyStoredPassword` 。

## <a name="see-also"></a>请参阅
- [缓存数据](../vsto/caching-data.md)
- [如何：缓存数据以便脱机使用或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：以编程方式在 Office 文档中缓存数据源](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
