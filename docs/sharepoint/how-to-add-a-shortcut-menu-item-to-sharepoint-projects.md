---
title: 如何：将快捷菜单项添加到 SharePoint 项目 | Microsoft Docs
titleSuffix: ''
description: 在 Visual Studio 中将快捷菜单项添加到 SharePoint 项目。 右键单击解决方案资源管理器中的项目节点时，将显示菜单项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: df2baff33b1eaa56a8d595fb95a6f46cf7d811a8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665023"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>如何：将快捷菜单项添加到 SharePoint 项目
  可以将快捷菜单项添加到 SharePoint 项目。 当用户在解决方案资源管理器中右键单击项目节点时，将显示菜单项。

 以下步骤假设已创建项目扩展。 有关更多信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>将快捷菜单项添加到 SharePoint 项目的步骤

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 实现的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 方法中，处理 projectService 参数的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> 事件。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> 事件的事件处理程序中，将新的 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 对象添加到事件参数的 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A> 或 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A> 集合中。

3. 在新 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 对象的 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> 事件处理程序中，执行希望在用户单击快捷菜单项时执行的任务。

## <a name="example"></a>示例
 以下代码示例演示了如何将快捷菜单项添加到解决方案资源管理器中的 SharePoint 项目节点。 当用户右键单击项目节点并单击“将消息写入输出窗口”菜单项时，Visual Studio 会在“输出”窗口中显示一条消息 。 此示例使用 SharePoint 项目服务来显示消息。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs" id="Snippet1":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，其中包含对以下程序集的引用：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
