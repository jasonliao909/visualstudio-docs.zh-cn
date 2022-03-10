---
title: Copy 任务 | Microsoft Docs
description: 了解如何使用 MSBuild Copy 任务将文件复制到文件系统中的新文件或文件夹位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Copy
- MSBuild.Copy.SourceFileNotFound
- MSBuild.Copy.Retrying
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Copy task
- Copy task [MSBuild]
ms.assetid: a46ba9da-3e4e-4890-b4ea-09a099b6bc40
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 331d4088ba78bc043b24cb3fc1c2a10e82a31b83
ms.sourcegitcommit: b0ec2d8b7e32a9a6b50e462d588c64d471665533
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/10/2022
ms.locfileid: "139704046"
---
# <a name="copy-task"></a>Copy 任务

将文件复制到文件系统的一个新位置。

## <a name="parameters"></a>参数

下表描述了 `Copy` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`CopiedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含已成功复制的项，包括尚未进行实际复制但由于其已为最新且 `SkipUnchangedFiles` 为 `true` 因此被跳过的项。|
|`DestinationFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要对其复制源文件的文件的列表。 此列表应与 `SourceFiles` 参数中指定的列表具有一对一的映射关系。 也就是说，`SourceFiles` 中指定的第一个文件将复制到 `DestinationFiles` 中指定的第一个位置，依次类推。|
|`DestinationFolder`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要将文件复制到其中的目录。 这必须是目录，而不能是文件。 如果该目录不存在，将自动创建它。|
|`OverwriteReadOnlyFiles`|可选 `Boolean` 参数。<br /><br /> 覆盖文件，即使它们标记为只读文件|
|`Retries`|可选 `Int32` 参数。<br /><br /> 指定之前的所有尝试都失败后，尝试复制的次数。 默认为零。<br /><br /> 注意：重试的使用可以屏蔽生成过程中的同步问题。<br /><br /> **注意：** 尽管任务默认为零次重试，但任务的使用通常会传递 `$(CopyRetryCount)`，这在默认情况下为非零值。|
|`RetryDelayMilliseconds`|可选 `Int32` 参数。<br /><br /> 指定任何必需的重试之间的延迟。 默认值为传递给 CopyTask 构造函数的 RetryDelayMillisecondsDefault 参数。|
|`SkipUnchangedFiles`|可选 `Boolean` 参数。<br /><br /> 如果为`true` ，则跳过复制在源和目标之间保持不变的文件。 如果文件的大小和上次修改时间相同，则 `Copy` 任务认为文件保持不变。 <br /><br /> **注意：** 如果此参数设置为 `true`，则不应对包含目标使用依赖关系分析，因为如果源文件的上次修改时间比目标文件的上次修改时间更新，则只运行该任务。|
|`SourceFiles`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要复制的文件。|
|`UseHardlinksIfPossible`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则创建已复制文件的硬链接，而不是复制该文件。|

## <a name="warnings"></a>警告

警告将被记录，其中包括：

- `Copy.DestinationIsDirectory`

- `Copy.SourceIsDirectory`

- `Copy.SourceFileNotFound`

- `Copy.CreatesDirectory`

- `Copy.HardLinkComment`

- `Copy.RetryingAsFileCopy`

- `Copy.FileComment`

- `Copy.RemovingReadOnlyAttribute`

## <a name="remarks"></a>备注

必须指定 `DestinationFolder` 或 `DestinationFiles` 参数，但不能对两者都进行指定。 如果指定了两者，则任务失败并记录一条错误。

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example-1"></a>示例 1

以下示例将 `MySourceFiles` 项集合中的项复制到文件夹 c:\MyProject\Destination。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MySourceFiles Include="a.cs;b.cs;c.cs"/>
    </ItemGroup>

    <Target Name="CopyFiles">
        <Copy
            SourceFiles="@(MySourceFiles)"
            DestinationFolder="c:\MyProject\Destination"
        />
    </Target>

</Project>
```

## <a name="example-2"></a>示例 2

以下示例演示如何执行递归复制。 此项目以递归方式将所有文件从 c:\MySourceTree 复制到 c:\MyDestinationTree，同时保留目录结构 。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <Target Name="CopyFiles">
        <ItemGroup>
            <!-- Because this ItemGroup is inside the target, this will enumerate
                 all files just before calling Copy. If the ItemGroup were outside
                 the target , it would enumerate the files during evaluation, before
                 the build starts, which may miss files created during the build. -->
            <MySourceFiles Include="c:\MySourceTree\**\*.*"/>
        </ItemGroup>

        <Copy
            SourceFiles="@(MySourceFiles)"
            DestinationFiles="c:\MyDestinationTree\%(RecursiveDir)%(Filename)%(Extension)"
        />
    </Target>

</Project>
```

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
