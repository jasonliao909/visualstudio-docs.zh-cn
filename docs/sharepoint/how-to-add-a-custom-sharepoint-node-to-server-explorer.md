---
title: 如何：将自定义SharePoint节点添加到服务器资源管理器 |Microsoft Docs
titleSuffix: ''
description: 将自定义SharePoint节点添加到 服务器资源管理器 Visual Studio。 默认情况下SharePoint显示未显示在服务器资源管理器组件。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600641"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>如何：将自定义SharePoint节点添加到服务器资源管理器
  可以在 中的"连接"SharePoint **下** 添加自定义 **服务器资源管理器。** 当你想要显示默认情况下未显示在SharePoint的其他组件时 **，服务器资源管理器** 很有用。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

 若要添加自定义节点，请首先创建一个定义新节点的类。 然后创建一个扩展，该扩展将节点添加为现有节点的子节点。

### <a name="to-define-the-new-node"></a>定义新节点

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio。SharePoint

    - Microsoft.VisualStudio。SharePoint。Explorer.Extensions

    - System.ComponentModel.Composition

    - System.Drawing

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口的类。

4. 将以下属性添加到 类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此属性使Visual Studio发现和加载 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 类型传递给属性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. 在节点定义中，此属性指定新节点的字符串标识符。 建议使用格式"公司 *名称"。**节点名称*，以确保所有节点都有唯一标识符。

5. 在 方法的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> 实现中，使用 *typeDefinition* 参数的成员来配置新节点的行为。 此参数是 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> 一个对象，提供对接口中定义的事件 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 的访问。

     下面的代码示例演示如何定义新节点。 此示例假定项目包含名为 CustomChildNodeIcon 的图标作为嵌入资源。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet6":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet6":::

### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>将新节点添加为现有节点的子节点

1. 在节点定义的同一项目中，创建实现 接口的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类。

2. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此属性使Visual Studio发现和加载 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类型传递给属性构造函数。

3. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 在节点扩展中，此属性指定要扩展的节点类型的字符串标识符。

     若要指定由 Visual Studio提供的内置节点类型，请向属性构造函数传递以下枚举值之一：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值指定站点连接节点， (中显示站点 URL 的) 、站点节点或所有其他父 **服务器资源管理器。**

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值指定一个内置节点，这些节点表示 SharePoint 站点上的单个组件，例如表示列表、字段或内容类型的节点。

4. 在 方法的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> 实现中，处理 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> 参数的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> 事件。

5. 在事件处理程序中，将新节点添加到由事件参数参数公开的 对象的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> 子节点集合。

     下面的代码示例演示如何将新节点添加为 SharePoint 站点节点的 **服务器资源管理器。**

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet7":::

## <a name="complete-example"></a>完整示例
 下面的代码示例提供了用于定义简单节点的完整代码，并将其添加到 服务器资源管理器 中的 SharePoint 站点 **节点的子服务器资源管理器。**

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet5":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet5":::

## <a name="compiling-the-code"></a>编译代码
 此示例假定项目包含名为 CustomChildNodeIcon 的图标作为嵌入资源。 此示例还需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

- System.Drawing

## <a name="deploy-the-extension"></a>部署扩展
 若要部署 **服务器资源管理器** 扩展，请 (该程序集) 的 VSIX 文件包以及要随扩展一起分发的其他任何文件 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 有关详细信息，请参阅 在 Visual Studio 中为[SharePoint 工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [如何：扩展SharePoint节点服务器资源管理器](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
