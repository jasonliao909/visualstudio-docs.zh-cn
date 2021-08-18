---
title: 向项目项扩展SharePoint快捷菜单项
titleSuffix: ''
description: 通过使用项目中的项目项扩展SharePoint将快捷菜单项添加到现有项目Visual Studio。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122136087"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>如何：向项目项扩展SharePoint快捷菜单项
  可以使用项目项扩展将快捷菜单项SharePoint现有项目项。 当用户右键单击中的项目项时，将显示 **解决方案资源管理器。**

 以下步骤假定已创建项目项扩展名。 有关详细信息，请参阅[如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>在项目项扩展中添加快捷菜单项

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 实现的方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> *projectItemType* 参数的 事件。

2. 在 事件的事件处理程序中，向 事件参数参数的 或 集合 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> 添加新对象。

3. 在新 对象的事件处理程序中，执行用户单击快捷菜单项 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 时要执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何向事件接收器项目项添加快捷菜单项。 当用户右键单击项目中的项目 **项** 解决方案资源管理器单击"写入消息"输出窗口 **菜单项时**，Visual Studio"输出"**窗口中显示** 一条消息。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs" id="Snippet1":::

 此示例使用 SharePoint 项目服务将消息写入"输出 **"** 窗口。 有关详细信息，请参阅使用[SharePoint 项目服务。](../sharepoint/using-the-sharepoint-project-service.md)

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，该项目引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：向项目项扩展SharePoint属性](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [扩展SharePoint项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展SharePoint项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
