---
title: 如何：添加自定义属性 |Microsoft Docs
description: 了解如何使用 Visual Studio BDC 资源管理器中的 "属性编辑器"，在 SharePoint 中将自定义属性添加到业务数据连接 (bdc) 模型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.Property_Editor
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], custom properties
- BDC [SharePoint development in Visual Studio], custom properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 35dd7210258d48a446704d02aae09303ed274a1bdc3d5c1fb764692721821c2e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121228787"
---
# <a name="how-to-add-a-custom-property"></a>如何：添加自定义属性
  您可以使用 **属性编辑器** 向模型中添加自定义属性。 您可以在代码中访问这些属性，以便在运行时检索连接字符串和其他数据等信息。

### <a name="to-add-a-custom-property"></a>添加自定义属性

1. 在 " **BDC 资源管理器**" 中，选择表示要对其应用自定义属性的模型元素的节点。

2. 在菜单栏上，选择 "**查看**  >  **属性窗口**"。

3. 在 "**属性**" 窗口中，选择 "**自定义属性**" 属性，然后选择省略号按钮 (![ASP.NET 移动设计器](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")"") "。

     此时将显示 " **属性编辑器** " 对话框。

4. 在 " **名称** " 列的文本框中，指定属性的名称。

5. 对于自定义属性的 " **类型** " 字段，请选择适当的数据类型。

6. 对于自定义属性的 **值** 字段，请指定一个值，然后选择 **"确定"** 按钮。

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
