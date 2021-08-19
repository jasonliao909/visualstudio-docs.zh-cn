---
title: 如何：在 SharePoint 中扩展 服务器资源管理器 |Microsoft Docs
description: 了解如何使用 SharePoint 连接服务器资源管理器扩展 SharePoint 节点。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130970"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>如何：扩展SharePoint节点服务器资源管理器
  可以在 中扩展 SharePoint **连接** 节点下的 **服务器资源管理器。** 当你想要将新的子节点、快捷菜单项或属性添加到现有节点时，这很有用。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>扩展 SharePoint 节点服务器资源管理器

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio。SharePoint

    - Microsoft.VisualStudio。SharePoint。Explorer.Extensions

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口的类。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此属性使Visual Studio发现和加载 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类型传递给属性构造函数。

5. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 此属性指定要扩展的节点类型的字符串标识符。

     若要指定由 Visual Studio 提供的内置节点类型，请向属性构造函数传递以下枚举值之一：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值指定站点连接节点， (中显示站点 URL 的节点) 、站点节点或所有其他 **父服务器资源管理器。**

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值指定一个内置节点，这些节点表示 SharePoint 站点上的单个组件，例如表示列表、字段或内容类型的节点。

6. 在 方法的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> 实现中，使用 *nodeType* 参数的成员向节点添加功能。 此参数是 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> 一个对象，提供对接口中定义的事件 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 的访问。 例如，可以处理以下事件：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>：处理此事件以将新的子节点添加到节点。 有关详细信息，请参阅[如何：将自定义SharePoint节点添加到 服务器资源管理器。](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>：处理此事件以向节点添加自定义快捷菜单项。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>：处理此事件以将自定义属性添加到节点。 选择节点时 **，属性** 将显示在"属性"窗口中。

## <a name="example"></a>示例
 下面的代码示例演示如何创建两种不同类型的节点扩展：

- 向站点节点添加上下文菜单项的SharePoint扩展。 单击菜单项时，将显示单击的节点的名称。

- 一个扩展，用于将名为 **ContosoExampleProperty** 的自定义属性添加到表示名为 **Body** 的字段的每个节点。

  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs" id="Snippet9":::
  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb" id="Snippet9":::

  此扩展将可编辑的字符串属性添加到节点。 还可以创建自定义属性，用于显示来自 SharePoint 数据的只读数据。 有关演示如何执行此操作的示例，请参阅演练：扩展服务器资源管理器 [以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- Microsoft.VisualStudio。SharePoint。Explorer.Extensions

- System.ComponentModel.Composition

- System.Windows.Forms

## <a name="deploy-the-extension"></a>部署扩展
 若要部署 **服务器资源管理器** 扩展，请 (程序集的 VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [如何：将自定义SharePoint节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [将自定义数据与 SharePoint 工具扩展关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
