---
title: 向自定义 SharePoint 项目项类型添加快捷菜单项
titleSuffix: ''
description: 了解如何向自定义的 SharePoint 项目项类型添加快捷菜单项。 右键单击解决方案资源管理器中的项目项时，将显示菜单项。
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
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>如何：向自定义 SharePoint 项目项类型添加快捷菜单项
  定义自定义 SharePoint 项目项类型时，可以将快捷菜单项添加到项目项。 当用户在 **解决方案资源管理器** 中右键单击项目项时，将显示菜单项。

 以下步骤假定您已定义了自己的 SharePoint 项目项类型。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>向自定义项目项类型添加快捷菜单项

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 实现的方法中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> ，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> *projectItemTypeDefinition* 参数的事件。

2. 在事件的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> ，向 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> 事件参数参数的或集合添加一个新的对象。

3. 在 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> 新对象的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> ，执行用户选择快捷菜单项时要执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将上下文菜单项添加到自定义项目项类型。 当用户在 **解决方案资源管理器** 中打开项目项的快捷菜单并选择 "将 **消息写入输出窗口**" 菜单项时，Visual Studio 将在 "**输出**" 窗口中显示一条消息。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs" id="Snippet4":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb" id="Snippet4":::

 此示例使用 SharePoint 项目服务将消息写入到 "**输出**" 窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，其中包含对以下程序集的引用：

- VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员可以使用您的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅为[SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 程序集、模板和要与项目项分发的任何其他文件创建一个扩展 (VSIX) 包。 有关详细信息，请参阅[Visual Studio 中的 SharePoint 工具的部署扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：向自定义 SharePoint 项目项类型添加属性](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
