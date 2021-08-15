---
title: 使用项目模板创建站点列项目项，第 2 部分
titleSuffix: ''
description: 向站点列项目模板添加向导，以在使用模板创建包含项目项的 SharePoint项目时从用户收集数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], creating template wizards
- SharePoint project items, creating template wizards
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c4530a43787b2e29c2600476a44c808132d668ceaa89b851efeddd403c2c30e6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352808"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>演练：使用项目模板创建站点列项目项，第 2 部分
  定义项目项的自定义SharePoint并将其与 Visual Studio 中的项目模板关联后，可能还需要为模板提供向导。 当用户使用模板创建包含项目项的新项目时，可以使用向导从用户收集信息。 收集的信息可用于初始化项目项。

 在此演练中，你将向"站点列"项目模板添加一个向导，该模板在演练：使用模板创建站点列Project项第[1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)部分Project演示。 当用户创建站点列项目时，向导将收集有关站点列 (例如其基类型和组) 的信息，并将此信息添加到新项目中的 *Elements.xml* 文件。

 本演练演示了下列任务：

- 为自定义模板创建SharePoint与项目模板关联的项目项类型。

- 定义一个自定义向导 UI，该 UI 类似于 SharePoint 项目中的内置Visual Studio。

- 创建两 *SharePoint，* 用于在向导运行时调用本地 SharePoint 站点。 SharePoint命令是一些扩展Visual Studio调用 SharePoint 对象模型中的 API 的方法。 有关详细信息，请参阅调用[对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 使用可替换参数SharePoint向导中收集的数据初始化项目文件。

- 在每个新的站点列项目实例中创建新的 .snk 文件。 此文件用于对项目输出进行签名，以便SharePoint程序集部署到全局程序集缓存。

- 调试和测试向导。

> [!NOTE]
> 有关一系列示例工作流，请参阅SharePoint[示例](/sharepoint/dev/general-development/sharepoint-workflow-samples)。

## <a name="prerequisites"></a>必备条件
 若要执行本演练，必须先完成演练：使用 Project 模板创建站点列 Project 项（第[1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)部分）来创建 SiteColumnProjectItem 解决方案。

 还需要开发计算机上以下组件才能完成本演练：

- 支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的 **VSIX Project** 模板创建 VSIX 包来部署项目项。 有关详细信息，请参阅扩展 SharePoint[中的 Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)工具。

  了解以下概念有助于完成演练，但这不是必需的：

- 项目中项目和项模板的Visual Studio。 有关详细信息，请参阅[如何：将向导与Project和](../extensibility/how-to-use-wizards-with-project-templates.md) <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口一起使用。

- 站点列中的SharePoint。 有关详细信息，请参阅 [列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))。

## <a name="understand-the-wizard-components"></a>了解向导组件
 本演练中演示的向导包含多个组件。 下表介绍了这些组件。

|组件|说明|
|---------------|-----------------|
|向导实现|这是一个名为 的类 `SiteColumnProjectWizard` ，它实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口。 此接口定义在向导Visual Studio完成时，以及向导运行时某些时间调用的方法。|
|向导 UI|这是一个名为 的基于 WPF 的窗口 `WizardWindow` 。 此窗口包括名为 和 的两个用户 `Page1` 控件 `Page2` 。 这些用户控件表示向导的两页。<br /><br /> 在此演练中，向导 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 实现的方法显示向导 UI。|
|向导数据模型|这是一个名为 的中间类 `SiteColumnWizardModel` ，它提供向导 UI 和向导实现之间的层。 此示例使用此类帮助抽象化向导实现和向导 UI;此类不是所有向导的必需组件。<br /><br /> 在此演练中，向导实现在显示向导 UI 时 `SiteColumnWizardModel` 将 对象传递给向导窗口。 向导 UI 使用此对象的方法在 UI 中保存控件的值，并执行验证输入站点 URL 是否有效的任务。 用户完成向导后，向导实现将使用 `SiteColumnWizardModel` 对象来确定 UI 的最终状态。|
|Project签名管理器|这是一个名为 的帮助程序类，向导实现使用该类在每个新项目实例中创建新的 `ProjectSigningManager` key.snk 文件。|
|SharePoint 命令|这些是向导数据模型用于在向导运行时调用本地SharePoint站点的方法。 由于SharePoint命令必须面向 .NET Framework 3.5，因此这些命令在向导代码的其余部分不同的程序集中实现。|

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，需要将多个项目添加到在演练：使用项目模板创建站点列项目项（第 [1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)部分）中创建的 SiteColumnProjectItem 解决方案：

- WPF 项目。 你将实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，并在此项目中定义向导 UI。

- 一个类库项目，用于定义SharePoint命令。 此项目必须面向 the.NET Framework 3.5。

  通过创建项目来开始演练。

#### <a name="to-create-the-wpf-project"></a>创建 WPF 项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，打开 SiteColumnProjectItem 解决方案。

2. 在 **解决方案资源管理器** 中，打开 **SiteColumnProjectItem** 解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。**

3. 在"添加新版本Project"对话框的顶部，确保在 .NET Framework 版本列表中选择 **4.5** .NET Framework。 

4. 展开 **Visual C#** 节点 **或Visual Basic节点**，**然后选择Windows节点**。

5. 在项目模板列表中，选择 **"WPF 用户控制** 库"，将项目命名 **"ProjectTemplateWizard"，** 然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **ProjectTemplateWizard** 项目添加到解决方案，并打开默认的 UserControl1.xaml 文件。

6. 从项目中删除 UserControl1.xaml 文件。

#### <a name="to-create-the-sharepoint-commands-project"></a>创建 SharePoint 命令项目

1. 在 **解决方案资源管理器** 中，打开 SiteColumnProjectItem 解决方案节点的快捷菜单，选择"添加"，然后选择"新建 **Project"。**

2. 在"**添加新版本Project** 对话框的顶部，.NET Framework版本列表中选择 **"3.5".NET Framework。**

3. 展开 **Visual C#** 节点或 **Visual Basic节点，****然后选择Windows节点**。

4. 选择类 **库** 项目模板，将项目命名 **SharePointCommands**，然后选择"确定 **"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **SharePointCommands** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 创建向导之前，必须将一些代码文件和程序集引用添加到项目。

#### <a name="to-configure-the-wizard-project"></a>配置向导项目

1. 在 **解决方案资源管理器** 中，打开 **ProjectTemplateWizard** 项目节点的快捷菜单，然后选择"属性 **"。**

2. 在 Project **设计器** 中，为 Visual  C# 项目选择"应用程序"选项卡，或为项目选择"Visual Basic"选项卡。

3. 请确保目标框架设置为 .NET Framework 4.5，而不是 .NET Framework 4.5 客户端配置文件。

     有关详细信息，请参阅[如何：面向](../ide/visual-studio-multi-targeting-overview.md)版本.NET Framework。

4. 打开 **ProjectTemplateWizard 项目的快捷菜单，选择**"**添加**"，然后选择"**新建项"。**

5. 选择" **窗口 (WPF)** 项，将项 **命名 WizardWindow**，然后选择"添加 **"** 按钮。

6. 将两 **个用户控件 (WPF)** 项目，并命名 **Page1** 和 **Page2。**

7. 将四个代码文件添加到项目，并赋予它们以下名称：

    - SiteColumnProjectWizard

    - SiteColumnWizardModel

    - ProjectSigningManager

    - CommandIds

8. 打开 **ProjectTemplateWizard** 项目节点的快捷菜单，然后选择"**添加引用"。**

9. 展开 **"程序集"** 节点，选择"扩展 **"** 节点，然后选择以下程序集旁边的复选框：

    - EnvDTE

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio。SharePoint

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.Shell.Interop.10.0

    - Microsoft.VisualStudio.Shell.Interop.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

10. 选择 " **确定"** 按钮，将程序集添加到项目。

11. 在 **解决方案资源管理器** 的 **ProjectTemplateWizard** 项目的 "**引用**" 文件夹下，选择 " **EnvDTE**"。

12. 在 " **属性** " 窗口中，将 " **嵌入互操作类型** " 属性的值更改为 " **False**"。

13. 如果要开发 Visual Basic 项目，请使用 **Project 设计器** 将 ProjectTemplateWizard 命名空间导入项目中。

     有关详细信息，请参阅[如何：添加或移除导入的命名空间 &#40;Visual Basic&#41;](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)。

#### <a name="to-configure-the-sharepointcommands-project"></a>配置 SharePointcommands 项目

1. 在 **解决方案资源管理器** 中，选择 " **SharePointCommands** " 项目节点。

2. 在菜单栏上，选择 " **Project**" "**添加现有项**"。

3. 在 " **添加现有项** " 对话框中，浏览到包含 ProjectTemplateWizard 项目的代码文件的文件夹，然后选择 " **CommandIds** " 代码文件。

4. 选择 " **添加** " 按钮旁边的箭头，然后在出现的菜单上选择 " **添加为链接** " 选项。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将代码文件作为链接添加到 **SharePointCommands** 项目。 代码文件位于 **ProjectTemplateWizard** 项目中，但文件中的代码也在 **SharePointCommands** 项目中编译。

5. 在 **SharePointCommands** 项目中，添加另一个名为命令的代码文件。

6. 选择 SharePointCommands 项目，然后在菜单栏上选择 **Project**  >  **添加引用**"。

7. 展开 " **程序集** " 节点，选择 " **扩展** " 节点，然后选中以下程序集旁的复选框：

    - 微软.SharePoint

    - VisualStudio。SharePoint。命令

8. 选择 " **确定"** 按钮，将程序集添加到项目。

## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>创建向导模型、签名管理器和 SharePoint 命令 id
 将代码添加到 ProjectTemplateWizard 项目，以实现示例中的以下组件：

- SharePoint 的命令 id。 这些字符串标识向导使用的 SharePoint 命令。 稍后在本演练中，您将向 SharePointCommands 项目添加代码以实现这些命令。

- 向导数据模型。

- 项目签名管理器。

  有关这些组件的详细信息，请参阅 [了解向导组件](#understand-the-wizard-components)。

#### <a name="to-define-the-sharepoint-command-ids"></a>定义 SharePoint 命令 id

1. 在 ProjectTemplateWizard 项目中，打开 CommandIds 代码文件，并将此文件的全部内容替换为以下代码。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs" id="Snippet5":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb" id="Snippet5":::

#### <a name="to-create-the-wizard-model"></a>创建向导模型

1. 打开 SiteColumnWizardModel 代码文件，并将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb" id="Snippet6":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs" id="Snippet6":::

#### <a name="to-create-the-project-signing-manager"></a>创建项目签名管理器

1. 打开 ProjectSigningManager 代码文件，并将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb" id="Snippet8":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs" id="Snippet8":::

## <a name="create-the-wizard-ui"></a>创建向导 UI
 添加 XAML 以定义向导窗口的 UI 和两个为向导页提供 UI 的用户控件，并添加代码以定义窗口和用户控件的行为。 你创建的向导与 Visual Studio 中的 SharePoint 项目的内置向导类似。

> [!NOTE]
> 在下面的步骤中，你的项目将在你将 XAML 或代码添加到你的项目后出现一些编译错误。 当你在后续步骤中添加代码时，这些错误将消失。

#### <a name="to-create-the-wizard-window-ui"></a>创建向导窗口 UI

1. 在 ProjectTemplateWizard 项目中，打开 WizardWindow 文件的快捷菜单，然后选择 " **打开** " 以在设计器中打开该窗口。

2. 在设计器的 "XAML" 视图中，将当前 XAML 替换为以下 XAML。 XAML 定义了一个 UI，其中包含一个标题、一个 <xref:System.Windows.Controls.Grid> 包含向导页的和一个导航按钮。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml" id="Snippet10":::

    > [!NOTE]
    > 在此 XAML 中创建的窗口派生自 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基类。 当您将自定义 WPF 对话框添加到 Visual Studio 时，我们建议您从此类派生对话框，以便与其他 Visual Studio 对话框保持一致的样式，并避免出现可能出现的模式对话框问题。 有关详细信息，请参阅 [创建和管理模式对话框](../extensibility/creating-and-managing-modal-dialog-boxes.md)。

3. 如果要开发 Visual Basic 项目，请 `ProjectTemplateWizard` 从 `WizardWindow` 元素的属性中的类名称中删除该命名空间 `x:Class` `Window` 。 此元素位于 XAML 的第一行。 完成后，第一行应如下例所示。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. 打开 WizardWindow 文件的代码隐藏文件。

5. 将此文件的内容替换为 `using` 以下代码，但文件顶部的声明除外。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb" id="Snippet4":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs" id="Snippet4":::

#### <a name="to-create-the-first-wizard-page-ui"></a>创建第一个向导页 UI

1. 在 ProjectTemplateWizard 项目中，打开 "Page1" 文件的快捷菜单，然后选择 " **打开** " 以在设计器中打开该用户控件。

2. 在设计器的 "XAML" 视图中，将当前 XAML 替换为以下 XAML。 XAML 定义了一个 UI，其中包含一个文本框，用户可以在其中输入要用于调试的本地网站的 URL。 UI 还包括选项按钮，用户可通过这些按钮指定是否对项目进行沙盒处理。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml" id="Snippet11":::

3. 如果要开发 Visual Basic 项目，请 `ProjectTemplateWizard` `Page1` 在元素的属性中从类名称中删除该命名空间 `x:Class` `UserControl` 。 这位于 XAML 的第一行。 完成后，第一行应该如下所示。

    ```xml
    <UserControl x:Class="Page1"
    ```

4. 将 Page1 文件的内容替换为除文件顶部的声明之外的内容， `using` 并提供以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs" id="Snippet2":::

#### <a name="to-create-the-second-wizard-page-ui"></a>创建第二个向导页 UI

1. 在 ProjectTemplateWizard 项目中，打开 Page2 文件的快捷菜单，然后选择 " **打开**"。

     用户控件将在设计器中打开。

2. 在 XAML 视图中，将当前 XAML 替换为以下 XAML。 XAML 定义了一个 UI，该 UI 包含一个下拉列表，用于选择网站列的基类型、用于指定在库中显示 "网站" 列的内置或自定义组的组合框以及用于指定网站列名称的文本框。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml" id="Snippet12":::

3. 如果要开发 Visual Basic 项目，请 `ProjectTemplateWizard` `Page2` 在元素的属性中从类名称中删除该命名空间 `x:Class` `UserControl` 。 这位于 XAML 的第一行。 完成后，第一行应该如下所示。

    ```xml
    <UserControl x:Class="Page2"
    ```

4. 将 Page2 文件的代码隐藏文件的内容替换为除文件顶部的声明之外的代码， `using` 并提供以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs" id="Snippet3":::

## <a name="implement-the-wizard"></a>实现向导
 通过实现接口，定义向导的主要功能 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 。 此接口定义在向导启动和完成时 Visual Studio 调用的方法，以及在向导运行时的特定时间。

#### <a name="to-implement-the-wizard"></a>实现向导

1. 在 ProjectTemplateWizard 项目中，打开 SiteColumnProjectWizard 代码文件。

2. 将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs" id="Snippet7":::

## <a name="create-the-sharepoint-commands"></a>创建 SharePoint 命令
 创建两个调用 SharePoint 服务器对象模型的自定义命令。 一个命令确定用户在向导中键入的网站 URL 是否有效。 另一个命令获取指定 SharePoint 站点中的所有字段类型，以便用户可以选择要用作其新网站列的基础的字段类型。

#### <a name="to-define-the-sharepoint-commands"></a>定义 SharePoint 命令

1. 在 **SharePointCommands** 项目中，打开命令代码文件。

2. 将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb" id="Snippet9":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs" id="Snippet9":::

## <a name="checkpoint"></a>Checkpoint
 在本演练的这一阶段，向导的所有代码现在都在项目中。 生成项目以确保它在编译时不会出错。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

## <a name="removing-the-keysnk-file-from-the-project-template"></a>从项目模板删除密钥 .snk 文件
 [演练：使用项目模板创建网站栏项目项（第1部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)）你创建的项目模板包含一个用于对每个网站列项目实例进行签名的 .snk 文件。 此密钥 .snk 文件不再是必需的，因为向导现在为每个项目生成新的密钥 .snk 文件。 从项目模板中删除密钥 .snk 文件，并删除对此文件的引用。

#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>从项目模板中删除密钥 .snk 文件

1. 在 **解决方案资源管理器** 的 " **SiteColumnProjectTemplate** " 节点下，打开 " **密钥 .snk** " 文件的快捷菜单，然后选择 " **删除**"。

2. 在随即出现的确认对话框中，选择 **“确定”** 按钮。

3. 在 **SiteColumnProjectTemplate** 节点下，打开 SiteColumnProjectTemplate 文件，然后从其删除以下元素。

    ```xml
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
    ```

4. 保存并关闭该文件。

5. 在 **SiteColumnProjectTemplate** 节点下，打开 ProjectTemplate 或 ProjectTemplate 文件，然后从中删除以下 `PropertyGroup` 元素。

    ```xml
    <PropertyGroup>
      <SignAssembly>true</SignAssembly>
      <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
    </PropertyGroup>
    ```

6. 删除以下 `None` 元素。

    ```xml
    <None Include="key.snk" />
    ```

7. 保存并关闭该文件。

## <a name="associating-the-wizard-with-the-project-template"></a>将向导与项目模板关联
 现在，你已实现向导，你必须将该向导与 " **网站列** " 项目模板相关联。 要执行此操作，必须完成三个过程：

1. 使用强名称对向导程序集进行签名。

2. 获取向导程序集的公钥标记。

3. 在 **网站列** 项目模板的 .vstemplate 文件中添加对向导程序集的引用。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>使用强名称对向导程序集进行签名

1. 在 **解决方案资源管理器** 中，打开 **ProjectTemplateWizard** 项目的快捷菜单，然后选择 " **属性**"。

2. 在“签名”选项卡上，选中“为程序集签名”复选框。

3. 在 " **选择强名称密钥文件** " 列表中，选择 **\<New...>** 。

4. 在 " **创建强名称密钥** " 对话框中，输入新密钥文件的名称，清除 " **使用密码保护密钥文件** " 复选框，然后选择 " **确定"** 按钮。

5. 打开 **ProjectTemplateWizard** 项目的快捷菜单，然后选择 " **生成** " 以创建 ProjectTemplateWizard.dll 文件。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>获取向导程序集的公钥标记

1. 在 "**开始" 菜单** 上，选择 "**所有程序**"，选择 " **Microsoft Visual Studio**"，选择 " **Visual Studio Tools**"，然后选择 "**开发人员命令提示**"。

     此时将打开 Visual Studio 命令提示符窗口。

2. 运行以下命令，将 *PathToWizardAssembly* 替换为开发计算机上 ProjectTemplateWizard 项目的生成的 ProjectTemplateWizard.dll 程序集的完整路径：

    ```cmd
    sn.exe -T PathToWizardAssembly
    ```

     将 ProjectTemplateWizard.dll 程序集的公钥标记写入 Visual Studio 命令提示符 "窗口。

3. 使 Visual Studio 命令提示符窗口保持打开状态。 在下一个过程中，你将需要公钥标记。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>向 .vstemplate 文件中的向导程序集添加引用

1. 在 **解决方案资源管理器** 中，展开 " **SiteColumnProjectTemplate** " 项目节点并打开 "SiteColumnProjectTemplate" 文件。

2. 在文件末尾附近， `WizardExtension` 在和标记之间添加以下元素 `</TemplateContent>` `</VSTemplate>` 。 将属性的 *标记* 值替换 `PublicKeyToken` 为你在上一过程中获取的公钥标记。

    ```xml
    <WizardExtension>
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>
    </WizardExtension>
    ```

     有关元素的详细信息 `WizardExtension` ，请参阅[WizardExtension 元素 &#40;Visual Studio 模板&#41;](../extensibility/wizardextension-element-visual-studio-templates.md)。

3. 保存并关闭该文件。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>将可替换参数添加到项目模板中的 Elements.xml 文件
 将多个可替换参数添加到 SiteColumnProjectTemplate 项目中的 *Elements.xml* 文件。 这些参数在 `RunStarted` 之前定义的类的方法中进行初始化 `SiteColumnProjectWizard` 。 当用户创建网站列项目时，Visual Studio 会自动将新项目中的 *Elements.xml* 文件中的这些参数替换为在向导中指定的值。

 可替换参数是以美元符号 ($) 字符开头和结尾的令牌。 除了定义你自己的可替换参数外，还可以使用由 SharePoint 项目系统定义和初始化的内置参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>向 Elements.xml 文件添加可替换参数

1. 在 SiteColumnProjectTemplate 项目中，将 *Elements.xml* 文件的内容替换为以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
             Name="$fieldname$"
             DisplayName="$fieldname$"
             Type="$selectedfieldtype$"
             Group="$selectedgrouptype$">
      </Field>
    </Elements>
    ```

     新 XML 会将 `Name` 、 `DisplayName` 、和属性的值更改 `Type` `Group` 为自定义的可替换参数。

2. 保存并关闭该文件。

## <a name="add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包
 若要用包含 "网站列" 项目模板的 VSIX 包部署向导，请将对向导项目和 SharePoint 命令项目的引用添加到 vsix 项目中的 source.extension.vsixmanifest 文件。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包

1. 在 **解决方案资源管理器** 的 **SiteColumnProjectItem** 项目中，打开 **source.extension.vsixmanifest** 文件的快捷菜单，然后选择 " **打开**"。

     Visual Studio 将在清单编辑器中打开该文件。

2. 在编辑器的 " **资产** " 选项卡上，选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

3. 在 " **类型** " 列表中，选择 " **VisualStudio**"。

4. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

5. 在 **Project** 列表中，选择 " **ProjectTemplateWizard**"，然后选择 "**确定"** 按钮。

6. 在编辑器的 " **资产** " 选项卡上，再次选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

7. 在 "**类型**" 列表中，输入 **SharePoint。命令。**

8. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

9. 在 **Project** 列表中，选择 " **SharePointCommands** " 项目，然后选择 "**确定"** 按钮。

10. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**"，然后确保解决方案生成时没有错误。

## <a name="test-the-wizard"></a>测试向导
 你现在已准备好测试向导。 首先，开始调试 Visual Studio 的实验实例中的 SiteColumnProjectItem 解决方案。 然后，在 Visual Studio 的实验实例中测试网站列项目的向导。 最后，生成并运行项目，以验证网站列是否按预期方式工作。

#### <a name="to-start-debugging-the-solution"></a>开始调试解决方案

1. 用管理凭据重新启动 Visual Studio，然后打开 SiteColumnProjectItem 解决方案。

2. 在 ProjectTemplateWizard 项目中，打开 SiteColumnProjectWizard 代码文件，然后向方法中的第一个代码行添加一个断点 `RunStarted` 。

3. 在菜单栏上，选择 "**调试**  >  **异常**"。

4. 在 "**异常**" 对话框中，确保清除了 "**公共语言运行时异常****引发** 的和 **用户未处理** 的" 复选框，然后选择 **"确定"** 按钮。

5. 选择 **F5** 键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"，开始调试。

     Visual Studio 会将扩展安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0，并启动 Visual Studio 的实验实例。 你将在 Visual Studio 的此实例中测试项目项。

#### <a name="to-test-the-wizard-in-visual-studio"></a>在 Visual Studio 中测试向导

1. 在 Visual Studio 的实验实例的菜单栏上，选择 "**文件**" "  >  **新建**  >  **Project**"。

2. 展开 " **Visual c #** " 节点或 **Visual Basic** "节点 (根据项目模板支持的语言) ，展开" **SharePoint** "节点，然后选择" **2010** "节点。

3. 在项目模板列表中，选择 " **网站列**"，将项目命名为 " **SiteColumnWizardTest**"，然后选择 **"确定"** 按钮。

4. 验证 Visual Studio 的另一个实例中的代码在您之前在方法中设置的断点处停止 `RunStarted` 。

5. 通过选择 **F5** 键，或在菜单栏上选择 "**调试** 继续"，继续调试项目  >  。

6. 在 " **SharePoint 自定义向导**" 中，输入要用于调试的站点的 URL，然后选择 "**下一步**" 按钮。

7. 在 **SharePoint 自定义向导** 的第二页中，进行以下选择：

   - 在 " **类型** " 列表中，选择 " **布尔**"。

   - 在 " **组** " 列表中，选择 **"自定义是/否列**"。

   - 在 " **名称** " 框中，输入 **"是/否" 列**，然后选择 " **完成** " 按钮。

     在 **解决方案资源管理器** 中，会显示一个新项目，其中包含名为 **Field1** 的项目项，Visual Studio 在编辑器中打开该项目的 *Elements.xml* 文件。

8. 验证 *Elements.xml* 是否包含你在向导中指定的值。

#### <a name="to-test-the-site-column-in-sharepoint"></a>测试中的 "站点" 列 SharePoint

1. 在 Visual Studio 的实验实例中，选择 **F5** 键。

     "网站" 列将打包并部署到 "**网站 URL** " 属性指定的 SharePoint 站点。 Web 浏览器将打开此站点的默认页面。

    > [!NOTE]
    > 如果出现 " **脚本调试已禁用** " 对话框，请选择 " **是"** 按钮继续调试项目。

2. 在 "**站点操作**" 菜单上，选择 "**站点设置**"。

3. 在 "站点设置" 页上的 "**库**" 下，选择 "**网站列**" 链接。

4. 在站点列列表中，验证 **自定义的 "是/否" 列** 组是否包含名为 **"是/否" 列** 的列，然后关闭 web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成项目项测试后，从 Visual Studio 的实验实例中删除项目模板。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**工具**" "  >  **扩展和更新**"。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择 " **网站列**"，然后选择 " **卸载** " 按钮。

3. 在出现的对话框中，选择 " **是"** 按钮，确认要卸载该扩展，然后选择 " **立即重新启动** " 按钮以完成卸载。

4. 关闭 Visual Studio 的实验实例和在其中打开 CustomActionProjectItem 解决方案的实例。

     有关如何部署扩展的信息 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，请参阅[装运 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

## <a name="see-also"></a>另请参阅
- [演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
