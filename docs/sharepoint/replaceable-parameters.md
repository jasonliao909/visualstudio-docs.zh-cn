---
title: 可替换参数|Microsoft Docs
description: 查看可替换 (参数) 标记，该参数指定在设计时SharePoint实际值未知的解决方案项的项目文件内的值。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, tokens
- tokens [SharePoint development in Visual Studio]
- replaceable parameters [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, replaceable parameters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload: office
ms.openlocfilehash: 7f7def73b011134a670cc79346d1a4e289d9e67252c9889a01a8599ebd603190
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121367482"
---
# <a name="replaceable-parameters"></a>可替换参数
  可在项目文件内使用可替换参数或标记，为SharePoint实际值在设计时不知道的解决方案项提供值。 它们在功能上类似于标准 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 模板令牌。 有关详细信息，请参阅 [模板参数](../ide/template-parameters.md)。

## <a name="token-format"></a>令牌格式
 令牌以美元符号开头和结尾， ($) 字符。 在部署时，将项目打包到 *.wsp* 文件包中的 SharePoint 解决方案包 (使用的任何令牌) 。 例如，令牌 **$SharePoint。Package.Name$** 可能解析为字符串"Test SharePoint Package"。

## <a name="token-rules"></a>令牌规则
 以下规则适用于令牌：

- 可以在行中的任何位置指定标记。

- 标记不能跨多行。

- 可以在同一行和同一文件中多次指定同一标记。

- 可以在同一行中指定不同的标记。

  不遵循这些规则的令牌将被忽略，并且不会生成警告或错误。

  在清单转换后立即使用字符串值替换标记。 此替换允许用户使用令牌编辑清单模板。

### <a name="token-name-resolution"></a>令牌名称解析
 在大多数情况下，令牌解析为特定值，而不考虑其包含位置。 但是，如果令牌与包或功能相关，则令牌的值取决于其包含位置。 例如，如果某个功能位于包 A 中，则令牌 `$SharePoint.Package.Name$` 解析为值"包 A"。 如果包 B 中具有相同的功能，则 `$SharePoint.Package.Name$` 解析为"包 B"。

## <a name="tokens-list"></a>令牌列表
 下表列出了可用的令牌。

|名称|说明|
|----------|-----------------|
|$SharePoint。Project。FileName$|包含项目文件的名称，例如 *NewProj.csproj*。|
|$SharePoint。Project。FileNameWithoutExtension$|不包含文件扩展名的包含项目文件的名称。 例如，"NewProj"。|
|$SharePoint。Project。AssemblyFullName$|显示名称 (包含) 程序集的强名称。|
|$SharePoint。Project。AssemblyFileName$|包含项目的输出程序集的名称。|
|$SharePoint。Project。AssemblyFileNameWithoutExtension$|包含项目的输出程序集的名称，不带文件扩展名。|
|$SharePoint。Project。AssemblyPublicKeyToken$|包含项目的输出程序集的公钥标记，已转换为字符串。  ("x2"十六进制格式的 16 个字符) |
|$SharePoint。Package.Name$|包含包的名称。|
|$SharePoint。Package.FileName$|包含包的定义文件的名称。|
|$SharePoint。Package.FileNameWithoutExtension$|名称 (不包含) 包的定义文件的扩展名。|
|$SharePoint。Package.Id$|包含SharePoint的 ID。 如果功能用于多个包中，则此值将更改。|
|$SharePoint。Feature.FileName$|包含功能的定义文件的名称，如 *Feature1.feature*。|
|$SharePoint。Feature.FileNameWithoutExtension$|功能定义文件的名称，不带文件扩展名。|
|$SharePoint。Feature.DeploymentPath$|包中包含该功能的文件夹的名称。 此令牌相当于功能设计器中的"部署路径"属性。 例如，"Project1_Feature1"。|
|$SharePoint。Feature.Id$|包含SharePoint的 ID。 与所有功能级令牌一样，此令牌仅可用于通过功能包含在包中的文件，不能直接添加到功能外部的包中。|
|$SharePoint。ProjectItem.Name$|项目项的名称 (其文件名) ，如从 **ISharePointProjectItem.Name 获取**。|
|$SharePoint。键入 \<GUID> 。。AssemblyQualifiedName$|与标记的 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 匹配的类型的程序集限定名。 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 的格式为小写，并与 Guid.ToString("D") 格式（即 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx）对应。|
|$SharePoint。键入 \<GUID> 。。FullName$|与令牌中的 GUID 匹配的类型的全名。 GUID 的格式为小写，对应于 Guid.ToString ("D") 格式 (即 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxxxx) 。|

## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>将扩展添加到令牌替换文件扩展名列表
 尽管理论上，属于包中包含的 SharePoint 项目项的任何文件都可以使用令牌，但默认情况下，仅在包文件、清单文件和具有以下扩展名的文件中搜索 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 令牌：

- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]

- ASCX

- ASPX

- Webpart

- DWP

  这些扩展由 `<TokenReplacementFileExtensions>` Microsoft.VisualStudio.SharePoint.targets 文件中位于 ... 中的 元素定义。 \\<\> \MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools 文件夹。

  但是，可以将其他文件扩展名添加到列表中。 将 元素添加到 SharePoint 项目文件的任何 PropertyGroup，该文件在 SharePoint `<TokenReplacementFileExtensions>` \<Import> 文件之前定义。

> [!NOTE]
> 由于令牌替换在编译项目后发生，因此不应为编译的文件类型（如 *.cs、.vb* 或 *.resx）添加文件扩展* 名。  仅在未编译的文件中替换令牌。

 例如，若要将文件扩展名 (*.myextension* 和 *.yourextension*) 添加到令牌替换文件扩展名列表中，需要将以下内容添加到项目 (*.csproj*) 文件：

```xml
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
.
.
.
    <!-- Define the following property to add your extension to the list of token replacement file extensions.  -->
<TokenReplacementFileExtensions>myextension;yourextension</TokenReplacementFileExtensions>
</PropertyGroup>
```

 可以将扩展插件直接添加到 *.targets* (中) 目标。 但是，添加扩展会更改打包在本地系统SharePoint所有项目（而不只是你自己的项目）的扩展列表。 如果你是系统的唯一开发人员，或者大多数项目需要此扩展，则此扩展可能很方便。 但是，由于此方法特定于系统，因此不可移植，因此建议改为向项目文件添加任何扩展名。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
