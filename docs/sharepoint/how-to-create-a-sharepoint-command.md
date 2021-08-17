---
title: 如何：创建 SharePoint 命令|Microsoft Docs
description: 了解如何创建自定义 SharePoint 命令，以调用 SharePoint 扩展中的服务器对象模型的 API。
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
ms.openlocfilehash: 7973cd0c3a52ae4433c85b9b0fa71cecc085827c4d33d542232229b7034d9f63
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121228683"
---
# <a name="how-to-create-a-sharepoint-command"></a>如何：创建 SharePoint 命令
  如果要在 SharePoint 扩展中使用服务器对象模型，则必须创建自定义 SharePoint *命令* 来调用 API。 可以在可直接SharePoint对象模型的程序集中定义命令。

 有关命令用途SharePoint，请参阅[调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-create-a-sharepoint-command"></a>创建 SharePoint 命令

1. 创建具有以下配置的类库项目：

    - 面向 .NET Framework 3.5。 有关选择目标框架的信息，请参阅[如何：](../ide/visual-studio-multi-targeting-overview.md)面向目标版本.NET Framework。

    - 面向 AnyCPU 或 x64 平台。 默认情况下，类库项目的目标平台为 AnyCPU。 有关选择目标平台的信息，请参阅 [如何：将项目配置为目标平台](../ide/how-to-configure-projects-to-target-platforms.md)。

    > [!NOTE]
    > 不能在定义 SharePoint 工具扩展的同一项目中实现 SharePoint 命令，因为 SharePoint 命令面向 .NET Framework 3.5，SharePoint 工具扩展面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 。 必须在单独的SharePoint定义扩展使用的任何命令。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio。SharePoint。命令

    - 微软。SharePoint

3. 在项目中的类中，创建一个定义 SharePoint 命令的方法。 方法必须符合以下准则：

    - 它可以有一个或两个参数。

         第一个参数必须是 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 对象。 此对象提供 Microsoft。SharePoint。SPSite 或 Microsoft。SharePoint。执行命令的 SPWeb。 它还提供一 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger> 个 对象，该对象可用于将消息写入"输出"窗口或"错误列表"窗口Visual Studio。

         第二个参数可以是你选择的类型，但此参数是可选的。 如果需要将数据从 SharePoint SharePoint 工具扩展传递到命令，可以将此参数添加到 SharePoint 命令。

    - 它可以具有返回值，但这是可选的。

    - 第二个参数和返回值必须是一个类型，该类型可通过 WINDOWS Communication Foundation (WCF) 。 有关详细信息，请参阅数据 [协定序列化程序支持的类型和使用](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer) [XmlSerializer 类](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class)。

    - 方法可以具有公共、 (或专用) 的任何可见性，并且可以是静态的或非静态的。 

4. 将 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 应用于 方法。 此属性指定命令的唯一标识符;此标识符不需要与方法名称匹配。

     从工具扩展调用命令时，必须指定SharePoint标识符。 有关详细信息，请参阅[如何：执行SharePoint命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。

## <a name="example"></a>示例
 下面的代码示例演示一个SharePoint标识符 为 的命令 `Contoso.Commands.UpgradeSolution` 。 此命令使用服务器对象模型中的 API 升级到已部署的解决方案。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs" id="Snippet5":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb" id="Snippet5":::

 除了隐式第一个参数，此命令还包含一个自定义字符串参数，该参数包含要升级到 SharePoint 站点的 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> .wsp 文件的完整路径。 若要在较大示例的上下文中查看此代码，请参阅[演练：为项目创建自定义SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="compiling-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint。命令

- 微软。SharePoint

## <a name="deploying-the-command"></a>部署命令
 若要部署命令，请在同一扩展 ([!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] *vsix*) 包中包括命令程序集以及使用该命令的扩展程序集。 还必须在 extension.vsixmanifest 文件中为命令程序集添加一个条目。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：执行SharePoint命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
