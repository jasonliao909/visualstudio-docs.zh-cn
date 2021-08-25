---
title: ParameterGroup 元素 | Microsoft Docs
description: 了解 MSBuild ParameterGroup 元素，它包含可选的参数列表，这些参数显示在由 UsingTask TaskFactory 生成的任务上。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ParameterGroup> element [MSBuild]
- ParameterGroup element [MSBuild]
ms.assetid: c3275e69-a427-4889-bc1d-51bff2c285fa
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: c56eb3b3bfb79bd7896657719157fc6a4bd8e99c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122100668"
---
# <a name="parametergroup-element"></a>ParameterGroup 元素

包含一系列可选参数，这些参数将显示在通过使用 `UsingTask` `TaskFactory` 生成的任务上。 有关详细信息，请参阅 [UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)。

 \<Project> \<UsingTask>
 \<ParameterGroup>

## <a name="syntax"></a>语法

```xml
<ParameterGroup />
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[参数](../msbuild/parameter-element.md)|包含某个任务的特定参数信息，该任务可通过使用 `UsingTask` `TaskFactory` 生成。 元素的名称就是该参数的名称。|

### <a name="parent-elements"></a>父元素

| 元素 | 说明 |
| - | - |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | 提供在 MSBuild 中注册任务的方法。 项目中可能有零个或零个以上的 `UsingTask` 元素。 |

## <a name="example"></a>示例

 下面的示例演示如何使用 `ParameterGroup` 元素。

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

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
