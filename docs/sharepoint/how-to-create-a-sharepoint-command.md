---
title: 操作说明：创建 SharePoint 命令 | Microsoft Docs
description: 了解如何创建自定义 SharePoint 命令，以从 SharePoint 工具扩展调用服务器对象模型 API。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: caaca2226b80a1e1aef4246094a01c158b8e2951
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667479"
---
# <a name="how-to-create-a-sharepoint-command"></a>如何：创建 SharePoint 命令
  如果要在 SharePoint 工具扩展中使用服务器对象模型，必须创建自定义 SharePoint 命令来调用 API。 在可直接调入服务器对象模型的程序集中定义 SharePoint 命令。

 有关 SharePoint 命令用途的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-create-a-sharepoint-command"></a>创建 SharePoint 命令

1. 创建一个具有以下配置的类库项目：

    - 面向 .NET Framework 3.5。 有关选择目标框架的详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/visual-studio-multi-targeting-overview.md)。

    - 面向 AnyCPU 或 x64 平台。 默认情况下，类库项目的目标平台是 AnyCPU。 有关选择目标平台的详细信息，请参阅[如何：配置项目以面向目标平台](../ide/how-to-configure-projects-to-target-platforms.md)。

    > [!NOTE]
    > 不能在定义 SharePoint 工具扩展的同一项目中执行 SharePoint 命令，因为 SharePoint 命令面向的是 .NET Framework 3.5，SharePoint 工具扩展面向的是 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。 必须定义由单独的项目中的扩展使用的任何 SharePoint 命令。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint.Commands

    - Microsoft.SharePoint

3. 在项目的类中，创建一个定义 SharePoint 命令的方法。 该方法必须符合以下准则：

    - 它可以有一个或两个参数。

         第一个参数必须是 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 对象。 此对象提供执行命令的 Microsoft.SharePoint.SPSite 或 Microsoft.SharePoint.SPWeb。 它还提供用于将消息写入 Visual Studio 中的“输出”窗口或“错误列表”窗口的 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger> 对象 。

         第二个参数可以是你选择的类型，但此参数是可选的。 如果需要将数据从 SharePoint 工具扩展传递到命令，则可以将此参数添加到 SharePoint 命令。

    - 它可以有返回值，但这是可选的。

    - 第二个参数和返回值必须是可以由 Windows Communication Foundation (WCF) 序列化的类型。 有关详细信息，请参阅[数据协定序列化程序支持的类型](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer)和[使用 XmlSerializer 类](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class)。

    - 该方法可以具有任何可见性（公开、内部或专用），并且可以是静态的或非静态的  。

4. 将 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 应用于方法。 此属性指定该命令的唯一标识符；此标识符不必与方法名称匹配。

     从 SharePoint 工具扩展调用命令时，必须指定相同的唯一标识符。 有关详细信息，请参阅[如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。

## <a name="example"></a>示例
 下面的代码示例演示一个具有标识符 `Contoso.Commands.UpgradeSolution` 的 SharePoint 命令。 此命令使用服务器对象模型中的 API 升级到已部署的解决方案。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs" id="Snippet5":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb" id="Snippet5":::

 除了第一个隐式 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数，此命令还具有自定义字符串参数，该参数包含正在升级到 SharePoint 站点的 .wsp 文件的完整路径。 若要在更大的上下文示例中查看此代码，请参阅[演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="compiling-the-code"></a>编译代码
 本示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint.Commands

- Microsoft.SharePoint

## <a name="deploying-the-command"></a>部署命令
 若要部署命令，请在同一 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (vsix) 包中包括命令程序集以及使用该命令的扩展程序集。 还必须在 extension.vsixmanifest 文件中为命令程序集添加一个项。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
