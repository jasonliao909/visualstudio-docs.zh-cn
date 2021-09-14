---
title: 如何：添加Project输出引用|Microsoft Docs
description: 了解如何添加项目输出引用，以便可以在 Silverlight 项目中部署非 SharePoint 项目程序集 (或 .xap 文件) SharePoint。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: d3d7bea0d57e4351fc022b2f4c45ecc1b6423e4b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600624"
---
# <a name="how-to-add-a-project-output-reference"></a>如何：添加项目输出引用
  若要在 Silverlight SharePoint中部署 (或 .xap 文件的非) 项目SharePoint，请将它们添加为项目输出引用。

 此过程在两个项目之间创建解决方案生成依赖项。 与项目输出引用关联的项目是在生成SharePoint部署项目之前构建的。

### <a name="to-add-a-project-output-reference"></a>添加项目输出引用

1. 加载至少包含一个SharePoint和一个非SharePoint的解决方案。

2. 在 **解决方案资源管理器** 中，选择项目节点SharePoint项。

3. 在"**属性"****窗口中**，选择"Project引用"属性，然后选择"移动设计器"旁边的省略号 (ASP.NET ![](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")省略号) 按钮。

4. 在 **"Project引用**"对话框中，选择"添加 **"** 按钮。

5. 在属性窗格中，选择"部署类型"属性旁边的箭头，然后为所引用的非SharePoint项选择适当的值，例如 **ElementFile**。

6. 选择"名称Project旁边的箭头，选择非SharePoint项目项的名称，然后选择"确定 **"** 按钮。

## <a name="see-also"></a>另请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
