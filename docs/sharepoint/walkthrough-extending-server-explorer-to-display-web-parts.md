---
title: 演练：扩展要显示 Web 部件的服务器资源管理器 |Microsoft Docs
titleSuffix: ''
description: 在本演练中，扩展服务器资源管理器以便它在每个连接的 SharePoint 站点上显示 Web 部件库。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint commands
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 7654b6b4f73ea3245cb4d21480eb4db4ceabc648
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148761"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>演练：扩展服务器资源管理器以显示 web 部件
  在 Visual Studio 中，你可以使用 **服务器资源管理器** 的 **SharePoint 连接**"节点来查看 SharePoint 站点上的组件。 但是，默认情况下 **服务器资源管理器** 不显示某些组件。 在本演练中，你将扩展 **服务器资源管理器**，以便它在每个连接的 SharePoint 站点上显示 Web 部件库。

 本演练演示了下列任务：

- 创建通过以下方式扩展 **服务器资源管理器** 的 Visual Studio 扩展：

  - 此扩展在 **服务器资源管理器** 中的每个 SharePoint 网站节点下添加一个 **Web 部件库** 节点。 此新节点包含表示站点上 Web 部件库中的每个 Web 部件的子节点。

  - 扩展定义了表示 Web 部件实例的新节点类型。 此新节点类型是 "新建 **Web 部件库** " 节点下的子节点的基础。 新 Web 部件节点类型在 " **属性** " 窗口中显示有关它所表示的 Web 部件的信息。 节点类型还包括一个自定义快捷菜单项，您可以将其用作执行与 Web 部件相关的其他任务的起点。

- 创建扩展程序集调用的两个自定义 SharePoint 命令。 SharePoint 命令是扩展程序集可以调用的方法，以便在 SharePoint 的服务器对象模型中使用 api。 在本演练中，您将创建用于从开发计算机上的本地 SharePoint 站点检索 Web 部件信息的命令。 有关详细信息，请参阅[调入到 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)中。

- 生成 Visual Studio 扩展 (VSIX) 包以部署扩展。

- 调试和测试扩展。

> [!NOTE]
> 对于本演练的替代版本，该版本使用 SharePoint 的客户端对象模型而不是其服务器对象模型，请参阅[演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="prerequisites"></a>必备条件
 若要完成本演练，开发计算机上需要以下组件：

- Windows、SharePoint 和 Visual Studio 的受支持版本。

- Visual Studio SDK。 本演练使用 SDK 中的 **vsix Project** 模板来创建用于部署项目项的 vsix 包。 有关详细信息，请参阅[Visual Studio 中的扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  以下概念的知识非常有用，但不是必需的，无法完成本演练：

- 使用服务器对象模型进行 SharePoint。 有关详细信息，请参阅[使用 SharePoint Foundation Server-Side 对象模型](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))。

- SharePoint 解决方案中的 Web 部件。 有关详细信息，请参阅[Web 部件概述](/previous-versions/office/ms432401(v=office.14))。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，必须创建三个项目：

- 用于创建 VSIX 包以部署扩展的 VSIX 项目。

- 实现扩展的类库项目。 此项目必须针对 .NET Framework 4.5。

- 一个类库项目，用于定义自定义 SharePoint 命令。 此项目必须以 the.NET Framework 3.5 为目标。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建 Project** " 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**" 节点。

    > [!NOTE]
    > 仅当安装 Visual Studio SDK 时，"**扩展性**" 节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

4. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

5. 选择 " **VSIX Project** " 模板，将项目命名为 " **WebPartNode**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **WebPartNode** 项目添加到 **解决方案资源管理器**。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建 Project**"。

2. 在 "**新建 Project** " 对话框中，展开 " **Visual c #** " 节点或 **Visual Basic** "节点，然后选择" **Windows** "节点。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "4.5** "。

4. 在项目模板列表中，选择 " **类库**"，将项目命名为 " **WebPartNodeExtension**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **WebPartNodeExtension** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

#### <a name="to-create-the-sharepoint-commands-project"></a>创建 SharePoint 命令项目

1. 在 **解决方案资源管理器** 中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建 Project**"。

2. 在 "**新建 Project** " 对话框中，展开 " **Visual c #** " 节点或 **Visual Basic** "节点，然后选择" **Windows** "节点。

3. 在对话框顶部，选择 .NET Framework 的版本列表中 **.NET Framework "3.5** "。

4. 在项目模板列表中，选择 " **类库**"，将项目命名为 " **WebPartCommands**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **WebPartCommands** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 在编写代码以创建扩展之前，你必须添加代码文件和程序集引用，并配置项目设置。

#### <a name="to-configure-the-webpartnodeextension-project"></a>配置 WebPartNodeExtension 项目

1. 在 WebPartNodeExtension 项目中，添加四个具有以下名称的代码文件：

    - SiteNodeExtension

    - WebPartNodeTypeProvider

    - WebPartNodeInfo

    - WebPartCommandIds

2. 打开 **WebPartNodeExtension** 项目的快捷菜单，然后选择 " **添加引用**"。

3. 在 " **引用管理器-WebPartNodeExtension** " 对话框中，选择 " **框架** " 选项卡，然后选中以下每个程序集对应的复选框：

    - System.ComponentModel.Composition

    - System.Windows.Forms

4. 选择 "**扩展**" 选项卡，选中 VisualStudio 的复选框。SharePoint "程序集"，然后选择 "**确定"** 按钮。

5. 在 **解决方案资源管理器** 中，打开 **WebPartNodeExtension** 项目节点的快捷菜单，然后选择 " **属性**"。

     将打开“项目设计器”  。

6. 选择“应用程序”选项卡。

7. 在 " **默认命名空间** " 框中 (c # ) 或 " **根命名空间** " 框 ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) 中，输入 **WebPartNode**。

#### <a name="to-configure-the-webpartcommands-project"></a>配置 webpartcommands 项目

1. 在 WebPartCommands 项目中，添加一个名为 WebPartCommands 的代码文件。

2. 在 **解决方案资源管理器** 中，打开 **WebPartCommands** 项目节点的快捷菜单，选择 " **添加**"，然后选择 " **现有项**"。

3. 在 " **添加现有项** " 对话框中，浏览到包含 WebPartNodeExtension 项目的代码文件的文件夹，然后选择 "WebPartNodeInfo" 和 "WebPartCommandIds" 代码文件。

4. 选择 " **添加** " 按钮旁边的箭头，然后在出现的菜单中选择 " **添加为链接** "。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将代码文件作为链接添加到 WebPartCommands 项目中。 因此，代码文件位于 WebPartNodeExtension 项目中，但文件中的代码也编译在 WebPartCommands 项目中。

5. 再次打开 **WebPartCommands** 项目的快捷菜单，然后选择 " **添加引用**"。

6. 在 " **引用管理器-WebPartCommands** " 对话框中，选择 " **扩展** " 选项卡，选中以下每个程序集对应的复选框，然后选择 " **确定"** 按钮：

    - 微软.SharePoint

    - VisualStudio。SharePoint。命令

7. 在 **解决方案资源管理器** 中，再次打开 **WebPartCommands** 项目的快捷菜单，然后选择 " **属性**"。

     将打开“项目设计器”  。

8. 选择“应用程序”选项卡。

9. 在 " **默认命名空间** " 框中 (c # ) 或 " **根命名空间** " 框 ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) 中，输入 **WebPartNode**。

## <a name="create-icons-for-the-new-nodes"></a>创建新节点的图标
 为 **服务器资源管理器** 扩展创建两个图标： "新建 **Web 部件库** " 节点的图标，以及 " **web 部件库** " 节点下的每个子 Web 部件节点的另一个图标。 稍后在本演练中，你将编写用于将这些图标与节点关联的代码。

#### <a name="to-create-icons-for-the-nodes"></a>创建节点的图标

1. 在 **解决方案资源管理器** 中，打开 **WebPartNodeExtension** 项目的快捷菜单，然后选择 " **属性**"。

2. 将打开“项目设计器”  。

3. 选择" **资源** "选项卡，然后选择" **此项目不包含默认资源文件"。单击此处创建一个** 链接。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建一个资源文件，在设计器中打开它。

4. 在设计器顶部，选择"添加资源"菜单命令旁边的箭头，然后在出现的菜单中选择"添加新图标"。

5. 在" **添加新资源"对话框中** ，将新图标命名 **WebPartsNode**，然后选择"添加 **"** 按钮。

     新图标将在图像编辑器 **中打开**。

6. 编辑图标的 16x16 版本，以便它具有易于识别的设计。

7. 打开图标的 32x32 版本的快捷菜单，然后选择"**删除映像类型"。**

8. 重复步骤 5 到 8，将第二个图标添加到项目资源，并将此图标命名 **为 WebPart**。

9. 在 **解决方案资源管理器** 中，在 **WebPartNodeExtension** 项目的 Resources 文件夹下，打开 **WebPartsNode.ico 的快捷菜单**。

10. 在"**属性**"窗口中，选择"生成操作"旁边的 **箭头，然后在** 出现的菜单中选择"嵌入的资源"。

11. 对 **WebPart.ico** 重复最后两个步骤。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>将"Web 部件库"节点添加到服务器资源管理器
 创建一个类，将新的 Web 部件 **库** 节点添加到每个SharePoint节点。 若要添加新节点，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口。 每当要扩展中现有节点的行为时，服务器资源管理器实现此接口，例如将子节点添加到节点。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>将"Web 部件库"节点添加到服务器资源管理器

1. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，然后将以下代码粘贴到该文件中。

    > [!NOTE]
    > 添加此代码后，项目将发生一些编译错误，但在稍后的步骤中添加代码时，这些错误将消失。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>定义表示 Web 部分的节点类型
 创建一个类，该类定义表示 Web 部件的新类型的节点。 Visual Studio使用此新节点类型在"Web 部件库"节点下 **显示子** 节点。 每个子节点都表示子站点上的一SharePoint部件。

 若要定义新的节点类型，类实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口。 每当想要在 中定义新类型的节点时，都实现此 **服务器资源管理器。**

#### <a name="to-define-the-web-part-node-type"></a>定义 Web 部件节点类型

1. 在 WebPartNodeExtension 项目中，打开 WebPartNodeTypeProvder 代码文件，然后将以下代码粘贴到该文件中。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::

## <a name="define-the-web-part-data-class"></a>定义 Web 部件数据类
 定义一个类，该类包含有关站点中单个 Web 部件SharePoint的数据。 本演练稍后将创建一个自定义 SharePoint 命令，该命令检索有关站点上每个 Web 部件的数据，然后将数据分配给此类的实例。

#### <a name="to-define-the-web-part-data-class"></a>定义 Web 部件数据类

1. 在 WebPartNodeExtension 项目中，打开 WebPartNodeInfo 代码文件，然后将以下代码粘贴到该文件中。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs" id="Snippet3":::

## <a name="define-the-ids-for-the-sharepoint-commands"></a>为命令定义SharePoint的 ID
 定义多个字符串，用于标识自定义SharePoint命令。 你将在此演练的稍后部分实现这些命令。

#### <a name="to-define-the-command-ids"></a>定义命令 ID

1. 在 WebPartNodeExtension 项目中，打开 WebPartCommandIds 代码文件，然后将以下代码粘贴到该文件中。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb" id="Snippet4":::

## <a name="create-the-custom-sharepoint-commands"></a>创建自定义 SharePoint 命令
 创建自定义命令，这些命令调用服务器对象模型SharePoint以检索有关 Web 部件 站点上SharePoint的数据。 每个命令都是一个应用了 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 的方法。

#### <a name="to-define-the-sharepoint-commands"></a>定义SharePoint命令

1. 在 WebPartCommands 项目中，打开 WebPartCommands 代码文件，然后将以下代码粘贴到该文件中。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs" id="Snippet6":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb" id="Snippet6":::

## <a name="checkpoint"></a>Checkpoint
 在此演练中，Web 部件库节点和 SharePoint 命令的所有代码现在都位于项目中。 生成解决方案以确保这两个项目编译时不会出错。

#### <a name="to-build-the-solution"></a>生成解决方案

1. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

    > [!WARNING]
    > 此时，WebPartNode 项目可能有生成错误，因为 VSIX 清单文件没有 Author 值。 在稍后的步骤中添加值时，此错误将消失。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>创建 VSIX 包以部署扩展
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-the-vsix-package"></a>配置 VSIX 包

1. 在 **解决方案资源管理器** 中，在 WebPartNode 项目下，在清单编辑器中打开 **source.extension.vsixmanifest** 文件。

     source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 extension.vsixmanifest 文件的基础。 有关此文件的信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在"**产品名称"** 框中，输入 **Web 部件库节点服务器资源管理器。**

3. 在"**创作"** 框中，输入 **"Contoso"。**

4. 在"**说明"** 框中，**输入"将自定义 Web 部件库"节点添加到"SharePoint连接"节点服务器资源管理器。此扩展使用自定义 SharePoint 命令调用服务器对象模型。**

5. 选择 **编辑器的"** 资产"选项卡，然后选择"新建 **"** 按钮。

     将出现 **"添加新资产** "对话框。

6. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.MefComponent"。**

    > [!NOTE]
    > 此值对应于 `MefComponent` extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[MEFComponent 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))

7. 在"  **源"** 列表中， **选择当前解决方案 中的项目**。

8. 在 **"Project"** 列表中，选择 **"WebPartNodeExtension"，** 然后选择"确定 **"** 按钮。

9. 在清单编辑器中，再次 **选择"新建"** 按钮。

     将出现 **"添加新资产** "对话框。

10. 在"**类型"** 框中，**输入SharePoint。Commands.v4**。

    > [!NOTE]
    > 此元素指定要包括在扩展插件中的Visual Studio扩展。 有关详细信息，请参阅[ASSET Element (VSX Schema) 。 ](/previous-versions/dd393737(v=vs.110))

11. 在" **源"** 列表中，选择 **当前解决方案列表项中的 A** 项目。

12. 在 **"Project"** 列表中，选择 **"WebPartCommands"，** 然后选择"确定 **"** 按钮。

13. 在菜单栏上，选择"**生成** 生成解决方案"，并确保解决方案  >  编译时不会出错。

14. 确保 WebPartNode 项目的生成输出文件夹现在包含 WebPartNode.vsix 文件。

     默认情况下，生成输出文件夹为 。包含项目文件的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-extension"></a>测试扩展
 现在可以在 中测试新的 **Web** 部件 **库服务器资源管理器。** 首先，开始在 Visual Studio 试验实例中调试扩展。 然后，在 **的Web 部件** 实例中，使用新的节点 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

#### <a name="to-start-debugging-the-extension"></a>开始调试扩展

1. 使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 管理凭据重启，然后打开 WebPartNode 解决方案。

2. 在 WebPartNodeExtension 项目中，打开 SiteNodeExtension 代码文件，然后将断点添加到 和 方法的第一行 `NodeChildrenRequested` `CreateWebPartNodes` 代码。

3. 选择 **F5** 键以开始调试。

     Visual Studio将扩展安装到适用于 服务器资源管理器\1.0 的 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web 部件库节点扩展，并启动 Visual Studio 的实验实例。 你将在此实例中测试项目项Visual Studio。

#### <a name="to-test-the-extension"></a>测试扩展

1. 在 的实验实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，在菜单栏上，选择"**查看**  >  **服务器资源管理器"。**

2. 如果要用于测试SharePoint的站点未显示在 服务器资源管理器 中的"连接"节点下 **SharePoint****执行服务器资源管理器：**

    1. 在 **服务器资源管理器** 中，打开"连接SharePoint **菜单**，然后选择"添加 **连接"。**

    2. 在 **"SharePoint** 连接"对话框中，输入要SharePoint站点 URL，然后选择"确定 **"** 按钮。

         若要指定开发SharePoint站点，请输入 **http://localhost** 。

3. 展开显示站点 (URL 的站点连接节点) ，然后展开子站点节点 (例如"团队站点") 。 

4. 验证其他 实例中的代码是否停止在之前在 方法中设置的断点上，然后选择 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] `NodeChildrenRequested` **F5** 以继续调试项目。

5. 在 Visual Studio 实例中，验证顶级站点节点下是否显示名为 **"Web** 部件库"的新节点，然后展开 **"Web 部件库"** 节点。

6. 验证其他 实例中的代码Visual Studio之前在 方法中设置的断点处停止，然后选择 `CreateWebPartNodes` **F5** 键以继续调试项目。

7. 在 Visual Studio 的实验实例中，Web 部件连接站点上的所有项目是否显示在 服务器资源管理器 的"Web **部件库"节点下**。

8. 在 **服务器资源管理器** 中，打开其中一个属性的快捷Web 部件，然后选择"属性 **"。**

9. 在要调试的实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，验证有关 Web 部件的详细信息是否出现在 " **属性** " 窗口中。

## <a name="uninstall-the-extension-from-visual-studio"></a>从 Visual Studio 卸载扩展
 完成扩展测试后，从 Visual Studio 卸载扩展。

#### <a name="to-uninstall-the-extension"></a>卸载扩展

1. 在的实验实例中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，在菜单栏上选择 "**工具**" "  >  **扩展和更新**"。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择 " **Web 部件库" "服务器资源管理器" 的 "Web 部件库" 节点扩展**，然后选择 " **卸载** " 按钮。

3. 在出现的对话框中，选择 " **是"** 按钮，确认要卸载该扩展，然后选择 " **立即重新启动** " 按钮以完成卸载。

4. 关闭实验实例 (Visual Studio 的两个实例，以及在其中) 打开 WebPartNode 解决方案的 Visual Studio 的实例。

## <a name="see-also"></a>请参阅
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：在服务器资源管理器扩展中调入 SharePoint 的客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [为图标 &#40;图像编辑器创建图标或其他图像&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)