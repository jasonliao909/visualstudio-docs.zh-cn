---
title: 如何：添加 Project 输出引用 |Microsoft Docs
description: 了解如何添加项目输出引用，以便可以将不 SharePoint 的项目程序集部署 (或 Silverlight 项目中的 .xap 文件) 到 SharePoint。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600624"
---
# <a name="how-to-add-a-project-output-reference"></a>如何：添加项目输出引用
  若要将不 SharePoint 的项目程序集部署 (或 Silverlight 项目中的 .xap 文件) 到 SharePoint，请将它们添加为项目输出引用。

 此过程将在两个项目之间创建一个解决方案生成依赖项。 与项目输出引用关联的项目在生成和部署 SharePoint 项目之前生成。

### <a name="to-add-a-project-output-reference"></a>添加项目输出引用

1. 加载包含至少一个 SharePoint 项目和一个非 SharePoint 项目的解决方案。

2. 在 **解决方案资源管理器** 中，选择 "SharePoint 项目" 节点中的项。

3. 在 "**属性**" 窗口中，选择 " **Project 输出引用**" 属性，然后选择它旁边的省略号 (![ASP.NET 移动设计器](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")"省略号) " 按钮。

4. 在 " **Project 输出引用**" 对话框中，选择 "**添加**" 按钮。

5. 在 "属性" 窗格中，选择 "**部署类型**" 属性旁边的箭头，然后为所引用的非 SharePoint 项选择适当的值，例如 **ElementFile**。

6. 选择 " **Project 名称**" 旁边的箭头，选择非 SharePoint 项目项的名称，然后选择 "**确定"** 按钮。

## <a name="see-also"></a>另请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
