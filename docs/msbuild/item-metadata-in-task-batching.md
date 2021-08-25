---
title: 任务批处理中的项元数据 | Microsoft Docs
description: 了解 MSBuild 如何使用任务批处理中的项元数据将项列表划分到不同的类别/批次并对每批逐一运行任务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
- task batching [MSBuild]
- MSBuild, task batching
ms.assetid: 31e480f8-fe4d-4633-8c54-8ec498e2306d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: b3afd2b860d56fd78d01cf9509c7e3c75fc9c4e5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122136880"
---
# <a name="item-metadata-in-task-batching"></a>任务批处理中的项元数据

MSBuild 可基于项元数据将项列表划分为不同类别或批次，并对每批逐一运行任务。 要准确了解哪个批中正在传递什么项可能比较困难。 本主题介绍了以下涉及批处理的常见方案。

- 将一个项列表划分为多个批

- 将多个项列表划分为多个批

- 一次对一个项进行批处理

- 筛选项列表

有关 MSBuild 批处理的详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。

## <a name="divide-an-item-list-into-batches"></a>将一个项列表划分为多个批

通过批处理可基于项元数据将一个项列表划分为不同的批，并将其中每个批单独传递到任务。 这对生成附属程序集非常有用。

以下示例演示了如何基于项元数据将一个项列表划分为多个批。 `ExampColl` 项列表基于 `Number` 项元数据被划分为三个批。 若 `Text` 属性中存在 `%(ExampColl.Number)`，则会通知 MSBuild 应执行批处理。 `ExampColl` 项列表基于 `Number` 元数据被划分为三个批，其中每个批被单独传递到任务。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <ExampColl Include="Item1">
            <Number>1</Number>
        </ExampColl>
        <ExampColl Include="Item2">
            <Number>2</Number>
        </ExampColl>
        <ExampColl Include="Item3">
            <Number>3</Number>
        </ExampColl>
        <ExampColl Include="Item4">
            <Number>1</Number>
        </ExampColl>
        <ExampColl Include="Item5">
            <Number>2</Number>
        </ExampColl>
        <ExampColl Include="Item6">
            <Number>3</Number>
        </ExampColl>
    </ItemGroup>

    <Target Name="ShowMessage">
        <Message
            Text = "Number: %(ExampColl.Number) -- Items in ExampColl: @(ExampColl)"/>
    </Target>

</Project>
```

[Message 任务](../msbuild/message-task.md)将显示以下信息：

`Number: 1 -- Items in ExampColl: Item1;Item4`

`Number: 2 -- Items in ExampColl: Item2;Item5`

`Number: 3 -- Items in ExampColl: Item3;Item6`

## <a name="divide-several-item-lists-into-batches"></a>将多个项列表划分为多个批

MSBuild 可基于相同元数据将多个项列表划分为多个批。 这样可以轻松地将不同项列表划分为多个批来生成多个程序集。 例如，可将 .cs 文件的项列表划分为一个应用程序批和一个程序集批，并将资源文件的项列表划分为一个应用程序批和程序集批。 然后，可以使用批处理将这些项列表传递到一个任务，并生成应用程序和程序集。

> [!NOTE]
> 如果正被传递到任务的项列表不包含任何具有引用元数据的项，则该项列表中的每个项会被传递到每个批。

以下示例演示了如何基于项元数据将多个项列表划分为多个批。 `ExampColl` 项列表和 `ExampColl2` 项列表基于 `Number` 项元数据分别被划分为三个批。 若 `Text` 属性中存在 `%(Number)`，则会通知 MSBuild 应执行批处理。 `ExampColl` 项列表和 `ExampColl2` 项列表基于 `Number` 元数据被划分为三个批，其中每个批被单独传递到任务。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>

        <ExampColl Include="Item1">
            <Number>1</Number>
        </ExampColl>
        <ExampColl Include="Item2">
            <Number>2</Number>
        </ExampColl>
        <ExampColl Include="Item3">
            <Number>3</Number>
        </ExampColl>

        <ExampColl2 Include="Item4">
            <Number>1</Number>
        </ExampColl2>
        <ExampColl2 Include="Item5">
            <Number>2</Number>
        </ExampColl2>
        <ExampColl2 Include="Item6">
            <Number>3</Number>
        </ExampColl2>

    </ItemGroup>

    <Target Name="ShowMessage">
        <Message
            Text = "Number: %(Number) -- Items in ExampColl: @(ExampColl) ExampColl2: @(ExampColl2)"/>
    </Target>

</Project>
```

[Message 任务](../msbuild/message-task.md)将显示以下信息：

`Number: 1 -- Items in ExampColl: Item1 ExampColl2: Item4`

`Number: 2 -- Items in ExampColl: Item2 ExampColl2: Item5`

`Number: 3 -- Items in ExampColl: Item3 ExampColl2: Item6`

## <a name="batch-one-item-at-a-time"></a>一次对一个项进行批处理

此外，还可对创建时分配给每个项的常见项元数据执行批处理。 这保证了集合中每个项具有用于批处理的元数据。 `Identity` 元数据值可用于将项列表中的每个项划分为单独的批。 若要获得常见项元数据的完整列表，请参阅[常见项元数据](../msbuild/msbuild-well-known-item-metadata.md)。

以下示例演示了如何一次对项列表中的每个项执行批处理。 `ExampColl` 项列表分为六个批，每个批都包含项列表的一个项。 若 `Text` 属性中存在 `%(Identity)`，则会通知 MSBuild 应执行批处理。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>

        <ExampColl Include="Item1"/>
        <ExampColl Include="Item2"/>
        <ExampColl Include="Item3"/>
        <ExampColl Include="Item4"/>
        <ExampColl Include="Item5"/>
        <ExampColl Include="Item6"/>

    </ItemGroup>

    <Target Name="ShowMessage">
        <Message
            Text = "Identity: '%(Identity)' -- Items in ExampColl: @(ExampColl)"/>
    </Target>

</Project>
```

[Message 任务](../msbuild/message-task.md)将显示以下信息：

```output
Identity: 'Item1' -- Items in ExampColl: Item1
Identity: 'Item2' -- Items in ExampColl: Item2
Identity: 'Item3' -- Items in ExampColl: Item3
Identity: 'Item4' -- Items in ExampColl: Item4
Identity: 'Item5' -- Items in ExampColl: Item5
Identity: 'Item6' -- Items in ExampColl: Item6
```

但 `Identity` 无法保证是唯一的，其值是 `Include` 属性的评估最终值。 因此，如果多次使用任何 `Include` 属性，则会对它们一起进行批处理。 如以下示例所示，此方法要求 `Include` 属性对于组中每个项都是唯一的。 为了说明这点，请考虑下列代码：

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <ItemGroup>
    <Item Include="1">
      <M>1</M>
    </Item>
    <Item Include="1">
      <M>2</M>
    </Item>
    <Item Include="2">
      <M>3</M>
    </Item>
  </ItemGroup>

  <Target Name="Batching">
    <Warning Text="@(Item->'%(Identity): %(M)')" Condition=" '%(Identity)' != '' "/>
  </Target>
</Project>
```

输出显示前两个项位于同一批中，因为 `Include` 属性对于它们是相同的：

```output
test.proj(15,5): warning : 1: 1;1: 2
test.proj(15,5): warning : 2: 3
```

## <a name="filter-item-lists"></a>筛选器项目列表

在传递到任务之前，可使用批处理从项列表中筛选出某些特定项。 例如，通过筛选 `Extension` 常见项元数据值可仅对具有特定扩展名的文件运行任务。

以下示例演示如何基于项元数据将一个项列表划分为多个批，以及如何在这些批传递到任务时对这些批进行筛选。 `ExampColl` 项列表基于 `Number` 项元数据被划分为三个批。 任务的 `Condition` 属性指定仅将 `Number` 项元数据值为 `2` 的批传递到任务

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>

        <ExampColl Include="Item1">
            <Number>1</Number>
        </ExampColl>
        <ExampColl Include="Item2">
            <Number>2</Number>
        </ExampColl>
        <ExampColl Include="Item3">
            <Number>3</Number>
        </ExampColl>
        <ExampColl Include="Item4">
            <Number>1</Number>
        </ExampColl>
        <ExampColl Include="Item5">
            <Number>2</Number>
        </ExampColl>
        <ExampColl Include="Item6">
            <Number>3</Number>
        </ExampColl>

    </ItemGroup>

    <Target Name="Exec">
        <Message
            Text = "Items in ExampColl: @(ExampColl)"
            Condition="'%(Number)'=='2'"/>
    </Target>

</Project>
```

[Message 任务](../msbuild/message-task.md)将显示以下信息：

```
Items in ExampColl: Item2;Item5
```

## <a name="see-also"></a>请参阅

- [常见项元数据](../msbuild/msbuild-well-known-item-metadata.md)
- [Item 元素 (MSBuild)](../msbuild/item-element-msbuild.md)
- [ItemMetadata 元素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)
- [批处理](../msbuild/msbuild-batching.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
