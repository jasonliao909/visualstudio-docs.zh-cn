---
title: MSBuild .targets 文件 | Microsoft Docs
description: 了解包含用于常见方案的项、属性、目标和任务的 MSBuild .targets 文件。
ms.custom: SEO-VS-2020
ms.date: 02/24/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- .targets files
- MSBuild, .targets files
ms.assetid: f6d98eb4-d2fa-49b7-8e3c-bae1ca3cf596
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: b30aaf73a49c1ef75f0778e619cbfb4a4b69846d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093615"
---
# <a name="msbuild-targets-files"></a>MSBuild .targets 文件

MSBuild 包括多个 .targets  文件，文件内容包含常见方案的项、属性、目标和任务。 这些文件将自动导入到大多数 Visual Studio 项目文件中，以便简化维护，增强可读性。

 项目通常会导入一个或多个 .targets 文件以定义它们的生成进程  。 例如由 Visual Studio 创建的 C# 项目将导入 Microsoft.CSharp.targets  ，它可导入 Microsoft.Common.targets  。 C# 项目本身会定义特定于该项目的项和属性，但 C# 项目的标准生成规则在导入的 .targets  文件中进行定义。

 `$(MSBuildToolsPath)` 值指定这些公用 .targets 文件的路径  。 如果 `ToolsVersion` 为 4.0，则文件位于以下位置：\<WindowsInstallationPath>\Microsoft.NET\Framework\v4.0.30319\\

> [!NOTE]
> 若要了解如何创建自己的目标，请参阅[目标](../msbuild/msbuild-targets.md)。 有关如何使用 `Import` 元素将项目文件插入到其他项目文件的详细信息，请参阅 [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md) 和[如何：在多个项目文件中使用同一目标](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)。

## <a name="common-targets-files"></a>公用 .targets 文件

| .targets 文件  | 描述 |
|---------------------------------| - |
| *Microsoft.Common.targets* | 定义 Visual Basic 和 C# 项目标准生成过程中的步骤。<br /><br /> 由 Microsoft.CSharp.targets 和 Microsoft.VisualBasic.targets 文件导入，其中包括以下语句：`<Import Project="Microsoft.Common.targets" />`   |
| *Microsoft.CSharp.targets* | 定义 Visual C# 项目标准生成过程中的步骤。<br /><br /> 由 Visual C# 项目文件 (.csproj) 导入，其中包括以下语句：`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`  |
| *Microsoft.VisualBasic.targets* | 定义 Visual Basic 项目标准生成过程中的步骤。<br /><br /> 由 Visual Basic 项目文件 (.vbproj) 导入，其中包括以下语句：`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`  |

## <a name="directorybuildtargets"></a>Directory.Build.targets

Directory.Build.targets 是用户定义的对目录下的项目提供自定义选项的文件  。 除非属性 ImportDirectoryBuildTargets 设为 false，否则该文件将从 Microsoft.Common.targets 自动导入    。 有关详细信息，请参阅[自定义生成](customize-your-build.md)。

## <a name="see-also"></a>请参阅

- [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
