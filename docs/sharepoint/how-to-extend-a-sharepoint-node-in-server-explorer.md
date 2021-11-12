---
title: 如何：扩展服务器资源管理器中的 SharePoint 节点 | Microsoft Docs
description: 了解如何使用 SharePoint 连接节点在服务器资源管理器中扩展 SharePoint 节点。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 8ae10e800473eccd347f5dc1398510255d5b7ee4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666181"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>如何：扩展服务器资源管理器中的 SharePoint 节点
  可以在服务器资源管理器中的 SharePoint 连接节点下扩展节点 。 要向现有节点添加新的子节点、快捷菜单项或属性时，这很有用。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>扩展服务器资源管理器中的 SharePoint 节点

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.SharePoint.Explorer.Extensions

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口的类。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此属性使 Visual Studio 能够发现并加载 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类型传递给属性构造函数。

5. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 此属性为要扩展的节点的类型指定字符串标识符。

     若要指定 Visual Studio 提供的内置节点类型，请将以下枚举值之一传递给属性构造函数：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值指定站点连接节点（显示站点 URL 的节点）、站点节点或服务器资源管理器中的所有其他父级节点。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值指定表示 SharePoint 站点上单个组件的内置节点之一，例如表示列表、字段或内容类型的节点。

6. 在 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> 方法的实现中，使用 nodeType 参数的成员向节点添加功能。 该参数是一个 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> 对象，可访问 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 接口中定义的事件。 例如，你可以处理以下事件：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>：处理此事件，以向节点添加新的子节点。 有关详细信息，请参阅[如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>：处理此事件，以向节点添加自定义快捷菜单项。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>：处理此事件，以向节点添加自定义属性。 选择节点时，“属性”窗口中会显示各个属性。

## <a name="example"></a>示例
 以下代码示例演示如何创建两种不同类型的节点扩展：

- 将上下文菜单项添加到 SharePoint 站点节点的扩展。 单击菜单项时，它会显示所单击节点的名称。

- 将名为 ContosoExampleProperty 的自定义属性添加到表示名为 Body 的字段的每个节点的扩展 。

  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs" id="Snippet9":::
  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb" id="Snippet9":::

  该扩展向节点添加可编辑的字符串属性。 你还可以创建自定义属性，以显示来自 SharePoint 服务器的只读数据。 有关演示如何执行此操作的示例，请参阅[演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="compile-the-code"></a>编译代码
 本示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.SharePoint.Explorer.Extensions

- System.ComponentModel.Composition

- System.Windows.Forms

## <a name="deploy-the-extension"></a>部署扩展
 若要部署服务器资源管理器扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
