---
title: ResolveNativeReference 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 ResolveNativeReference 任务通过实现 Microsoft.Build.Tasks.ResolveNativeReference 类来解析本机引用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveNativeReference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveNativeReference task
- ResolveNativeReference task [MSBuild]
ms.assetid: 56acd101-de77-4eec-92c6-f5c6d2187579
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 212239348ba1f4caf80be1ac9feb029bb702cee3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122136672"
---
# <a name="resolvenativereference-task"></a>ResolveNativeReference 任务

解析本机引用。 实现 <xref:Microsoft.Build.Tasks.ResolveNativeReference> 类。 此类支持 .NET Framework 基础结构，但不适合直接在代码中使用。

## <a name="task-parameters"></a>任务参数

 下表描述了 `ResolveNativeReference` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`AdditionalSearchPaths`|必选 <xref:System.String?displayProperty=fullName>`[]` 参数。<br /><br /> 获取或设置用于解析本机引用的程序集标识的搜索路径。|
|`ContainedComComponents`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 获取或设置本机程序集的 COM 组件。|
|`ContainedLooseEtcFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 获取或设置本机清单中列出的松散 Etc 文件。|
|`ContainedLooseTlbFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 获取或设置本机程序集的宽松 .tlb 文件。|
|`ContainedPrerequisiteAssemblies`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 获取或设置在可使用清单前必须存在的程序集。|
|`ContainedTypeLibraries`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 获取或设置本机程序集的类型库。|
|`ContainingReferenceFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 获取或设置引用文件。|
|`NativeReferences`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 获取或设置 Win32 本机程序集引用。|

## <a name="remarks"></a>备注

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
