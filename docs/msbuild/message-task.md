---
title: Message 任务 | Microsoft Docs
description: 了解在生成期间记录消息的 MSBuild Message 任务的参数和设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Message
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Message task
- Message task [MSBuild]
ms.assetid: 2293309d-42b6-46dc-9684-8c146f66bc28
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 0b9ee3a2514d89c5b2d436666b2ff512feb8a1b4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122077200"
---
# <a name="message-task"></a>Message 任务

在生成期间记录消息。

## <a name="parameters"></a>参数

 下表描述了 `Message` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`Importance`|可选 `String` 参数。<br /><br /> 指定消息的重要性。 此参数的值可以是 `high`、`normal` 或 `low`。 默认值为 `normal`。|
|`Text`|可选 `String` 参数。<br /><br /> 要记录的错误文本。|

## <a name="remarks"></a>注解

 通过 `Message` 任务，MSBuild 项目可以在生成过程中的不同阶段将消息发送到记录器中。

 如果 `Condition` 参数的计算结果为 `true`，则将会记录 `Text` 参数值，并继续执行生成。 如果 `Condition` 参数不存在，则将记录消息文本。 有关日志记录的详细信息，请参阅[获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)。

 默认情况下，消息将发送到所有已注册的记录器。 记录器解释 `Importance` 参数。 通常，当记录器详细级别设置为 <xref:Microsoft.Build.Framework.LoggerVerbosity> `Minimal` 时，将发送设置为 `high` 的消息。 或更高版本。 当记录器详细级别设置为 <xref:Microsoft.Build.Framework.LoggerVerbosity> `Detailed` 时，将发送设置为 `low` 的消息。

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

 下面的代码示例将消息记录到所有已注册的记录器。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="DisplayMessages">
        <Message Text="Project File Name = $(MSBuildProjectFile)" />
        <Message Text="Project Extension = $(MSBuildProjectExtension)" />
    </Target>
    ...
</Project>
```

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
- [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)
