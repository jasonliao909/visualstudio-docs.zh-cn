---
title: 用项目模板创建网站栏项目项（第1部分）
titleSuffix: ''
description: 定义用于创建网站列的项目项类型，然后创建用于创建包含项目项 SharePoint 项目的项目模板。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665275"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-1"></a>演练：使用项目模板创建网站栏项目项（第1部分）
  SharePoint 项目是一个或多个 SharePoint 项目项的容器。 你可以通过创建自己的 SharePoint 项目项类型，然后将其与项目模板关联，来扩展 Visual Studio 中的 SharePoint 项目系统。 在本演练中，您将定义用于创建网站列的项目项类型，然后您将创建一个可用于创建包含网站列项目项的新项目的项目模板。

 本演练演示了下列任务：

- 创建一个为网站列定义新类型的 SharePoint 项目项的 Visual Studio 扩展。 项目项类型包含一个简单的自定义属性，该属性显示在 " **属性** " 窗口中。

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]为项目项创建项目模板。

- 生成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包部署项目模板和扩展程序集。

- 调试和测试项目项。

  这是一个独立的演练。 完成本演练后，您可以通过向项目模板添加向导来增强项目项。 有关详细信息，请参阅 [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

> [!NOTE]
> 有关一系列示例工作流，请参阅[SharePoint 工作流示例](/sharepoint/dev/general-development/sharepoint-workflow-samples)。

## <a name="prerequisites"></a>先决条件
 若要完成本演练，开发计算机上需要以下组件：

- Microsoft Windows、SharePoint 和支持的版本 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] 本演练使用 SDK 中的 **vsix Project** 模板来创建用于部署项目项的 vsix 包。 有关详细信息，请参阅[Visual Studio 中的扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  以下概念的知识非常有用，但并不是必需的，无法完成本演练：

- SharePoint 中的网站列。 有关详细信息，请参阅 [列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))。

- Project Visual Studio 中的模板。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，需要创建三个项目：

- 一个 VSIX 项目。 此项目将创建用于部署网站列项目项和项目模板的 VSIX 包。

- 项目模板项目。 此项目创建一个项目模板，该模板可用于创建新的 SharePoint 项目，该项目包含网站列项目项。

- 一个类库项目。 此项目实现一个 Visual Studio 扩展，该扩展定义网站列项目项的行为。

  通过创建项目开始演练。

#### <a name="to-create-the-vsix-project"></a>创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在 "**新建 Project** " 对话框的顶部，确保在 .NET Framework 版本的列表中选择 **.NET Framework 4.5** 。

4. 展开 " **Visual Basic** " 或 " **Visual c #** " 节点，然后选择 "**扩展性**" 节点。

    > [!NOTE]
    > 仅当安装 Visual Studio SDK 时，"**扩展性**" 节点才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

5. 在项目模板列表中，选择 " **VSIX Project**"。

6. 在 " **名称** " 框中，输入 **SiteColumnProjectItem**，然后选择 " **确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **SiteColumnProjectItem** 项目添加到 **解决方案资源管理器**。

#### <a name="to-create-the-project-template-project"></a>创建项目模板项目

1. 在 **解决方案资源管理器** 中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建 Project**"。

2. 在 "**新建 Project** " 对话框的顶部，确保在 .NET Framework 版本的列表中选择 **.NET Framework 4.5** 。

3. 展开 " **Visual c #** " 或 " **Visual Basic** " 节点，然后选择 "**扩展性**" 节点。

4. 在项目模板列表中，选择 " **c # Project 模板** 或 **Visual Basic Project 模板**" 模板。

5. 在 " **名称** " 框中，输入 **SiteColumnProjectTemplate**，然后选择 " **确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **SiteColumnProjectTemplate** 项目添加到解决方案。

6. 从项目中删除 Class1 代码文件。

7. 如果创建了一个 Visual Basic 项目，还会从项目中删除以下文件：

    - *MyApplication*

    - MyApplication myapp

    - *资源. 设计器 .vb*

    - *资源 .resx*

    - *设置。设计器 .vb*

    - 设置。设置

#### <a name="to-create-the-extension-project"></a>创建扩展项目

1. 在 **解决方案资源管理器** 中，打开 "解决方案" 节点的快捷菜单，选择 "**添加**"，然后选择 "**新建 Project**"。

2. 在 "**新建 Project** " 对话框的顶部，确保在 .NET Framework 版本的列表中选择 **.NET Framework 4.5** 。

3. 展开 " **Visual c #** " 或 " **Visual Basic** " 节点，选择 " **Windows** " 节点，然后选择 **"类库" 模板。**

4. 在 " **名称** " 框中，输入 **ProjectItemTypeDefinition** ，然后选择 " **确定"** 按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 **ProjectItemTypeDefinition** 项目添加到解决方案，并打开默认的 Class1 代码文件。

5. 从项目中删除 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 添加代码文件和程序集引用以配置扩展项目。

#### <a name="to-configure-the-project"></a>配置项目

1. 在 ProjectItemTypeDefinition 项目中，添加一个名为 **SiteColumnProjectItemTypeProvider** 的代码文件。

2. 在菜单栏上，选择“项目” > “添加引用”。

3. 在 " **引用管理器-ProjectItemTypeDefinition** " 对话框中，展开 " **程序集** " 节点，选择 " **框架** " 节点，然后选择 "system.componentmodel" 复选框。

4. 选择 "**扩展**" 节点，选中 VisualStudio 旁边的复选框。SharePoint "程序集"，然后选择 "**确定"** 按钮。

## <a name="define-the-new-sharepoint-project-item-type"></a>定义新的 SharePoint 项目项类型
 创建一个类，该类实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口以定义新项目项类型的行为。 每当要定义新类型的项目项时都实现此接口。

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>定义新的 SharePoint 项目项类型

1. 在 **SiteColumnProjectItemTypeProvider** 代码文件中，将默认代码替换为以下代码，然后保存该文件。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.vb" id="Snippet1":::

## <a name="create-a-visual-studio-project-template"></a>创建 Visual Studio 项目模板
 通过创建项目模板，可让其他开发人员创建包含网站列项目项 SharePoint 项目。 SharePoint 项目模板包括 Visual Studio 中的所有项目（如 *.csproj* 或 *.vbproj* 和 *.vstemplate* 文件）所需的文件，以及特定于 SharePoint 项目的文件。 有关详细信息，请参阅为[SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 在此过程中，您将创建一个空的 SharePoint 项目以生成特定于 SharePoint 项目的文件。 然后，将这些文件添加到 SiteColumnProjectTemplate 项目，以便将其包含在此项目生成的模板中。 你还将配置 SiteColumnProjectTemplate 项目文件以指定项目模板在 "**新建 Project** " 对话框中的显示位置。

#### <a name="to-create-the-files-for-the-project-template"></a>为项目模板创建文件

1. 使用管理凭据启动的第二个实例 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

2. 创建一个名为 **BaseSharePointProject** 的 SharePoint 2010 项目。

   > [!IMPORTANT]
   > 在 **SharePoint 自定义向导** 中，请不要选择 "**部署为场解决方案**" 选项按钮。

3. 向项目中添加一个空元素项，然后将该项命名为 **Field1**。

4. 保存项目，然后关闭的第二个实例 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

5. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 已打开 SiteColumnProjectItem 解决方案的实例中，在 **解决方案资源管理器** 中打开 " **SiteColumnProjectTemplate** " 项目节点的快捷菜单，选择 " **添加**"，然后选择 " **现有项**"。

6. 在 " **添加现有项** " 对话框中，打开文件扩展名列表，然后选择 " **所有文件" (\* " \*)**"。

7. 在包含 BaseSharePointProject 项目的目录中，选择 "密钥 .snk" 文件，然后选择 " **添加** " 按钮。

   > [!NOTE]
   > 在本演练中，你创建的项目模板使用相同的密钥 .snk 文件对使用模板创建的每个项目进行签名。 若要了解如何扩展此示例以为每个项目实例创建不同的 .snk 文件，请参阅 [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

8. 重复步骤5-8 以从 BaseSharePointProject 目录的指定子文件夹中添加以下文件：

   - *\Field1\Elements.xml*

   - *\Field1\SharePointProjectItem.spdata*

   - *\Features\Feature1\Feature1.feature*

   - *\Features\Feature1\Feature1.Template.xml*

   - *\Package\Package.package*

   - *\Package\Package.Template.xml*

     将这些文件直接添加到 SiteColumnProjectTemplate 项目;请勿在项目中重新创建 Field1、Features 或 Package 子文件夹。 有关这些文件的详细信息，请参阅[创建项目模板和项目模板SharePoint项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

#### <a name="to-configure-how-developers-discover-the-project-template-in-the-new-project-dialog-box"></a>在"新建项目"对话框中配置开发人员Project模板

1. 在 **解决方案资源管理器** 中，打开 **SiteColumnProjectTemplate** 项目 **节点** 的快捷菜单，然后选择"卸载Project"。 如果系统提示你保存对任意文件的更改，请选择" **是"** 按钮。

2. 再次打开 **SiteColumnProjectTemplate** 节点的快捷菜单，然后选择"编辑 **SiteColumnProjectTemplate.csproj"** 或"**编辑 SiteColumnProjectTemplate.vbproj"。**

3. 在项目文件中，找到以下 `VSTemplate` 元素。

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
    ```

4. 将此元素替换为以下 XML。

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素在生成项目时创建项目模板的路径中指定其他文件夹。 此处指定的文件夹可确保项目模板仅在客户打开"新建 Project"对话框、展开"SharePoint"节点，然后选择 **"2010"** 节点时可用。 

5. 保存并关闭该文件。

6. 在 **解决方案资源管理器** 中，打开 **SiteColumnProjectTemplate** 项目的快捷菜单，然后选择"重载 **Project"。**

## <a name="edit-the-project-template-files"></a>编辑项目模板文件
 在 SiteColumnProjectTemplate 项目中，编辑以下文件以定义项目模板的行为：

- *AssemblyInfo.cs* 或 *AssemblyInfo.vb*

- Elements.xml

- *SharePointProjectItem.spdata*

- *Feature1.feature*

- *Package.package*

- *SiteColumnProjectTemplate.vstemplate*

- *ProjectTemplate.csproj* 或 *ProjectTemplate.vbproj*

  在下列过程，你将向其中一些文件添加可替换参数。 可替换参数是一种以美元符号开头和结尾的标记， ($) 字符。 当用户使用此项目模板创建项目时，Visual Studio自动将新项目中的这些参数替换为特定值。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-edit-the-assemblyinfocs-or-assemblyinfovb-file"></a>编辑 AssemblyInfo.cs 或 AssemblyInfo.vb 文件

1. 在 SiteColumnProjectTemplate 项目中，打开 *AssemblyInfo.cs* 或 *AssemblyInfo.vb* 文件，然后将以下语句添加到其顶部：

    ```vb
    Imports System.Security
    ```

    ```csharp
    using System.Security;
    ```

     当项目 **沙盒解决方案** 属性SharePoint设置为 **True** 时，Visual Studio将 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 添加到 AssemblyInfo 代码文件。 但是，默认情况下，项目模板中的 AssemblyInfo 代码文件不会 <xref:System.Security> 导入命名空间。 必须添加此 **using 或** **Imports** 语句以防止编译错误。

2. 保存并关闭该文件。

#### <a name="to-edit-the-elementsxml-file"></a>编辑Elements.xml文件

1. 在 SiteColumnProjectTemplate 项目中，将Elements.xml *文件的内容* 替换为以下 XML。

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

     新 XML 添加一个 元素，该元素定义站点列的名称、其基类型和要列出库中 `Field` 的站点列的组。 有关此文件的内容详细信息，请参阅 [字段定义架构](/previous-versions/office/developer/sharepoint-2010/ms196289(v=office.14))。

2. 保存并关闭该文件。

#### <a name="to-edit-the-sharepointprojectitemspdata-file"></a>编辑 SharePointProjectItem.spdata 文件

1. 在 SiteColumnProjectTemplate 项目中，将 *SharePointProjectItem.spdata* 文件的内容替换为以下 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <ProjectItem Type="Contoso.SiteColumn" DefaultFile="Elements.xml"
                xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
     <Files>
       <ProjectItemFile Source="Elements.xml" Target="$safeprojectname$\" Type="ElementManifest" />
     </Files>
   </ProjectItem>
   ```

    新 XML 对文件进行以下更改：

   - 将 元素的 属性更改为传递给项目项定义上的 的相同字符串， (之前在此演练中创建的 `Type` `ProjectItem` <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> `SiteColumnProjectItemTypeProvider` 类) 。

   - 从 元素 `SupportedTrustLevels` `SupportedDeploymentScopes` 中删除 和 `ProjectItem` 属性。 由于信任级别和部署范围在 ProjectItemTypeDefinition 项目的 类中指定，因此不需要 `SiteColumnProjectItemTypeProvider` 这些属性值。

     有关 *.spdata* 文件内容的详细信息，请参阅 SharePoint [项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-feature1feature-file"></a>编辑 Feature1.feature 文件

1. 在 SiteColumnProjectTemplate 项目中，将 *Feature1.feature* 文件的内容替换为以下 XML。

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

    新 XML 对文件进行以下更改：

   - 将 元素的 `Id` 和 `featureId` 属性的值 `feature` 更改为 `$guid4$` 。

   - 将 元素的 `itemId` 属性的值 `projectItemReference` 更改为 `$guid2$` 。

     有关 *.feature 文件的详细信息*，请参阅创建项目模板和项目模板 [SharePoint项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-packagepackage-file"></a>编辑 Package.package 文件

1. 在 SiteColumnProjectTemplate 项目中，将 *Package.package* 文件的内容替换为以下 XML。

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

    新 XML 对文件进行以下更改：

   - 将 元素的 `Id` 和 `solutionId` 属性的值 `package` 更改为 `$guid3$` 。

   - 将 元素的 `itemId` 属性的值 `featureReference` 更改为 `$guid4$` 。

     有关 *.package 文件的详细信息*，请参阅创建项目模板和项目模板 [SharePoint项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

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

   - 如果要创建一个Visual Basic模板，请使用以下 XML。

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

    新 XML 对文件进行以下更改：

   - 将 `Name` 元素设置为值 **Site Column**。  (此名称将显示在"**新建Project对话框中**) 。

   - 为 `ProjectItem` 每个项目实例中包含的每个文件添加元素。

   - 使用命名空间 `http://schemas.microsoft.com/developer/vstemplate/2005` 。 此解决方案中的其他项目文件使用 `http://schemas.microsoft.com/developer/msbuild/2003` 命名空间。 因此，将生成 XML 架构警告消息，但可以在此演练中忽略它们。

     有关 *.vstemplate* 文件的内容详细信息，请参阅 Visual Studio [模板架构参考](../extensibility/visual-studio-template-schema-reference.md)。

2. 保存并关闭该文件。

#### <a name="to-edit-the-projecttemplatecsproj-or-projecttemplatevbproj-file"></a>编辑 projecttemplate.csproj 或 projecttemplate.vbproj 文件

1. 在 SiteColumnProjectTemplate 项目中，将 *ProjectTemplate.csproj* 文件或 *ProjectTemplate.vbproj* 文件的内容替换为以下 XML 部分之一。

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

    1. 如果要创建一个Visual Basic模板，请使用以下 XML。

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

     新 XML 对文件进行以下更改：

    - 使用 `TargetFrameworkVersion` 元素指定 .NET Framework 3.5，而不是 4.5。

    - 添加 `SignAssembly` `AssemblyOriginatorKeyFile` 和 元素以对项目输出进行签名。

    - 为 `Reference` 项目使用的程序集引用SharePoint元素。

    - 为项目的每个默认文件添加元素，例如Elements.xml *SharePointProjectItem.spdata*。

2. 保存并关闭该文件。

## <a name="create-a-vsix-package-to-deploy-the-project-template"></a>创建 VSIX 包以部署项目模板
 若要部署扩展，请使用 **SiteColumnProjectItem** 解决方案中的 VSIX 项目创建 VSIX 包。 首先，通过修改 VSIX 项目中包含的 source.extension.vsixmanifest 文件来配置 VSIX 包。 然后，通过生成解决方案创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>配置和创建 VSIX 包

1. 在 **解决方案资源管理器** 中，在 **SiteColumnProjectItem** 项目中，在清单编辑器中打开 source.extension.vsixmanifest 文件。

     source.extension.vsixmanifest 文件是所有 VSIX 包都需要的 extension.vsixmanifest 文件的基础。 有关此文件的信息，请参阅 [VSIX 扩展架构 1.0 参考](/previous-versions/dd393700(v=vs.110))。

2. 在"**产品名称"** 框中，输入"**站点列"。**

3. 在"**创作"** 框中，输入 **"Contoso"。**

4. 在"**说明"** 框中，**输入SharePoint创建站点列的一个项目**。

5. 选择" **资产"** 选项卡，然后选择"新建 **"** 按钮。

     " **添加新资产"** 对话框随即打开。

6. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.ProjectTemplate"。**

    > [!NOTE]
    > 此值对应于 `ProjectTemplate` extension.vsixmanifest 文件中的元素。 此元素标识包含项目模板的 VSIX 包中的子文件夹。 有关详细信息，请参阅[PROJECTTemplate 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\))

7. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

8. 在 **"Project"** 列表中，选择 **"SiteColumnProjectTemplate"，** 然后选择"确定 **"** 按钮。

9. 再次选择 **"新建** "按钮。

     " **添加新资产"** 对话框随即打开。

10. 在"**类型"** 列表中，选择 **"Microsoft.VisualStudio.MefComponent"。**

    > [!NOTE]
    > 此值对应于 `MefComponent` extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中扩展程序集的名称。 有关详细信息，请参阅[MEFComponent 元素 (VSX 架构) 。 ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))

11. 在" **源"** 列表中， **选择当前解决方案 中的项目**。

12. 在 **Project，** 选择 **"ProjectItemTypeDefinition"，** 然后选择"确定 **"** 按钮。

13. 在菜单栏上，选择"**生成**  >  **生成解决方案**"，并确保项目编译时不会出错。

## <a name="test-the-project-template"></a>测试项目模板
 现在，可以测试项目模板了。 首先，开始调试 Visual Studio 实验实例中的 SiteColumnProjectItem 解决方案。 然后，在实例 **的实验** 实例中测试站点列Visual Studio。 最后，生成并运行SharePoint项目，以验证站点列是否正常工作。

#### <a name="to-start-debugging-the-solution"></a>开始调试解决方案

1. 使用Visual Studio凭据重启应用程序，然后打开 SiteColumnProjectItem 解决方案。

2. 在 SiteColumnProjectItemTypeProvider 代码文件中，将断点添加到 方法的第一行代码，然后选择 `InitializeType` **F5** 键以开始调试。

     Visual Studio将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Site Column\1.0 并启动 Visual Studio 的实验实例。 你将在此实例中测试项目项Visual Studio。

#### <a name="to-test-the-project-in-visual-studio"></a>在项目中测试Visual Studio

1. 在菜单栏上的Visual Studio实例中，选择"文件""新建  >    >  **Project"。**

2. 根据项目模板Visual Basic语言 () Visual **C#** 或 SharePoint 节点，展开 **SharePoint** 节点，然后选择 **2010** 节点。

3. 在项目模板列表中，选择"站点 **列"** 模板。

4. 在" **名称"** 框中，输入 **"SiteColumnTest"，** 然后选择"确定 **"** 按钮。

     在 **解决方案资源管理器** 中，将显示一个新项目，其项目项名为 **Field1**。

5. 验证其他 实例中的代码Visual Studio在之前在 方法中设置的断点处停止，然后选择 `InitializeType` **F5** 键以继续调试项目。

6. 在 **解决方案资源管理器** 中，选择 **"Field1"** 节点，然后选择 **F4** 键。

     此时将打开“属性”窗口。

7. 在属性列表中，验证属性" **示例属性"是否** 显示。

#### <a name="to-test-the-site-column-in-sharepoint"></a>测试站点列中的站点SharePoint

1. 在 **解决方案资源管理器** 中，选择 **"SiteColumnTest"** 节点。

2. 在 **"属性** "窗口的"站点 **URL"** 属性旁边的文本框中，输入 **http://localhost** 。

     此步骤指定SharePoint用于调试的开发计算机上本地站点。

    > [!NOTE]
    > " **站点 URL"** 属性默认为空，因为在创建项目时，"站点列"项目模板不提供用于收集此值的向导。 若要了解如何添加一个向导，要求开发人员提供此值，然后在新项目中配置此属性，请参阅演练：使用项目模板创建站点列项目项，第 [2 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

3. 选择 F5。

     该站点列打包并部署到SharePoint的"站点 **URL"** 属性中指定的站点站点。 Web 浏览器将打开此站点的默认页面。

    > [!NOTE]
    > 如果显示 **"脚本调试已禁用** "对话框，请选择" **是** "按钮以继续调试项目。

4. 在"**站点操作"** 菜单上，选择"**站点设置"。**

5. 在"**站点设置"** 页上的"**库"** 列表下，选择"**站点列"** 链接。

6. 在站点列列表中，验证自定义 **列组是否** 包含名为 **SiteColumnTest 的列**。

7. 关闭 Web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 完成项目测试后，从项目的实验实例中删除项目Visual Studio。

#### <a name="to-clean-up-the-development-computer"></a>清理开发计算机

1. 在 Visual Studio实验实例的菜单栏上，选择"**工具**  >  **扩展和更新"。**

     此时，“扩展和更新”对话框打开。

2. 在扩展列表中，选择"站点 **列** "扩展，然后选择"卸载 **"** 按钮。

3. 在出现的对话框中，选择" **是"** 按钮以确认要卸载扩展。

4. 选择" **关闭** "按钮以完成卸载。

5. 关闭实验实例Visual Studio (SiteColumnProjectItem 解决方案打开的 Visual Studio 实例的两个实例) 。

## <a name="next-steps"></a>后续步骤
 完成本演练后，可以将向导添加到项目模板。 当用户创建站点列项目时，向导会要求用户输入用于调试的站点 URL，以及新解决方案是否沙盒，并且向导使用此信息配置新项目。 向导还会收集有关列 (例如基类型和在站点列库中列出列的组) 并将此信息添加到新项目中的 *Elements.xml* 文件。 有关详细信息，请参阅演练：使用项目模板创建站点列项目项 [，第 2 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>另请参阅

- [演练：使用项目模板创建站点列项目项，第 2 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为项目项创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [将数据保存在项目系统的SharePoint扩展中](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)