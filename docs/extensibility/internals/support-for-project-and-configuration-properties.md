---
title: 支持Project和配置属性|Microsoft Docs
description: 了解如何在 IDE 中为你自己的项目类型提供Visual Studio页，该页可以显示项目和配置扩展属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project properties, supporting with Visual Studio SDK
- configuration properties, supporting with Visual Studio SDK
ms.assetid: 9fcfaa0f-7b41-4b68-82ec-7a151dca5d7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5d29e1d4b280454f8f5724dce207a6cf527b2c0d79b95b8ce799b88c8a7bf34e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337781"
---
# <a name="support-for-project-and-configuration-properties"></a>支持项目和配置属性
集成 **开发** 环境中 IDE (" [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 属性) 可以显示项目和配置属性。 可以为自己的项目类型提供属性页，以便用户可以设置应用程序的属性。

 通过在 解决方案资源管理器 中选择项目节点，然后单击"Project"菜单上的"属性"，**可以** 打开包含项目和配置属性的对话框。 在 和 中以及派生自这些语言的项目类型中，此对话框在"常规"的"环境"和"选项"对话框中显示为 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [选项卡式页面](../../ide/reference/general-environment-options-dialog-box.md)。 有关详细信息，请参阅不在生成中：演练：公开Project和配置属性[ (C#) 。 ](/previous-versions/bb166517(v=vs.100))

 用于项目的托管包框架 (MPFProj) 提供了用于创建和管理新项目系统的帮助程序类。 可以在 MPF for Projects - Visual Studio 2013[中查找源代码和编译Visual Studio 2013。](https://github.com/tunnelvisionlabs/MPFProj10)

## <a name="persistence-of-project-and-configuration-properties"></a>属性和Project的持久性
 Project和配置属性将保留于具有与项目类型关联的任何文件扩展名的项目文件中，例如 .csproj、.vbproj 和 .myproj。 语言项目通常使用模板文件生成项目文件。 但是，实际上有几种方法可以关联项目类型和模板。 有关详细信息，请参阅模板 [目录说明 (。Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)。

 Project项添加到模板文件，创建属性和配置属性。 然后，这些属性可用于使用此模板的项目类型创建的任何项目。 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]项目和 MPFProj 都使用不在生成MSBuild[模板](/previous-versions/visualstudio/visual-studio-2008/ms171452(v=vs.90))文件的概述架构。 这些文件具有每个配置的 PropertyGroup 节。 项目的属性通常保留于第一个 PropertyGroup 节中，该节的 Configuration 参数设置为 null 字符串。

 以下代码显示项目MSBuild的开始。

```
<Project MSBuildVersion="2.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Name>SomeProjectSix</Name>
    <SchemaVersion>2.0</SchemaVersion>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
    <Optimize>false</Optimize>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <Optimize>true</Optimize>
```

 在此项目文件中， `<Name>` 和 `<SchemaVersion>` 是项目属性， `<Optimize>` 是配置属性。

 项目负责保留项目文件的项目和配置属性。

> [!NOTE]
> 项目可以通过仅保留与默认值不同的属性值来优化持久性。

## <a name="support-for-project-and-configuration-properties"></a>支持项目和配置属性
 类 `Microsoft.VisualStudio.Package.SettingsPage` 实现项目和配置属性页。 的默认实现 `SettingsPage` 向泛型属性网格中的用户提供公共属性。 方法 `Microsoft.VisualStudio.Package.HierarchyNode.GetPropertyPageGuids` 为项目属性网格选择派生 `SettingsPage` 自 的类。 方法 `Microsoft.VisualStudio.Package.ProjectNode.GetConfigPropertyPageGuids` 为配置属性网格选择 `SettingsPage` 派生自 的类。 项目类型应重写这些方法以选择适当的属性页。

 类 `SettingsPage` 和 `Microsoft.VisualStudio.Package.ProjectNode` 类提供以下方法来保存项目和配置属性：

- `Microsoft.VisualStudio.Package.ProjectNode.GetProjectProperty` 和 `Microsoft.VisualStudio.Package.ProjectNode.SetProjectProperty` 保留项目属性。

- `Microsoft.VisualStudio.Package.SettingsPage.GetConfigProperty` 和 `Microsoft.VisualStudio.Package.SettingsPage.SetConfigProperty` 保留配置属性。

  > [!NOTE]
  > 和 类的实现使用 (MSBuild) 方法从项目文件获取和 `Microsoft.VisualStudio.Package.SettingsPage` `Microsoft.VisualStudio.Package.ProjectNode` `Microsoft.Build.BuildEngine` 设置项目和配置属性。

  派生自 的类 `SettingsPage` 必须实现 `Microsoft.VisualStudio.Package.SettingsPage.ApplyChanges` 和 `Microsoft.VisualStudio.Package.SettingsPage.BindProperties` ，以保留项目文件的项目或配置属性。

## <a name="provideobjectattribute-and-registry-path"></a>ProvideObjectAttribute 和注册表路径
 派生自 `SettingsPage` 的类设计为在 VSPackage 之间共享。 若要使 VSPackage 能够创建派生自 的类，请 `SettingsPage` 向派生自 `Microsoft.VisualStudio.Shell.ProvideObjectAttribute` 的类添加 `Microsoft.VisualStudio.Shell.Package` 。

 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/vssdksupportprojectconfigurationpropertiespackage.cs" id="Snippet1":::
 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/vssdksupportprojectconfigurationpropertiespackage.vb" id="Snippet1":::

 属性附加到的 VSPackage 并不重要。 向 注册 VSPackage 时，将注册 (对象的 CLSID) 的类 ID，以便对 的调用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry.CreateInstance%2A> 可以创建它。

 可通过组合 、单词、CLSID 和对象类型的 guid 来确定可创建的对象的 <xref:Microsoft.VisualStudio.Shell.Package.UserRegistryRoot%2A> 注册表路径。 如果类的 `MyProjectPropertyPage` guid 为 {3c693da2-5bca-49b3-bd95-ffe0a39dd723} 且 UserRegistryRoot 为 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp，则注册表路径为 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0Exp\CLSID\\ {3c693da2-5bca-49b3-bd95-ffe0a39dd723}。

## <a name="project-and-configuration-property-attributes-and-layout"></a>Project属性属性和布局
 、 和 属性确定泛型属性页中的项目和配置属性的布局、 <xref:System.ComponentModel.CategoryAttribute> <xref:System.ComponentModel.DisplayNameAttribute> <xref:System.ComponentModel.DescriptionAttribute> 标记和说明。 这些属性分别确定选项的类别、显示名称和说明。

> [!NOTE]
> 等效属性、SRCategory、LocDisplayName 和 SRDescription 使用字符串资源进行本地化，在[MPF 中为 Projects -](https://github.com/tunnelvisionlabs/MPFProj10)Visual Studio 2013。

 考虑以下代码片断：

 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/vb/myprojectpropertypage.vb" id="Snippet2":::
 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdksupportprojectconfigurationproperties/cs/myprojectpropertypage.cs" id="Snippet2":::

 配置属性在配置属性页上显示为类别"我的类别"中的"我的 `MyConfigProp` **配置属性"。**  如果选择了该选项，说明面板中将显示说明" **我的** 说明"。

## <a name="see-also"></a>请参阅
- [添加和删除属性页](../../extensibility/adding-and-removing-property-pages.md)
- [项目](../../extensibility/internals/projects.md)
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)