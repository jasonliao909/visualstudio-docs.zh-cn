---
title: 使用 AspNetCompiler 任务预编译 ASP.NET
description: 使用 MSBuild AspNetCompiler 任务可包装 aspnet_compiler.exe，它是预编译 ASP.NET 应用程序的实用工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AspNetCompiler
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, AspNetCompiler task
- AspNetCompiler task [MSBuild]
ms.assetid: f811c019-a67b-4d54-82e6-e29549496f6e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- aspnet
ms.openlocfilehash: 23639025f7592f0b688adc2402dae9f81ee7865b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122150503"
---
# <a name="aspnetcompiler-task"></a>AspNetCompiler 任务

`AspNetCompiler` 任务包装 aspnet_compiler.exe  ，它是预编译 ASP.NET 应用程序的实用工具。

## <a name="task-parameters"></a>任务参数

下表描述了 `AspNetCompiler` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`AllowPartiallyTrustedCallers`|可选 `Boolean` 参数。<br /><br /> 如果此参数为 `true`，则具有强名称的程序集将允许部分信任的调用方。|
|`Clean`|可选的 `Boolean` 参数<br /><br /> 如果此参数为 `true`，则将以全新方式生成预编译的应用程序。 将重新编译任何之前编译的组件。 默认值为 `false`。 此参数对应于 aspnet_compiler.exe 上的 -c 开关   。|
|`Debug`|可选 `Boolean` 参数。<br /><br /> 如果此参数为 `true`，则将在编译期间发出调试信息（.PDB 文件）。 默认值为 `false`。 此参数对应于 aspnet_compiler.exe 上的 -d 开关   。|
|`DelaySign`|可选 `Boolean` 参数。<br /><br /> 如果此参数为 `true`，则该程序集在创建后未完全签名。|
|`FixedNames`|可选 `Boolean` 参数。<br /><br /> 如果此参数为 `true`，则编译的程序集将拥有固定的名称。|
|`Force`|可选的 `Boolean` 参数<br /><br /> 如果此参数为 `true`，则任务将覆盖目标目录（如果已存在）。 现有内容将丢失。 默认值为 `false`。 此参数对应于 aspnet_compiler.exe 上的 -f 开关   。|
|`KeyContainer`|可选 `String` 参数。<br /><br /> 指定强名称密钥容器。|
|`KeyFile`|可选 `String` 参数。<br /><br /> 指定强名称密钥文件的物理路径。|
|`MetabasePath`|可选 `String` 参数。<br /><br /> 指定应用程序的完整 IIS 元数据库路径。 此参数不能与 `VirtualPath` 或 `PhysicalPath` 参数合并。 此参数对应于 aspnet_compiler.exe 上的 -m 开关   。|
|`PhysicalPath`|可选 `String` 参数。<br /><br /> 指定要编译的应用程序的物理路径。 如果缺少此参数，则将使用 IIS 元数据库查找该应用程序。 此参数对应于 aspnet_compiler.exe 上的 -p 开关   。|
|`TargetFrameworkMoniker`|可选 `String` 参数。<br /><br /> 指定 TargetFrameworkMoniker，它指示应使用的 aspnet_compiler.exe 的 .NET Framework 版本  。 仅接受 .NET Framework 名字对象。|
|`TargetPath`|可选 `String` 参数。<br /><br /> 指定将应用程序编译到的物理路径。 如果未指定，则将就地预编译应用程序。|
|`Updateable`|可选 `Boolean` 参数。<br /><br /> 如果此参数为 `true`，则预编译的应用程序将为可更新。  默认值为 `false`。 此参数对应于 aspnet_compiler.exe 上的 -u 开关   。|
|`VirtualPath`|可选 `String` 参数。<br /><br /> 要编译的应用程序的虚拟路径。 如果指定 `PhysicalPath`，则物理路径将用于查找应用程序。 否则，将使用 IIS 元数据库，并假定应用程序位于默认站点中。 此参数对应于 aspnet_compiler.exe 上的 -v 开关   。|

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="example"></a>示例

以下代码示例使用 `AspNetCompiler` 任务预编译 ASP.NET 应用程序。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="PrecompileWeb">
        <AspNetCompiler
            VirtualPath="/MyWebSite"
            PhysicalPath="c:\inetpub\wwwroot\MyWebSite\"
            TargetPath="c:\precompiledweb\MyWebSite\"
            Force="true"
            Debug="true"
        />
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅

* [任务](../msbuild/msbuild-tasks.md)
* [任务参考](../msbuild/msbuild-task-reference.md)
* [ASP.NET 编译工具 (aspnet_compiler)](/previous-versions/ms229863(v=vs.100))
