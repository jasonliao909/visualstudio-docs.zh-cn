---
title: 如何：添加自定义属性|Microsoft Docs
description: 了解如何使用 Visual Studio 的 BDC 资源管理器中的属性编辑器，将自定义属性添加到 SharePoint 中的业务数据连接 (BDC) 模型。
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
ms.openlocfilehash: d72343bff4367e813bc8e75c1afffc2be5af9742
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122060123"
---
# <a name="how-to-add-a-custom-property"></a>如何：添加自定义属性
  可以使用属性编辑器 将自定义属性 **添加到模型**。 可以在代码中访问这些属性，以检索信息，例如连接字符串和其他数据。

### <a name="to-add-a-custom-property"></a>添加自定义属性

1. 在 **BDC 资源管理器** 中，选择表示要应用自定义属性的模型元素的节点。

2. 在菜单栏上，选择"查看  >  **属性窗口"。**

3. 在"**属性"** 窗口中，选择"自定义属性"属性，然后选择"移动设计器"省略号 (ASP.NET 省略 ![号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) 。

     将显示 **"属性** 编辑器"对话框。

4. 在"名称" **列的** 文本框中，指定属性的名称。

5. 对于 **自定义** 属性的"类型"字段，选择适当的数据类型。

6. 对于 **自定义属性** 的"值"字段，指定一个值，然后选择"确定 **"** 按钮。

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
