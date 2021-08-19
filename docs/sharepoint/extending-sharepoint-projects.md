---
title: 扩展 SharePoint 项目 |Microsoft Docs
description: 了解如何在要自定义 SharePoint 项目的项目级别功能时创建项目扩展。
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
ms.openlocfilehash: 79cd81292f6551a922744dc03ac9a83da8990e05
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122149463"
---
# <a name="extend-sharepoint-projects"></a>扩展 SharePoint 项目
  如果要自定义 SharePoint 项目的项目级功能，请创建项目扩展。 例如，你可以添加自定义项目属性，或响应用户在 Visual Studio 中开发 SharePoint 解决方案时引发的项目级事件。

## <a name="create-project-extensions"></a>创建项目扩展
 若要扩展项目项，请生成一个实现接口的 Visual Studio 扩展程序集 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

 创建项目扩展时，还可以将以下功能添加到 SharePoint 项目中：

- 添加快捷菜单项。 当您在 **解决方案资源管理器** 中打开 SharePoint 项目节点的快捷菜单时，将显示该菜单项，方法是右键单击该节点，或选择该节点，然后选择 **Shift** + **F10** 键。 有关详细信息，请参阅[如何：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)。

- 添加自定义属性。 当您在 **解决方案资源管理器** 中选择 SharePoint 项目时，属性将显示在 "**属性**" 窗口中。 有关详细信息，请参阅[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

  有关演示如何创建、部署和测试项目扩展的演练，请参阅[演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)。

## <a name="understand-the-relationship-between-project-extensions-and-project-instances"></a>了解项目扩展与项目实例之间的关系
 当你创建项目扩展时，将在中打开任何类型 SharePoint 项目时加载该扩展 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]包含若干 SharePoint 项目模板，如列表定义、内容类型和事件接收器。 但只有一个 SharePoint 项目类型。 出现在 "**新建 Project** " 对话框中的项目类型只是将一个或多个 SharePoint 项目项捆绑在一起的模板。 由于只有一个 SharePoint 项目类型，因此为一个项目创建的扩展将应用于所有 SharePoint 项目。 例如，你不能创建仅适用于 **内容类型** 项目的扩展。

 若要访问特定项目实例，请 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents> 在方法的实现中处理 *projectService* 参数的一个事件 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 。 例如，若要确定何时将 SharePoint 项目添加到解决方案中，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> 事件。 有关详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：将快捷菜单项添加到 SharePoint 项目中](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [如何：将属性添加到 SharePoint 项目中](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
