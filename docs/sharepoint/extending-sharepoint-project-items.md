---
title: 扩展 SharePoint 项目项 | Microsoft Docs
description: 查看用于扩展 SharePoint 项目项的任务。 了解项目项扩展插件和项目项实例是如何相关的。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: dc36a1323b9ce1a1a3db0428a35ad9dd5d092629
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600660"
---
# <a name="extend-sharepoint-project-items"></a>扩展 SharePoint 项目项
  在想要将功能添加到已安装在 Visual Studio 中的 SharePoint 项目项类型时创建项目项扩展。 例如，可以在 Visual Studio 中为内置“事件接收器”或“列表定义”项目项创建扩展，也可以为自定义项目项类型创建扩展。 还可以为所有类型的 SharePoint 项目项创建扩展。

## <a name="tasks-for-extending-sharepoint-project-items"></a>用于扩展 SharePoint 项目项的任务
 若要扩展项目项，生成一个实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 接口的 Visual Studio 扩展程序集。 有关更多信息，请参阅[操作说明：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

 扩展自定义项目项时，还可以将以下功能添加到项目项：

- 将快捷菜单项添加到项目项。 当你在“解决方案资源管理器”中打开项目项的快捷菜单时，将显示菜单项。 可通过右键单击项目项或选择它，然后选择 Shift+F10 键来访问快捷菜单。 有关详细信息，请参阅[操作说明：将快捷菜单项添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)。

- 将自定义属性添加到项目项。 当你在“解决方案资源管理器”中选择项目项时，属性将显示在“属性”窗口中。 有关详细信息，请参阅[操作说明：将属性添加到 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)。

  有关演示如何创建、部署和测试项目项扩展的演练，请参阅[演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)。

## <a name="understand-the-relationship-between-project-item-extensions-and-project-item-instances"></a>了解项目扩展项扩展与项目项实例之间的关系
 创建项目项扩展时，Visual Studio 在将关联类型的项目项添加到 SharePoint 项目时加载扩展。 例如，如果为“事件接收器”项目项创建扩展，当用户向项目添加“事件接收器”项目项时，Visual Studio 将加载该扩展。 对于关联项目项类型的所有实例，Visual Studio 都使用相同的扩展实例。 在上面的示例中，如果用户将第二个“事件接收器”项目项添加到项目中，那么扩展的同一实例将用于自定义第二个项目项。

 若要访问正在扩展的项目项类型的特定实例，请在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 方法的实现中处理 projectItemType 参数的一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 事件。 例如，若要确定何时将正在扩展的项目项类型添加到项目，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 事件。 有关更多信息，请参阅[操作说明：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

## <a name="identifiers-for-sharepoint-project-items"></a>SharePoint 项目项标识符
 每个 SharePoint 项目项都有相应的字符串标识符。 如果要执行以下任务，则必须知道项目项标识符：

- 为项目项创建扩展。 在这种情况下，你必须将要扩展的项目项标识符传递给 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 构造函数。 若要为所有项目项类型创建扩展，请传递 \\* 字符串值。

- 以编程方式将项目项添加到项目。 在这种情况下，必须将项目项标识符传递给 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemCollection.Add%2A> 方法。

  下表列出了包含在 Visual Studio 中的 SharePoint 项目项的标识符。

|项目项名称|字符串标识符|
|-----------------------|-----------------------|
|业务数据目录模型|Microsoft.VisualStudio.SharePoint.BusinessDataConnectivity|
|内容类型|Microsoft.VisualStudio.SharePoint.ContentType|
|事件接收器|Microsoft.VisualStudio.SharePoint.EventHandler|
|空元素|Microsoft.VisualStudio.SharePoint.GenericElement|
|列表定义<br /><br /> 内容类型中的列表定义|Microsoft.VisualStudio.SharePoint.ListDefinition|
|列表实例|Microsoft.VisualStudio.SharePoint.ListInstance|
|模块|Microsoft.VisualStudio.SharePoint.Module|
|顺序工作流<br /><br /> 状态机工作流|Microsoft.VisualStudio.SharePoint.Workflow|
|网站定义|Microsoft.VisualStudio.SharePoint.SiteDefinition|
|可视 Web 部件|Microsoft.VisualStudio.SharePoint.VisualWebPart|
|Web 部件|Microsoft.VisualStudio.SharePoint.WebPart|
|工作流关联窗体|Microsoft.VisualStudio.SharePoint.WorkflowAssociation|

## <a name="see-also"></a>另请参阅
- [操作说明：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [操作说明：将快捷菜单项添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [操作说明：将属性添加到 SharePoint 项目项扩展](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
