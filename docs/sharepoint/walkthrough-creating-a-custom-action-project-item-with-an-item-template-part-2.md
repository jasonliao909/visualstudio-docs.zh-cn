---
title: 用项模板创建自定义操作项目项（第2部分）
titleSuffix: ''
description: 在本演练中，添加一个向导，以便在用户使用项模板在 SharePoint 网站上添加自定义操作项目项时从用户收集信息。
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
ms.openlocfilehash: b31a68bcc8c3dac0cb0056a4c3f429063747b4df
ms.sourcegitcommit: 42aec4a2ea6dec67dbe4c93bcf0fa1116a4b93d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2021
ms.locfileid: "122980490"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>演练：使用项模板创建自定义操作项目项（第2部分）
  在定义 SharePoint 项目项的自定义类型并将其与 Visual Studio 中的项模板关联后，你可能还需要为模板提供向导。 当用户使用模板向项目添加项目项的新实例时，可以使用该向导收集用户的信息。 你收集的信息可用于初始化项目项。

 在本演练中，您将向 " [演练：使用项模板创建自定义操作项目项，第1部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)" 中所示的自定义操作项目项添加向导。 当用户将自定义操作项目项添加到 SharePoint 项目中时，向导会收集有关自定义操作的信息 (例如，当最终用户选择自定义操作时该操作的位置和要导航到的 URL) 并将此信息添加到新项目项中的 *Elements.xml* 文件中。

 本演练演示了下列任务：

- 为与项模板关联的自定义 SharePoint 项目项类型创建向导。

- 定义类似于 Visual Studio 中的 SharePoint 项目项的内置向导的自定义向导 UI。

- 使用可替换参数通过在向导中收集的数据初始化 SharePoint 项目文件。

- 调试和测试向导。

> [!NOTE]
> 可以从 [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) 下载示例，其中演示了如何为工作流创建自定义活动。

## <a name="prerequisites"></a>必备条件
 若要执行本演练，必须先完成 [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)，以创建 CustomActionProjectItem 解决方案。

 在开发计算机上还需要以下组件来完成本演练：

- Windows、SharePoint 和 Visual Studio 的受支持版本。

- Visual Studio SDK。 本演练使用 SDK 中的 **vsix Project** 模板来创建用于部署项目项的 vsix 包。 有关详细信息，请参阅[Visual Studio 中的扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  以下概念的知识非常有用，但不是必需的，无法完成本演练：

- Visual Studio 中的项目和项模板的向导。 有关详细信息，请参阅[如何：将向导与 Project 模板和接口结合使用](../extensibility/how-to-use-wizards-with-project-templates.md) <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 。

- SharePoint 中的自定义操作。 有关详细信息，请参阅 [自定义操作](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14))。

## <a name="create-the-wizard-project"></a>创建向导项目
 若要完成本演练，必须将项目添加到在 [演练：创建具有项模板的自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)中创建的 CustomActionProjectItem 解决方案。 你将实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，并在此项目中定义向导 UI。

#### <a name="to-create-the-wizard-project"></a>创建向导项目

1. 在 Visual Studio 中，打开 CustomActionProjectItem 解决方案

2. 在 **解决方案资源管理器** 中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建 Project**"。

3. 在 "**新建 Project** " 对话框中，展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 " **Windows** " 节点。

4. 在 "**新建 Project** " 对话框的顶部，确保在 .NET Framework 版本的列表中选择 **.NET Framework 4.5** 。

5. 选择 " **WPF 用户控件库** " 项目模板，将项目命名为 " **ItemTemplateWizard**"，然后选择 **"确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **ItemTemplateWizard** 项目添加到解决方案。

6. 从项目中删除 UserControl1 项。

## <a name="configure-the-wizard-project"></a>配置向导项目
 在创建向导之前，必须向项目添加 Windows Presentation Foundation (WPF) 窗口、代码文件和程序集引用。

#### <a name="to-configure-the-wizard-project"></a>配置向导项目

1. 在 **解决方案资源管理器** 中，打开 **ItemTemplateWizard** 项目节点的快捷菜单，然后选择 " **属性**"。

2. 在 **Project 设计器** 中，确保将目标框架设置为 .NET Framework 4.5。

     对于 Visual c # 项目，可以在 "**应用程序**" 选项卡上设置此值。对于 Visual Basic 项目，可以在 "**编译**" 选项卡上设置此值。有关详细信息，请参阅 [如何：面向 .NET Framework 版本](../ide/visual-studio-multi-targeting-overview.md)。

3. 在 **ItemTemplateWizard** 项目中，将 **WPF) 项 (** 添加到项目，然后将该项命名为 **WizardWindow**。

4. 添加两个名为 CustomActionWizard 和 String 的代码文件。

5. 打开 **ItemTemplateWizard** 项目的快捷菜单，然后选择 " **添加引用**"。

6. 在 " **引用管理器-ItemTemplateWizard** " 对话框中的 " **程序集** " 节点下，选择 " **扩展** " 节点。

7. 选中以下程序集旁的复选框，然后选择 **"确定"** 按钮：

    - EnvDTE

    - VisualStudio 11。0

    - Microsoft.VisualStudio.TemplateWizardInterface

8. 在 **解决方案资源管理器** 的 ItemTemplateWizard 项目的 " **引用** " 文件夹中，选择 **EnvDTE** 引用。

9. 在 " **属性** " 窗口中，将 " **嵌入互操作类型** " 属性的值更改为 " **False**"。

## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>定义自定义操作的默认位置和 ID 字符串
 每个自定义操作都有一个在Elements.xml文件中的 `GroupID` 元素的和属性中指定的位置和 ID `Location` `CustomAction` 。  在此步骤中，将为 ItemTemplateWizard 项目中的这些属性定义一些有效的字符串。 完成本演练后，当用户在向导中指定位置和 ID 时，这些字符串将写入自定义操作项目项中的 *Elements.xml* 文件。

 为简单起见，此示例仅支持部分可用的默认位置和 Id。 有关完整列表，请参阅 [默认自定义操作位置和 id](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))。

#### <a name="to-define-the-default-location-and-id-strings"></a>定义默认位置和 ID 字符串

1. 未.

2. 在 **ItemTemplateWizard** 项目中，将字符串代码文件中的代码替换为以下代码。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs" id="Snippet6":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb" id="Snippet6":::

## <a name="create-the-wizard-ui"></a>创建向导 UI
 添加 XAML 以定义向导的 UI，并添加一些代码，将向导中的某些控件绑定到 ID 字符串。 你创建的向导与 Visual Studio 中的 SharePoint 项目的内置向导类似。

#### <a name="to-create-the-wizard-ui"></a>创建向导 UI

1. 在 **ItemTemplateWizard** 项目中，打开 **WizardWindow** 文件的快捷菜单，然后选择 " **打开** " 以在设计器中打开该窗口。

2. 在 XAML 视图中，将当前 XAML 替换为以下 XAML。 XAML 定义了一个 UI，该 UI 包含一个标题、用于指定自定义操作的行为的控件以及该窗口底部的导航按钮。

    > [!NOTE]
    > 添加此代码后，你的项目将有一些编译错误。 当你在后续步骤中添加代码时，这些错误将消失。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml" id="Snippet9":::

    > [!NOTE]
    > 在此 XAML 中创建的窗口派生自 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基类。 当您将自定义 WPF 对话框添加到 Visual Studio 时，我们建议您从此类派生对话框，以便与 Visual Studio 中的其他对话框保持一致的样式，并避免在模式对话框中可能出现的问题。 有关详细信息，请参阅 [创建和管理模式对话框](../extensibility/creating-and-managing-modal-dialog-boxes.md)。

3. 如果要开发 Visual Basic 项目，请 `ItemTemplateWizard` 从 `WizardWindow` 元素的属性中的类名称中删除该命名空间 `x:Class` `Window` 。 此元素位于 XAML 的第一行。 完成后，第一行应类似于以下代码：

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. 在 WizardWindow 文件的代码隐藏文件中，将当前代码替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs" id="Snippet7":::

## <a name="implement-the-wizard"></a>实现向导
 通过实现接口定义向导功能 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 。

#### <a name="to-implement-the-wizard"></a>实现向导

1. 在 **ItemTemplateWizard** 项目中，打开 **CustomActionWizard** 代码文件，然后将此文件中的当前代码替换为以下代码：

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs" id="Snippet8":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb" id="Snippet8":::

## <a name="checkpoint"></a>检查点
 在本演练的这一阶段，向导的所有代码现在都在项目中。 生成项目以确保它在编译时不会出错。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

## <a name="associate-the-wizard-with-the-item-template"></a>将向导与项模板关联
 现在，你已经实现了向导，你必须完成三个主要步骤，才能将它与 **自定义操作** 项模板关联：

1. 使用强名称对向导程序集进行签名。

2. 获取向导程序集的公钥标记。

3. 为 **自定义操作** 项模板的 .vstemplate 文件中的向导程序集添加引用。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>使用强名称对向导程序集进行签名

1. 在 **解决方案资源管理器** 中，打开 **ItemTemplateWizard** 项目节点的快捷菜单，然后选择 " **属性**"。

2. 在“签名”选项卡上，选中“为程序集签名”复选框。

3. 在 " **选择强名称密钥文件** " 列表中，选择 **\<New...>** 。

4. 在 " **创建强名称密钥** " 对话框中，输入名称，清除 " **使用密码保护密钥文件** " 复选框，然后选择 **"确定"** 按钮。

5. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>获取向导程序集的公钥标记

1. 在 Visual Studio 的命令提示符窗口中，运行以下命令，并将 *PathToWizardAssembly* 替换为开发计算机上 ItemTemplateWizard 项目的生成的 ItemTemplateWizard.dll 程序集的完整路径。

    ```xml
    sn.exe -T PathToWizardAssembly
    ```

     将 *ItemTemplateWizard.dll* 程序集的公钥标记写入 Visual Studio 命令提示符 "窗口。

2. 使 Visual Studio 命令提示符窗口保持打开状态。 需要公钥标记才能完成下一个过程。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>向 .vstemplate 文件中的向导程序集添加引用

1. 在 **解决方案资源管理器** 中，展开 **itemtemplate** 项目节点，然后打开 *itemtemplate .vstemplate* 文件。

2. 在文件末尾附近， `WizardExtension` 在和标记之间添加以下元素 `</TemplateContent>` `</VSTemplate>` 。 将该属性的 *YourToken* 值替换 `PublicKeyToken` 为你在上一过程中获取的公钥标记。

    ```xml
    <WizardExtension>
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>
    </WizardExtension>
    ```

     有关元素的详细信息 `WizardExtension` ，请参阅[WizardExtension 元素 &#40;Visual Studio 模板&#41;](../extensibility/wizardextension-element-visual-studio-templates.md)。

3. 保存并关闭该文件。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>将可替换参数添加到项模板中的 *Elements.xml* 文件
 向 ItemTemplate 项目中的 *Elements.xml* 文件添加几个可替换参数。 这些参数在 `PopulateReplacementDictionary` 之前定义的类的方法中进行初始化 `CustomActionWizard` 。 当用户将自定义操作项目项添加到项目时，Visual Studio 会自动将新项目项的 *Elements.xml* 文件中的这些参数替换为在向导中指定的值。

 可替换参数是以美元符号 ($) 字符开头和结尾的令牌。 除了定义你自己的可替换参数外，还可以使用 SharePoint 项目系统定义和初始化的内置参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>向 *Elements.xml* 文件添加可替换参数

1. 在 ItemTemplate 项目中，将 *Elements.xml* 文件的内容替换为以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="$IdValue$"
                    GroupId="$GroupIdValue$"
                    Location="$LocationValue$"
                    Sequence="1000"
                    Title="$TitleValue$"
                    Description="$DescriptionValue$" >
        <UrlAction Url="$UrlValue$"/>
      </CustomAction>
    </Elements>
    ```

     新 XML 会将、、、和属性的值更改 `Id` `GroupId` `Location` `Description` `Url` 为可替换参数。

2. 保存并关闭该文件。

## <a name="add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包
 在 VSIX 项目的 source.extension.vsixmanifest 文件中，添加对向导项目的引用，以便将其与包含项目项的 VSIX 包一起部署。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包

1. 在 **解决方案资源管理器** 中，在 CustomActionProjectItem 项目中打开 **source.extension.vsixmanifest** 文件中的快捷菜单，然后选择 " **打开** "，在清单编辑器中打开该文件。

2. 在清单编辑器中，选择 " **资产** " 选项卡，然后选择 " **新建** " 按钮。

     此时将显示 " **添加新资产** " 对话框。

3. 在 " **类型** " 列表中，选择 " **VisualStudio**"。

4. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

5. 在 **Project** 列表中，选择 " **ItemTemplateWizard**"，然后选择 "**确定"** 按钮。

6. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**"，然后确保解决方案在编译时不会出错。

## <a name="test-the-wizard"></a>测试向导
 你现在已准备好测试向导。 首先，开始调试 Visual Studio 的实验实例中的 CustomActionProjectItem 解决方案。 然后，在 Visual Studio 的实验实例中的 SharePoint 项目中，为自定义操作项目项测试向导。 最后，生成并运行 SharePoint 项目，以验证自定义操作是否按预期方式工作。

#### <a name="to-start-to-debug-the-solution"></a>开始调试解决方案

1. 用管理凭据重新启动 Visual Studio，然后打开 CustomActionProjectItem 解决方案。

2. 在 ItemTemplateWizard 项目中，打开 CustomActionWizard 代码文件，然后向方法中的第一个代码行添加一个断点 `RunStarted` 。

3. 在菜单栏上，选择 "**调试**  >  **异常**"。

4. 在 "**异常**" 对话框中，确保清除了 "**公共语言运行时异常****引发** 的和 **用户未处理** 的" 复选框，然后选择 **"确定"** 按钮。

5. 选择 **F5** 键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"，开始调试。

     Visual Studio 将 Project Item\1.0 的扩展安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom 操作，并启动 Visual Studio 的实验实例。 你将在 Visual Studio 的此实例中测试项目项。

#### <a name="to-test-the-wizard-in-visual-studio"></a>在 Visual Studio 中测试向导

1. 在 Visual Studio 的实验实例的菜单栏上，选择 "**文件**" "  >  **新建**  >  **Project**"。

2. 展开 " **Visual c #** " 或 " **Visual Basic** " 节点 (根据项模板支持的语言) ，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在项目模板列表中，选择 **SharePoint 2010 Project**，将项目命名为 " **CustomActionWizardTest**"，然后选择 **"确定"** 按钮。

4. 在 " **SharePoint 自定义向导**" 中，输入要用于调试的站点的 URL，然后选择 "**完成**" 按钮。

5. 在 **解决方案资源管理器** 中，打开项目节点的快捷菜单，选择 " **添加**"，然后选择 " **新建项**"。

6. 在 "**添加新项-CustomItemWizardTest** " 对话框中，展开 " **SharePoint** " 节点，然后展开 " **2010** " 节点。

7. 在项目项列表中，选择 " **自定义操作** " 项，然后选择 " **添加** " 按钮。

8. 验证 Visual Studio 的另一个实例中的代码在您之前在方法中设置的断点处停止 `RunStarted` 。

9. 通过选择 **F5** 键，或在菜单栏上选择 "**调试** 继续"，继续调试项目  >  。

     “SharePoint 自定义向导”随即出现。

10. 在 " **位置**" 下，选择 " **列表编辑** " 选项按钮。

11. 在 " **组 ID** " 列表中，选择 " **通信**"。

12. 在 "**标题**" 框中，输入 **SharePoint 开发人员中心**"。

13. 在 "**说明**" 框中，输入 **打开 SharePoint 开发人员中心网站**。

14. 在 " **URL** " 框中输入 `https://docs.microsoft.com/sharepoint/dev/` ，然后选择 " **完成** " 按钮。

     Visual Studio 会将名为 **CustomAction1** 的项添加到项目中，并在编辑器中打开 *Elements.xml* 文件。 验证 *Elements.xml* 是否包含你在向导中指定的值。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>测试中的自定义操作 SharePoint

1. 在 Visual Studio 的实验实例中，选择 **F5** 键，或在菜单栏上选择 "**调试**" "  >  **开始调试**"。

     自定义操作打包并部署到由项目的 "**网站 URL** " 属性指定的 SharePoint 站点，web 浏览器将打开到此站点的默认页面。

    > [!NOTE]
    > 如果出现 " **脚本调试已禁用** " 对话框，请选择 " **是"** 按钮。

2. 在 SharePoint 站点的 "列表" 区域中，选择 "**任务**" 链接。

     此时将显示 " **任务-所有任务** " 页。

3. 在功能区的 "**列表工具**" 选项卡上，选择 "**列表**" 选项卡，然后在 "**设置**" 组中，选择 "**列出设置**"。

     此时将显示 "**设置列表**" 页。

4. 在页面顶部附近的 "**通信**" 标题下，选择 " **SharePoint 开发人员中心**" 链接，确认浏览器打开网站 `https://docs.microsoft.com/sharepoint/dev/` ，然后关闭浏览器。

## <a name="cleaning-up-the-development-computer"></a>清理开发计算机
 完成项目项测试后，从 Visual Studio 的实验实例中删除项目项模板。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio 的实验实例中，在菜单栏上选择 "**工具**" "  >  **扩展和更新**"。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择 "**自定义操作 Project 项**" 扩展，然后选择 "**卸载**" 按钮。

3. 在出现的对话框中，选择 " **是"** 按钮，确认要卸载该扩展，然后选择 " **立即重新启动** " 按钮以完成卸载。

4. 关闭实验实例 (Visual Studio 的两个实例，以及在其中) 打开 CustomActionProjectItem 解决方案的 Visual Studio 的实例。

## <a name="see-also"></a>请参阅
- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
- [默认自定义操作位置和 Id](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))
