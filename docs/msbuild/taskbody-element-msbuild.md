---
title: UsingTask 的 Task 元素 (MSBuild) | Microsoft Docs
description: 了解 MSBuild UsingTask 的 Task 元素，它包含传递给 UsingTask TaskFactory 的数据。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Task element [MSBuild]
- <Task> element [MSBuild]
ms.assetid: 49d8741b-f1ea-4470-94fd-a1ac27341a6a
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 6e5156d0d128bce8b927bbdc8faacdd93834e167
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642469"
---
# <a name="task-element-of-usingtask-msbuild"></a>UsingTask 的 Task 元素 (MSBuild)

包含传递给 `UsingTask` `TaskFactory` 的数据。 有关详细信息，请参阅 [UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)。

 \<Project> \<UsingTask>
 \<Task>

## <a name="syntax"></a>语法

```xml
<Task Evaluate="true/false" />
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|`Evaluate`|可选布尔属性。<br /><br /> 如果值为 `true`，任务实例化时，MSBuild 对所有内部元素求值，并在将信息传递到 `TaskFactory` 前扩展项和属性。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|数据|`Task` 标记之间的文本一字不差地发送到 `TaskFactory`。|

### <a name="parent-elements"></a>父元素

| 元素 | 说明 |
| - | - |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | 提供在 MSBuild 中注册任务的方法。 项目中可能有零个或零个以上的 `UsingTask` 元素。 |

## <a name="example"></a>示例

 下面的示例演示如何将 `Task` 元素和 `Evaluate` 属性结合使用。

```xml
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">
       <ParameterGroup>
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>
              ...
</ParameterGroup>
       <Task Evaluate="true">
       ... Task factory-specific data ...
       </Task>
</UsingTask>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
