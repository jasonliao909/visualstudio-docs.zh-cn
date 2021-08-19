---
title: 服务器资源管理器：扩展 SharePoint 连接节点
titleSuffix: ''
description: 在此演练中，请参阅如何从 SharePoint 中的 SharePoint 连接节点的扩展调用 服务器资源管理器 客户端对象服务器资源管理器。
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
ms.openlocfilehash: cf618a3fa237035ead1540a64bc772d325954ff4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122156105"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>演练：调用 SharePoint 扩展中的 服务器资源管理器 客户端对象模型
  本演练演示如何从 SharePoint 中的 SharePoint **连接** 节点的扩展调用 服务器资源管理器 **客户端对象服务器资源管理器。** 有关如何使用客户端对象模型SharePoint，请参阅[调用 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

 本演练演示了下列任务：

- 创建 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展以下列SharePoint **扩展** 服务器资源管理器连接节点：

  - 该扩展在 **服务器资源管理器** 中的每个站点SharePoint下添加一个 Web 部件 **库服务器资源管理器。** 此新节点包含子节点，这些子节点表示站点上 Web 部件库中的每个 Web 部件。

  - 扩展定义表示 Web 部件实例的新类型的节点。 此新节点类型是新 Web 部件库节点下子 **节点的基础** 。 新的"Web 部件"节点类型在"属性 **"** 窗口中显示有关节点表示的 Web 部件的信息。

- 使用 VSIX Visual Studio生成 (扩展) 部署扩展。

- 调试和测试扩展。

> [!NOTE]
> 本演练创建的扩展类似于在演练：扩展服务器资源管理器 Web 部件中创建的 [扩展](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。 该演练使用 SharePoint对象模型，但本演练使用客户端对象模型完成相同的任务。

## <a name="prerequisites"></a>必备条件
 需要开发计算机上以下组件才能完成本演练：

- 支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的 **VSIX Project** 模板创建 VSIX 包来部署扩展。 有关详细信息，请参阅扩展 SharePoint[中的 Visual Studio。](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)

了解以下概念有助于完成演练，但这不是必需的：

- 使用 SharePoint客户端对象模型。 有关详细信息，请参阅托管 [客户端对象模型](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14))。

- Web 部件SharePoint。 有关详细信息，请参阅 Web 部件[概述](/previous-versions/office/ms432401(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建两个项目：

- 一个 VSIX 项目，用于创建 VSIX 包以部署 **服务器资源管理器** 扩展。

- 实现扩展的类 **服务器资源管理器项目。**

  通过创建项目来开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在"**新建Project"** 对话框中，展开 **Visual C#** 或Visual Basic **节点，** 然后选择"**扩展性"。**

    > [!NOTE]
    > "**扩展性"** 节点仅在安装 Visual Studio SDK 时可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，选择.NET Framework版本列表中的 **4.5** .NET Framework。

     SharePoint工具扩展需要此版本的 .NET Framework。

5. 选择 **VSIX Project** 模板。

6. 在" **名称"** 框中，键入 **"WebPartNode"，** 然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将 **WebPartNode** 项目添加到 **解决方案资源管理器。**

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。** 

2. 在"**新建Project"** 对话框中，展开 **"Visual C#"** 或 **Visual Basic节点，** 然后选择"Windows"。 

3. 在对话框顶部，选择.NET Framework版本列表中的 **4.5** .NET Framework。

4. 在项目模板列表中，选择"类 **库"。**

5. 在" **名称"** 框中，输入 **"WebPartNodeExtension"，** 然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **WebPartNodeExtension** 项目添加到解决方案，并打开默认的 Class1 代码文件。

6. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 在编写代码以创建扩展之前，必须将代码文件和程序集引用添加到项目，并且必须更新默认命名空间。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 **WebPartNodeExtension** 项目中，添加两个名为 SiteNodeExtension 和 WebPartNodeTypeProvider 的代码文件。

2. 打开 WebPartNodeExtension 项目的快捷菜单，然后选择"添加 **引用"。**

3. 在"**引用管理器 - WebPartNodeExtension"** 对话框中，选择"**框架**"节点，然后选择"System.ComponentModel.Composition"和"System"的复选框。Windows。窗体程序集。

4. 选择 **"扩展"** 节点，选中以下每个程序集的复选框，然后选择"确定 **"** 按钮：

    - 微软。SharePoint。客户

    - 微软。SharePoint。Client.Runtime

    - Microsoft.VisualStudio。SharePoint

5. 打开 **WebPartNodeExtension** 项目的快捷菜单，然后选择"属性 **"。**

     将打开“项目设计器”  。

6. 选择“应用程序”选项卡。

7. 在"**默认命名空间**"框中 (C#) 或 **根命名空间** (Visual Basic) ，输入 **ServerExplorer.SharePointConnections.WebPartNode**。

## <a name="create-icons-for-the-new-nodes"></a>创建新节点的图标
 为扩展创建服务器资源管理器图标：新 **Web** 部件库节点的图标，以及 Web 部件库节点下每个子 Web 部件 **节点的另一** 个图标。 本演练稍后将编写代码，以将这些图标与节点关联。

#### <a name="to-create-icons-for-the-nodes"></a>为节点创建图标

1. 在 **WebPartNodeExtension** 项目的 Project 设计器中，选择"资源 **"** 选项卡。

2. 选择链接 **此项目不包含默认资源文件。单击此处创建一个。**

     Visual Studio创建一个资源文件，在设计器中打开它。

3. 在设计器顶部，选择"添加资源"菜单命令 **上的** 箭头，然后选择"**添加新图标"。**

4. 输入 **WebPartsNode** 作为新图标名称，然后选择"添加 **"** 按钮。

     新图标将在图像编辑器 **中打开**。

5. 编辑图标的 16x16 版本，以便它具有易于识别的设计。

6. 打开图标的 32x32 版本的快捷菜单，然后选择"**删除映像类型"。**

7. 重复步骤 3 到步骤 7，将第二个图标添加到项目资源，并将此图标命名 **为 WebPart**。

8. 在 **解决方案资源管理器** 中，在 **WebPartNodeExtension** 项目的"**资源**"文件夹中，选择 *"WebPartsNode.ico"。*

9. 在"**属性"** 窗口中，打开"**生成操作**"列表，然后选择"**嵌入资源"。**

10. 对 *WebPart.ico* 重复最后两个步骤。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器
 创建一个类，将新的 Web 部件 **库** 节点添加到每个SharePoint节点。 若要添加新节点，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口。 每当你想要扩展中现有节点的行为时，服务器资源管理器实现此接口，例如向节点添加新的子节点。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器

1. 将以下代码粘贴到 **WebPartNodeExtension** 项目的 **SiteNodeExtension 代码** 文件中。

    > [!NOTE]
    > 添加此代码后，项目将发生一些编译错误。 在稍后的步骤中添加代码时，这些错误将消失。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>定义表示 Web 部分的节点类型
 创建一个类，该类定义表示 Web 部件的新类型的节点。 Visual Studio使用此新节点类型在"Web 部件库"节点下 **显示子** 节点。 每个子节点都表示该子站点上的一SharePoint部件。

 若要定义新的节点类型，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口。 每当想要在 中定义新类型的节点时，都实现此 **服务器资源管理器。**

#### <a name="to-define-the-web-part-node-type"></a>定义 Web 部件节点类型

1. 将以下代码粘贴到 **WebPartNodeExtension 项目的 WebPartNodeTypeProvider** **代码** 文件中。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::

## <a name="checkpoint"></a>Checkpoint
 在演练的此时，Web 部件库节点的所有代码现在都位于项目中。 生成 **WebPartNodeExtension** 项目，以确保它编译时不会出错。

#### <a name="to-build-the-project"></a>生成项目

1. 在 **解决方案资源管理器** 中，打开 **WebPartNodeExtension** 项目的快捷菜单，然后选择"生成 **"。**

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后通过生成解决方案来创建 VSIX 包。

#### <a name="to-configure-the-vsix-package"></a>配置 VSIX 包

1. 在 **解决方案资源管理器** 中，在 **WebPartNode** 项目中，在清单编辑器中打开 **source.extension.vsixmanifest** 文件。

     source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 extension.vsixmanifest 文件的基础。 有关此文件的信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在"**产品名称"** 框中，输入 **Web 部件库节点服务器资源管理器。**

3. 在"**创作"** 框中，输入 **"Contoso"。**

4. 在"**说明"** 框中，输入 **"将自定义 Web** 部件库"节点添加到 服务器资源管理器 中的"SharePoint连接"节点。

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

1. 重启Visual Studio管理凭据，然后打开 **WebPartNode** 解决方案。

2. 在 WebPartNodeExtension 项目中，打开 **SiteNodeExtension** 代码文件，然后将断点添加到 和 方法的第一行 `NodeChildrenRequested` `CreateWebPartNodes` 代码。

3. 选择 **F5** 键以开始调试。

     Visual Studio将扩展安装到适用于 服务器资源管理器\1.0 的 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web 部件库节点扩展，并启动 Visual Studio 的实验实例。 你将在此实例中测试项目项Visual Studio。

#### <a name="to-test-the-extension"></a>测试扩展

1. 在 Visual Studio 实验实例的菜单栏上，选择"查看  >  **服务器资源管理器"。**

2. 验证SharePoint测试的站点是否显示在 SharePoint **中的**"连接 **"服务器资源管理器。** 如果未列出，请执行以下步骤：

    1. 打开"连接SharePoint **菜单**，然后选择"添加 **连接"。**

    2. 在 **"SharePoint连接**"对话框中，输入要SharePoint站点 URL，然后选择"确定 **"** 按钮。

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