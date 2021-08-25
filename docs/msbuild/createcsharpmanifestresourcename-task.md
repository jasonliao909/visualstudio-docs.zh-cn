---
title: CreateCSharpManifestResourceName 任务 | Microsoft Docs
description: 使用 MSBuild CreateCSharpManifestResourceName 任务可根据给定的 .resx 文件名或其他资源创建 C# 样式的清单名称。
ms.custom: SEO-VS-2020
ms.date: 11/15/2020
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateCSharpManifestResourceName task
- CreateCSharpManifestResourceName task [MSBuild]
ms.assetid: 2ace88c1-d757-40a7-8158-c1d3f5ff0511
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 2c8633972152cb1d8c08b21a2f6dd44bb20e77bd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122054907"
---
# <a name="createcsharpmanifestresourcename-task"></a>CreateCSharpManifestResourceName 任务

根据给定的 .resx 文件名或其他资源创建 C# 样式的清单名称。

## <a name="parameters"></a>参数

 下表描述 [CreateCSharpManifestResourceName 任务](../msbuild/createcsharpmanifestresourcename-task.md)的参数。

| 参数 | 说明 |
| - | - |
| `ManifestResourceNames` | <xref:Microsoft.Build.Framework.ITaskItem> `[]` 输出只读参数。<br /><br /> 生成的清单名称。 |
| `ResourceFiles` | 必选 `String` 参数。<br /><br /> 从中创建 C# 清单名称的资源文件的名称。 |
| `RootNamespace` | 可选 `String` 参数。<br /><br /> 资源文件的根命名空间，通常取自于项目文件。 可为 `null`。 |
| `PrependCultureAsDirectory` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则将区域性名称作为目录名称添加到清单资源名称前。 默认值为 `true`。 |
| `ResourceFilesWithManifestResourceNames` | 可选的 `String` 只读输出参数。<br /><br /> 返回现在包括清单资源名称的资源文件的名称。 |

## <a name="remarks"></a>注解

 [CreateCSharpManifestResourceName 任务](../msbuild/createcsharpmanifestresourcename-task.md)决定了要分配到给定 .resx 或其他资源文件的相应清单资源名称。 该任务向资源文件提供一个逻辑名称，然后将其作为元数据附加到输出参数。

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
