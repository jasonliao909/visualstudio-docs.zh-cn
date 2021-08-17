---
title: 如何：添加快捷菜单项以SharePoint项目|Microsoft Docs
titleSuffix: ''
description: 将快捷菜单项添加到 SharePoint 项目Visual Studio。 右键单击项目中的项目节点时，将显示解决方案资源管理器。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122027027"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>如何：添加快捷菜单项以SharePoint项目
  可以将快捷菜单项添加到任何项目SharePoint项目。 当用户右键单击中的项目节点时，将显示 **解决方案资源管理器。**

 以下步骤假定已创建项目扩展。 有关详细信息，请参阅[如何：创建SharePoint扩展。](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>向项目添加快捷SharePoint项

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 实现的方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> *projectService 参数* 的 事件。

2. 在 事件的事件处理程序中，向 事件参数参数的 或 集合 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A> 添加新对象。

3. 在新 对象的事件处理程序中，执行用户单击快捷菜单项 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 时要执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将快捷菜单项添加到 SharePoint 中的项目 **解决方案资源管理器。** 当用户右键单击项目节点并单击"写入消息"输出窗口 **菜单项时**，Visual Studio"输出"窗口中 **显示** 一条消息。 此示例使用 SharePoint 项目服务 来显示消息。 有关详细信息，请参阅使用[SharePoint 项目服务。](../sharepoint/using-the-sharepoint-project-service.md)

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs" id="Snippet1":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，该项目引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [扩展SharePoint项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建SharePoint扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：向项目SharePoint属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
