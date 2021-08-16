---
title: 服务器资源管理器：扩展 SharePoint 连接 "节点
titleSuffix: ''
description: 在本演练中，请参阅如何从服务器资源管理器中 SharePoint 连接 "节点的扩展调用 SharePoint 客户端对象模型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint commands [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 1062d98eb88d028480fa74f4733f6896c9c812ae97abac1d8ab18f4c9e373d0a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121409327"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>演练：在服务器资源管理器扩展中调入 SharePoint 的客户端对象模型
  本演练演示如何从 **服务器资源管理器** 中 **SharePoint 连接**"节点的扩展调用 SharePoint 客户端对象模型。 有关如何使用 SharePoint 客户端对象模型的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

 本演练演示了下列任务：

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]通过以下方式创建扩展 **服务器资源管理器** 的 **SharePoint 连接** 节点的扩展：

  - 此扩展在 **服务器资源管理器** 中的每个 SharePoint 网站节点下添加一个 **Web 部件库** 节点。 此新节点包含表示站点上 Web 部件库中的每个 Web 部件的子节点。

  - 扩展定义了表示 Web 部件实例的新节点类型。 此新节点类型是 "新建 **Web 部件库** " 节点下的子节点的基础。 新 Web 部件节点类型在 " **属性** " 窗口中显示有关该节点所表示的 Web 部件的信息。

- 生成 Visual Studio 扩展 (VSIX) 包以部署扩展。

- 调试和测试扩展。

> [!NOTE]
> 你在本演练中创建的扩展类似于你在演练中创建的扩展 [： "扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。 该演练使用 SharePoint server 对象模型，但本演练使用客户端对象模型来完成相同的任务。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，开发计算机上需要以下组件：

- Windows、SharePoint 和 Visual Studio 的受支持版本。

- Visual Studio SDK。 本演练使用 SDK 中的 **vsix Project** 模板来创建用于部署扩展的 vsix 包。 有关详细信息，请参阅[Visual Studio 中的扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

以下概念的知识非常有用，但不是必需的，无法完成本演练：

- 使用 SharePoint 客户端对象模型。 有关详细信息，请参阅 [托管客户端对象模型](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14))。

- SharePoint 中的 Web 部件。 有关详细信息，请参阅[Web 部件概述](/previous-versions/office/ms432401(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，您必须创建两个项目：

- 用于创建 VSIX 包以部署 **服务器资源管理器** 扩展的 vsix 项目。

- 一个实现 **服务器资源管理器** 扩展的类库项目。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建 Project** " 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**"。

    > [!NOTE]
    > 仅当安装 Visual Studio SDK 时，"**扩展性**" 节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

     SharePoint 工具扩展需要此版本 .NET Framework 中的功能。

5. 选择 **VSIX Project** 模板。

6. 在 " **名称** " 框中，键入 **WebPartNode**，然后选择 " **确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **WebPartNode** 项目添加到 **解决方案资源管理器**。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建 Project**"。

2. 在 "**新建 Project** " 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 " **Windows**"。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

4. 在项目模板列表中 **，选择 "类库"**。

5. 在 " **名称** " 框中，输入 **WebPartNodeExtension**，然后选择 " **确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **WebPartNodeExtension** 项目添加到解决方案，并打开默认的 Class1 代码文件。

6. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 在编写代码以创建扩展之前，你必须将代码文件和程序集引用添加到你的项目，并且必须更新默认命名空间。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 **WebPartNodeExtension** 项目中，添加两个名为 SiteNodeExtension 和 WebPartNodeTypeProvider 的代码文件。

2. 打开 WebPartNodeExtension 项目的快捷菜单，然后选择 " **添加引用**"。

3. 在 "**引用管理器-WebPartNodeExtension** " 对话框中，选择 "**框架**" 节点，然后选中 "System.componentmodel" 和 "系统" 复选框。Windows。Forms 程序集。

4. 选择 " **扩展** " 节点，选中下列每个程序集对应的复选框，然后选择 **"确定"** 按钮：

    - 微软.SharePoint。机

    - 微软.SharePoint。Client。运行时

    - VisualStudio。SharePoint

5. 打开 **WebPartNodeExtension** 项目的快捷菜单，然后选择 " **属性**"。

     将打开“项目设计器”  。

6. 选择“应用程序”选项卡。

7. 在 "**默认命名空间**" 框中 (c # ) 或 "**根命名空间**" 框 (Visual Basic) 中，输入 **WebPartNode**。

## <a name="create-icons-for-the-new-nodes"></a>创建新节点的图标
 为 **服务器资源管理器** 扩展创建两个图标： "新建 **web 部件库** " 节点的图标以及 " **Web 部件库** " 节点下的每个子 Web 部件节点的另一个图标。 稍后在本演练中，你将编写用于将这些图标与节点关联的代码。

#### <a name="to-create-icons-for-the-nodes"></a>创建节点的图标

1. 在 WebPartNodeExtension 项目的 **Project 设计器** 中，选择 "**资源**" 选项卡。

2. 选择 " **此项目不包含默认资源文件的链接"。单击此处创建一个。**

     Visual Studio 创建一个资源文件并在设计器中将其打开。

3. 在设计器的顶部，选择 " **添加资源** " 菜单命令上的箭头，然后选择 " **添加新图标**"。

4. 输入 " **WebPartsNode** " 作为新图标名称，然后选择 " **添加** " 按钮。

     此时会在 **图像编辑器** 中打开 "新建" 图标。

5. 编辑该图标的16x16 版本，使其具有可轻松识别的设计。

6. 打开32x32 版图标的快捷菜单，然后选择 " **删除图像类型**"。

7. 重复步骤3到步骤7，将第二个图标添加到项目资源，并将其命名为 " **Web 部件**"。

8. 在 **解决方案资源管理器** 的 **WebPartNodeExtension** 项目的 **Resources** 文件夹中，选择 *WebPartsNode*。

9. 在 " **属性** " 窗口中，打开 " **生成操作** " 列表，然后选择 " **嵌入资源**"。

10. 对于 *WebPart*，重复最后两个步骤。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>将 web 部件库节点添加到服务器资源管理器
 创建一个类，用于将新的 **Web 部件库** 节点添加到每个 SharePoint 站点节点。 为了添加新节点，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口。 每当要扩展 **服务器资源管理器** 中现有节点的行为（例如，将新的子节点添加到节点）时，请实现此接口。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>将 web 部件库节点添加到服务器资源管理器

1. 将以下代码粘贴到 **WebPartNodeExtension** 项目的 **SiteNodeExtension** 代码文件中。

    > [!NOTE]
    > 添加此代码后，项目将会出现一些编译错误。 当你在后续步骤中添加代码时，这些错误将消失。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>定义表示 web 部件的节点类型
 创建一个类，用于定义表示 Web 部件的新类型的节点。 Visual Studio 使用此新节点类型显示 " **Web 部件库**" 节点下的子节点。 其中每个子节点表示 SharePoint 站点上的单个 Web 部件。

 若要定义新的节点类型，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口。 如果要在 **服务器资源管理器** 中定义新类型的节点，请实现此接口。

#### <a name="to-define-the-web-part-node-type"></a>定义 web 部件节点类型

1. 将以下代码粘贴到 **WebPartNodeExtension** 项目的 **WebPartNodeTypeProvider** 代码文件中。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::

## <a name="checkpoint"></a>Checkpoint
 在本演练的这一时间点， **Web 部件库** 节点的所有代码现在都在项目中。 生成 **WebPartNodeExtension** 项目以确保它在编译时不会出错。

#### <a name="to-build-the-project"></a>生成项目

1. 在 **解决方案资源管理器** 中，打开 **WebPartNodeExtension** 项目的快捷菜单，然后选择"生成 **"。**

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后通过生成解决方案来创建 VSIX 包。

#### <a name="to-configure-the-vsix-package"></a>配置 VSIX 包

1. 在 **解决方案资源管理器** 中，在 **WebPartNode** 项目中，在清单编辑器中打开 **source.extension.vsixmanifest** 文件。

     source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 extension.vsixmanifest 文件的基础。 有关此文件的信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在"**产品名称"** 框中，输入 **Web 部件库节点服务器资源管理器。**

3. 在"**创作"** 框中，输入 **"Contoso"。**

4. 在"**说明"** 框中，输入"将自定义 Web 部件库"节点添加到 SharePoint **中的"服务器资源管理器"。**

5. 在编辑器 **的"** 资产"选项卡上，选择"新建 **"** 按钮。

6. 在"**添加新资产"对话框** 的"类型 **"** 列表中，选择 **"Microsoft.VisualStudio.MefComponent"。**

    > [!NOTE]
    > 此值对应于 `MefComponent` extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[MEFComponent 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))

7. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

8. 在 **"Project"** 列表中，选择 **"WebPartNodeExtension"，** 然后选择"确定 **"** 按钮。

9. 在菜单栏上，选择"**生成** 生成解决方案"，并确保解决方案  >  编译时不会出错。

10. 确保 WebPartNode 项目的生成输出文件夹现在包含 WebPartNode.vsix 文件。

     默认情况下，生成输出文件夹为 。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-extension"></a>测试扩展
 现在可以在 中测试新的 Web 部件 **库****服务器资源管理器。** 首先，开始调试 Visual Studio 的实验实例中的扩展Visual Studio。 然后 **，在** Web 部件 实验实例中使用新的 Visual Studio。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. 使用Visual Studio凭据重启应用程序，然后打开 **WebPartNode** 解决方案。

2. 在 WebPartNodeExtension 项目中，打开 **SiteNodeExtension** 代码文件，然后将断点添加到 和 方法的第一行 `NodeChildrenRequested` `CreateWebPartNodes` 代码。

3. 选择 **F5** 键以开始调试。

     Visual Studio将扩展安装到适用于 服务器资源管理器\1.0 的 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web 部件库节点扩展，并启动 Visual Studio 的实验实例。 你将在此实例中测试项目项Visual Studio。

#### <a name="to-test-the-extension"></a>测试扩展

1. 在菜单栏上的Visual Studio实例中，选择"查看  >  **服务器资源管理器"。**

2. 验证SharePoint用于测试的站点是否显示在 服务器资源管理器 中的 SharePoint **连接****服务器资源管理器。** 如果未列出，请执行以下步骤：

    1. 打开"连接SharePoint **菜单**，然后选择"**添加连接"。**

    2. 在 **"SharePoint** 连接"对话框中，输入要SharePoint站点 URL，然后选择"确定 **"** 按钮。

         若要指定开发SharePoint站点，请键入 **http://localhost** 。

3. 展开显示站点 (URL 的站点连接节点) ，然后展开子站点节点 (例如"团队站点") 。 

4. 验证其他 实例中的代码Visual Studio之前在 方法中设置的断点处停止，然后选择 `NodeChildrenRequested` **F5** 键以继续调试项目。

5. 在 Visual Studio 实例中，展开 **"Web** 部件库"节点，该节点显示在顶层站点节点下。

6. 验证其他 实例中的代码Visual Studio之前在 方法中设置的断点处停止，然后选择 `CreateWebPartNodes` **F5** 键以继续调试项目。

7. 在 Visual Studio 的实验实例中，Web 部件连接站点上的所有项目是否都显示在 服务器资源管理器 **中。** 

8. 打开 Web 部件快捷菜单，然后选择"属性 **"。**

9. 在" **属性** "窗口中，验证是否显示有关 Web 部件的详细信息。

10. 在 **服务器资源管理器** 中，打开同一 Web 部件快捷菜单，然后选择"**显示消息"。**

     在显示的消息框中，选择"确定 **"** 按钮。

## <a name="uninstall-the-extension-from-visual-studio"></a>从应用程序卸载Visual Studio
 完成扩展测试后，请将其从 Visual Studio。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在 Visual Studio实验实例的菜单栏上，选择"**工具**  >  **扩展和更新"。**

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择 **"Web** 部件库节点"作为服务器资源管理器"，然后选择" **卸载"** 按钮。

3. 在出现的对话框中，选择"是 **"** 按钮。

4. 选择" **立即重启** "按钮以完成卸载。

     项目项也会卸载。

5. 关闭试验实例Visual Studio (WebPartNode 解决方案打开的 Visual Studio 实例的两个实例) 。

## <a name="see-also"></a>请参阅
- [调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [在图标图像编辑器&#40;图标编辑器创建图标或其他&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)