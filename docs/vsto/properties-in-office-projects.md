---
title: Office 项目中的属性
description: 了解可 Office 用于 Visual Studio 通过属性窗口的项目的属性。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Trust Assemblies Location property
- Cache in Document property
- properties [Office development in Visual Studio]
- Namespace for Host Item property
- Office projects [Office development in Visual Studio], properties
- projects [Office development in Visual Studio], properties
- Value2 property
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: b26826769c86bc23064f9475df595a10abd47050
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155585"
---
# <a name="properties-in-office-projects"></a>Office 项目中的属性
  有几个重要属性可用于 Visual Studio 中的 Office 项目。 可在 **“属性”** 窗口中访问这些属性。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="namespace-for-host-item"></a>主机项的命名空间
 使用 " **主机项的命名空间** " 属性可以更改主机项类的命名空间 (例如， `ThisAddIn` `ThisWorkbook` `ThisDocument` 在 Visual c # 项目中) 的、或类。 选择文档级项目中的文档节点时，此属性将出现在 "**属性**" 窗口中 (例如 *ExcelWorkbook1.xlsx* 或 *WordDocument1.docx*) 或 VSTO 外接程序项目中的应用程序节点 (例如 Excel 或 **)** 中的 Word 解决方案资源管理器。

 创建 Visual C# Office 项目时，将根据项目名称为主机项指定命名空间。 建议使用 **“主机项的命名空间”** 属性来更改命名空间，而不要直接编辑代码文件。 使用此属性时，将在生成的（隐藏）代码文件中和可见代码文件中更改命名空间。

## <a name="cacheindocument"></a>CacheInDocument
 在 Visual Studio 设计器中选择 **的实例时，文档级项目的** “属性” **窗口中将显示** “CacheInDocument” <xref:System.Data.DataSet> 属性。 仅可缓存公共成员；如果要缓存 **，请确保将** “修饰符” **属性设置为** “公共” <xref:System.Data.DataSet>。

 此属性采用布尔值：

- 选择 **true** 可将数据集缓存到文档中。

- 如果不希望将数据集缓存到文档中，请选择 **false** 。

  有关缓存数据的详细信息，请参阅 [文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)。

## <a name="value2"></a>Value2
 **“Value2”** 属性仅可用于 Excel 工作簿或模板项目。 在工作表设计器中选择 **控件时，该属性将显示在** “属性” **窗口中的** “数据绑定” <xref:Microsoft.Office.Tools.Excel.NamedRange> 属性节点之下。

 使用 **“属性”** 窗口中的 **“Value2”** 属性将 <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> 的 <xref:Microsoft.Office.Tools.Excel.NamedRange> 属性绑定到数据源中的字段。

## <a name="see-also"></a>请参阅
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
- [Office 项目中的事件](../vsto/events-in-office-projects.md)
