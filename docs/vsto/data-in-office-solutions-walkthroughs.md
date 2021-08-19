---
title: Office 解决方案演练中的数据
description: 了解如何使用文档级自定义项中的数据，并 VSTO Microsoft Word 和 Microsoft Excel 的外接程序。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], walkthroughs
- walkthroughs [Office development in Visual Studio], data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 1d8df3bae055c1d827562e9da8d0022ae9e7c2b2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122053735"
---
# <a name="data-in-office-solutions-walkthroughs"></a>Office 解决方案演练中的数据
  下列演练演示了如何将文档级自定义项和 VSTO 外接程序中的数据用于 Microsoft Office Word 和 Microsoft Office Excel。

## <a name="bind-controls-to-data"></a>将控件绑定到数据
- [演练：文档级项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)演示如何将 SQL Server 数据库中的单个数据字段绑定到 <xref:Microsoft.Office.Tools.Excel.NamedRange> Excel 文档级自定义项中的。

- [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)演示如何将 SQL Server 数据库中的表绑定到 <xref:Microsoft.Office.Tools.Excel.ListObject> Excel 文档级自定义项中的。

- [演练： VSTO 外接程序项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)演示如何将 SQL Server 数据库中的单个数据字段绑定到 Word 的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> VSTO 外接程序中的。

- [演练： VSTO 外接程序项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)演示如何将 SQL Server 数据库中的表绑定到 <xref:Microsoft.Office.Tools.Excel.ListObject> 用于 Excel 的 VSTO 外接程序中的。

- [演练：将数据绑定到 Excel 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)演示如何将绑定到数据源的控件添加到 Excel 中的操作窗格。

- [演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md) 演示如何将操作窗格上的控件绑定到数据。 控件演示 SQL Server 数据库中表之间的主/从关系。

- [演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md) 演示如何将 Word 文档中的内容控件绑定到文档中存储的 XML 数据。

## <a name="cache-data-in-document-level-solutions"></a>缓存文档级解决方案中的数据
- [演练：使用缓存的数据集创建主/从关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md) 演示如何在工作表上创建主/从关系以及缓存数据，以便可以脱机使用该解决方案。

- [演练：将数据插入到服务器上的工作簿](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)演示如何将数据插入到 Microsoft Office Excel 工作簿中缓存的数据集，而无需启动 Excel。

- [演练：从服务器上的工作簿中检索缓存的数据](../vsto/walkthrough-retrieving-cached-data-from-a-workbook-on-a-server.md)演示如何从 Microsoft Office Excel 工作簿中缓存的数据集检索数据而无需启动 Excel。

- [演练：更改服务器上的工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)演示如何修改 Microsoft Office Excel 工作簿中缓存的数据集，而无需启动 Excel。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
- [OfficeUI 自定义演练](../vsto/office-ui-customization-walkthroughs.md)
- [安全和部署演练](../vsto/security-and-deployment-walkthroughs.md)
- [Office 开发示例](../vsto/office-development-samples.md)
- [&#40;Visual Studio 中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
