---
title: FindInList 任务 | Microsoft Docs
description: 了解如何使用 MSBuild FindInList 任务在指定列表中查找具有匹配 itemspec 的项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- FindInList task [MSBuild]
- MSBuild, FindInList task
ms.assetid: d49b9f84-52a2-4242-9269-b741a7a7e9f7
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 09390421bbf4a64486ffa59ab91bf361f0227b2b
ms.sourcegitcommit: 76541583274c4af4218ac2a8ab4308077a7e340e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2021
ms.locfileid: "132733135"
---
# <a name="findinlist-task"></a>FindInList 任务

在指定的列表中查找具有匹配的 itemspec 的项。

## <a name="parameters"></a>参数

 下表描述了 [FindInList 任务](../msbuild/findinlist-task.md)的参数。

|参数|说明|
|---------------|-----------------|
|`CaseSensitive`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则搜索区分大小写，否则不区分大小写。 默认值为 `false`。|
|`FindLastMatch`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则返回最后一个匹配项；否则返回第一个匹配项。 默认值为 `false`。|
|`ItemFound`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读输出参数。<br /><br /> 在列表中发现的第一个匹配项（如有）。|
|`ItemSpecToFind`|必选 `String` 参数。<br /><br /> 要搜索的 itemspec。|
|`List`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 要在其中搜索 itemspec 的列表。|
|`MatchFileNameOnly`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，只需对 itemspec 的文件名部分进行匹配；否则对整个 itemspec 进行匹配。 默认值是 `true`。|

## <a name="remarks"></a>备注

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
