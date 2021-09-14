---
title: 使用 MSBuild | Microsoft Docs
description: MSBuild提供可扩展的 XML 格式，用于创建项目文件，以完全描述要生成的项目项、生成任务和生成配置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0e9839812175d3e74b3e2d42ad04c3a32f7caa09
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600855"
---
# <a name="using-msbuild"></a>使用 MSBuild
MSBuild提供了定义明确的可扩展 XML 格式，用于创建项目文件，以完全描述要生成的项目项、生成任务和生成配置。

## <a name="general-msbuild-considerations"></a>常规MSBuild注意事项
 MSBuild项目文件（例如 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] .csproj 和 .vbproj 文件）包含生成时使用的数据，但也可以包含在设计时 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 使用的数据。 生成时数据使用 MSBuild 基元存储，包括[Item Element (MSBuild) ](../../msbuild/item-element-msbuild.md)和 Property Element [ (MSBuild) 。 ](../../msbuild/property-element-msbuild.md) 设计时数据（特定于项目类型和任何相关项目子类型的数据）以为它保留的自由格式 XML 存储。

 MSBuild对配置对象没有本机支持，但提供了用于指定配置特定数据的条件属性。 例如：

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 有关条件属性详细信息，请参阅 [条件构造](../../msbuild/msbuild-conditional-constructs.md)。

### <a name="extending-msbuild-for-your-project-type"></a>扩展MSBuild类型的Project类型
 MSBuild接口和 API 在 的未来版本中可能会更改 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 因此，将托管包框架用于 MPF (类是) ，因为它们提供对更改的防护。

 用于项目的托管包框架 (MPFProj) 提供了用于创建和管理新项目系统的帮助程序类。 可以在 MPF for [Projects - Visual Studio 2013。](https://github.com/tunnelvisionlabs/MPFProj10)

 特定于项目的 MPF 类如下所示：

|类|实现|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement`类是一个包装器MSBuild项。

#### <a name="single-file-generators-vs-msbuild-tasks"></a>单个文件生成器与MSBuild任务
 单个文件生成器只能在设计时访问，MSBuild和生成时可以使用单个文件生成器。 因此，为了获得最大的灵活性，MSBuild任务来转换和生成代码。 有关详细信息，请参阅自定义 [工具](../../extensibility/internals/custom-tools.md)。

## <a name="see-also"></a>另请参阅
- [MSBuild 参考](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [自定义工具](../../extensibility/internals/custom-tools.md)
