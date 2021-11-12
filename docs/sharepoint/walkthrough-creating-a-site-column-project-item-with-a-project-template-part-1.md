---
title: 使用项目模板创建网站栏项目项（第 1 部分）
titleSuffix: ''
description: 定义用于创建网站栏的项目项类型，然后创建项目模板，以用于创建包含项目项的 SharePoint 项目。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 6ede65c0360a747c21d640e15b28c8b1dffe0583
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665275"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-1"></a>演练：使用项目模板创建网站栏项目项（第 1 部分）
  SharePoint 项目是一个或多个 SharePoint 项目项的容器。 可以通过创建自己的 SharePoint 项目项类型，然后将它们与项目模板相关联，从而在 Visual Studio 中扩展 SharePoint 项目系统。 在本演练中，你将定义用于创建网站栏的项目项类型，然后创建项目模板，这些模板可用于创建包含网站栏项目项的新项目。

 本演练演示了下列任务：

- 创建 Visual Studio 扩展，该扩展可定义网站栏的 SharePoint 项目项的新类型。 项目项类型包括显示在“属性”窗口中的简单自定义属性。

- 为项目项创建 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目模板。

- 生成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包以部署项目模板和扩展程序集。

- 调试和测试项目项。

  这是独立的演练。 完成本演练后，可通过向项目模板添加向导来增强项目项。 有关详细信息，请参阅[演练：使用项目模板创建网站栏项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

> [!NOTE]
> 有关一系列示例工作流，请参阅 [SharePoint 工作流示例](/sharepoint/dev/general-development/sharepoint-workflow-samples)。

## <a name="prerequisites"></a>先决条件
 需要在开发计算机上使用以下组件来完成本演练：

- 受支持的 Microsoft Windows、SharePoint 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 版本。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] 本演练使用 SDK 中的“VSIX 项目”模板来创建用于部署项目项的 VSIX 包。 有关详细信息，请参阅[在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念将很有用，但对于完成本演练来说，并不是必需的：

- SharePoint 中的网站栏。 有关详细信息，请参阅[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))。

- Visual Studio 中的项目模板。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，需要创建三个项目：

- 一个 VSIX 项目。 此项目创建用于部署网站栏项目项和项目模板的 VSIX 包。

- 一个项目模板项目。 此项目创建一个项目模板，该模板可用于创建包含网站栏项目项的新 SharePoint 项目。

- 一个类库项目。 此项目实现一个 Visual Studio 扩展，用于定义网站栏项目项的行为。

  通过创建这些项目来开始进行演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在“新建项目”对话框顶部，确保已在 .NET Framework 版本列表中选中“.NET Framework 4.5” 。

4. 展开“Visual Basic”或“Visual C#”节点，然后选择“扩展性”节点  。

    > [!NOTE]
    > “扩展性”节点仅在安装了 Visual Studio SDK 时可用。 有关详细信息，请参阅本主题前面的“先决条件”部分。

5. 在项目模板列表中，选择“VSIX 项目”。

6. 在“名称”框中输入“SiteColumnProjectItem”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将 SiteColumnProjectItem 项目添加到解决方案资源管理器 。

#### <a name="to-create-the-project-template-project"></a>创建项目模板项目

1. 在“解决方案资源管理器”中，打开解决方案节点的快捷菜单，选择“添加”，然后选择“新建项目”  。

2. 在“新建项目”对话框顶部，确保已在 .NET Framework 版本列表中选中“.NET Framework 4.5” 。

3. 展开“Visual C#”或“Visual Basic”节点，然后选择“扩展性”节点  。

4. 在项目模板列表中，选择“C# 项目模板”或“Visual Basic 项目模板”模板 。

5. 在“名称”框中输入“SiteColumnProjectTemplate”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将 SiteColumnProjectTemplate 项目添加到解决方案。

6. 从项目中删除 Class1 代码文件。

7. 如果创建了 Visual Basic 项目，还需要从项目中删除以下文件：

    - *MyApplication.Designer.vb*

    - MyApplication.myapp

    - *Resources.Designer.vb*

    - *Resources.resx*

    - *Settings.Designer.vb*

    - Settings.settings

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在“解决方案资源管理器”中，打开解决方案节点的快捷菜单，选择“添加”，然后选择“新建项目”  。

2. 在“新建项目”对话框顶部，确保已在 .NET Framework 版本列表中选中“.NET Framework 4.5” 。

3. 展开“Visual C#”或“Visual Basic”节点，选择“Windows”节点，然后选择“类库”模板   。

4. 在“名称”框中输入“ProjectItemTypeDefinition”，然后选择“确定”按钮  。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将 ProjectItemTypeDefinition 项目添加到解决方案，并打开默认 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 添加代码文件和程序集引用以配置扩展项目。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 ProjectItemTypeDefinition 项目中，添加名为 SiteColumnProjectItemTypeProvider 的代码文件。

2. 在菜单栏上，选择“项目” > “添加引用”。

3. 在“引用管理器 - ProjectItemTypeDefinition”对话框中，展开“程序集”节点，选择“Framework”节点，然后选中“System.ComponentModel.Composition”复选框  。

4. 选择“扩展”节点，选中 Microsoft.VisualStudio.SharePoint 程序集旁边的复选框，然后选择“确认”按钮 。

## <a name="define-the-new-sharepoint-project-item-type"></a>定义新的 SharePoint 项目项类型
 创建一个可实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的类，以定义新项目项类型的行为。 每当要定义新类型的项目项时都实现此接口。

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>定义新的 SharePoint 项目项类型

1. 在 SiteColumnProjectItemTypeProvider 代码文件中，将默认代码替换为以下代码，然后保存该文件。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.vb" id="Snippet1":::

## <a name="create-a-visual-studio-project-template"></a>创建一个 Visual Studio 项目模板
 通过创建项目模板，可让其他开发人员创建包含网站栏项目项的 SharePoint 项目。 SharePoint 项目模板包括 Visual Studio 中所有项目所需的文件，例如 .csproj 或 .vbproj 和 .vstemplate 文件，以及特定于 SharePoint 项目的文件  。 有关详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 在此过程中，你将创建一个空 SharePoint 项目以生成特定于 SharePoint 项目的文件。 然后，将这些文件添加到 SiteColumnProjectTemplate 项目，使这些文件包含在从此项目生成的模板中。 还可以配置 SiteColumnProjectTemplate 项目文件，以指定项目模板在“新建项目”对话框中的显示位置。

#### <a name="to-create-the-files-for-the-project-template"></a>创建项目模板的文件

1. 使用管理凭据启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的第二个实例。

2. 创建名为 BaseSharePointProject 的 SharePoint 2010 项目。

   > [!IMPORTANT]
   > 在“SharePoint 自定义向导”中，请勿选择“部署为场解决方案”选项按钮 。

3. 向项目添加一个“空元素”项，然后将该项命名为“Field1”。

4. 保存项目，然后关闭 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的第二个实例。

5. 在打开了 SiteColumnProjectItem 解决方案的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 实例中，在“解决方案资源管理器”中打开“SiteColumnProjectTemplate”项目节点的快捷菜单，选择“添加”，然后选择“现有项”   。

6. 在“添加现有项”对话框中，打开文件扩展名列表，然后选择“所有文件”(\*.\*) 。

7. 在包含 BaseSharePointProject 项目的目录中，选择 key.snk 文件，然后选择“添加”按钮。

   > [!NOTE]
   > 在本演练中，创建的项目模板会使用相同的 key.snk 文件对使用该模板创建的每个项目进行签名。 若要了解如何扩展此示例来为每个项目实例创建不同的 key.snk 文件，请参阅[演练：使用项目模板创建网站栏项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

8. 重复步骤 5-8，从 BaseSharePointProject 目录中指定的子文件夹添加以下文件：

   - *\Field1\Elements.xml*

   - *\Field1\SharePointProjectItem.spdata*

   - *\Features\Feature1\Feature1.feature*

   - *\Features\Feature1\Feature1.Template.xml*

   - *\Package\Package.package*

   - *\Package\Package.Template.xml*

     将这些文件直接添加到 SiteColumnProjectTemplate 项目；请勿在项目中重新创建 Field1、Features 或 Package 子文件夹。 有关这些文件的详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

#### <a name="to-configure-how-developers-discover-the-project-template-in-the-new-project-dialog-box"></a>配置开发人员在“新建项目”对话框中发现项目模板的方式

1. 在“解决方案资源管理器”中，打开“SiteColumnProjectTemplate”项目节点的快捷菜单，然后选择“卸载项目”  。 如果系统提示你保存对任意文件的更改，请选择“是”按钮。

2. 再次打开“SiteColumnProjectTemplate”节点的快捷菜单，然后选择“编辑 SiteColumnProjectTemplate.csproj”或“编辑 SiteColumnProjectTemplate.vbproj”  。

3. 在项目文件中找到以下 `VSTemplate` 元素。

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
    ```

4. 将此元素替换为以下 XML。

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath` 元素指定在生成项目时创建项目模板所在路径中的其他文件夹。 此处指定的文件夹可确保项目模板仅在客户打开“新建项目”对话框、展开“SharePoint”节点，然后选择“2010”节点时可用  。

5. 保存并关闭该文件。

6. 在“解决方案资源管理器”中，打开“SiteColumnProjectTemplate”项目的快捷菜单，然后选择“重新加载项目”  。

## <a name="edit-the-project-template-files"></a>编辑项目模板文件
 在 SiteColumnProjectTemplate 项目中，编辑以下文件以定义项目模板的行为：

- *AssemblyInfo.cs* 或 *AssemblyInfo.vb*

- Elements.xml

- *SharePointProjectItem.spdata*

- *Feature1.feature*

- *Package.package*

- *SiteColumnProjectTemplate.vstemplate*

- *ProjectTemplate.csproj* 或 *ProjectTemplate.vbproj*

  在以下过程中，你将向其中一些文件添加可替换参数。 可替换参数是以美元符号 ($) 字符开头和结尾的标记。 当用户使用此项目模板创建项目时，Visual Studio 会自动将新项目中的这些参数替换为特定值。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-edit-the-assemblyinfocs-or-assemblyinfovb-file"></a>编辑 AssemblyInfo.cs 或 AssemblyInfo.vb 文件

1. 在 SiteColumnProjectTemplate 项目中，打开 AssemblyInfo.cs 或 AssemblyInfo.vb 文件，然后在文件顶部添加以下语句 ：

    ```vb
    Imports System.Security
    ```

    ```csharp
    using System.Security;
    ```

     当 SharePoint 项目的“沙盒解决方案”属性设置为“True”时，Visual Studio 会将 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 添加到 AssemblyInfo 代码文件中 。 但是，默认情况下，项目模板中的 AssemblyInfo 代码文件不会导入 <xref:System.Security> 命名空间。 必须添加此“using”或“Imports”语句以防止编译错误 。

2. 保存并关闭该文件。

#### <a name="to-edit-the-elementsxml-file"></a>编辑 Elements.xml 文件

1. 在 SiteColumnProjectTemplate 项目中，将 Elements.xml 文件的内容替换为以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
          Name="$safeprojectname$"
          DisplayName="$projectname$"
          Type="Text"
          Group="Custom Columns">
      </Field>
    </Elements>
    ```

     新的 XML 会添加一个 `Field` 元素，该元素定义网站栏的名称、其基类型以及在库中列出网站栏的组。 有关此文件内容的详细信息，请参阅[字段定义架构](/previous-versions/office/developer/sharepoint-2010/ms196289(v=office.14))。

2. 保存并关闭该文件。

#### <a name="to-edit-the-sharepointprojectitemspdata-file"></a>编辑 SharePointProjectItem.spdata 文件

1. 在 SiteColumnProjectTemplate 项目中，将 SharePointProjectItem.spdata 文件的内容替换为以下 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <ProjectItem Type="Contoso.SiteColumn" DefaultFile="Elements.xml"
                xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
     <Files>
       <ProjectItemFile Source="Elements.xml" Target="$safeprojectname$\" Type="ElementManifest" />
     </Files>
   </ProjectItem>
   ```

    新的 XML 对文件进行了以下更改：

   - 将 `ProjectItem` 元素的 `Type` 属性更改为与在项目项定义（之前在本演练中创建的 `SiteColumnProjectItemTypeProvider` 类）上传递给 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 的相同字符串。

   - 从 `ProjectItem` 元素中删除 `SupportedTrustLevels` 和 `SupportedDeploymentScopes` 属性。 由于信任级别和部署范围是在 ProjectItemTypeDefinition 项目的 `SiteColumnProjectItemTypeProvider` 类中指定的，因此不需要这些属性值。

     有关 .spdata 文件内容的详细信息，请参阅 [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-feature1feature-file"></a>编辑 Feature1.feature 文件

1. 在 SiteColumnProjectTemplate 项目中，将 Feature1.feature 文件的内容替换为以下 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <feature xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="$guid4$" featureId="$guid4$"
            imageUrl="" solutionId="00000000-0000-0000-0000-000000000000" title="Site Column Feature1" version=""
            deploymentPath="$SharePoint.Project.FileNameWithoutExtension$_$SharePoint.Feature.FileNameWithoutExtension$"
            xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/FeatureModel">
     <projectItems>
       <projectItemReference itemId="$guid2$" />
     </projectItems>
   </feature>
   ```

    新的 XML 对文件进行了以下更改：

   - 将 `feature` 元素的 `Id` 和 `featureId` 属性的值更改为 `$guid4$`。

   - 将 `projectItemReference` 元素的 `itemId` 属性的值更改为 `$guid2$`。

     有关 .feature 文件的详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-packagepackage-file"></a>编辑 Package.package 文件

1. 在 SiteColumnProjectTemplate 项目中，将 Package.package 文件的内容替换为以下 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <package xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0"
            Id="$guid3$" solutionId="$guid3$" resetWebServer="false" name="$safeprojectname$"
            xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/PackageModel">
     <features>
       <featureReference itemId="$guid4$" />
     </features>
   </package>
   ```

    新的 XML 对文件进行了以下更改：

   - 将 `package` 元素的 `Id` 和 `solutionId` 属性的值更改为 `$guid3$`。

   - 将 `featureReference` 元素的 `itemId` 属性的值更改为 `$guid4$`。

     有关 .package 文件的详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-sitecolumnprojecttemplatevstemplate-file"></a>编辑 sitecolumnprojecttemplate.vstemplate 文件

1. 在 SiteColumnProjectTemplate 项目中，将 SiteColumnProjectTemplate.vstemplate 文件的内容替换为以下 XML 部分之一。

   - 如果要创建 Visual C# 项目模板，请使用以下 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">
     <TemplateData>
       <Name>Site Column</Name>
       <Description>Creates a new site column in SharePoint</Description>
       <FrameworkVersion>3.5</FrameworkVersion>
       <ProjectType>CSharp</ProjectType>
       <CreateNewFolder>true</CreateNewFolder>
       <CreateInPlace>true</CreateInPlace>
       <ProvideDefaultName>true</ProvideDefaultName>
       <DefaultName>SiteColumn</DefaultName>
       <LocationField>Enabled</LocationField>
       <EnableLocationBrowseButton>true</EnableLocationBrowseButton>
       <PromptForSaveOnCreation>true</PromptForSaveOnCreation>
       <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
       <Icon>SiteColumnProjectTemplate.ico</Icon>
       <SortOrder>1000</SortOrder>
     </TemplateData>
     <TemplateContent>
       <Project TargetFileName="SharePointProject1.csproj" File="ProjectTemplate.csproj" ReplaceParameters="true">
         <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>
         <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
       </Project>
     </TemplateContent>
   </VSTemplate>
   ```

   - 如果要创建 Visual Basic 项目模板，请使用以下 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">
     <TemplateData>
       <Name>Site Column</Name>
       <Description>Creates a new site column in SharePoint</Description>
       <FrameworkVersion>3.5</FrameworkVersion>
       <ProjectType>VisualBasic</ProjectType>
       <CreateNewFolder>true</CreateNewFolder>
       <CreateInPlace>true</CreateInPlace>
       <ProvideDefaultName>true</ProvideDefaultName>
       <DefaultName>SiteColumn</DefaultName>
       <LocationField>Enabled</LocationField>
       <EnableLocationBrowseButton>true</EnableLocationBrowseButton>
       <PromptForSaveOnCreation>true</PromptForSaveOnCreation>
       <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
       <Icon>SiteColumnProjectTemplate.ico</Icon>
       <SortOrder>1000</SortOrder>
     </TemplateData>
     <TemplateContent>
       <Project TargetFileName="SharePointProject1.vbproj" File="ProjectTemplate.vbproj" ReplaceParameters="true">
         <ProjectItem ReplaceParameters="true" TargetFileName="My Project\AssemblyInfo.vb">AssemblyInfo.vb</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>
         <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
       </Project>
     </TemplateContent>
   </VSTemplate>
   ```

    新的 XML 对文件进行了以下更改：

   - 将 `Name` 元素设置为值“Site Column”。 （此名称出现在“新建项目”对话框中）。

   - 为每个项目实例中包含的每个文件添加 `ProjectItem` 元素。

   - 使用 `http://schemas.microsoft.com/developer/vstemplate/2005` 命名空间。 此解决方案中的其他项目文件使用 `http://schemas.microsoft.com/developer/msbuild/2003` 命名空间。 因此，将生成 XML 架构警告消息，但在本演练中可以忽略它们。

     有关 .vstemplate 文件内容的详细信息，请参阅 [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-projecttemplatecsproj-or-projecttemplatevbproj-file"></a>编辑 projecttemplate.csproj 或 projecttemplate.vbproj 文件

1. 在 SiteColumnProjectTemplate 项目中，将 ProjectTemplate.csproj 文件或 ProjectTemplate.vbproj 文件的内容替换为以下 XML 部分之一 。

    - 如果要创建 Visual C# 项目模板，请使用以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid>{$guid1$}</ProjectGuid>
        <OutputType>Library</OutputType>
        <AppDesignerFolder>Properties</AppDesignerFolder>
        <RootNamespace>$safeprojectname$</RootNamespace>
        <AssemblyName>$safeprojectname$</AssemblyName>
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
        <FileAlignment>512</FileAlignment>
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{14822709-B5A1-4724-98CA-57A101D1B079};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineConstants>DEBUG;TRACE</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <DebugType>pdbonly</DebugType>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <DefineConstants>TRACE</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
      <PropertyGroup>
        <SignAssembly>true</SignAssembly>
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="System" />
        <Reference Include="System.Core" />
        <Reference Include="System.Data" />
        <Reference Include="System.Data.DataSetExtensions" />
        <Reference Include="System.Web" />
        <Reference Include="System.Xml" />
        <Reference Include="System.Xml.Linq" />
        <Reference Include="Microsoft.SharePoint" />
        <Reference Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="Properties\AssemblyInfo.cs" />
      </ItemGroup>
      <ItemGroup>
        <None Include="Field1\SharePointProjectItem.spdata">
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>
        </None>
        <None Include="Field1\Elements.xml" />
      </ItemGroup>
      <ItemGroup>
        <None Include="key.snk" />
        <None Include="Package\Package.package">
          <PackageId>{$guid3$}</PackageId>
        </None>
        <None Include="Package\Package.Template.xml">
          <DependentUpon>Package.package</DependentUpon>
        </None>
        <None Include="Features\Feature1\Feature1.feature">
          <FeatureId>{$guid4$}</FeatureId>
        </None>
        <None Include="Features\Feature1\Feature1.Template.xml">
          <DependentUpon>Feature1.feature</DependentUpon>
        </None>
      </ItemGroup>
      <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />
    </Project>
    ```

    1. 如果要创建 Visual Basic 项目模板，请使用以下 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
        <ProductVersion>
        </ProductVersion>
        <SchemaVersion>
        </SchemaVersion>
        <ProjectGuid>{$guid1$}</ProjectGuid>
        <OutputType>Library</OutputType>
        <RootNamespace>$safeprojectname$</RootNamespace>
        <AssemblyName>$safeprojectname$</AssemblyName>
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
        <FileAlignment>512</FileAlignment>
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{D59BE175-2ED0-4C54-BE3D-CDAA9F3214C8};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>
        <OptionExplicit>On</OptionExplicit>
        <OptionCompare>Binary</OptionCompare>
        <OptionStrict>Off</OptionStrict>
        <OptionInfer>On</OptionInfer>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <DefineDebug>true</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <OutputPath>bin\Debug\</OutputPath>
        <WarningLevel>4</WarningLevel>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <DebugType>pdbonly</DebugType>
        <DefineDebug>false</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup>
        <SignAssembly>true</SignAssembly>
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="System" />
        <Reference Include="System.Core" />
        <Reference Include="System.Data" />
        <Reference Include="System.Data.DataSetExtensions" />
        <Reference Include="System.Xml" />
        <Reference Include="System.Xml.Linq" />
        <Reference Include="Microsoft.SharePoint" />
        <Reference Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Import Include="Microsoft.VisualBasic" />
        <Import Include="System" />
        <Import Include="System.Collections" />
        <Import Include="System.Collections.Generic" />
        <Import Include="System.Data" />
        <Import Include="System.Diagnostics" />
        <Import Include="System.Linq" />
        <Import Include="System.Xml.Linq" />
        <Import Include="Microsoft.SharePoint" />
        <Import Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="My Project\AssemblyInfo.vb" />
      </ItemGroup>
      <ItemGroup>
        <AppDesigner Include="My Project\" />
      </ItemGroup>
      <ItemGroup>
        <None Include="Features\Feature1\Feature1.feature">
          <FeatureId>{$guid4$}</FeatureId>
        </None>
        <None Include="Field1\SharePointProjectItem.spdata">
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>
        </None>
        <None Include="key.snk" />
        <None Include="Package\Package.package">
          <PackageId>{$guid3$}</PackageId>
        </None>
        <None Include="Package\Package.Template.xml">
          <DependentUpon>Package.package</DependentUpon>
        </None>
      </ItemGroup>
      <ItemGroup>
        <None Include="Features\Feature1\Feature1.Template.xml">
          <DependentUpon>Feature1.feature</DependentUpon>
        </None>
        <None Include="Field1\Elements.xml" />
      </ItemGroup>
      <Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />
    </Project>
    ```

     新的 XML 对文件进行了以下更改：

    - 使用 `TargetFrameworkVersion` 元素指定 .NET Framework 3.5，而不是 4.5。

    - 添加 `SignAssembly` 和 `AssemblyOriginatorKeyFile` 元素以对项目输出进行签名。

    - 为 SharePoint 项目使用的程序集引用添加 `Reference` 元素。

    - 为项目中的每个默认文件添加元素，例如 Elements.xml 和 SharePointProjectItem.spdata 。

2. 保存并关闭该文件。

## <a name="create-a-vsix-package-to-deploy-the-project-template"></a>创建 VSIX 包以部署项目模板
 若要部署扩展，请使用“SiteColumnProjectItem”解决方案中的 VSIX 项目来创建 VSIX 包。 首先，通过修改 VSIX 项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后通过生成解决方案来创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在“解决方案资源管理器”中，在 SiteColumnProjectItem 项目中，在清单编辑器里打开 source.extension.vsixmanifest 文件 。

     source.extension.vsixmanifest 文件是所有 VSIX 包所需的 extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在“产品名称”框中，输入“网站栏” 。

3. 在“作者”框中，输入“Contoso” 。

4. 在“说明”框中，输入“用于创建网站栏的 SharePoint 项目” 。

5. 选择“资产”选项卡，然后选择“新建”按钮 。

     随即将打开“添加新资产”对话框。

6. 在“类型”列表中，选择“Microsoft.VisualStudio.ProjectTemplate” 。

    > [!NOTE]
    > 此值与 extension.vsixmanifest 文件中的 `ProjectTemplate` 元素相对应。 此元素标识包含项目模板的 VSIX 包中的子文件夹。 有关详细信息，请参阅 [ProjectTemplate 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\))。

7. 在“源”列表中，选择“当前解决方案中的项目” 。

8. 在“项目”列表中，选择“SiteColumnProjectTemplate”，然后选择“确定”按钮  。

9. 再次选择“新建”按钮。

     随即将打开“添加新资产”对话框。

10. 在“类型”列表中，选择“Microsoft.VisualStudio.MefComponent” 。

    > [!NOTE]
    > 此值与 extension.vsixmanifest 文件中的 `MefComponent` 元素相对应。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅 [MEFComponent 元素（VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

11. 在“源”列表中，选择“当前解决方案中的项目” 。

12. 在“项目”列表中，选择“ProjectItemTypeDefinition”，然后选择“确定”按钮  。

13. 在菜单栏上，选择“生成” > “生成解决方案”，然后确保项目编译时没有出错 。

## <a name="test-the-project-template"></a>测试项目模板
 现在你可以测试项目模板了。 首先，在 Visual Studio 的实验性实例中开始调试 SiteColumnProjectItem 解决方案。 然后，在 Visual Studio 的实验性实例中测试“网站栏”项目。 最后，生成并运行 SharePoint 项目来验证网站栏是否按预期工作。

#### <a name="to-start-debugging-the-solution"></a>开始调试解决方案

1. 使用管理凭据重启 Visual Studio，然后打开 SiteColumnProjectItem 解决方案。

2. 在 SiteColumnProjectItemTypeProvider 代码文件中，将一个断点添加到 `InitializeType` 方法中的第一行代码，然后选择“F5”键开始调试。

     Visual Studio 将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Site Column\1.0，并启动 Visual Studio 的实验性实例。 你将在此 Visual Studio 实例中测试项目项。

#### <a name="to-test-the-project-in-visual-studio"></a>在 Visual Studio 中测试项目

1. 在 Visual Studio 的实验性实例中的菜单栏上，选择“文件” > “新建” > “项目”  。

2. 展开“Visual C#”或“Visual Basic”节点（具体取决于你的项目模板支持的语言），展开“SharePoint”节点，然后选择“2010”节点   。

3. 在项目模板列表中，选择“网站栏”模板。

4. 在“名称”框中，输入“SiteColumnTest”，然后选择“确定”按钮  。

     在“解决方案资源管理器”中，会显示一个新项目，其中包含名为“Field1”的项目项 。

5. 验证 Visual Studio 的其他实例中的代码是否在你之前在 `InitializeType` 方法中设置的断点处停止，然后选择“F5”键以继续调试项目。

6. 在“解决方案资源管理器”中，选择“Field1”节点，然后选择“F4”键  。

     此时将打开“属性”窗口。

7. 在属性列表中，验证是否显示了属性“示例属性”。

#### <a name="to-test-the-site-column-in-sharepoint"></a>测试 SharePoint 中的网站栏

1. 在“解决方案资源管理器”中，选择“SiteColumnTest”节点 。

2. 在“属性”窗口中，在“站点 URL”属性旁边的文本框中输入 http://localhost  。

     此步骤指定要用于调试的开发计算机上的本地 SharePoint 站点。

    > [!NOTE]
    > 默认情况下，“站点 URL”属性为空，因为“网站栏”项目模板不提供用于在创建项目时收集此值的向导。 若要了解如何添加向导来向开发人员询问此值并在新项目中配置此属性，请参阅[演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

3. 选择 F5。

     网站栏会打包并部署到项目的“站点 URL”属性中指定的 SharePoint 站点。 Web 浏览器将打开此站点的默认页面。

    > [!NOTE]
    > 如果显示“脚本调试已禁用”对话框，请选择“是”按钮以继续调试项目 。

4. 在“网站操作”菜单上，选择“网站设置” 。

5. 在“网站设置”页上的“库”列表下，选择“网站栏”链接  。

6. 在网站栏列表中，验证“自定义栏”组中是否包含名为“SiteColumnTest”的栏 。

7. 关闭 Web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成项目测试后，从 Visual Studio 的实验性实例中删除项目模板。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio 的实验性实例中的菜单栏上，选择“工具” > “扩展和更新” 。

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择“网站栏”扩展，然后选择“卸载”按钮 。

3. 在出现的对话框中，选择“是”按钮以确认要卸载扩展。

4. 选择“关闭”按钮以完成卸载。

5. 关闭 Visual Studio 的两个实例（实验性实例和打开了 SiteColumnProjectItem 解决方案的 Visual Studio 实例）。

## <a name="next-steps"></a>后续步骤
 完成本演练后，可向项目模板添加一个向导。 当用户创建“网站栏”项目时，向导会要求用户提供用于调试的站点 URL 以及询问用户是否对新的解决方案进行了沙盒处理，向导将使用此信息配置新的项目。 向导还会收集有关该栏的信息（例如基类型和网站栏库中列出该栏的组）并将此信息添加到新项目中的 Elements.xml 文件中。 有关详细信息，请参阅[演练：使用项目模板创建网站栏项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>另请参阅

- [演练：使用项目模板创建网站栏项目项（第 2 部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)