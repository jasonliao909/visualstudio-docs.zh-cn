---
title: 定义自定义 SharePoint 项目项类型 | Microsoft Docs
description: 若要创建新类型的 SharePoint 项目项，请定义自定义 SharePoint 项目项类型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 01360612f19c40d574ea176246e68a1fd0f18ad8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671938"
---
# <a name="define-custom-sharepoint-project-item-types"></a>定义自定义 SharePoint 项目项类型
  若要创建新类型的 SharePoint 项目项，请定义新的 SharePoint 项目项类型。 例如，Visual Studio 不包含用于将字段或自定义操作添加到 SharePoint 站点的 SharePoint 项目项。 但是，也可以定义你自己的 SharePoint 项目项，用于创建字段、自定义操作或其他类型的 SharePoint 组件。

## <a name="tasks-for-defining-sharepoint-project-item-types"></a>用于定义 SharePoint 项目项类型的任务
 若定义自定义项目项类型，请生成一个实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的 Visual Studio 扩展程序集。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

 定义自定义项目项类型时，还可以将以下功能添加到项目项：

- 将快捷菜单项添加到项目项。 当你在“解决方案资源管理器”中打开项目项的快捷菜单时，通过右键单击项目项或选择该项目项，然后选择 Shift+F10 键，即可显示该菜单项。 有关详细信息，请参阅[如何：将快捷菜单项添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)。

- 将自定义属性添加到项目项。 当你在“解决方案资源管理器”中选择项目项时，属性将显示在“属性”窗口中。 有关详细信息，请参阅[如何：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  若要使其他开发人员能够在 Visual Studio 中使用项目项，请创建 .spdata 文件，并创建与项目项关联的项模板或项目模板。 有关详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>了解项目扩展项类型与项目项实例之间的关系
 定义 SharePoint 项目项类型时，Visual Studio 在将关联类型的项目项添加到 SharePoint 项目时加载扩展。 例如，如果定义新的“自定义操作”项目项类型，Visual Studio 会在用户将“自定义操作”项目项添加到项目时加载扩展。  对于关联项目项类型的所有实例，Visual Studio 都使用相同的扩展实例。 在上面的示例中，如果用户将第二个“自定义操作”项目项添加到项目中，那么扩展的同一实例将用于自定义第二个项目项。

 若要访问项目项类型的特定实例，请在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 方法的实现中处理 projectService 参数的一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 事件。 例如，若要确定何时将自定义类型的项目项添加到项目，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 事件。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="see-also"></a>另请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板创建站点列项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项模板创建自定义操作项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板创建站点列项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
