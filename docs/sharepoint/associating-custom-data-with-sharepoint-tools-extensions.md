---
title: 将自定义数据与 SharePoint 工具扩展关联 | Microsoft Docs
description: 将自定义数据与 SharePoint 工具扩展关联。 查看可包含自定义数据的对象列表。 添加和检索自定义数据。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], associating custom data
- project items [SharePoint development in Visual Studio], associating custom data
- SharePoint project items, associating custom data
- SharePoint projects, associating custom data
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 6650af3f431fcd2168812be1d589050926ba2d5e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664244"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>将自定义数据与 SharePoint 工具扩展关联
  可以将自定义数据添加到 SharePoint工具扩展中的特定对象。 当你在扩展的某个部分拥有数据，并且希望稍后从扩展中的其他代码访问这些数据时，这非常有用。 可以将数据与扩展中的对象关联，然后稍后从同一对象检索数据，而无需实现存储和访问数据的自定义方法。

 当你希望保留与 Visual Studio 中特定项相关的数据时，向对象添加自定义数据也很有用。 SharePoint 工具扩展在 Visual Studio 中只加载一次，因此扩展可能随时用于多个不同的项（例如项目、项目项或“服务器资源管理器”节点）。 如果有仅与特定项相关的自定义数据，可以将数据添加到表示该项的对象。

 将自定义数据添加到 SharePoint 工具扩展中的对象时，数据不会持久保存。 数据仅在对象的生命周期内可用。 垃圾回收回收对象后，数据将丢失。

 在 SharePoint 项目系统扩展中，还可以保存卸载扩展后保留的字符串数据。 有关详细信息，请参阅[在 SharePoint 项目系统扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="objects-that-can-contain-custom-data"></a>可以包含自定义数据的对象
 可以将自定义数据添加到实现 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> 接口的 SharePoint 工具对象模型中的任何对象。 此接口仅定义一个属性 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A>，该属性是自定义数据对象的集合。 以下类型实现 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject>：

- <xref:Microsoft.VisualStudio.SharePoint.IMappedFolder>

- <xref:Microsoft.VisualStudio.SharePoint.IMenuItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectMember>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>

- <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentContext>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition>

## <a name="add-and-retrieve-custom-data"></a>添加和检索自定义数据
 若要将自定义数据添加到 SharePoint 工具扩展中的对象，请获取要将数据添加到的对象的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性，然后使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> 方法将数据添加到该对象。

 若要从 SharePoint 工具扩展中的对象检索自定义数据，请获取该对象的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性，然后使用以下方法之一：

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. 如果数据对象存在，此方法将返回 true；如果数据对象不存在，则返回 false。 可以使用此方法检索值类型或引用类型的实例。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. 如果数据对象退出，此方法将返回该对象；如果数据对象不存在，则返回 NULL。 只能使用此方法检索引用类型的实例。

  下面的代码示例确定某个数据对象是否已与项目项关联。 如果数据对象尚未与项目项关联，则代码会将该对象添加到项目项的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性。 若要在较大示例的上下文中查看此示例，请参阅[操作说明：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet13":::
  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet13":::

## <a name="see-also"></a>另请参阅
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [操作说明：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [操作说明：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
