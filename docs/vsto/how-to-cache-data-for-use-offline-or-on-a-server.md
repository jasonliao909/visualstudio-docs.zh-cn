---
title: 如何：缓存数据以脱机或在服务器上使用
description: 将数据项标记为缓存在文档中，以便其脱机可用。 这样，文档中的数据就有可能由其他代码操作。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], server use
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- offline data [Office development in Visual Studio]
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio], offline use
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2bc34986f6ea077e7bd822eeaa3ff0d254557b7f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122100122"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>如何：缓存数据以脱机或在服务器上使用
  可以将要缓存在文档中的数据项标记为脱机可用。 这样，当文档存储在服务器上时，其他代码也能够操作文档中的数据。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 在代码中声明数据项时，可以将要缓存的数据项标记为缓存;如果使用 ，则可以通过在"属性"窗口中设置 <xref:System.Data.DataSet> **属性来标记数据** 项。 如果缓存的数据项不是 或 ，请确保它满足文档中 <xref:System.Data.DataSet> <xref:System.Data.DataTable> 缓存的条件。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

> [!NOTE]
> 使用标记为"已缓存"和 **"WithEvents** ("的 Visual Basic 创建的数据集，包括从"数据源"窗口拖动的数据集或将 **CacheInDocument** 属性设置为 **True**) 的工具箱在缓存中以下划线作为名称前缀。  例如，如果创建数据集并命名 **"Customers"，** 则名称_Customers <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> 缓存中。  使用 访问 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 此缓存项时，必须指定 _Customers而不是 **Customers**。

### <a name="to-cache-data-in-the-document-using-code"></a>使用代码缓存文档中的数据

1. 将数据项的公共字段或属性声明为项目中宿主项类的成员，例如 Word 项目中的 t 类或项目Excel `ThisDocumen` `ThisWorkbook` 类。

2. 将 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性应用于成员，以标记要存储在文档的数据缓存中的数据项。 以下示例将此属性应用于 的字段声明 <xref:System.Data.DataSet> 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet11":::

3. 添加代码以创建数据项的实例，如果适用，则从数据库加载它。

     数据项仅在首次创建时加载;此后，缓存将保留在文档中，你必须编写其他代码来更新它。

### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>使用资源库在文档中缓存属性窗口

1. 使用数据集设计器中的工具将数据集添加到项目Visual Studio例如，通过使用"数据源"窗口将数据源 **添加到** 项目。

2. 创建数据集的实例（如果还没有实例）并选择设计器中的实例。

3. 在" **属性"** 窗口中，将 **CacheInDocument 属性** 设置为 **True**。

     有关详细信息，请参阅项目[中的Office属性](../vsto/properties-in-office-projects.md)。

4. 在"**属性"** 窗口中，将 **"修饰** 符"属性设置为"公共 (默认为 **"内部**) " 。

## <a name="see-also"></a>请参阅
- [缓存数据](../vsto/caching-data.md)
- [如何：以编程方式将数据源缓存在Office文档中](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/save-data-back-to-the-database.md)
