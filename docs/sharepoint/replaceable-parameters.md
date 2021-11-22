---
title: 可替换参数 | Microsoft Docs
description: 查看可替换参数（令牌），它们在项目文件中指定 SharePoint 解决方案项的值，这些实际值在设计时是未知的。
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
ms.openlocfilehash: e36edf6d8482fcb48a6a77695a6631aed1868203
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602537"
---
# <a name="replaceable-parameters"></a>可替换参数
  可替换参数（令牌）可在项目文件中用于提供 SharePoint 解决方案项的值，这些实际值在设计时是未知的。 它们在功能上类似于标准 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 模板令牌。 有关详细信息，请参阅[模板参数](../ide/template-parameters.md)。

## <a name="token-format"></a>令牌格式
 令牌以美元符号 ($) 字符开头和结尾。 部署时，如果项目打包到 SharePoint 解决方案包（.wsp 文件），则使用的任何令牌均替换为实际值。 例如，令牌 $SharePoint.Package.Name$ 可能解析为字符串“Test SharePoint Package”。

## <a name="token-rules"></a>令牌规则
 以下规则适用于令牌：

- 可以在行中的任意位置指定令牌。

- 令牌不能跨多个行。

- 同一令牌可以在同一行和同一文件中指定多次。

- 可以在同一行中指定不同的令牌。

  不遵循这些规则的令牌将被忽略，不会导致警告或错误。

  在清单转换后立即用字符串值替换令牌。 此替换功能允许用户用令牌编辑清单模板。

### <a name="token-name-resolution"></a>令牌名称解析
 在大多数情况下，令牌解析为特定值，而不考虑它的包含位置。 但是，如果令牌与包或功能相关，则令牌的值取决于它的包含位置。 例如，如果某个功能在包 A 中，则令牌 `$SharePoint.Package.Name$` 解析为“Package A”值。 如果同一功能在包 B 中，则 `$SharePoint.Package.Name$` 解析为“Package B”。

## <a name="tokens-list"></a>令牌列表
 下表列出了可用的令牌。

|名称|说明|
|----------|-----------------|
|$SharePoint.Project.FileName$|包含项目文件的名称，如 NewProj.csproj。|
|$SharePoint.Project.FileNameWithoutExtension$|不包含文件扩展名的包含项目文件的名称。 例如“NewProj”。|
|$SharePoint.Project.AssemblyFullName$|包含项目的输出程序集的显示名称（强名称）。|
|$SharePoint.Project.AssemblyFileName$|包含项目的输出程序集的名称。|
|$SharePoint.Project.AssemblyFileNameWithoutExtension$|包含项目输出程序集的名称，没有文件扩展名。|
|$SharePoint.Project.AssemblyPublicKeyToken$|包含项目输出程序集的公钥令牌，已转换为字符串。 （“x2”十六进制格式的 16 个字符。）|
|$SharePoint.Package.Name$|包含包的名称。|
|$SharePoint.Package.FileName$|包含包的定义文件的名称。|
|$SharePoint.Package.FileNameWithoutExtension$|包含包的定义文件的名称（不带扩展名）。|
|$SharePoint.Package.Id$|包含包的 SharePoint ID。 如果在多个包中使用某一功能，则此值将更改。|
|$SharePoint.Feature.FileName$|包含功能的定义文件的名称，如 Feature1.feature。|
|$SharePoint.Feature.FileNameWithoutExtension$|功能定义文件的名称，不带文件扩展名。|
|$SharePoint.Feature.DeploymentPath$|包中包含功能的文件夹的名称。 此令牌等同于功能设计器中的“部署路径”属性。 示例值为“Project1_Feature1”。|
|$SharePoint.Feature.Id$|包含功能的 SharePoint ID。 与所有功能级令牌一样，此令牌只能通过功能由包中包含的文件使用，而不会直接添加到功能外的包中。|
|$SharePoint.ProjectItem.Name$|项目项的名称（非文件名），从 ISharePointProjectItem.Name 中获取。|
|$SharePoint.Type.\<GUID>.AssemblyQualifiedName$|与标记的 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 匹配的类型的程序集限定名。 [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] 的格式为小写，并与 Guid.ToString("D") 格式（即 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx）对应。|
|$SharePoint.Type.\<GUID>.FullName$|与令牌中的 GUID 匹配的类型的完整名称。 GUID 的格式为小写，对应 Guid.ToString("D") 格式（即 xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx）。|

## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>向令牌替换文件扩展名列表添加扩展名
 虽然在理论上，令牌可以由包中包含的 SharePoint 项目项的任何文件使用，但默认情况下，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 仅搜索包文件、清单文件和具有以下扩展名的文件中的令牌：

- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]

- ASCX

- ASPX

- Webpart

- DWP

  这些扩展名由 Microsoft.VisualStudio.SharePoint.targets 文件中的 `<TokenReplacementFileExtensions>` 元素定义，该文件位于 ...\\<program files\>\MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools 文件夹中。

  但是，你可以向列表添加其他文件扩展名。 请将 `<TokenReplacementFileExtensions>` 元素添加到在 SharePoint 目标文件的 \<Import> 之前定义的 SharePoint 项目文件中的任意 PropertyGroup 中。

> [!NOTE]
> 由于令牌替换在编译项目后发生，因此不应为编译的文件类型添加文件扩展名，如 .cs、.vb 或 .resx。 令牌只在未编译的文件中被替换。

 例如，若要将文件扩展名（.myextension 和 .yourextension）添加到令牌替换文件扩展名列表中，需要将以下内容添加到项目 ( *.csproj*) 文件：

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

 可以直接将扩展名添加到目标 (.targets) 文件。 但是，添加扩展名会改变在本地系统上打包的所有 SharePoint 项目的扩展名列表，而不只是你自己的扩展名列表。 如果你是系统上的唯一开发人员，或者你的大多数项目都需要此扩展名，则此扩展名可能很方便。 但是，因为它是特定于系统的，所以此方法是不可移植的，因此建议改为将任何扩展名添加到项目文件。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
