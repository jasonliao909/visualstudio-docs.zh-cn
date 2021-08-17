---
title: 使用项模板创建自定义操作项目项，第 1 部分
titleSuffix: ''
description: 使用项模板创建一个项目项，该项目项可添加到 SharePoint 项目，以在 SharePoint 站点上创建自定义操作。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 8662dfb53be04ef86e6587b26ff2897f869939bef2bbdea99c747e3d79145daa
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121385128"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-1"></a>演练：使用项模板创建自定义操作项目项，第 1 部分
  可以通过创建自己的SharePoint项类型Visual Studio扩展项目系统。 本演练将创建一个项目项，该项目项可添加到 SharePoint 项目，以在 SharePoint 站点上创建自定义操作。 自定义操作将菜单项添加到自定义站点的"站点操作"SharePoint菜单中。

 本演练演示了下列任务：

- 创建Visual Studio一个扩展，该扩展定义自定义SharePoint项目项的新类型。 新项目项类型实现多个自定义功能：

  - 一个快捷菜单，作为与项目项相关的其他任务的起始点，例如，在项目中显示自定义Visual Studio。

  - 当开发人员更改项目项及其包含的项目的某些属性时运行的代码。

  - 一个自定义图标，显示在 中项目项 **解决方案资源管理器。**

- 创建Visual Studio项模板。

- 生成VISUAL STUDIO扩展 (VSIX) 包以部署项目项模板和扩展程序集。

- 调试和测试项目项。

  这是独立的演练。 完成本演练后，可以通过向项模板添加向导来增强项目项。 有关详细信息，请参阅 [演练：使用项模板创建自定义操作项目项，第 2 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

> [!NOTE]
> 可以从 [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) 下载演示如何为工作流创建自定义活动的示例。

## <a name="prerequisites"></a>先决条件
 需要开发计算机上以下组件才能完成本演练：

- 支持的 Microsoft Windows、SharePoint 和 Visual Studio 版本。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 本演练使用 **SDK 中的 VSIX Project** 模板创建 VSIX 包来部署项目项。 有关详细信息，请参阅扩展 SharePoint[中的 Visual Studio。](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)

  了解以下概念有助于完成演练，但这不是必需的：

- 自定义操作SharePoint。 有关详细信息，请参阅自定义 [操作](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14))。

- 模板中的项Visual Studio。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，需要创建三个项目：

- VSIX 项目。 此项目创建 VSIX 包以部署SharePoint项目项。

- 项模板项目。 此项目创建一个项模板，该模板可用于将SharePoint项目项添加到SharePoint项目。

- 类库项目。 此项目实现定义Visual Studio项的行为的 SharePoint扩展。

  通过创建项目来开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在"新建Project"对话框顶部的列表中，确保.NET Framework **4.5。**

4. 在"**新建Project"** 对话框中，展开 **Visual C#** 或Visual Basic **节点，** 然后选择"**扩展性"** 节点。

    > [!NOTE]
    > "**扩展性"** 节点仅在安装 Visual Studio SDK 时可用。 有关详细信息，请参阅本主题前面的先决条件部分。

5. 选择 **VSIX Project** 模板。

6. 在" **名称"** 框中，输入 **CustomActionProjectItem**，然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将 **CustomActionProjectItem** 项目添加到 **解决方案资源管理器。**

#### <a name="to-create-the-item-template-project"></a>创建项模板项目

1. 在 **解决方案资源管理器** 中，打开解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。** 

2. 在"新建Project"对话框顶部的列表中，确保.NET Framework **4.5。**

3. 在"**新建Project"** 对话框中，展开 **Visual C#** 或Visual Basic **节点，** 然后选择"**扩展性"** 节点。

4. 在项目模板列表中，选择 **"C#** 项模板"或 **"Visual Basic模板"。**

5. 在" **名称"** 框中，输入 **ItemTemplate**，然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **ItemTemplate** 项目添加到解决方案。

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。** 

2. 在"新建Project"对话框顶部的列表中，确保.NET Framework **4.5。**

3. 在 **"新建Project"** 对话框中，展开 **"Visual C#"** 或Visual Basic节点，选择"Windows"节点，**然后选择**"类 **库**"项目模板。

4. 在" **名称"** 框中，输入 **"ProjectItemDefinition"，** 然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **ProjectItemDefinition** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 在编写代码以定义SharePoint项类型之前，必须添加对扩展项目的代码文件和程序集引用。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 **解决方案资源管理器** 中，打开 **ProjectItemDefinition** 项目的快捷菜单，选择"添加 **"，然后选择**"**新建项"。**

2. 在项目项列表中，选择"代码 **文件"。**

3. 在" **名称** "框中，输入具有相应文件扩展名的名称 **CustomAction，** 然后选择"添加 **"** 按钮。

4. 在 **解决方案资源管理器** 中，打开 **ProjectItemDefinition** 项目的快捷菜单，然后选择"添加 **引用"。**

5. 在" **引用管理器 - ProjectItemDefinition"** 对话框中，选择"程序集 **"** 节点，然后选择" **框架"** 节点。

6. 选中以下每个程序集旁边的复选框：

    - System.ComponentModel.Composition

    - System.Windows.Forms

7. 选择 **"扩展"** 节点，选中 Microsoft.VisualStudio.Sharepoint 程序集旁边的复选框，然后选择"确定 **"** 按钮。

## <a name="define-the-new-sharepoint-project-item-type"></a>定义新的SharePoint项目项类型
 创建实现 接口的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 类，以定义新项目项类型的行为。 每当要定义新类型的项目项时，都实现此接口。

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>定义新的项目SharePoint项类型

1. 在 ProjectItemDefinition 项目中，打开 CustomAction 代码文件。

2. 将此文件中的代码替换为以下代码。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/projectitemtypedefinition/customaction.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/projectitemdefinition/customaction.vb" id="Snippet1":::

## <a name="create-an-icon-for-the-project-item-in-solution-explorer"></a>为项目中的项目项创建解决方案资源管理器
 在项目项SharePoint时，可以将图像 (图标或位图) 与项目项关联。 此图像显示在 中项目 **项解决方案资源管理器。**

 在下面的过程中，你将为项目项创建一个图标，并将该图标嵌入扩展程序集中。 此图标由前面 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute> 创建的 `CustomActionProjectItemTypeProvider` 类的 引用。

#### <a name="to-create-a-custom-icon-for-the-project-item"></a>为项目项创建自定义图标

1. 在 **解决方案资源管理器** 中，打开 **ProjectItemDefinition** 项目的快捷菜单，选择"添加 **"，然后选择**"**新建项..."。**

2. 在项目项列表中，选择"图标 **文件"** 项。

    > [!NOTE]
    > 在Visual Basic中，必须选择"常规 **"** 节点以显示"图标 **文件"** 项。

3. 在" **名称"** 框中， **输入 CustomAction_SolutionExplorer.ico**，然后选择"添加 **"** 按钮。

     新图标将在图像编辑器 **中打开**。

4. 编辑图标文件的 16x16 版本，以便其具有可识别的设计，然后保存图标文件。

5. 在 **解决方案资源管理器** 中，选择 **"CustomAction_SolutionExplorer.ico"。**

6. 在" **属性"** 窗口中，选择"生成操作"属性 **旁边的** 箭头。

7. 在出现的列表中，选择"**嵌入资源"。**

## <a name="checkpoint"></a>Checkpoint
 在演练的此时，项目项的所有代码现在都位于项目中。 生成项目以验证其编译是否未出错。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 打开 **ProjectItemDefinition** 项目的快捷菜单，然后选择 " **生成**"。

## <a name="create-a-visual-studio-item-template"></a>创建 Visual Studio 项模板
 若要使其他开发人员可以使用您的项目项，您必须创建一个项目模板或项模板。 开发人员在 Visual Studio 中使用这些模板，通过创建新的项目或向现有项目中添加项来创建项目项的实例。 对于本演练，请使用 ItemTemplate 项目配置项目项。

#### <a name="to-create-the-item-template"></a>创建项模板

1. 从 ItemTemplate 项目中删除 Class1 代码文件。

2. 在 ItemTemplate 项目中，打开 *itemtemplate .vstemplate* 文件。

3. 将该文件的内容替换为以下 XML，然后保存并关闭该文件。

    > [!NOTE]
    > 以下 XML 适用于 Visual c # 项模板。 如果要创建 Visual Basic 项模板，请将元素的值替换 `ProjectType` 为 `VisualBasic` 。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
      <TemplateData>
        <DefaultName>CustomAction</DefaultName>
        <Name>Custom Action</Name>
        <Description>SharePoint Custom Action by Contoso</Description>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>1000</SortOrder>
        <Icon>ItemTemplate.ico</Icon>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
      <TemplateContent>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\Elements.xml">Elements.xml</ProjectItem>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\SharePointProjectItem.spdata">CustomAction.spdata</ProjectItem>
      </TemplateContent>
    </VSTemplate>
    ```

     此文件定义项模板的内容和行为。 有关此文件的内容的详细信息，请参阅[Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)。

4. 在 **解决方案资源管理器** 中，打开 **ItemTemplate** 项目的快捷菜单，选择 " **添加**"，然后选择 " **新建项**"。

5. 在 " **添加新项** " 对话框中，选择 " **文本文件** " 模板。

6. 在 " **名称** " 框中，输入 **CustomAction. spdata**，然后选择 " **添加** " 按钮。

7. 向 *CustomAction* 文件添加以下 XML，然后保存并关闭该文件。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ProjectItem Type="Contoso.CustomAction" DefaultFile="Elements.xml"
     xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
      <Files>
        <ProjectItemFile Source="Elements.xml" Target="$fileinputname$\" Type="ElementManifest" />
      </Files>
    </ProjectItem>
    ```

     此文件包含有关项目项所包含的文件的信息。 `Type`元素的属性 `ProjectItem` 必须设置为在项目项定义上传递到的相同字符串 (在 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> `CustomActionProjectItemTypeProvider` 本演练前面部分中创建的类) 。 有关 *spdata* 文件的内容的详细信息，请参阅 [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。

8. 在 **解决方案资源管理器** 中，打开 **ItemTemplate** 项目的快捷菜单，选择 " **添加**"，然后选择 " **新建项**"。

9. 在 " **添加新项** " 对话框中，选择 " **XML 文件** " 模板。

10. 在 " **名称** " 框中，输入 **Elements.xml**，然后选择 " **添加** " 按钮。

11. 将 *Elements.xml* 文件的内容替换为以下 XML，然后保存并关闭该文件。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="Replace this with a GUID or some other unique string"
                    GroupId="SiteActions"
                    Location="Microsoft.SharePoint.StandardMenu"
                    Sequence="1000"
                    Title="Replace this with your title"
                    Description="Replace this with your description" >
        <UrlAction Url="~site/Lists/Tasks/AllItems.aspx"/>
      </CustomAction>
    </Elements>
    ```

     此文件定义一个默认自定义操作，该操作可在 SharePoint 站点的 "**站点操作**" 菜单上创建菜单项。 当用户选择菜单项时， `UrlAction` 会在 web 浏览器中打开在元素中指定的 URL。 有关可用于定义自定义操作的 XML 元素的详细信息，请参阅 [自定义操作定义](/sharepoint/dev/schema/custom-action-definition-schema)。

12. （可选）打开 *ItemTemplate .ico* 文件并对其进行修改，使其具有可识别的设计。 此图标将显示在 " **添加新项** " 对话框中的项目项旁边。

13. 在 **解决方案资源管理器** 中，打开 **ItemTemplate** 项目的快捷菜单，然后选择 "**卸载 Project**"。

14. 再次打开 **ItemTemplate** 项目的快捷菜单，然后选择 " **编辑 itemtemplate. .csproj** " 或 " **编辑 .vbproj**"。

15. `VSTemplate`在项目文件中查找以下元素。

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
    ```

16. 将此 `VSTemplate` 元素替换为以下 XML，然后保存并关闭该文件。

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素指定在生成项目时创建项模板的路径中的其他文件夹。 此处指定的文件夹确保项模板仅在客户打开 "**添加新项**" 对话框时可用，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

17. 在 **解决方案资源管理器** 中，打开 **ItemTemplate** 项目的快捷菜单，然后选择 "**重载" Project**。

## <a name="create-a-vsix-package-to-deploy-the-project-item"></a>创建 VSIX 包以部署项目项
 若要部署扩展，请使用解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在 **解决方案资源管理器** 中，在 CustomActionProjectItem 项目中打开 **source.extension.vsixmanifest** 文件的快捷菜单，然后选择 " **打开**"。

     Visual Studio 将在清单编辑器中打开该文件。 Source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 source.extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅 [VSIX 扩展架构1.0 引用](/previous-versions/dd393700(v=vs.110))。

2. 在 "**产品名称**" 框中，输入 **自定义操作 Project 项**。

3. 在 " **作者** " 框中，输入 " **Contoso**"。

4. 在 "**说明**" 框中，输入 **一个表示自定义操作的 SharePoint 项目项**。

5. 在 " **资产** " 选项卡上，选择 " **新建** " 按钮。

     此时将显示 " **添加新资产** " 对话框。

6. 在 " **类型** " 列表中，选择 " **VisualStudio**"。

    > [!NOTE]
    > 此值与 `ItemTemplate` source.extension.vsixmanifest 文件中的元素相对应。 此元素标识 VSIX 包中包含项目项模板的子文件夹。 有关详细信息，请参阅 [ItemTemplate 元素 (VSX Schema) ](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))。

7. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

8. 在 **Project** 列表中，选择 " **ItemTemplate**"，然后选择 **"确定"** 按钮。

9. 在 " **资产** " 选项卡中，再次选择 " **新建** " 按钮。

     此时将显示 " **添加新资产** " 对话框。

10. 在 " **类型** " 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。

    > [!NOTE]
    > 此值与 `MefComponent` source.extension.vsixmanifest 文件中的元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅 [Microsoft.visualstudio.mefcomponent 元素 (VSX Schema) ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

11. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

12. 在 **Project** 列表中，选择 " **ProjectItemDefinition**"。

13. 选择 **“确定”** 按钮。

14. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**"，然后确保项目编译时不会出错。

15. 请确保 CustomActionProjectItem 项目的生成输出文件夹包含 CustomActionProjectItem 文件。

     默认情况下，生成输出文件夹为。包含 CustomActionProjectItem 项目的文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-project-item"></a>测试项目项
 你现在已准备好测试项目项。 首先，开始调试 Visual Studio 的实验实例中的 CustomActionProjectItem 解决方案。 然后，在 Visual Studio 实验实例的 SharePoint 项目中测试 **自定义操作** 项目项。 最后，生成并运行 SharePoint 项目，以验证自定义操作是否按预期方式工作。

#### <a name="to-start-debugging-the-solution"></a>开始调试解决方案

1. 用管理凭据重新启动 Visual Studio，然后打开 CustomActionProjectItem 解决方案。

2. 打开 CustomAction 代码文件，然后将一个断点添加到方法中的第一行代码 `InitializeType` 。

3. 选择 **F5** 键开始调试。

     Visual Studio 将 Project Item\1.0 的扩展安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Custom 操作，并启动 Visual Studio 的实验实例。 你将在 Visual Studio 的此实例中测试项目项。

#### <a name="to-test-the-project-item-in-visual-studio"></a>测试中的项目项 Visual Studio

1. 在 Visual Studio 的实验实例的菜单栏上，选择 "**文件**" "  >  **新建**  >  **Project**"。

2. 展开 " **Visual c #** " 或 " **Visual Basic** (，具体取决于项模板支持的语言) ，展开" **SharePoint**"，然后选择" **2010** "节点。

3. 在项目模板列表中，选择 **SharePoint 2010 Project**。

4. 在 " **名称** " 框中，输入 **CustomActionTest**，然后选择 " **确定"** 按钮。

5. 在 " **SharePoint 自定义向导**" 中，输入要用于调试的站点的 URL，然后选择 "**完成**" 按钮。

6. 在 **解决方案资源管理器** 中，打开项目节点的快捷菜单，选择 " **添加**"，然后选择 " **新建项**"。

7. 在 "**添加新项**" 对话框中，选择 " **SharePoint** " 节点下的 " **2010** " 节点。

     验证 **自定义操作** 项是否显示在项目项的列表中。

8. 选择 " **自定义操作** " 项，然后选择 " **添加** " 按钮。

     Visual Studio 会将名为 **CustomAction1** 的项添加到项目中，并在编辑器中打开 *Elements.xml* 文件。

9. 验证 Visual Studio 的另一个实例中的代码在您之前在方法中设置的断点处停止 `InitializeType` 。

10. 选择 **F5** 键以继续调试项目。

11. 在 Visual Studio 的实验实例的 **解决方案资源管理器** 中，打开 **CustomAction1** 节点的快捷菜单，然后选择 "**查看自定义操作设计器**"。

12. 确认出现消息框，然后选择 **"确定"** 按钮。

     您可以使用此快捷菜单为开发人员提供其他选项或命令，例如，为自定义操作显示设计器。

13. 在菜单栏上，选择 "**查看**  >  **输出**"。

     此时将打开 " **输出** " 窗口。

14. 在 **解决方案资源管理器** 中，打开 **CustomAction1** 项目的快捷菜单，然后将其名称更改为 **MyCustomAction**。

     在 " **输出** " 窗口中，将显示一条确认消息。 此消息由 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemNameChanged> 您在类中定义的事件处理程序来编写 `CustomActionProjectItemTypeProvider` 。 开发人员修改项目项时，可以处理此事件和其他项目项事件来实现自定义行为。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>测试自定义操作SharePoint

1. 在 myCustomAction Visual Studio实例中，Elements.xml **MyCustomAction** 项目项的子级文件。

2. 在 *Elements.xml* 文件中，进行以下更改，然后保存该文件：

    - 在 `CustomAction` 元素中，将 属性设置为 GUID 或其他一些唯一 `Id` 字符串，如以下示例所示：

        ```xml
        Id="cd85f6a7-af2e-44ab-885a-0c795b52121a"
        ```

    - 在 `CustomAction` 元素中， `Title` 设置 属性，如以下示例所示：

        ```xml
        Title="SharePoint Developer Center"
        ```

    - 在 `CustomAction` 元素中， `Description` 设置 属性，如以下示例所示：

        ```xml
        Description="Opens the SharePoint Developer Center Web site."
        ```

    - 在 `UrlAction` 元素中， `Url` 设置 属性，如以下示例所示：

        ```xml
        Url="https://docs.microsoft.com/sharepoint/dev/"
        ```

3. 选择 F5。

     自定义操作打包并部署到SharePoint的"站点 **URL"属性中** 指定的站点。 Web 浏览器将打开此站点的默认页面。

    > [!NOTE]
    > 如果显示 **"脚本调试已禁用** "对话框，请选择" **是** "按钮以继续调试项目。

4. 在"**站点操作**"菜单上 **，SharePoint** 开发人员中心"，验证浏览器是否打开了网站 https://docs.microsoft.com/sharepoint/dev/ ，然后关闭 Web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成项目项测试后，从项目的实验实例中删除项目项Visual Studio。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio实验实例的菜单栏上，选择"**工具**  >  **扩展和更新"。**

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择"自定义操作 **Project项"，** 然后选择"**卸载"** 按钮。

3. 在出现的对话框中，选择" **是"** 按钮以确认要卸载扩展。

4. 选择" **立即重启** "按钮以完成卸载。

5. 关闭 Visual Studio实验实例和 CustomActionProjectItem 解决方案打开的实例。

## <a name="next-steps"></a>后续步骤
 完成本演练后，可以将向导添加到项模板。 当用户将自定义操作项目项添加到 SharePoint 项目时，向导将收集有关操作 (的信息，例如其位置和在选择操作) 时要导航到的 URL，并将此信息添加到新项目项中的 *Elements.xml* 文件。 有关详细信息，请参阅 [演练：使用项模板创建自定义操作项目项，第 2 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

## <a name="see-also"></a>请参阅

- [演练：使用项模板创建自定义操作项目项，第 2 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为项目项创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [使用SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [在图标图像编辑器&#40;图标编辑器创建图标或其他&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)