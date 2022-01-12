---
title: Warning 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 Warning 任务在生成期间根据已评估的条件语句记录警告。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Warning
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Warning task [MSBuild]
- MSBuild, Warning task
ms.assetid: 96ba5507-8b43-4f54-a1d7-9b15644dd56c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 9906e901d1d793e80a6e099b1f003659515bf6e3
ms.sourcegitcommit: 1d44a5509772c3926f5ad13b1796485d6d8c441e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135963924"
---
# <a name="warning-task"></a>Warning 任务

基于评估的条件语句，在生成期间记录警告。

## <a name="parameters"></a>参数

 下表描述了 `Warning` 任务的参数。

| 参数 | 说明 |
|---------------| - |
| `Code` | 可选 `String` 参数。<br /><br /> 与警告相关联的警告代码。 |
| `File` | 可选 `String` 参数。<br /><br /> 指定相关文件（如果有）。 如果未提供任何文件，则使用包含 Warning 任务的文件。 |
| `HelpKeyword` | 可选 `String` 参数。<br /><br /> 与警告关联的 Help 关键字。 仅限内部使用。 |
| `HelpLink` | 可选 `String` 参数。<br/><br /> 指向有关警告详细信息的链接。 |
| `Text` | 可选 `String` 参数。<br /><br /> 如果 `Condition` 参数计算结果为 `true`，则为 MSBuild 记录的警告文本。 |

## <a name="remarks"></a>注解

 `Warning` 任务使 MSBuild 项目可以在继续下一个生成步骤之前，先检查必需的配置或属性是否存在。

 当 `Warning` 任务的 `Condition` 参数的计算结果为 `true` 时，将记录 `Text` 参数的值，并继续执行生成操作。 如果 `Condition` 参数不存在，则记录警告文本。 有关日志记录的详细信息，请参阅[获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)。

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

`HelpKeyword`由 Visual Studio 用于支持 F1 (上下文) 。 可以使用 将 `HelpLink` 联机帮助页与错误消息关联。

## <a name="example"></a>示例

 以下代码示例检查在命令行上设置的属性。 如果未设置任何属性，则项目将引发警告事件，并记录 `Warning` 任务的 `Text` 参数的值。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="ValidateCommandLine">
        <Warning
            Text=" The 0 property was not set on the command line."
            Condition="'$(0)' == ''" />
        <Warning
            Text=" The FREEBUILD property was not set on the command line."
            Condition="'$(FREEBUILD)' == ''" />
    </Target>
    ...
</Project>
```

## <a name="see-also"></a>另请参阅

- [获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
