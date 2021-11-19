---
title: 向 SharePoint 项目项扩展添加快捷菜单项
titleSuffix: ''
description: 使用 Visual Studio 中的项目项扩展将快捷菜单项添加到现有 SharePoint 项目项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c50f6b763aa8a56aa1049c1d0394f9878a39fe83
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600620"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>如何：将快捷菜单项添加到 SharePoint 项目项扩展
  可以使用项目项扩展将快捷菜单项添加到现有 SharePoint 项目项。 当用户在 **解决方案资源管理器** 中右键单击项目项时，将显示菜单项。

 以下步骤假设已创建项目项扩展。 有关详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>在项目项扩展中添加快捷菜单项

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 实现的方法中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> ，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> *projectItemType* 参数的事件。

2. 在事件的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> ，向 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> 事件参数参数的或集合添加一个新的对象。

3. 在 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> 新对象的事件处理程序中 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> ，执行用户单击快捷菜单项时要执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何向事件接收器项目项添加快捷菜单项。 当用户在 **解决方案资源管理器** 中右键单击项目项并单击 "将 **消息写入输出窗口**" 菜单项时，Visual Studio 将在 "**输出**" 窗口中显示一条消息。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs" id="Snippet1":::

 此示例使用 SharePoint 项目服务将消息写入到 "**输出**" 窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，其中包含对以下程序集的引用：

- VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展 (VSIX) 包，并为您要使用该扩展分发的任何其他文件创建该扩展。 有关详细信息，请参阅[Visual Studio 中的 SharePoint 工具的部署扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：将属性添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
