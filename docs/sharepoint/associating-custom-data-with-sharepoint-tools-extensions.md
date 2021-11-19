---
title: 将自定义数据与 SharePoint Tools 扩展|Microsoft Docs
description: 将自定义数据与SharePoint扩展关联。 查看可包含自定义数据的对象列表。 添加和检索自定义数据。
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
  可以将自定义数据添加到工具扩展SharePoint对象。 当扩展的一部分数据以后想要从扩展中的其他代码访问时，这非常有用。 你可以将数据与扩展中的对象关联，然后稍后从同一对象检索数据，而不是实现存储和访问数据的自定义方法。

 若要保留与对象中的特定项相关的数据，将自定义数据添加到对象Visual Studio。 SharePoint工具扩展在 Visual Studio 中只加载一次，因此扩展可能随时处理多个不同的项 (例如项目、项目项或 **服务器资源管理器** 节点) 。 如果有仅与特定项相关的自定义数据，可以将数据添加到表示该项的 对象。

 将自定义数据添加到 SharePoint 扩展中的对象时，数据不会持久保存。 数据仅在对象的生命周期内可用。 垃圾回收回收对象后，数据将丢失。

 在项目SharePoint扩展中，还可以保存卸载扩展后保留的字符串数据。 有关详细信息，请参阅[将数据保存到项目SharePoint扩展中](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="objects-that-can-contain-custom-data"></a>可以包含自定义数据的对象
 可以将自定义数据添加到实现 接口SharePoint工具对象模型中的任何 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> 对象。 此接口仅定义一个 属性 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> ，该属性是自定义数据对象的集合。 以下类型实现 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> ：

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
 若要将自定义数据添加到 SharePoint 工具扩展中的对象，请获取要将数据添加到的对象的 属性，然后使用 方法 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> 将数据添加到 对象。

 若要从 SharePoint 工具扩展中的对象检索自定义数据，请获取 对象的 属性，然后使用以下方法 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 之一：

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. 如果数据对象存在，则此方法返回 **true;** 如果数据对象不存在，则返回 false。  可以使用此方法检索值类型或引用类型的实例。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. 此方法返回数据对象（如果退出）或 **null（** 如果不存在）。 只能使用此方法检索引用类型的实例。

  下面的代码示例确定某个数据对象是否已与项目项关联。 如果数据对象尚未与项目项关联，则代码会将该对象添加到 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 项目项的 属性。 若要在较大示例的上下文中查看此示例，请参阅如何：将属性添加到自定义SharePoint[项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet13":::
  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet13":::

## <a name="see-also"></a>另请参阅
- [SharePoint 工具扩展的编程概念和功能](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [演练：使用项模板创建自定义操作项目项，第 1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [如何：向项目SharePoint属性](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [如何：将属性添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
