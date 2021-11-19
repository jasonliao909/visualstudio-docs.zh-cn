---
title: 将快捷菜单项添加到自定义 SharePoint 项目项类型
titleSuffix: ''
description: 了解如何将快捷菜单项添加到自定义 SharePoint 项目项类型。 当你在“解决方案资源管理器”中右键单击项目项时，将显示菜单项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: b966f3a721a9f4330325712c3268f3fe593eb149
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600619"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>如何：将快捷菜单项添加到自定义 SharePoint 项目项类型
  定义自定义 SharePoint 项目项类型时，可以将快捷菜单项添加到项目项。 当用户在“解决方案资源管理器”中右键单击项目项时，将显示菜单项。

 以下步骤假定你已定义了自己的 SharePoint 项目项类型。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>将快捷菜单项添加到自定义项目项类型

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 实现的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 方法中，处理 projectItemTypeDefinition 参数的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> 事件。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> 事件的事件处理程序中，将新的 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 对象添加到事件自变量参数的 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> 或 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> 集合中。

3. 在新 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 对象的 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> 事件处理程序中，执行希望在用户选择快捷菜单项时执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将上下文菜单项添加到自定义项目项类型。 当用户从“解决方案资源管理器”中的项目项打开快捷菜单并选择“将消息写入输出窗口”菜单项时，Visual Studio 会在“输出”窗口中显示一条消息  。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs" id="Snippet4":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb" id="Snippet4":::

 此示例使用 SharePoint 项目服务将消息写入“输出”窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，其中包含对以下程序集的引用：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员能使用你的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为程序集、模板以及要随项目项分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
