---
title: 使用 ServerDocument 类管理服务器上的文档
description: 了解如何使用 Visual Studio Tools for Office 运行时中的 ServerDocument 类来管理文档级自定义项的几个方面。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], managing on server
- Office documents [Office development in Visual Studio, managing on server
- ServerDocument class, managing documents on server
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d48de91ebe28ef50b5529800b2777b845a3833fa79cd51c888ef290d5249a338
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121243531"
---
# <a name="manage-documents-on-a-server-by-using-the-serverdocument-class"></a>使用 ServerDocument 类管理服务器上的文档
  可以使用 中的 类来管理文档级自定义项的几个方面，即使未Microsoft Office Word 和 `ServerDocument` [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] Microsoft Office Excel。 你可以执行下列任务：

- 访问和修改文档或工作簿的数据缓存中的数据。 有关详细信息，请参阅 [使用文档中的缓存数据](#CachedData)。

- 管理与文档关联的自定义程序集。 有关详细信息，请参阅 [管理文档自定义](#CustomizationInfo)。

  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="understand-the-serverdocument-class"></a>了解 ServerDocument 类
 `ServerDocument`类旨在用于未安装 Office 的计算机上。 因此，通常在未与 Office 集成的应用程序（如控制台项目或 Windows Forms 项目）中，而不是在 Office 项目中使用此类。 在 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 程序集中Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll类。

 `ServerDocument`类可用于对使用 创建的文档级自定义进行操作 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 。

 有关 Office Runtime 的 Visual Studio 2010 工具以及 Office 扩展.NET Framework，请参阅 Visual Studio Tools for Office[运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

> [!NOTE]
> 如果旧版应用程序使用系统 (版本 3.0 运行时) 中的 类，则必须在运行该应用程序的计算机上安装系统 (版本 `ServerDocument` `Visual Studio Tools for Office` `Visual Studio Tools for Office` 3.0 运行时) 。 `Visual Studio 2010 Tools for Office runtime`无法运行这些应用程序。

## <a name="work-with-cached-data-in-the-document"></a><a name="CachedData"></a> 使用文档中的缓存数据
 `ServerDocument`类提供可用于处理自定义文档中的数据缓存的成员。 有关缓存数据详细信息，请参阅缓存[数据和](../vsto/caching-data.md)[访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

 下表列出了可用于处理缓存数据的成员。

|任务|供使用的成员|
|----------|-------------------|
|确定文档是否具有数据缓存。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.IsCacheEnabled%2A> 方法。|
|访问文档中缓存的数据。<br /><br /> 有关详细信息，请参阅 [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 属性。|

## <a name="manage-the-document-customization"></a><a name="CustomizationInfo"></a> 管理文档自定义
 可以使用 类的成员 `ServerDocument` 来管理与文档关联的自定义程序集。 例如，可以通过编程方式从文档中删除自定义项，使文档不再是自定义的一部分。

 下表列出了可用于管理自定义程序集的成员。

|任务|供使用的成员|
|----------|-------------------|
|确定文档是否是文档级自定义项的一部分。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.GetCustomizationVersion%2A> 方法。|
|以编程方式将自定义项运行时附加到文档。<br /><br /> 有关详细信息，请参阅 [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)|方法 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> 之一。|
|以编程方式运行时从文档中删除自定义项。<br /><br /> 有关详细信息，请参阅 [如何：从文档 中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> 方法。|
|获取与文档关联的部署清单的 URL。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.DeploymentManifestUrl%2A> 属性。|

## <a name="see-also"></a>另请参阅
- [如何：将托管代码扩展附加到文档](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
- [如何：从文档中删除托管代码扩展](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Visual Studio Tools for Office运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [缓存数据](../vsto/caching-data.md)
