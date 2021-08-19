---
title: 在解决方案概述Office本地数据库文件
description: 了解如何在 Office 解决方案中包括数据库文件，例如 SQL Server Express (.mdf) 文件或 Microsoft Office Access (.mdb) 文件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- data [Office development in Visual Studio], local
- local data [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f2e7dc3346ccb2104e5350968d2f983b1c2e1c69
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099420"
---
# <a name="use-local-database-files-in-office-solutions-overview"></a>在解决方案概述Office本地数据库文件
  可以在 Office 解决方案中包括数据库文件，例如 SQL Server Express (*.mdf*) 文件或 Microsoft Office Access (*.mdb*) 文件。 这样，最终用户能够在不需要维护集中式数据库的情况下（例如，在仅在一台计算机中使用的本地清单解决方案中）维护本地数据库。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="import-the-database-file-into-a-project"></a>将数据库文件导入项目
 若要将数据库文件导入项目，请使用数据源配置 **向导** 基于数据库文件创建数据源。 向导会将数据库文件和类型数据集添加到项目。

## <a name="deploy-the-database-file"></a>部署数据库文件
 数据源 **配置向导** 使用相对路径创建与本地数据库文件的连接。 这样，在保持文件的相对位置时，你可以将解决方案从一台计算机复制到另一台计算机。

 如果将解决方案部署到服务器，然后将文档分发给每个最终用户，则还必须手动分发数据库文件，并将其安装在与文档相同的位置。 这意味着最终用户无法将文档移动到其计算机上的新位置，除非他/她也移动了数据库文件。

## <a name="local-database-files-and-caching-the-dataset"></a>本地数据库文件和缓存数据集
 在 Word 和 Microsoft Office Excel Microsoft Office 文档级解决方案中，可以通过将数据集实例标记为 属性来缓存文档中的数据集 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 。 使用数据源配置向导将数据库文件添加到项目时，会自动将类型数据集添加到项目中。 很少需要应用于此 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 数据集，因为数据已在用户计算机上本地。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

## <a name="see-also"></a>请参阅
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：使用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用来自主机控件的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
- [缓存数据](../vsto/caching-data.md)
