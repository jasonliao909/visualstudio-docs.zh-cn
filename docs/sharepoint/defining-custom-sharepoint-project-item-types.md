---
title: 定义自定义SharePoint Project项类型|Microsoft Docs
description: 若要创建SharePoint类型的项目项，请定义一个自定义SharePoint项目项类型。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122149242"
---
# <a name="define-custom-sharepoint-project-item-types"></a>定义自定义SharePoint项目项类型
  若要创建新的SharePoint项目项类型，请为项目项SharePoint类型。 例如，Visual Studio不包含用于SharePoint字段或自定义操作添加到自定义站点SharePoint项。 可以定义自己的项目SharePoint，以创建字段、自定义操作或其他类型的SharePoint组件。

## <a name="tasks-for-defining-sharepoint-project-item-types"></a>用于定义SharePoint项类型的任务
 若要定义自定义项目项类型，请Visual Studio接口的扩展 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 程序集。 有关详细信息，请参阅[如何：定义SharePoint项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

 定义自定义项目项类型时，还可以将以下功能添加到项目项：

- 向项目项添加快捷菜单项。 通过右键单击项目项或选择项目项 **，然后选择 Shift**  + **F10** 键，在 解决方案资源管理器 中打开项目项的快捷菜单时，将显示菜单项。 有关详细信息，请参阅[如何：将快捷](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)菜单项添加到自定义SharePoint项目项类型 。

- 向项目项添加自定义属性。 在 中选择项目 **项** 时，属性将显示在"属性 **"解决方案资源管理器。** 有关详细信息，请参阅如何：将属性添加到自定义SharePoint[项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  若要使其他开发人员能够使用项目中的项目Visual Studio，请创建一个 .spdata 文件，并创建与项目项关联的项模板或项目模板。 有关详细信息，请参阅[为项目项 创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

## <a name="understand-the-relationship-between-project-item-types-and-project-item-instances"></a>了解项目项类型和项目项实例之间的关系
 定义项目SharePoint类型时，Visual Studio将关联类型的项目项添加到项目时加载扩展SharePoint。 例如，如果定义新的自定义操作项目项类型，Visual Studio向项目添加自定义操作项目项时加载扩展。  Visual Studio对关联的项目项类型的所有实例使用相同的扩展实例。 在上一示例中，如果用户向项目添加第二个自定义操作项目项，则使用扩展的同一实例自定义第二个项目项。

 若要访问项目项类型的特定实例，请处理 方法实现中的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> *projectItemTypeDefinition* 参数的其中一 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 个事件。 例如，若要确定何时将自定义类型的项目项添加到项目中，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 事件。 有关详细信息，请参阅[如何：定义SharePoint项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="see-also"></a>请参阅
- [如何：定义SharePoint项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将属性添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [为项目项创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板创建自定义操作项目项，第 1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板创建站点列项目项，第 1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [演练：使用项模板创建自定义操作项目项，第 2 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [演练：使用项目模板创建站点列项目项，第 2 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
