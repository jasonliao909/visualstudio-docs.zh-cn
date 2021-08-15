---
title: 扩展SharePoint项目|Microsoft Docs
description: 了解如何在要自定义项目的项目级功能时创建SharePoint扩展。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c86d67b76169381c6b14d45e30fc6262dccf6d65cbf5897555397b7619bb5de0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425400"
---
# <a name="extend-sharepoint-projects"></a>扩展SharePoint项目
  若要自定义项目的项目级功能，请创建SharePoint扩展。 例如，可以添加自定义项目属性，或响应当用户在 Visual Studio 中开发解决方案时SharePoint级事件。

## <a name="create-project-extensions"></a>创建项目扩展
 若要扩展项目项，请Visual Studio接口的扩展 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 程序集。 有关详细信息，请参阅[如何：创建SharePoint扩展。](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

 创建项目扩展时，还可以将以下功能添加到SharePoint项目：

- 添加快捷菜单项。 通过右键单击该节点或选择该节点，然后选择 Shift   + **F10** 键，SharePoint打开 解决方案资源管理器 项目节点的快捷菜单时，将显示菜单项。 有关详细信息，请参阅[如何：向项目添加SharePoint菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)。

- 添加自定义属性。 在 中选择项目 **时**，属性 **SharePoint"解决方案资源管理器。** 有关详细信息，请参阅[如何：向项目SharePoint属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

  有关演示如何创建、部署和测试项目扩展的演练，请参阅[演练：](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)创建SharePoint扩展。

## <a name="understand-the-relationship-between-project-extensions-and-project-instances"></a>了解项目扩展插件与项目实例之间的关系
 创建项目扩展时，当 在 中打开任何类型的项目SharePoint将加载该扩展 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]包括多个SharePoint模板，例如列表定义、内容类型和事件接收器。 但是，只有一SharePoint项目类型。 "新建项目"对话框中显示的项目Project只是将一个或多个项目项捆绑在一起的SharePoint模板。 由于只有一个SharePoint类型，因此为一个项目创建的扩展将应用于所有SharePoint项目。 例如，不能创建仅应用于内容类型 **项目的扩展** 。

 若要访问特定项目实例，请处理 方法实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> *中的 projectService* 参数的其中一 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 个事件。 例如，若要确定何时将SharePoint添加到解决方案，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> 事件。 有关详细信息，请参阅[如何：创建SharePoint扩展。](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

## <a name="see-also"></a>另请参阅
- [如何：创建SharePoint扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：向项目添加SharePoint菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [如何：向项目SharePoint属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [演练：创建SharePoint扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [扩展SharePoint项](../sharepoint/extending-sharepoint-project-items.md)
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
