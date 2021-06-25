---
title: VSIX 扩展架构 2.0 参考|Microsoft Docs
description: VSIX 扩展架构 2.0 定义 VSIX 部署清单文件的文件格式，该文件描述 VSIX 包的内容。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- vsix
- extension schema
ms.assetid: 0da81b98-f5e3-40d3-ba9a-94551378d0b4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 66393bbe6383fcc6cae942a3d7e86f1d701a9634
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905236"
---
# <a name="vsix-extension-schema-20-reference"></a>VSIX 扩展架构 2.0 参考
VSIX 部署清单文件描述 VSIX 包的内容。 文件格式由架构控制。 此架构的版本 2.0 支持添加自定义类型和属性。  清单的架构是可扩展的。 清单加载程序忽略它无法理解的 XML 元素和属性。

> [!IMPORTANT]
> Visual Studio 2015 可以加载 Visual Studio 2010、Visual Studio 2012 或 Visual Studio 2013 格式的 VSIX 文件。

## <a name="package-manifest-schema"></a>包清单架构
 清单 XML 文件的根元素是 `<PackageManifest>` 。 它具有单个属性 `Version` ，即清单格式的版本。 如果对格式进行了重大更改，则更改版本格式。 本文介绍清单格式版本 2.0，该版本通过将 属性设置为 `Version` Version="2.0"的值在清单中指定。

### <a name="packagemanifest-element"></a>PackageManifest 元素
 在 `<PackageManifest>` 根元素中，可以使用以下元素：

- `<Metadata>` - 有关包本身的元数据和广告信息。 清单 `Metadata` 中只允许有一个元素。

- `<Installation>` - 本部分定义此扩展包的安装方式，包括它可以安装到的应用程序 SKUS。 清单 `Installation` 中只允许有一个元素。 清单必须具有 元素 `Installation` ，否则此包不会安装到任何 SKU 中。

- `<Dependencies>` - 此处定义了此包的依赖项的可选列表。

- `<Assets>` - 本部分包含此包中包含的所有资产。 如果没有本部分，此包将不会显示任何内容。

- `<AnyElement>*` - 清单架构足够灵活，允许任何其他元素。 清单加载程序无法识别的任何子元素在扩展管理器 API 中作为额外的 XmlElement 对象公开。 使用这些子元素，VSIX 扩展可以在清单文件中定义其他数据，在 Visual Studio 中运行的代码可以运行时访问这些数据。 请参阅 [Microsoft.VisualStudio.ExtensionManager.IExtension.AdditionalElements](/previous-versions/visualstudio/visual-studio-2013/hh265266(v=vs.120))。

### <a name="metadata-element"></a>Metadata 元素
 本部分是有关包、其标识和广告信息的元数据。 `<Metadata>` 包含以下元素：

- `<Identity>` - 定义此包的标识信息，并包含以下属性：

  - `Id` - 此属性必须是创建者选择的包的唯一 ID。 该名称的限定方式与 CLR 类型的命名空间相同：Company.Product.Feature.Name。 `Id`属性限制为 100 个字符。

  - `Version` - 定义此包的版本及其内容。 此属性遵循 CLR 程序集版本控制格式：Major.Minor.Build.Revision (1.2.40308.00) 。 版本号较高的包被视为对包的更新，可以通过现有已安装版本进行安装。

  - `Language` - 此属性是包的默认语言，对应于此清单中的文本数据。 此属性遵循资源程序集的 CLR 区域设置代码约定，例如：en-us、en、fr-fr。 可以指定以 `neutral` 声明将在任何版本的非特定语言扩展Visual Studio。 默认值为 `neutral`。

  - `Publisher` - 此属性标识此包的发布者（公司或个人名称）。 `Publisher`属性限制为 100 个字符。

- `<DisplayName>` - 此元素指定在扩展管理器 UI 中显示的用户友好包名称。 `DisplayName`内容限制为 50 个字符。

- `<Description>` - 此可选元素是扩展管理器 UI 中显示的包及其内容的简短说明。 `Description`内容可以包含任何需要的文本，但限制为 1000 个字符。

- `<MoreInfo>` - 此可选元素是联机页面的 URL，其中包含此包的完整说明。 协议必须指定为 http。

- `<License>` - 此可选元素是包中包含的许可证 (.txt .rtf) 的相对路径。

- `<ReleaseNotes>` - 此可选元素是包 (.txt.rtf) 中包含的发行说明文件的相对路径，或者是显示发行说明的网站的 URL。

- `<Icon>` - 此可选元素是包 (png、bmp、jpeg、ico) 图像文件的相对路径。 图标图像应为 32x32 像素 (或将收缩到该大小) 并出现在 listview UI 中。 如果 `Icon` 未指定元素，UI 将使用默认值。

- `<PreviewImage>` - 此可选元素是包中包含的 png、bmp、jpeg (图像) 的相对路径。 预览图像应为 200x200 像素，并显示在详细信息 UI 中。 如果 `PreviewImage` 未指定元素，UI 将使用默认值。

- `<Tags>` - 此可选元素列出用于搜索提示的其他分号分隔文本标记。 `Tags`元素限制为 100 个字符。

- `<GettingStartedGuide>` - 此可选元素是 HTML 文件的相对路径或网站的 URL，其中包含有关如何使用此包中的扩展名或内容的信息。 本指南作为安装的一部分启动。

- `<AnyElement>*` - 清单架构足够灵活，允许任何其他元素。 清单加载程序无法识别的任何子元素都公开为 XmlElement 对象的列表。 使用这些子元素，VSIX 扩展可以在清单文件中定义其他数据，并运行时枚举这些数据。

### <a name="installation-element"></a>Installation 元素
 本部分定义此包的安装方式以及可安装到的应用程序 SKUS。 本部分包含以下属性：

- `Experimental` - 如果当前为所有用户安装了扩展，但在同一计算机上开发更新的版本，则将此属性设置为 true。 例如，如果为所有用户安装了 MyExtension 1.0，但想要在同一计算机上调试 MyExtension 2.0，请设置 Experimental="true"。 此属性在 2015 Visual Studio 1 及更高版本中可用。

- `Scope` - 此属性可以取值"Global"或"ProductExtension"：

  - "全局"指定安装的范围不是特定 SKU。 例如，安装扩展 SDK 时，会使用此值。

  - "ProductExtension"指定安装了一个 (1.0) V1.0 Visual Studio VSIX 扩展。 这是默认值。

- `AllUsers` - 此可选属性指定是否将为所有用户安装此包。 默认情况下，此属性为 false，它指定包是每个用户。  (将此值设置为 true 时，安装用户必须提升为管理权限级别才能安装生成的 VSIX。

- `InstalledByMsi` - 此可选属性指定此包是否由 MSI 安装。 由 MSI 安装的包由 MSI (程序和功能) 而不是由 Visual Studio 扩展管理器安装和管理。  默认情况下，此属性为 false，它指定 MSI 未安装包。

- `SystemComponent` - 此可选属性指定是否应当将此包视为系统组件。 系统组件不会显示在扩展管理器 UI 中，并且无法更新。 默认情况下，此属性为 false，它指定包不是系统组件。

- `AnyAttribute*` - 元素接受一组开放式属性，这些属性将运行时作为名称 `Installation` /值对字典公开。

- `<InstallationTarget>` -此元素控制 VSIX 安装程序安装包的位置。 如果属性的值为"ProductExtension"，则包必须面向 SKU，该 SKU 已安装清单文件作为其内容的一部分，以向扩展播 `Scope` 发其可用性。 当 `<InstallationTarget>` 特性具有显式或默认值 `Scope` "ProductExtension"时，元素具有以下属性：

  - `Id` - 此属性标识包。  属性遵循命名空间约定：Company.Product.Feature.Name。 `Id`属性只能包含字母数字字符，并且限制为 100 个字符。 预期值：

    - Microsoft.VisualStudio.IntegratedShell

    - Microsoft.VisualStudio.Pro

    - Microsoft.VisualStudio.Premium

    - Microsoft.VisualStudio.Ultimate

    - Microsoft.VisualStudio.VWDExpress

    - Microsoft.VisualStudio.VPDExpress

    - Microsoft.VisualStudio.VSWinExpress

    - Microsoft.VisualStudio.VSLS

    - My.Shell.App

  - `Version` - 此属性指定具有此 SKU 支持的最低和最大版本的版本范围。 包可以详细说明它支持的 SKUS 版本。 版本范围表示法为 [10.0 - 11.0]，其中

    - [ - 最低版本（含）。

    - ] - 最大版本（含）。

    -  ( - 最低版本排他。

    - ) - 独占的最大版本。

    - 单版本 # - 仅指定版本。

    > [!IMPORTANT]
    > VSIX 架构版本 2.0 是在 2012 Visual Studio中引入的。 若要使用此架构，必须在计算机上安装 Visual Studio 2012 或更高版本，并使用VSIXInstaller.exe产品一部分的应用程序。 可以面向具有 Visual Studio 2012 Visual Studio更高版本的早期版本的 VSIXInstaller，但只能使用更高版本的安装程序。

    Visual Studio 2017 版本号，Visual Studio[版本号和发布日期。](../install/visual-studio-build-numbers-and-release-dates.md)

    在表示 2017 Visual Studio的版本时，次要版本应始终为 **0。** 例如，Visual Studio 2017 版本 15.3.26730.0 应表示为 [15.0.26730.0，16.0) 。 这仅适用于 Visual Studio 2017 及更高版本的版本号。

  - `AnyAttribute*` - 元素允许将一组开放式属性作为名称/值对字典运行时 `<InstallationTarget>` 公开。

### <a name="dependencies-element"></a>Dependencies 元素
 此元素包含此包声明的依赖项列表。 如果指定了任何依赖项，则 (之前必须) `Id` 标识这些包。

- `<Dependency>` 元素 - 此子元素具有以下属性：

  - `Id` - 此属性必须是依赖包的唯一 ID。 此标识值必须与此包 `<Metadata><Identity>Id` 所依赖的包的属性匹配。 属性 `Id` 遵循命名空间约定：Company.Product.Feature.Name。 属性只能包含字母数字字符，并且限制为 100 个字符。

  - `Version` - 此属性指定具有此 SKU 支持的最低和最大版本的版本范围。 包可以详细说明它支持的 SKUS 版本。 版本范围表示法为 [12.0， 13.0]，其中：

    - [ - 最低版本（含）。

    - ] - 最大版本（含）。

    -  ( - 最低版本排他。

    - ) - 独占的最大版本。

    - 单版本 # - 仅指定版本。

  - `DisplayName` - 此属性是依赖包的显示名称，在 UI 元素（如对话框和错误消息）中使用。 属性是可选的，除非 MSI 安装了依赖包。

  - `Location` - 此可选属性指定此 VSIX 中嵌套 VSIX 包的相对路径或依赖项下载位置的 URL。 此属性用于帮助用户查找必备组件包。

  - `AnyAttribute*` - 元素接受一组开放式属性，这些属性将运行时作为名称 `Dependency` /值对字典公开。

### <a name="assets-element"></a>Assets 元素
 此元素包含此 `<Asset>` 包显示的每个扩展或内容元素的标记列表。

- `<Asset>` - 此元素包含以下属性和元素：

  - `Type` - 扩展的类型或此元素表示的内容。 每个 `<Asset>` 元素都必须有一个 `Type` ，但多个 `<Asset>` 元素可能具有相同的 `Type` 。 根据命名空间约定，此属性应表示为完全限定的名称。 已知类型包括：

    1. Microsoft.VisualStudio.VsPackage

    2. Microsoft.VisualStudio.MefComponent

    3. Microsoft.VisualStudio.ToolboxControl

    4. Microsoft.VisualStudio.Samples

    5. Microsoft.VisualStudio.ProjectTemplate

    6. Microsoft.VisualStudio.ItemTemplate

    7. Microsoft.VisualStudio.Assembly

       你可以创建自己的类型，并赋予它们唯一的名称。 在 Visual Studio 中，代码可以通过扩展管理器 API 枚举和访问这些自定义类型。

  - `Path` - 包含资产的包中文件或文件夹的相对路径。

  - `TargetVersion` - 给定资产应用到的版本范围。 用于将多个版本的资产寄送到不同版本的Visual Studio。 要求Visual Studio 2017.3 或更高版本生效。

  - `AnyAttribute*` - 一组开放式属性，可运行时作为名称/值对字典公开。

    `<AnyElement>*` - 允许在开始标记和结束标记 `<Asset>` 之间使用任何结构化内容。 所有元素都作为 XmlElement 对象的列表公开。 VSIX 扩展可以在清单文件中定义特定于结构化类型的元数据，并运行时枚举这些元数据。

### <a name="sample-manifest"></a>示例清单

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
  <Metadata>
    <Identity Id="0000000-0000-0000-0000-000000000000" Version="1.0" Language="en-US" Publisher="Company" />
    <DisplayName>Test Package</DisplayName>
    <Description>Information about my package</Description>
    <MoreInfo>http://www.fabrikam.com/Extension1/</MoreInfo>
    <License>eula.rtf</License>
    <ReleaseNotes>notes.txt</ReleaseNotes>
    <Icon>Images\icon.png</Icon>
    <PreviewImage>Images\preview.png</PreviewImage>
  </Metadata>
  <Installation InstalledByMsi="false" AllUsers="false" SystemComponent="false" Scope="ProductExtension">
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="[11.0, 12.0]" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="[4.5,)" />
    <Dependency Id="Microsoft.VisualStudio.MPF.12.0" DisplayName="Visual Studio MPF 12.0" d:Source="Installed" Version="[12.0]" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.VsPackage" d:Source="Project" d:ProjectName="%CurrentProject%" Path="|%CurrentProject%;PkgdefProjectOutputGroup|" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>另请参阅

- [提供Visual Studio扩展](../extensibility/shipping-visual-studio-extensions.md)
