---
title: 服务器资源管理器：扩展“SharePoint 连接”节点
titleSuffix: ''
description: 在此演练中，了解如何从服务器资源管理器中的 SharePoint 连接节点的扩展调用 SharePoint 客户端对象模型。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664146"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型
  本演练演示如何从服务器资源管理器中的“SharePoint 连接”节点的扩展调用 SharePoint 客户端对象模型。  有关如何使用 SharePoint 客户端对象模型的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

 本演练演示了下列任务：

- 以下列方式创建扩展服务器资源管理器的“SharePoint 连接”节点的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 ：

  - 扩展在“服务器资源管理器”中的每个 SharePoint 站点节点下添加了一个“Web 部件库”节点 。 此新节点包含子节点，这些子节点表示站点上 Web 部件库中的每个 Web 部件。

  - 扩展定义了表示 Web 部件实例的新节点类型。 此新节点类型是新“Web 部件库”节点下的子节点的基础。 新的 Web 部件节点类型在“属性”窗口中显示有关节点所代表的 Web 部件的信息。

- 生成 Visual Studio 扩展 (VSIX) 包来部署扩展。

- 调试和测试扩展。

> [!NOTE]
> 本演练中创建的扩展类似于在[演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)中创建的扩展。 该演练使用 SharePoint 服务器对象模型，但本演练使用客户端对象模型完成相同的任务。

## <a name="prerequisites"></a>先决条件
 需要在开发计算机上使用以下组件来完成本演练：

- 受支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的“VSIX 项目”模板来创建用于部署扩展的 VSIX 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

了解以下概念将很有用，但对于完成本演练来说，并不是必需的：

- 使用 SharePoint 客户端对象模型。 有关详细信息，请参阅[托管客户端对象模型](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14))。

- SharePoint 中的 Web 部件。 有关详细信息，请参阅 [Web 部件概述](/previous-versions/office/ms432401(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建两个项目：

- VSIX 项目，用于创建 VSIX 包以部署服务器资源管理器扩展。

- 用于实现服务器资源管理器扩展的类库项目。

  通过创建项目开始本次演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在“新建项目”对话框中，展开“Visual C#”或“Visual Basic”节点，然后选择“可扩展性”   。

    > [!NOTE]
    > “扩展性”节点仅在安装了 Visual Studio SDK 时可用。 有关详细信息，请参阅本主题前面的“先决条件”部分。

4. 在对话框顶部，选择 .NET Framework 版本列表中的“.NET Framework 4.5”。

     SharePoint 工具扩展需要此 .NET Framework 版本中的功能。

5. 选择“VSIX 项目”模板。

6. 在“名称”框中，键入“WebPartNode”，然后选择“确定”按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 WebPartNode 项目添加到解决方案资源管理器 。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在解决方案资源管理器中，打开“解决方案”节点的快捷菜单，选择“添加”，然后选择“新建项目”  。

2. 在“新建项目”对话框中，展开“Visual C#”或“Visual Basic”节点，然后选择“Windows”   。

3. 在对话框顶部，选择 .NET Framework 版本列表中的“.NET Framework 4.5”。

4. 在项目模板列表中，选择“类库”。

5. 在“名称”框中输入“WebPartNodeExtension”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 WebPartNodeExtension 项目添加到解决方案，并打开默认 Class1 代码文件。

6. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 在编写代码以创建扩展之前，必须将代码文件和程序集引用添加到项目，并且必须更新默认命名空间。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 WebPartNodeExtension 项目中，添加两个名为 SiteNodeExtension 和 WebPartNodeTypeProvider 的代码文件。

2. 打开 WebPartNodeExtension 项目的快捷菜单，然后选择“添加引用”。

3. 在“引用管理器 - WebPartNodeExtension”对话框中，选择“Framework”节点，然后选择 System.ComponentModel.Composition 和 System.Windows.Forms 程序集的复选框 。

4. 选择“扩展”节点，选择以下每个程序集的复选框，然后选择“确定”按钮 ：

    - Microsoft.SharePoint.Client

    - Microsoft.SharePoint.Client.Runtime

    - Microsoft.VisualStudio.SharePoint

5. 打开 WebPartNodeExtension 项目的快捷菜单，然后选择“属性” 。

     将打开“项目设计器”  。

6. 选择“应用程序”选项卡。

7. 在“默认命名空间”框 (C#) 或“根命名空间”框 (Visual Basic) 中，输入 ServerExplorer.SharePointConnections.WebPartNode  。

## <a name="create-icons-for-the-new-nodes"></a>为新节点创建图标
 为“服务器资源管理器”扩展创建两个图标：一个图标用于新的“Web 部件库”节点，另一个图标用于“Web 部件库”下的每个子 Web 部件节点  。 本演练的稍后部分将编写代码，以将这些图标与节点关联起来。

#### <a name="to-create-icons-for-the-nodes"></a>为节点创建图标

1. 在 WebPartNodeExtension 项目的项目设计器中，选择“资源”选项卡。

2. 选择链接“此项目不包含默认的资源文件。单击此处可进行创建。”

     Visual Studio 创建一个资源文件，并在设计器中将其打开。

3. 在设计器顶部，选择“添加资源”菜单命令旁边的箭头，然后选择“添加新图标” 。

4. 输入“WebPartsNode”作为新图标名称，然后选择“添加”按钮。

     新图标将在“图像编辑器”中打开。

5. 编辑图标的 16x16 版本，使其具有可轻松识别的设计。

6. 打开图标的 32x32 版本的快捷菜单，然后选择“删除图像类型”。

7. 重复步骤 3 到步骤 7，将第二个图标添加到项目资源，并将此图标命名为 WebPart。

8. 在“解决方案资源管理器”中，在 WebPartNodeExtension 项目的“Resources”文件夹下，选择“WebPartsNode.ico”  。

9. 在“属性”窗口中，打开“生成操作”列表，然后选择“嵌入的资源”。

10. 针对 WebPart.ico 重复最后两个步骤。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器
 创建一个类，用于将新的 Web 部件库节点添加到每个 SharePoint 站点节点。 要添加新节点，该类需要实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口。 每当要扩展“服务器资源管理器”中现有节点的行为（例如，将新的子节点添加到节点）时，都需要实现此接口。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>将 Web 部件库节点添加到服务器资源管理器

1. 在 WebPartNodeExtension 项目中，将以下代码粘贴到 SiteNodeExtension 代码文件中。 

    > [!NOTE]
    > 添加此代码后，项目将发生一些编译错误。 在稍后的步骤中添加代码时，这些错误将消失。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>定义表示 Web 部件的节点类型
 创建一个类，用以定义表示 Web 部件的新节点类型。 Visual Studio 使用此新节点类型显示“Web 部件库”节点下的子节点。 每个子节点表示 SharePoint 站点上的单个 Web 部件。

 若要定义新节点类型，该类需要实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口。 每当要在“服务器资源管理器”中定义新节点类型时，都需要实现此接口。

#### <a name="to-define-the-web-part-node-type"></a>定义 Web 部件节点类型

1. 在 WebPartNodeExtension 项目中，将以下代码粘贴到 WebPartNodeTypeProvider 代码文件中。 

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::

## <a name="checkpoint"></a>检查点
 此时在本演练中，“Web 部件库”节点的所有代码现在都位于项目中。 生成 WebPartNodeExtension 项目并确保编译时没有出现错误。

#### <a name="to-build-the-project"></a>生成项目

1. 在“解决方案资源管理器”中，打开 WebPartNodeExtension 项目的快捷菜单，然后选择“生成”  。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后通过生成解决方案来创建 VSIX 包。

#### <a name="to-configure-the-vsix-package"></a>配置 VSIX 包

1. 在“解决方案资源管理器”的 WebPartNode 项目下，在清单编辑器中打开 source.extension.vsixmanifest 文件  。

     source.extension.vsixmanifest 文件是所有 VSIX 包所需的 extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在“产品名称”框中，输入“服务器资源管理器的 Web 部件库节点” 。

3. 在“作者”框中，输入“Contoso” 。

4. 在“说明”框中，输入“将自定义 Web 部件库节点添加到服务器资源管理器中的 SharePoint 连接节点。”

5. 在编辑器的“资产”选项卡中，选择“新建”按钮 。

6. 在“添加新资产”对话框中，在“类型”列表中选择“Microsoft.VisualStudio.MefComponent”  。

    > [!NOTE]
    > 此值与 extension.vsixmanifest 文件中的 `MefComponent` 元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅 [MEFComponent 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

7. 在“源”列表中，选择“当前解决方案中的项目” 。

8. 在“项目”列表中，选择“WebPartNodeExtension”，然后选择“确定”按钮  。

9. 在菜单栏上，选择“生成” > “生成解决方案”，然后确保解决方案在编译时不会出错 。

10. 确保 WebPartNode 项目的生成输出文件夹现在包含 WebPartNode.vsix 文件。

     默认情况下，生成输出文件夹为包含项目文件的文件夹下的 ..\bin\Debug 文件夹。

## <a name="test-the-extension"></a>测试扩展
 现在可以在“服务器资源管理器”中测试新的“Web 部件库”节点 。 首先，在 Visual Studio 的实验实例中开始调试扩展项目。 然后，在 Visual Studio 的实验实例中使用新的 Web 部件节点。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. 使用管理凭据重启 Visual Studio，然后打开 WebPartNode 解决方案。

2. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，然后将断点添加到 `NodeChildrenRequested` 和 `CreateWebPartNodes` 方法中的第一行代码。

3. 按 F5 键开始调试。

     Visual Studio 将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part Gallery Node Extension for Server Explorer\1.0，并启动 Visual Studio 的实验实例。 你将在此 Visual Studio 实例中测试项目项。

#### <a name="to-test-the-extension"></a>测试扩展

1. 在 Visual Studio 的实验实例中，在菜单栏上选择“查看” > “服务器资源管理器” 。

2. 验证要用于测试的 SharePoint 站点出现在“服务器资源管理器”中的“SharePoint 连接”节点下。  如果未列出，请执行以下步骤：

    1. 打开“SharePoint 连接”的快捷菜单，然后选择“添加连接” 。

    2. 在“添加 SharePoint 连接”对话框中，输入要连接的 SharePoint 站点的 URL，然后选择“确定”按钮 。

         若要在开发计算机上指定 SharePoint 站点，请键入 http://localhost。

3. 展开站点连接节点（显示站点的 URL），然后展开子站点节点（例如，团队站点）。

4. 验证 Visual Studio 的其他实例中的代码是否停在你之前使用 `NodeChildrenRequested` 方法设置的断点处，然后按 F5 键以继续调试项目。

5. 在 Visual Studio 的实验实例中，展开显示在顶级站点节点下的“Web 部件库”节点。

6. 验证 Visual Studio 的其他实例中的代码是否停在你之前使用 `CreateWebPartNodes` 方法设置的断点处，然后按 F5 键以继续调试项目。

7. 在 Visual Studio 的实验实例中，验证连接的站点上的所有 Web 部件是否都显示在“服务器资源管理器”中的“Web 部件库”节点下 。

8. 打开 Web 部件的快捷菜单，然后选择“属性”。

9. 在“属性”窗口中，验证是否显示有关 Web 部件的详细信息。

10. 在“服务器资源管理器”中，打开同一个 Web 部件的快捷菜单，然后选择“显示消息” 。

     在出现的消息框上，选择“确定”按钮。

## <a name="uninstall-the-extension-from-visual-studio"></a>从 Visual Studio 卸载扩展
 完成测试扩展后，请从 Visual Studio 卸载扩展。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在 Visual Studio 的实验实例的菜单栏上，选择“工具” > “扩展和更新” 。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择“服务器资源管理器的 Web 部件库节点”，然后选择“卸载”按钮 。

3. 在出现的对话框中，选择“是”按钮。

4. 选择“立即重新启动”按钮以完成卸载。

     项目项也会卸载。

5. 关闭 Visual Studio 的两个实例（实验实例和打开了 WebPartNode 解决方案的 Visual Studio 实例）。

## <a name="see-also"></a>另请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [创建图标或其他图像（图标的图像编辑器）](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)