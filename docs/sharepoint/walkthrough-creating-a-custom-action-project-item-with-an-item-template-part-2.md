---
title: 使用项模板创建自定义操作项目项（第 2 部分）
titleSuffix: ''
description: 本演练中将添加一个向导，以在用户使用项模板在 SharePoint 站点上添加“自定义操作”项目项时，从用户处收集信息。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665008"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>演练：使用项模板创建自定义操作项目项（第 2 部分）
  定义了自定义类型的 SharePoint 项目项并将其与 Visual Studio 中的项模板相关联后，你可能还需要为模板提供一个向导。 当用户使用模板向项目添加项目项的新实例时，可以使用此向导收集用户的信息。 收集的信息可用于初始化项目项。

 在此演练中，你将向自定义操作项目项添加向导，如[演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)所演示。 当用户将自定义操作项目项添加到 SharePoint 项目时，向导将收集有关自定义操作的信息（例如其位置以及最终用户选择信息时要导航到的 URL），并将此信息添加到新项目项中的 Elements.xml 文件。

 本演练演示了下列任务：

- 为与项模板关联的自定义 SharePoint 项目项类型创建向导。

- 定义类似于 Visual Studio 中 SharePoint 项目项内置向导的自定义向导 UI。

- 使用可替换参数和在向导中收集的数据初始化 SharePoint 项目文件。

- 调试和测试向导。

> [!NOTE]
> 可从 [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) 下载如何为工作流创建自定义活动的演示示例。

## <a name="prerequisites"></a>先决条件
 若要进行本演练，必须首先完成[演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)，来创建 CustomActionProjectItem 解决方案。

 在开发计算机上还需要以下组件来完成本演练：

- 受支持的 Windows、SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用 SDK 中的 VSIX 项目模板来创建用于部署项目项的 VSIX 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念有助于完成演练，但不是必需的：

- Visual Studio 中项目和项模板的向导。 有关详细信息，请参阅[操作说明：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)和 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口。

- SharePoint 中的自定义操作。 有关详细信息，请参阅[自定义操作](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14))。

## <a name="create-the-wizard-project"></a>创建向导项目
 若要完成本演练，必须将项目添加到你在[演练：使用项模板创建自定义操作项目（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)中创建的 CustomActionProjectItem 解决方案。 你将实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口，并在此项目中定义向导 UI。

#### <a name="to-create-the-wizard-project"></a>创建向导项目

1. 在 Visual Studio 中，打开 CustomActionProjectItem 解决方案

2. 在“解决方案资源管理器”中，打开解决方案节点的快捷菜单，选择“添加”，然后选择“新建项目”  。

3. 在“新建项目”对话框中，展开“Visual C#”或“Visual Basic”节点，然后选择“Windows”节点   。

4. 在“新建项目”对话框顶部，确保“.NET Framework 4.5”在 .NET Framework 版本列表中已选中 。

5. 选择“WPF 用户控件库”项目模板，将该项目命名为“ItemTemplateWizard”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将“ItemTemplateWizard”项目添加到解决方案。

6. 从项目中删除 UserControl1 项。

## <a name="configure-the-wizard-project"></a>配置向导项目
 在创建向导之前，必须向项目添加 Windows Presentation Foundation (WPF) 窗口、代码文件和程序集引用。

#### <a name="to-configure-the-wizard-project"></a>配置向导项目

1. 在“解决方案资源管理器”中，打开 ItemTemplateWizard 项目节点的快捷菜单，然后选择“属性”  。

2. 在“项目设计器”中，确保目标框架设置为“.NET Framework 4.5”。

     对于 Visual C# 项目，可以在“应用程序”选项卡上设置此值。对于 Visual Basic 项目，可以在“编译”选项卡上设置此值。有关详细信息，请参阅[操作方法：面向 .NET Framework 版本](../ide/visual-studio-multi-targeting-overview.md) 。

3. 在 ItemTemplateWizard 项目中，向项目添加 Window (WPF) 项，然后将该项命名为 WizardWindow  。

4. 添加两个名为 CustomActionWizard 和 String 的代码文件。

5. 打开 ItemTemplateWizard 项目的快捷菜单，然后选择“添加引用” 。

6. 在“引用管理器 - ItemTemplateWizard”对话框中的“程序集”节点下，选择“扩展”节点  。

7. 选中以下程序集旁边的复选框，然后选择“确定”按钮：

    - EnvDTE

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

8. 在“解决方案资源管理器”的 ItemTemplateWizard 项目的“引用”文件夹中，选择 EnvDTE 引用  。

9. 在“属性”窗口中，将“嵌入互操作类型”属性的值更改为“False”  。

## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>定义自定义操作的默认位置和 ID 字符串
 每个自定义操作都有一个位置和 ID，这些位置和 ID 在 Elements.xml 文件中 `CustomAction` 元素的 `GroupID` 和 `Location` 属性中指定。 在此步骤中，你将在 ItemTemplateWizard 项目中为这些属性定义一些有效字符串。 完成本演练后，当用户在向导中指定位置和 ID 时，这些字符串将写入自定义操作项目项中的 Elements.xml 文件。

 为简单起见，此示例仅支持一部分可用的默认位置和 ID。 有关完整列表，请参阅[默认自定义操作位置和 ID](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))。

#### <a name="to-define-the-default-location-and-id-strings"></a>定义默认位置和 ID 字符串

1. 打开。

2. 在 ItemTemplateWizard 项目中，将字符串代码文件中的代码替换为以下代码。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs" id="Snippet6":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb" id="Snippet6":::

## <a name="create-the-wizard-ui"></a>创建向导 UI
 添加 XAML 以定义向导的 UI，并添加一些代码以将向导中的某些控件绑定到 ID 字符串。 创建的向导类似于 Visual Studio 中 SharePoint 项目的内置向导。

#### <a name="to-create-the-wizard-ui"></a>创建向导 UI

1. 在 ItemTemplateWizard 项目中，打开 WizardWindow.xaml 文件的快捷菜单，然后选择“打开”以打开设计器中的窗口  。

2. 在 XAML 视图中，将当前 XAML 替换为以下 XAML。 XAML 定义一个 UI，其中包括标题、指定自定义操作行为的控件以及窗口底部的导航按钮。

    > [!NOTE]
    > 添加此代码后，项目将发生一些编译错误。 在稍后的步骤中添加代码时，这些错误将消失。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml" id="Snippet9":::

    > [!NOTE]
    > 在此 XAML 中创建的窗口派生自 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基类。 将自定义 WPF 对话框添加到 Visual Studio 时，建议你从此类派生对话框，以便与 Visual Studio 中的其他对话框保持样式一致，并避免模式对话框可能出现的问题。 有关详细信息，请参阅[创建和管理模式对话框](../extensibility/creating-and-managing-modal-dialog-boxes.md)。

3. 如果要开发 Visual Basic 项目，请从 `Window` 元素的 `x:Class` 属性中的 `WizardWindow` 类名删除 `ItemTemplateWizard` 命名空间。 此元素位于 XAML 的第一行。 完成后，第一行应类似于以下代码：

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. 在 WizardWindow.xaml 文件的代码隐藏文件中，将当前代码替换为以下代码。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs" id="Snippet7":::

## <a name="implement-the-wizard"></a>实现向导
 通过实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口定义向导的功能。

#### <a name="to-implement-the-wizard"></a>实现向导

1. 在 ItemTemplateWizard 项目中，打开 CustomActionWizard 代码文件，然后将此文件中的当前代码替换为以下代码 ：

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs" id="Snippet8":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb" id="Snippet8":::

## <a name="checkpoint"></a>检查点
 此时在本演练中，向导的所有代码现在都位于项目中。 生成项目，确保编译时不会产生错误。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="associate-the-wizard-with-the-item-template"></a>将向导与项模板关联
 实现向导后，必须完成三个主要步骤来将其与“自定义操作”项模板关联：

1. 使用强名称对向导程序集进行签名。

2. 获取向导程序集的公钥标记。

3. 在 .vstemplate 文件中为“自定义操作”项模板添加对向导程序集的引用。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>使用强名称对向导程序集进行签名

1. 在“解决方案资源管理器”中，打开 ItemTemplateWizard 项目节点的快捷菜单，然后选择“属性”  。

2. 在“签名”选项卡上，选中“为程序集签名”复选框。

3. 在“选择强名称密钥文件”列表中，选择“\<New...>” 。

4. 在“创建强名称密钥”对话框中，输入名称，取消选中“使用密码保护密钥文件”复选框，然后选择“确定”按钮  。

5. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>获取向导程序集的公钥标记

1. 在 Visual Studio 命令提示符窗口中，运行以下命令，将 PathToWizardAssembly 替换为开发计算机上 ItemTemplateWizard 项目的已生成 ItemTemplateWizard.dll 程序集的完整路径。

    ```xml
    sn.exe -T PathToWizardAssembly
    ```

     ItemTemplateWizard.dll 程序集的公钥标记被写入 Visual Studio 命令提示符窗口中。

2. 使 Visual Studio 命令提示符窗口保持在打开状态。 需要公钥标记才能完成下一过程。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>在 .vstemplate 文件中添加对向导程序集的引用

1. 在“解决方案资源管理器”中，展开 ItemTemplate 项目节点，然后打开 ItemTemplate.vstemplate 文件 。

2. 在临近文件末尾的位置，在 `</TemplateContent>` 和 `</VSTemplate>` 标记之间添加以下 `WizardExtension` 元素。 将 `PublicKeyToken` 属性的“YourToken”值替换为在上一过程中获取的公钥标记。

    ```xml
    <WizardExtension>
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>
    </WizardExtension>
    ```

     有关 `WizardExtension` 元素的详细信息，请参阅 [WizardExtension 元素（Visual Studio 模板）](../extensibility/wizardextension-element-visual-studio-templates.md)。

3. 保存并关闭该文件。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>向项模板中的 Elements.xml 文件添加可替换参数
 向 ItemTemplate 项目中的的 Elements.xml 文件添加几个可替换参数。 这些参数在之前定义的 `CustomActionWizard` 类的 `PopulateReplacementDictionary` 方法中初始化。 用户将“自定义操作”项目项添加到项目时，Visual Studio 会自动将新项目项中 Elements.xml 文件中的这些参数替换为它们在向导中指定的值。

 可替换参数是一个以美元符号 ($) 字符开头和结尾的标记。 除了定义自己的可替换参数之外，你还可以使用 SharePoint 项目系统定义和初始化的内置参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>向 Elements.xml 文件添加可替换参数

1. 在 ItemTemplate 项目中，将 Elements.xml 文件的内容替换为以下 XML。

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

     新的 XML 将 `Id`、`GroupId`、`Location`、`Description` 和 `Url` 属性的值更改为可替换参数。

2. 保存并关闭该文件。

## <a name="add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包
 在 VSIX 项目的 source.extension.vsixmanifest 文件中，添加对向导项目的引用，以便使用包含项目项的 VSIX 包进行部署。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包

1. 在“解决方案资源管理器”中，打开 CustomActionProjectItem 项目中的 source.extension.vsixmanifest 文件的快捷菜单，然后选择“打开”以打开清单编辑器中的文件  。

2. 选择清单编辑器中的“资产”选项卡，然后选择“新建”按钮 。

     这时将显示“添加新资产”对话框。

3. 在“类型”列表中，选择“Microsoft.VisualStudio.Assembly” 。

4. 在“源”列表中，选择“当前解决方案中的项目” 。

5. 在“项目”列表中，选择“ItemTemplateWizard”，然后选择“确定”按钮  。

6. 在菜单栏上，选择“生成” > “生成解决方案”，然后确保解决方案在编译时不会出错 。

## <a name="test-the-wizard"></a>测试向导
 现在，你已准备好测试向导。 首先，开始调试 Visual Studio 实验实例中的 CustomActionProjectItem 解决方案。 然后在 Visual Studio 实验实例中的 SharePoint 项目中测试“自定义操作”项目项的向导。 最后，生成并运行 SharePoint 项目，以验证自定义操作是否正常如期工作。

#### <a name="to-start-to-debug-the-solution"></a>开始调试解决方案

1. 使用管理凭据重启 Visual Studio，然后打开 CustomActionProjectItem 解决方案。

2. 在 ItemTemplateWizard 项目中，打开 CustomActionWizard 代码文件，然后将断点添加到 `RunStarted` 方法的第一行代码。

3. 在菜单栏上，选择“调试” > “异常” 。

4. 在“异常”对话框中，确保取消选中“公共语言运行时异常”的“引发”和“用户未处理”复选框，然后选择“确定”按钮    。

5. 通过选择 F5 键，或在菜单栏上选择“调试” > “开始调试”，以开始调试  。

     Visual Studio 将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Action Project Item\1.0，并启动 Visual Studio 的实验实例。 你将在此 Visual Studio 实例中测试项目项。

#### <a name="to-test-the-wizard-in-visual-studio"></a>在 Visual Studio 中测试向导

1. 在 Visual Studio 的实验实例的菜单栏上，选择“文件” > “新建” > “项目”  。

2. 展开“Visual C#”或“Visual Basic”节点（具体取决于你的项模板支持的语言），展开“SharePoint”节点，然后选择“2010”节点   。

3. 在项目模板列表中，选择“SharePoint 2010 项目”，将项目命名为“CustomActionWizardTest”，然后选择“确定”按钮  。

4. 在“SharePoint 自定义向导”中，输入要用于调试的站点的 URL，然后选择“完成”按钮 。

5. 在“解决方案资源管理器”中，打开项目节点的快捷菜单，选择“添加”，然后选择“新建项”  。

6. 在“添加新项目 - CustomItemWizardTest”对话框中，展开“SharePoint”节点，然后展开“2010”节点  。

7. 在项目项列表中，选择“自定义操作”项，然后选择“添加”按钮 。

8. 验证 Visual Studio 的其他实例中的代码是否在你之前在 `RunStarted` 方法中设置的断点处停止。

9. 通过选择 F5 键，或在菜单栏上选择“调试” > “继续”，以继续调试  。

     “SharePoint 自定义向导”随即出现。

10. 在“位置”下，选择“列表编辑”选项按钮 。

11. 在“组 ID”列表中，选择“通信” 。

12. 在“标题”框中，输入“SharePoint 开发人员中心” 。

13. 在“说明”框中，输入“打开 SharePoint 开发人员中心网站” 。

14. 在“URL”框中，输入 `https://docs.microsoft.com/sharepoint/dev/`，然后选择“完成”按钮 。

     Visual Studio 将一个名为“CustomAction1”的项添加到项目中，然后在编辑器中打开“Elements.xml”文件。 验证 Elements.xml 是否包含你在向导中指定的值。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>测试 SharePoint 中的自定义操作

1. 在 Visual Studio 的实验实例中，选择 F5 键，或在菜单栏上选择“调试” > “开始调试”  。

     自定义操作被打包并部署到由项目的“站点 URL”属性指定的 SharePoint 站点，Web 浏览器将打开此站点的默认页面。

    > [!NOTE]
    > 如果显示“脚本调试已禁用”对话框，请选择“是”按钮 。

2. 在 SharePoint 站点的“列表”区域中，选择“任务”链接。

     将显示“任务 - 所有任务”页。

3. 在功能区的“列表工具”选项卡上，选择“列表”选项卡，然后在“设置”组中选择“列表设置”   。

     将显示“列表设置”页。

4. 在靠近页面顶部的“通信”标题下，选择“SharePoint 开发人员中心”链接，验证浏览器是否打开了网站 `https://docs.microsoft.com/sharepoint/dev/`，然后关闭浏览器 。

## <a name="cleaning-up-the-development-computer"></a>清理开发计算机
 完成项目项测试后，从 Visual Studio 实验实例中删除项目项模板。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio 实验实例的菜单栏上，选择“工具” > “扩展和更新” 。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择“自定义操作项目项”扩展，然后选择“卸载”按钮 。

3. 在出现的对话框中，选择“是”按钮以确认要卸载扩展，然后选择“立即重启”按钮以完成卸载 。

4. 关闭 Visual Studio 的两个实例（实验实例和 CustomActionProjectItem 解决方案在其中打开的 Visual Studio 实例）。

## <a name="see-also"></a>另请参阅
- [演练：使用项模板创建自定义操作项目项（第 1 部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
- [默认自定义操作位置和 ID](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))
