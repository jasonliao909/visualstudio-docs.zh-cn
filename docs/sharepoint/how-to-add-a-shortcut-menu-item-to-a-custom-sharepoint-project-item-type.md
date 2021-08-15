---
title: 将快捷菜单项添加到自定义SharePoint项目项类型
titleSuffix: ''
description: 了解如何将快捷菜单项添加到自定义SharePoint项类型。 右键单击项目中的项目项时，将显示解决方案资源管理器。
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
ms.openlocfilehash: d948b2b368acc6e68cbd1f5817d8c1809ff08e4ee620ada0951c1048459492ed
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121332308"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>如何：将快捷菜单项添加到自定义SharePoint项目项类型
  定义自定义项目SharePoint类型时，可以将快捷菜单项添加到项目项。 当用户右键单击中的项目项时，将显示 **解决方案资源管理器。**

 以下步骤假定已定义自己的项目SharePoint类型。 有关详细信息，请参阅[如何：定义SharePoint项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>向自定义项目项类型添加快捷菜单项

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 实现的方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> *projectItemTypeDefinition 参数* 的 事件。

2. 在 事件的事件处理程序中，向 事件参数参数的 或 集合 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> 添加新对象。

3. 在新 对象的事件处理程序中，执行用户选择快捷菜单项时要 <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> 执行的任务。

## <a name="example"></a>示例
 下面的代码示例演示如何将上下文菜单项添加到自定义项目项类型。 当用户从 解决方案资源管理器 中的项目项打开快捷菜单 **并选择**"将消息写入 **输出窗口"菜单项** 时，Visual Studio"输出"窗口中 **显示** 一条消息。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs" id="Snippet4":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb" id="Snippet4":::

 此示例使用 SharePoint 项目服务将消息写入"输出 **"** 窗口。 有关详细信息，请参阅使用[SharePoint 项目服务。](../sharepoint/using-the-sharepoint-project-service.md)

## <a name="compile-the-code"></a>编译代码
 此示例需要一个类库项目，该项目引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员能够使用项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[为项目项 创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为程序集 (模板以及要随项目项分发的其他任何文件创建 VSIX) 包 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的扩展名。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [如何：定义SharePoint项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将属性添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
