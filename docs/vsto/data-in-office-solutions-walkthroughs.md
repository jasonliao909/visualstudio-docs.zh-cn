---
title: 解决方案Office数据演练
description: 了解如何使用文档级自定义项和数据VSTO外接程序Microsoft Word Microsoft Excel。
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
ms.openlocfilehash: 3028d532ce605b1c6cc275d879a5961ab546fe7893828e6b2ce75da23cb3f759
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424393"
---
# <a name="data-in-office-solutions-walkthroughs"></a>解决方案Office数据演练
  下列演练演示了如何将文档级自定义项和 VSTO 外接程序中的数据用于 Microsoft Office Word 和 Microsoft Office Excel。

## <a name="bind-controls-to-data"></a>将控件绑定到数据
- [演练：文档级项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)演示如何将 SQL Server 数据库中的单个数据字段绑定到文档级自定义项中的 <xref:Microsoft.Office.Tools.Excel.NamedRange> ，Excel。

- [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)演示如何将 SQL Server 数据库中的表绑定到文档级自定义项中的 <xref:Microsoft.Office.Tools.Excel.ListObject> ，Excel。

- [演练：在外接程序项目中VSTO数据绑定](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)演示如何将 SQL Server 数据库中的单个数据字段绑定到 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> VSTO For Word 外接程序中的 。

- [演练：外接程序项目中VSTO数据绑定](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)演示如何将 SQL Server 数据库中的表绑定到 VSTO <xref:Microsoft.Office.Tools.Excel.ListObject> 外接程序中的 Excel。

- [演练：将数据绑定到"操作"窗格中Excel控件](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)演示如何将绑定到数据源的控件添加到数据源中的操作Excel。

- [演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md) 演示如何将操作窗格上的控件绑定到数据。 控件演示 SQL Server 数据库中表之间的主/从关系。

- [演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md) 演示如何将 Word 文档中的内容控件绑定到存储在文档中的 XML 数据。

## <a name="cache-data-in-document-level-solutions"></a>在文档级解决方案中缓存数据
- [演练：使用缓存数据集创建主详细信息关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md) 演示如何在工作表上创建主/详细信息关系，并缓存数据，以便可以脱机使用解决方案。

- [演练：将数据插入到服务器的工作簿中](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)演示如何将数据插入数据集，该数据集缓存在 Microsoft Office Excel 工作簿中，而无需Excel。

- [演练：从服务器上工作簿中检索缓存的数据](../vsto/walkthrough-retrieving-cached-data-from-a-workbook-on-a-server.md)演示如何从缓存在数据工作簿中的数据集检索数据Microsoft Office Excel不启动Excel。

- [演练：更改服务器上工作簿中的缓存数据](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)演示如何修改缓存在数据工作簿中的数据集Microsoft Office Excel不启动Excel。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [使用 Excel](../vsto/walkthroughs-using-excel.md)
- [OfficeUI 自定义演练](../vsto/office-ui-customization-walkthroughs.md)
- [安全性和部署演练](../vsto/security-and-deployment-walkthroughs.md)
- [Office开发示例](../vsto/office-development-samples.md)
- [开始&#40;Office开发Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [编程中的Office任务](../vsto/common-tasks-in-office-programming.md)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
