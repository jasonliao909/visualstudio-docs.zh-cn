---
title: 扩展SharePoint Project项|Microsoft Docs
description: 查看用于扩展项目SharePoint的任务。 了解项目项扩展插件与项目项实例之间的关联。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600660"
---
# <a name="extend-sharepoint-project-items"></a>扩展SharePoint项目项
  若要将功能添加到已安装在 SharePoint 中的项目项的类型，请创建项目项Visual Studio。 例如，可以在 Visual Studio 中为内置事件接收器或列表定义项目项创建扩展，也可以为自定义项目项类型创建扩展。 还可以为所有类型的项目项创建SharePoint扩展。

## <a name="tasks-for-extending-sharepoint-project-items"></a>用于扩展项目SharePoint的任务
 若要扩展项目项，请Visual Studio接口的扩展 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 程序集。 有关详细信息，请参阅[如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

 扩展项目项时，还可以将以下功能添加到项目项：

- 向项目项添加快捷菜单项。 在 中打开项目项的快捷菜单时，将显示 **解决方案资源管理器。** 通过右键单击项目项或选择该项目项，然后选择 Shift  + **F10** 键来打开快捷菜单。 有关详细信息，请参阅[如何：将快捷菜单项添加到SharePoint项目项扩展。](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)

- 向项目项添加自定义属性。 在 中 **选择项目项** 时，属性将显示在"属性 **"解决方案资源管理器。** 有关详细信息，请参阅[如何：向](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)项目项扩展SharePoint属性。

  有关演示如何创建、部署和测试项目项扩展的演练，请参阅演练：扩展SharePoint[项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)。

## <a name="understand-the-relationship-between-project-item-extensions-and-project-item-instances"></a>了解项目项扩展插件与项目项实例之间的关系
 创建项目项扩展时，Visual Studio将关联类型的项目项添加到项目时加载SharePoint扩展。 例如，如果为事件接收器项目项创建扩展，Visual Studio向项目添加事件接收器项目项时加载扩展。  Visual Studio对关联的项目项类型的所有实例使用相同的扩展实例。 在上一示例中，如果用户向项目添加第二个事件接收器项目项，则扩展的同一实例用于自定义第二个项目项。

 若要访问要扩展的项目项类型的特定实例，请处理方法实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> *中的 projectItemType* 参数的其中一 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 个事件。 例如，若要确定何时将所扩展类型的项目项添加到项目中，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 事件。 有关详细信息，请参阅[如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

## <a name="identifiers-for-sharepoint-project-items"></a>项目项SharePoint标识符
 每个SharePoint项目项都有相应的字符串标识符。 如果要执行以下任务，必须知道项目项的标识符：

- 为项目项创建扩展。 在这种情况下，必须将要扩展的项目项的标识符传递给 的构造函数 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 。 若要创建所有项目项类型的扩展，请传递 **\\** * 字符串值。

- 以编程方式将项目项添加到项目。 在这种情况下，必须将项目项的标识符传递给 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemCollection.Add%2A> 方法。

  下表列出了项目包中包含的SharePoint项的标识符Visual Studio。

|Project项名称|字符串标识符|
|-----------------------|-----------------------|
|业务数据目录模型|Microsoft.VisualStudio。SharePoint。BusinessDataConnectivity|
|内容类型|Microsoft.VisualStudio。SharePoint。ContentType|
|事件接收器|Microsoft.VisualStudio。SharePoint。EventHandler|
|空元素|Microsoft.VisualStudio。SharePoint。GenericElement|
|列表定义<br /><br /> 从内容类型列出定义|Microsoft.VisualStudio。SharePoint。ListDefinition|
|列出实例|Microsoft.VisualStudio。SharePoint。ListInstance|
|模块|Microsoft.VisualStudio。SharePoint。模块|
|顺序工作流<br /><br /> 状态机工作流|Microsoft.VisualStudio。SharePoint。流程|
|站点定义|Microsoft.VisualStudio。SharePoint。SiteDefinition|
|Visual Web 部件|Microsoft.VisualStudio。SharePoint。VisualWebPart|
|Web 部件|Microsoft.VisualStudio。SharePoint。Webpart|
|工作流关联窗体|Microsoft.VisualStudio。SharePoint。WorkflowAssociation|

## <a name="see-also"></a>另请参阅
- [如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：向项目项扩展SharePoint快捷菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [如何：向项目项扩展SharePoint属性](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [演练：扩展SharePoint项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
