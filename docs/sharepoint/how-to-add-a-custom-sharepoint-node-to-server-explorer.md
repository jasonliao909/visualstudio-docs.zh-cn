---
title: 如何：将自定义 SharePoint 节点添加到服务器资源管理器 | Microsoft Docs
titleSuffix: ''
description: 在 Visual Studio 中将自定义 SharePoint 节点添加到服务器资源管理器。 默认情况下显示未显示在服务器资源管理器中的其他 SharePoint 组件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 73dac3ba52b31efd55a1c6621b0e32d098bdb997
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600641"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>如何：将自定义 SharePoint 节点添加到服务器资源管理器
  可以在服务器资源管理器中的 SharePoint 连接节点下添加自定义节点 。 如果想要显示默认情况下不显示在“服务器资源管理器”中的其他 SharePoint 组件，此方法非常有用。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

 若要添加自定义节点，请首先创建一个定义新节点的类。 然后创建一个扩展，该扩展将节点添加为现有节点的子节点。

### <a name="to-define-the-new-node"></a>若要定义新节点

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.SharePoint.Explorer.Extensions

    - System.ComponentModel.Composition

    - System.Drawing

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此属性使 Visual Studio 能够发现并加载 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 类型传递给属性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. 在节点定义中，该属性指定新节点的字符串标识符。 我们建议使用格式 company name. name 来确保所有节点都具有唯一标识符。

5. 在实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> 方法时，使用 typeDefinition 参数的成员来配置新节点的行为。 该参数是一个 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> 对象，可访问 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 接口中定义的事件。

     下面的代码示例演示如何定义新节点。 该示例假设项目包含一个名为 CustomChildNodeIcon 的图标作为嵌入资源。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet6":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet6":::

### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>若要将新节点添加为现有节点的子节点

1. 在节点定义的同一项目中，创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口的类。

2. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此属性使 Visual Studio 能够发现并加载 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类型传递给属性构造函数。

3. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 在节点扩展中，此属性为要扩展的节点的类型指定字符串标识符。

     若要指定 Visual Studio 提供的内置节点类型，请将以下枚举值之一传递给属性构造函数：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值指定站点连接节点（显示站点 URL 的节点）、站点节点或服务器资源管理器中的所有其他父级节点。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值指定表示 SharePoint 站点上单个组件的内置节点之一，例如表示列表、字段或内容类型的节点。

4. 在 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> 方法的实现中，处理 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> 参数的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> 事件。

5. 在 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> 事件处理程序中，将新节点添加到由事件自变量参数公开的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> 对象的子节点集中。

     以下代码示例演示了如何在“服务器资源管理器”中将新节点添加为 SharePoint 站点节点的子节点。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet7":::

## <a name="complete-example"></a>完整示例
 以下代码示例提供了完整代码，用于在“服务器资源管理器”中定义简单代码并将其添加为 SharePoint 站点节点的子节点。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet5":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet5":::

## <a name="compiling-the-code"></a>编译代码
 该示例假设项目包含一个名为 CustomChildNodeIcon 的图标作为嵌入资源。 本示例还需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

- System.Drawing

## <a name="deploy-the-extension"></a>部署扩展
 若要部署服务器资源管理器扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [操作说明：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
