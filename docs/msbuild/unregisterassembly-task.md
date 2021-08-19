---
title: UnregisterAssembly 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 UnregisterAssembly 任务出于 COM 互操作目的取消注册指定的程序集。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#UnregisterAssembly
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UnregisterAssembly task
- UnregisterAssembly task [MSBuild]
ms.assetid: 04f549dd-3591-4dda-9c3a-cf6ede9df2c3
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 79b9b607de3a8b4d8eafe46817612c62995d3a51
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122142775"
---
# <a name="unregisterassembly-task"></a>UnregisterAssembly 任务

注销用于 COM 互操作的指定程序集。 执行 [RegisterAssembly 任务](../msbuild/registerassembly-task.md)的相反任务。

## <a name="parameters"></a>参数

 下表描述了 `UnregisterAssembly` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`Assemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要注销的程序集。|
|`AssemblyListFile`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 包含有关 `RegisterAssembly` 任务和 `UnregisterAssembly` 任务之间状态的信息。 这样可以防止任务尝试注销无法在 `RegisterAssembly` 任务中注册的程序集。<br /><br /> 如果已指定此参数，则 `Assemblies` 和 `TypeLibFiles` 参数将被忽略。|
|`TypeLibFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 从指定的程序集中注销指定的类型库。 **注意：** 只有当类型库文件名不同于程序集名称时，此参数才是必需的。|

## <a name="remarks"></a>注解

 此任务的成功对是否存在程序集不作要求。 如果尝试注销不存在的程序集，则该任务将成功并且出现警告。 发生这种情况是因为此任务的工作就是从注册表中删除程序集注册。 如果该程序集不存在，则它不在注册表中，因此，任务将成功完成。

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.AppDomainIsolatedTaskExtension> 类继承参数，后者自身继承自 <xref:System.MarshalByRefObject> 类。 `MarshalByRefObject` 类提供与 <xref:Microsoft.Build.Utilities.Task> 类相同的功能，但它可以在其自己的应用程序域中进行实例化。

## <a name="example"></a>示例

 以下示例使用 `UnregisterAssembly` 任务注销 `OutputPath` 和 `FileName` 属性指定的路径处的程序集（如果存在）。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <OutputPath>\Output\</OutputPath>
        <FileName>MyFile.dll</FileName>
    </PropertyGroup>
    <Target Name="UnregisterAssemblies">
        <UnregisterAssembly
            Condition="Exists('$(OutputPath)$(FileName)')"
            Assemblies="$(OutputPath)$(FileName)" />
    </Target>

</Project>
```

## <a name="see-also"></a>另请参阅

- [RegisterAssembly 任务](../msbuild/registerassembly-task.md)
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)