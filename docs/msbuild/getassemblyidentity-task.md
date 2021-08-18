---
title: GetAssemblyIdentity 任务 | Microsoft Docs
description: 使用 MSBuild GetAssemblyIdentity 任务可从指定的文件中检索程序集标识并输出标识信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GetAssemblyIdentity
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GetAssemblyIdentity task
- GetAssemblyIdentity task [MSBuild]
ms.assetid: a977e072-37ad-4941-84a6-32a4483be55d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 28b26047a0893cc9e0ab783e83988b5c7ea1fb08
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143373"
---
# <a name="getassemblyidentity-task"></a>GetAssemblyIdentity 任务

从指定的文件检索程序集标识并输出标识信息。

## <a name="task-parameters"></a>任务参数

下表描述了 `GetAssemblyIdentity` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`Assemblies`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含检索到的程序集标识。|
|`AssemblyFiles`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要从中检索标识的文件。|

## <a name="remarks"></a>注解

由 `Assemblies` 参数输出的项包含名为 `Version`、`PublicKeyToken` 和 `Culture` 的项元数据条目。

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

以下示例检索 `MyAssemblies` 项中指定的文件的标识，然后将其输出到 `MyAssemblyIdentities` 项。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <MyAssemblies Include="File1.dll;File2.dll" />
    </ItemGroup>
    <Target Name="RetrieveIdentities">
        <GetAssemblyIdentity AssemblyFiles="@(MyAssemblies)">
            <Output TaskParameter="Assemblies" ItemName="MyAssemblyIdentities" />
        </GetAssemblyIdentity>
    </Target>
</Project>
```

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
