---
title: 操作说明：创建 SharePoint 项目项扩展 | Microsoft Docs
description: 了解在想要将功能添加到已安装在 Visual Studio 中的 SharePoint 项目项时如何创建项目项扩展。
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
ms.openlocfilehash: 198ae95dabcb65e96a2db6bd60fbfb3667ab2c08
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671935"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>操作说明：创建 SharePoint 项目项扩展
  在想要将功能添加到已安装在 Visual Studio 中的 SharePoint 项目项时创建项目项扩展。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

### <a name="to-create-a-project-item-extension"></a>若要创建项目项扩展

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此属性使 Visual Studio 能够发现并加载 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 类型传递给属性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. 在项目项扩展中，该属性标识要扩展的项目项。 将项目项的 ID 传递给属性构造函数。 有关 Visual Studio 附带的项目项的 ID 列表，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

5. 在实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 方法时，使用 projectItemType 参数的成员来定义扩展行为。 该参数是一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> 对象，可访问 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 和 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> 接口中定义的事件。 若要访问正在扩展的项目项类型的特定实例，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 事件，例如 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 和 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized>。

## <a name="example"></a>示例
 以下代码示例演示了如何为事件接收器项目项创建简单扩展。 每次用户将事件接收器项目项添加到 SharePoint 项目时，该扩展都会将消息写入“输出”窗口和“错误列表”窗口。 

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs" id="Snippet1":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb" id="Snippet1":::

 此示例使用 SharePoint 项目服务将消息写入“输出”窗口和“错误列表”窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 本示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
