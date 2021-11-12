---
title: 使用项目模板创建网站栏项目项（第 2 部分）
titleSuffix: ''
description: 向网站栏项目模板添加向导，以便在用户使用该模板创建包含项目项的 SharePoint 项目时从用户那里收集数据。
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
ms.openlocfilehash: f82d6ca09e67cd2911a0dc9803e65f14b85cca6c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665273"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>演练：使用项目模板创建网站栏项目项（第 2 部分）
  定义了自定义类型的 SharePoint 项目项并将它与 Visual Studio 中的项目模板相关联后，你可能还需要为模板提供一个向导。 可以使用该向导在用户使用你的模板创建包含项目项的新项目时从他们那里收集信息。 收集的信息可用于初始化项目项。

 在本演练中，你将向[演练：使用项目模板创建网站栏项目（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)中演示的网站栏项目模板添加向导。 在用户创建网站栏项目时，该向导会收集有关网站栏的信息（例如基类型和组）并将此信息添加到新项目中的 Elements.xml 文件中。

 本演练演示了下列任务：

- 为与项目模板关联的自定义 SharePoint 项目项类型创建向导。

- 定义类似于 Visual Studio 中 SharePoint 项目内置向导的自定义向导 UI。

- 创建两个 SharePoint 命令，用于在向导运行期间调入本地 SharePoint 站点。 SharePoint 命令是可供 Visual Studio 扩展用来调用 SharePoint 服务器对象模型中的 API 的方法。 有关详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 使用可替换参数通过在向导中收集的数据来初始化 SharePoint 项目文件。

- 在每个新的网站栏项目实例中创建一个新的 .snk 文件。 此文件用于对项目输出进行签名，以便可以将 SharePoint 解决方案程序集部署到全局程序集缓存。

- 调试和测试向导。

> [!NOTE]
> 有关一系列示例工作流，请参阅 [SharePoint 工作流示例](/sharepoint/dev/general-development/sharepoint-workflow-samples)。

## <a name="prerequisites"></a>先决条件
 若要进行本演练，必须首先完成[演练：使用项目模板创建网站栏项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)以创建 SiteColumnProjectItem 解决方案。

 还需要在开发计算机上使用以下组件来完成本演练：

- 受支持版本的 Windows、SharePoint 和 Visual Studio。

- Visual Studio SDK。 本演练使用 SDK 中的“VSIX 项目”模板来创建用于部署项目项的 VSIX 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念将很有用，但对于完成本演练来说，并不是必需的：

- Visual Studio 中项目和项模板的向导。 有关详细信息，请参阅[操作说明：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)和 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口。

- SharePoint 中的网站栏。 有关详细信息，请参阅[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))。

## <a name="understand-the-wizard-components"></a>了解向导组件
 本演练中演示的向导包含多个组件。 下表介绍了这些组件。

|组件|说明|
|---------------|-----------------|
|向导实现|这是名为 `SiteColumnProjectWizard` 的类，用于实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口。 此接口定义 Visual Studio 在向导启动和完成时以及在向导运行时的特定时间调用的方法。|
|向导 UI|这是一个基于 WPF 的窗口，名为 `WizardWindow`。 此窗口包含两个名为 `Page1` 和 `Page2` 的用户控件。 这些用户控件表示向导的两个页面。<br /><br /> 在本演练中，向导实现的 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> 方法显示向导 UI。|
|向导数据模型|这是名为 `SiteColumnWizardModel` 的中介类，用于在向导 UI 和向导实现之间提供一个层。 本示例使用此类帮助从向导实现中提取向导 UI 以及从向导 UI 中提取向导实现；此类不是所有向导的必需组件。<br /><br /> 在本演练中，向导实现在显示向导 UI 时将 `SiteColumnWizardModel` 对象传递给向导窗口。 向导 UI 使用此对象的方法将控件的值保存在 UI 中，并执行诸如验证输入站点 URL 是否有效等任务。 用户完成向导后，向导实现使用 `SiteColumnWizardModel` 对象来确定 UI 的最终状态。|
|项目签名管理器|这是一个名为 `ProjectSigningManager` 的帮助程序类，供向导实现用来在每个新的项目实例中创建一个新的 key.snk 文件。|
|SharePoint 命令|这些是向导数据模型在向导运行时用于调入本地 SharePoint 站点的方法。 由于 SharePoint 命令必须面向 .NET Framework 3.5，因此，这些命令是在与向导代码的其余部分不同的程序集中实现的。|

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，你需要将多个项目添加到在[演练：使用项目模板创建网站栏项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)中创建的 SiteColumnProjectItem 解决方案：

- WPF 项目。 你将实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，并在此项目中定义向导 UI。

- 定义 SharePoint 命令的类库项目。 此项目必须面向 .NET Framework 3.5。

  通过创建这些项目来开始进行演练。

#### <a name="to-create-the-wpf-project"></a>创建 WPF 项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，打开 SiteColumnProjectItem 解决方案。

2. 在“解决方案资源管理器”中，打开 SiteColumnProjectItem 解决方案节点的快捷菜单，选择“添加”，然后选择“新建项目”   。

3. 在“添加新项目”对话框顶部，确保已在 .NET Framework 版本列表中选中“.NET Framework 4.5” 。

4. 展开“Visual C#”节点或“Visual Basic”节点，然后选择“Windows”节点  。

5. 在项目模板列表中，选择“WPF 用户控件库”，将该项目命名为“ProjectTemplateWizard”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将 ProjectTemplateWizard 项目添加到解决方案，并打开默认的 UserControl1.xaml 文件。

6. 从项目中删除 UserControl1.xaml 文件。

#### <a name="to-create-the-sharepoint-commands-project"></a>创建 SharePoint 命令项目

1. 在“解决方案资源管理器”中，打开 SiteColumnProjectItem 解决方案节点的快捷菜单，选择“添加”，然后选择“新建项目”  。

2. 在“添加新项目”对话框顶部，选择 .NET Framework 版本列表中的“.NET Framework 3.5” 。

3. 展开“Visual C#”节点或“Visual Basic”节点，然后选择“Windows”节点  。

4. 选择“类库”项目模板，将项目命名为“SharePointCommands”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将 SharePointCommands 项目添加到解决方案，并打开默认 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 在创建向导之前，必须向项目中添加一些代码文件和程序集引用。

#### <a name="to-configure-the-wizard-project"></a>配置向导项目

1. 在“解决方案资源管理器”中，打开 ProjectTemplateWizard 项目节点的快捷菜单，然后选择“属性”  。

2. 在“项目设计器”中，选择“应用程序”选项卡（对于 Visual C# 项目）或“编译”选项卡（对于 Visual Basic 项目）  。

3. 确保将目标框架设置为 .NET Framework 4.5，而不是 .NET Framework 4.5 客户端配置文件。

     有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/visual-studio-multi-targeting-overview.md)。

4. 打开 ProjectTemplateWizard 项目的快捷菜单，选择“添加”，然后选择“新建项”  。

5. 选择“Window (WPF)”项，将该项命名为“WizardWindow”，然后选择“添加”按钮  。

6. 向项目添加两个“用户控件(WPF)”项，将它们命名为“Page1”和“Page2”  。

7. 将四个代码文件添加到项目中，并为它们指定以下名称：

    - SiteColumnProjectWizard

    - SiteColumnWizardModel

    - ProjectSigningManager

    - CommandIds

8. 打开 ProjectTemplateWizard 项目节点的快捷菜单，然后选择“添加引用” 。

9. 展开“程序集”节点，选择“扩展”节点，然后选中以下程序集旁的复选框 ：

    - EnvDTE

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.Shell.Interop.10.0

    - Microsoft.VisualStudio.Shell.Interop.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

10. 选择“确定”按钮以向项目添加程序集。

11. 在“解决方案资源管理器”中，在 ProjectTemplateWizard 项目的“References”文件夹下，选择“EnvDTE”   。

12. 在“属性”窗口中，将“嵌入互操作类型”属性的值更改为“False”  。

13. 如果要开发 Visual Basic 项目，请使用项目设计器将 ProjectTemplateWizard 命名空间导入到你的项目。

     有关详细信息，请参阅[操作说明：添加或移除导入的命名空间 (Visual Basic)](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)。

#### <a name="to-configure-the-sharepointcommands-project"></a>配置 SharePointcommands 项目

1. 在“解决方案资源管理器”中，选择“SharePointCommands”项目节点 。

2. 在菜单栏上，依次选择“项目”、“添加现有项” 。

3. 在“添加现有项”对话框中，浏览到包含 ProjectTemplateWizard 项目代码文件的文件夹，然后选择“CommandIds”代码文件 。

4. 选择“添加”按钮旁的箭头，然后在出现的菜单上选择“添加为链接”选项 。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会向 SharePointCommands 项目添加代码文件作为链接。 尽管此代码文件位于 ProjectTemplateWizard 项目中，但文件中的代码也是在 SharePointCommands 项目中编译的 。

5. 在 SharePointCommands 项目中，添加另一个名为“Commands”的代码文件。

6. 选择“SharePointCommands”项目，然后在菜单栏上选择“项目” > “添加引用” 。

7. 展开“程序集”节点，选择“扩展”节点，然后选中以下程序集旁的复选框 ：

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

8. 选择“确定”按钮以向项目添加程序集。

## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>创建向导模型、签名管理器和 SharePoint 命令 ID
 将代码添加到 ProjectTemplateWizard 项目，以在示例中实现以下组件：

- SharePoint 命令 ID。 这些字符串标识向导使用的 SharePoint 命令。 稍后在本演练中，你将向 SharePointCommands 项目添加代码以实现命令。

- 向导数据模型。

- 项目签名管理器。

  有关这些组件的详细信息，请参阅[了解向导组件](#understand-the-wizard-components)。

#### <a name="to-define-the-sharepoint-command-ids"></a>定义 SharePoint 命令 ID

1. 在 ProjectTemplateWizard 项目中，打开 CommandIds 代码文件，然后将此文件的全部内容替换为以下代码。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs" id="Snippet5":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb" id="Snippet5":::

#### <a name="to-create-the-wizard-model"></a>创建向导模型

1. 打开 SiteColumnWizardModel 代码文件，将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb" id="Snippet6":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs" id="Snippet6":::

#### <a name="to-create-the-project-signing-manager"></a>创建项目签名管理器

1. 打开 ProjectSigningManager 代码文件，然后将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb" id="Snippet8":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs" id="Snippet8":::

## <a name="create-the-wizard-ui"></a>创建向导 UI
 添加 XAML 来定义向导窗口的 UI 和用于提供向导页 UI 的两个用户控件，并添加代码来定义窗口和用户控件的行为。 创建的向导类似于 Visual Studio 中 SharePoint 项目的内置向导。

> [!NOTE]
> 在以下步骤中，在向项目添加 XAML 或代码后，项目将出现一些编译错误。 在稍后的步骤中添加代码时，这些错误将消失。

#### <a name="to-create-the-wizard-window-ui"></a>创建向导窗口 UI

1. 在 ProjectTemplateWizard 项目中，打开 WizardWindow.xaml 文件的快捷菜单，然后选择“打开”在设计器中打开窗口。

2. 在设计器的 XAML 视图中，将当前 XAML 替换为以下 XAML。 此 XAML 定义了一个 UI，其中包括一个标题、一个包含向导页的 <xref:System.Windows.Controls.Grid> 以及一个位于窗口底部的导航按钮。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml" id="Snippet10":::

    > [!NOTE]
    > 在此 XAML 中创建的窗口派生自 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基类。 向 Visual Studio 添加自定义 WPF 对话框时，建议从此类派生对话框，使样式与其他 Visual Studio 对话框保持一致，避免其他可能出现的模式对话框问题。 有关详细信息，请参阅[创建和管理模式对话框](../extensibility/creating-and-managing-modal-dialog-boxes.md)。

3. 如果要开发 Visual Basic 项目，请从 `Window` 元素的 `x:Class` 属性中的 `WizardWindow` 类名删除 `ProjectTemplateWizard` 命名空间。 此元素位于 XAML 的第一行。 完成后，第一行应如以下示例所示。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. 打开 WizardWindow.xaml 文件的代码隐藏文件。

5. 将此文件的内容（文件顶部的 `using` 声明除外）替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb" id="Snippet4":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs" id="Snippet4":::

#### <a name="to-create-the-first-wizard-page-ui"></a>创建第一个向导页 UI

1. 在 ProjectTemplateWizard 项目中，打开 Page1.xaml 文件的快捷菜单，然后选择“打开”在设计器中打开用户控件。

2. 在设计器的 XAML 视图中，将当前 XAML 替换为以下 XAML。 此 XAML 定义了一个 UI，其中包括一个文本框，用户可以在此文本框中输入要用于调试的本地网站的 URL。 此 UI 还包括选项按钮，供用户用来指定项目是否进行了沙盒处理。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml" id="Snippet11":::

3. 如果要开发 Visual Basic 项目，请从 `UserControl` 元素的 `x:Class` 属性中的 `Page1` 类名删除 `ProjectTemplateWizard` 命名空间。 这位于 XAML 的第一行。 完成后，第一行应如下所示。

    ```xml
    <UserControl x:Class="Page1"
    ```

4. 将 Page1.xaml 文件的内容（文件顶部的 `using` 声明除外）替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs" id="Snippet2":::

#### <a name="to-create-the-second-wizard-page-ui"></a>创建第二个向导页 UI

1. 在 ProjectTemplateWizard 项目中，打开 Page2.xaml 文件的快捷菜单，然后选择“打开”。

     用户控件将在设计器中打开。

2. 在 XAML 视图中，将当前 XAML 替换为以下 XAML。 此 XAML 定义了一个 UI，其中包括一个用于选择网站栏基类型的下拉列表、一个用于指定要在其中显示库中网站栏的内置组或自定义组的组合框，以及一个用于指定网站栏名称的文本框。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml" id="Snippet12":::

3. 如果要开发 Visual Basic 项目，请从 `UserControl` 元素的 `x:Class` 属性中的 `Page2` 类名删除 `ProjectTemplateWizard` 命名空间。 这位于 XAML 的第一行。 完成后，第一行应如下所示。

    ```xml
    <UserControl x:Class="Page2"
    ```

4. 将 Page2.xaml 文件的代码隐藏文件内容（文件顶部的 `using` 声明除外）替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs" id="Snippet3":::

## <a name="implement-the-wizard"></a>实现向导
 通过实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口定义向导的主要功能。 此接口定义 Visual Studio 在向导启动和完成时以及在向导运行时的特定时间调用的方法。

#### <a name="to-implement-the-wizard"></a>实现向导

1. 在 ProjectTemplateWizard 项目中，打开 SiteColumnProjectWizard 代码文件。

2. 将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs" id="Snippet7":::

## <a name="create-the-sharepoint-commands"></a>创建 SharePoint 命令
 创建两个自定义命令，用于调入 SharePoint 服务器对象模型。 一个命令用于确定用户在向导中键入的站点 URL 是否有效。 另一个命令用于从指定的 SharePoint 站点获取所有字段类型，使用户可以选择要用作他们新网站栏基础的字段类型。

#### <a name="to-define-the-sharepoint-commands"></a>定义 SharePoint 命令

1. 在 SharePointCommands 项目中，打开 Commands 代码文件。

2. 将此文件的全部内容替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb" id="Snippet9":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs" id="Snippet9":::

## <a name="checkpoint"></a>检查点
 此时在本演练中，向导的所有代码现在都位于项目中。 生成项目并确保编译时没有出现错误。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="removing-the-keysnk-file-from-the-project-template"></a>从项目模板中删除 key.snk 文件
 在[演练：使用项目模板创建网站栏项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)中，创建的项目模板包含用于为每个网站栏项目实例签名的 key.snk 文件。 不再需要此 key.snk 文件了，因为向导现在会为每个项目生成新的 key.snk 文件。 从项目模板中删除 key.snk 文件，并删除对此文件的引用。

#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>从项目模板中删除 key.snk 文件

1. 在“解决方案资源管理器”中，在 SiteColumnProjectTemplate 节点下，打开 key.snk 文件的快捷菜单，然后选择“删除”   。

2. 在随即出现的确认对话框中，选择 **“确定”** 按钮。

3. 在 SiteColumnProjectTemplate 节点下，打开 SiteColumnProjectTemplate.vstemplate 文件，然后从中删除以下元素。

    ```xml
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
    ```

4. 保存并关闭该文件。

5. 在 SiteColumnProjectTemplate 节点下，打开 ProjectTemplate.csproj 或 ProjectTemplate.vbproj 文件，然后从中删除以下 `PropertyGroup` 元素。

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
 在实现了向导后，必须将向导与“网站栏”项目模板关联。 为此，必须完成三个过程：

1. 使用强名称为向导程序集签名。

2. 为向导程序集获取公钥标记。

3. 在“网站栏”项目模板的 .vstemplate 文件中添加对向导程序集的引用。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>使用强名称为向导程序集签名

1. 在“解决方案资源管理器”中，打开 ProjectTemplateWizard 项目的快捷菜单，然后选择“属性”  。

2. 在“签名”选项卡上，选中“为程序集签名”复选框。

3. 在“选择强名称密钥文件”列表中，选择“\<New...>” 。

4. 在“创建强名称密钥”对话框中，输入新密钥文件的名称，取消选中“使用密码保护密钥文件”复选框，然后选择“确定”按钮  。

5. 打开 ProjectTemplateWizard 项目的快捷菜单，然后选择“生成”以创建 ProjectTemplateWizard.dll 文件 。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>为向导程序集获取公钥标记

1. 在“开始”菜单上，依次选择“所有程序”、“Microsoft Visual Studio”、“Visual Studio Tools”和“开发人员命令提示”    。

     随即将打开 Visual Studio 命令提示符窗口。

2. 运行以下命令，将 PathToWizardAssembly 替换为开发计算机上 ProjectTemplateWizard 项目的已生成 ProjectTemplateWizard.dll 程序集的完整路径：

    ```cmd
    sn.exe -T PathToWizardAssembly
    ```

     ProjectTemplateWizard.dll 程序集的公钥标记会被写入 Visual Studio 命令提示符窗口中。

3. 将 Visual Studio 命令提示符窗口保持为打开状态。 下一个过程中将会用到公钥标记。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>在 .vstemplate 文件中添加对向导程序集的引用

1. 在“解决方案资源管理器”中，展开 SiteColumnProjectTemplate 项目节点，然后打开 SiteColumnProjectTemplate.vstemplate 文件 。

2. 在临近文件末尾的位置，在 `</TemplateContent>` 和 `</VSTemplate>` 标记之间添加以下 `WizardExtension` 元素。 将 `PublicKeyToken` 属性的“your token”值替换为在上一过程中获取的公钥标记。

    ```xml
    <WizardExtension>
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>
    </WizardExtension>
    ```

     有关 `WizardExtension` 元素的详细信息，请参阅 [WizardExtension 元素（Visual Studio 模板）](../extensibility/wizardextension-element-visual-studio-templates.md)。

3. 保存并关闭该文件。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>向项目模板中的 Elements.xml 文件添加可替换参数
 向 SiteColumnProjectTemplate 项目中的 Elements.xml 文件添加多个可替换参数。 这些参数是在之前定义的 `SiteColumnProjectWizard` 类的 `RunStarted` 方法中初始化的。 用户创建网站栏项目时，Visual Studio 会自动将新项目中 Elements.xml 文件中的这些参数替换为他们在向导中指定的值。

 可替换参数是以美元符号 ($) 字符开头和结尾的标记。 除了定义自己的可替换参数外，还可以使用由 SharePoint 项目系统定义和初始化的内置参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>向 Elements.xml 文件添加可替换参数

1. 在 SiteColumnProjectTemplate 项目中，将 Elements.xml 文件的内容替换为以下 XML。

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

     新的 XML 将 `Name`、`DisplayName`、`Type` 和 `Group` 属性的值更改为自定义可替换参数。

2. 保存并关闭该文件。

## <a name="add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包
 若要使用包含网站栏项目模板的 VSIX 包部署向导，请向 VSIX 项目中的 source.extension.vsixmanifest 文件添加对向导项目和 SharePoint 命令项目的引用。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包

1. 在“解决方案资源管理器”中，打开 SiteColumnProjectItem 项目中 source.extension.vsixmanifest 文件的快捷菜单，然后选择“打开”   。

     Visual Studio 会在清单编辑器中打开该文件。

2. 在编辑器的“资产”选项卡中，选择“新建”按钮 。

     随即将打开“添加新资产”对话框。

3. 在“类型”列表中，选择“Microsoft.VisualStudio.Assembly” 。

4. 在“源”列表中，选择“当前解决方案中的项目” 。

5. 在“项目”列表中，选择“ProjectTemplateWizard”，然后选择“确定”按钮  。

6. 在编辑器的“资产”选项卡中，再次选择“新建”按钮 。

     随即将打开“添加新资产”对话框。

7. 在“类型”列表中，输入“SharePoint.Commands.v4” 。

8. 在“源”列表中，选择“当前解决方案中的项目” 。

9. 在“项目”列表中，选择“SharePointCommands”项目，然后选择“确定”按钮  。

10. 在菜单栏上，选择“生成” > “生成解决方案”，然后确保解决方案在生成时没有出错 。

## <a name="test-the-wizard"></a>测试向导
 现在可以测试向导了。 首先，在 Visual Studio 的实验性实例中开始调试 SiteColumnProjectItem 解决方案。 然后，在 Visual Studio 的实验性实例中测试网站栏项目的向导。 最后，生成并运行项目来验证网站栏是否按预期工作。

#### <a name="to-start-debugging-the-solution"></a>开始调试解决方案

1. 使用管理凭据重启 Visual Studio，然后打开 SiteColumnProjectItem 解决方案。

2. 在 ProjectTemplateWizard 项目中，打开 SiteColumnProjectWizard 代码文件，然后将断点添加到 `RunStarted` 方法中的第一行代码。

3. 在菜单栏上，选择“调试” > “异常” 。

4. 在“异常”对话框中，确保取消选中“公共语言运行时异常”的“已引发”和“用户未处理”复选框，然后选择“确定”按钮    。

5. 通过选择 F5 键或在菜单栏上选择“调试” > “开始调试”以开始进行调试  。

     Visual Studio 会将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0，并启动 Visual Studio 的实验性实例。 你将在此 Visual Studio 实例中测试项目项。

#### <a name="to-test-the-wizard-in-visual-studio"></a>在 Visual Studio 中测试向导

1. 在 Visual Studio 的实验性实例中的菜单栏上，选择“文件” > “新建” > “项目”  。

2. 展开“Visual C#”节点或“Visual Basic”节点（具体取决于你的项目模板支持的语言），展开“SharePoint”节点，然后选择“2010”节点   。

3. 在项目模板列表中，选择“网站栏”，将该项目命名为“SiteColumnWizardTest”，然后选择“确定”按钮  。

4. 验证 Visual Studio 的其他实例中的代码是否在你之前在 `RunStarted` 方法中设置的断点处停止。

5. 通过选择 F5 键或在菜单栏上选择“调试” > “继续”以继续进行调试  。

6. 在“SharePoint 自定义向导”中，输入要用于调试的网站的 URL，然后选择“下一步”按钮 。

7. 在“SharePoint 自定义向导”的第二页中，进行以下选择：

   - 在“类型”列表中，选择“布尔” 。

   - 在“组”列表中，选择“自定义是/否栏” 。

   - 在“名称”框中输入“我的是/否栏”，然后选择“完成”按钮  。

     在“解决方案资源管理器”中，将显示一个新项目，其中包含名为 Field1 的项目项，而 Visual Studio 会在编辑器中打开项目的 Elements.xml 文件 。

8. 验证 Elements.xml 是否包含你在向导中指定的值。

#### <a name="to-test-the-site-column-in-sharepoint"></a>测试 SharePoint 中的网站栏

1. 在 Visual Studio 的实验性实例中，选择 F5 键。

     网站栏会打包并部署到项目的“站点 URL”属性指定的 SharePoint 站点。 Web 浏览器将打开此站点的默认页面。

    > [!NOTE]
    > 如果显示“脚本调试已禁用”对话框，请选择“是”按钮以继续调试项目 。

2. 在“网站操作”菜单上，选择“网站设置” 。

3. 在“网站设置”页上的“库”下，选择“网站栏”链接 。

4. 在网站栏列表中，验证“自定义是/否栏”组中是否包含名为“我的是/否栏”的栏，然后关闭 Web 浏览器 。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成项目项测试后，从 Visual Studio 的实验性实例中删除项目模板。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio 的实验性实例中的菜单栏上，选择“工具” > “扩展和更新” 。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择“网站栏”，然后选择“卸载”按钮 。

3. 在出现的对话框中，选择“是”按钮以确认要卸载扩展，然后选择“立即重启”按钮以完成卸载 。

4. 关闭 Visual Studio 的实验性实例和打开了 CustomActionProjectItem 解决方案的实例。

     若要了解如何部署 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展，请参阅[提供 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

## <a name="see-also"></a>另请参阅
- [演练：使用项目模板创建网站栏项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
