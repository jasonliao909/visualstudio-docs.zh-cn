---
title: ResolveManifestFiles 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 ResolveManifestFiles 任务将生成过程中的项解析为用于生成清单的文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ResolveManifestFiles task [MSBuild]
- MSBuild, ResolveManifestFiles task
ms.assetid: e1e14f67-9b69-433f-94d4-a783a68676b2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 339dc003ff5c9275567633e05746ab042fd34439
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122136698"
---
# <a name="resolvemanifestfiles-task"></a>ResolveManifestFiles 任务

在生成过程中，将以下各项解析为文件以便生成清单：生成项、依赖项、附属项、内容、调试符号和文档。

## <a name="parameters"></a>参数

 下表描述了 `ResolveManifestFiles` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`DeploymentManifestEntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定部署清单的名称。|
|`EntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定作为清单入口点的托管程序集或 ClickOnce 清单引用。|
|`ExtraFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定额外文件。|
|`ManagedAssemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定托管程序集。|
|`NativeAssemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定本机程序集。|
|`OutputAssemblies`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定所生成的程序集。|
|`OutputDeploymentManifestEntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定输出部署清单入口点。|
|`OutputEntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定输出入口点。|
|`OutputFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定输出文件。|
|`PublishFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定发布文件。|
|`SatelliteAssemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定附属程序集。|
|`SigningManifests`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则清单已签名。|
|`TargetCulture`|可选 `String` 参数。<br /><br /> 指定附属程序集的目标区域性。|
|`TargetFrameworkVersion`|可选 `String` 参数。<br /><br /> 指定目标 .NET Framework 的版本。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
