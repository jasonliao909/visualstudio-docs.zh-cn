---
title: 项函数 | Microsoft Docs
description: 了解任务和目标中的 MSBuild 代码如何调用项函数来获取项目中各项的相关信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, Item functions
ms.assetid: 5e6df3cc-2db8-4cbd-8fdd-3ffd03ac0876
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 8150231e6ecf6c2b2f789da68fd4aae8d334854f
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133514501"
---
# <a name="item-functions"></a>项函数

任务和目标中的代码可以调用项函数来获取项目中各项的相关信息（MSBuild 4.0 及更高版本）。 这些函数简化不同项的获取过程，并且比循环遍历项的速度更快。

## <a name="string-item-functions"></a>字符串项函数

可以在 .NET Framework 中使用字符串方法和属性对任何项值进行操作。 对于 <xref:System.String> 方法，指定方法名称。 对于 <xref:System.String> 属性，请在“get_”之后指定属性名。

对于具有多个字符串的项，字符串方法或属性会对每个字符串运行。

下面的示例显示如何使用这些字符串项函数。

```xml
<ItemGroup>
    <theItem Include="andromeda;tadpole;cartwheel" />
</ItemGroup>

<Target Name = "go">
    <Message Text="IndexOf  @(theItem->IndexOf('r'))" />
    <Message Text="Replace  @(theItem->Replace('tadpole', 'pinwheel'))" />
    <Message Text="Length   @(theItem->get_Length())" />
    <Message Text="Chars    @(theItem->get_Chars(2))" />
</Target>

  <!--
  Output:
    IndexOf  3;-1;2
    Replace  andromeda;pinwheel;cartwheel
    Length   9;7;9
    Chars    d;d;r
  -->
```

## <a name="intrinsic-item-functions"></a>内部项函数

下表列出了可用于各项的内部函数。

:::moniker range="vs-2017"

|函数|示例|描述|
|--------------|-------------|-----------------|
|`Count`|`@(MyItem->Count())`|返回项计数。|
|`DirectoryName`|`@(MyItem->DirectoryName())`|返回每个项的 `Path.DirectoryName` 等效项。|
|`Distinct`|`@(MyItem->Distinct())`|返回具有不同 `Include` 值的项。 忽略元数据。 比较不区分大小写。|
|`DistinctWithCase`|`@(MyItem->DistinctWithCase())`|返回具有不同 `itemspec` 值的项。 忽略元数据。 比较是区分大小写的。|
|`Reverse`|`@(MyItem->Reverse())`|按相反顺序返回项。|
|`AnyHaveMetadataValue`|`@(MyItem->AnyHaveMetadataValue("MetadataName", "MetadataValue"))`|返回 `boolean`，指示是否有任何项具有给定的元数据名和值。 比较不区分大小写。|
|`ClearMetadata`|`@(MyItem->ClearMetadata())`|返回清除了元数据的项。 仅保留 `itemspec`。|
|`HasMetadata`|`@(MyItem->HasMetadata("MetadataName"))`|返回具有给定元数据名的项。 比较不区分大小写。|
|`Metadata`|`@(MyItem->Metadata("MetadataName"))`|返回具有元数据名的元数据的值。|
|`WithMetadataValue`|`@(MyItem->WithMetadataValue("MetadataName", "MetadataValue"))`|返回具有给定元数据名和值的项。 比较不区分大小写。|

:::moniker-end
:::moniker range=">=vs-2019"

|函数|示例|说明|
|--------------|-------------|-----------------|
|`Combine`|`@(MyItems->Combine('path'))`|返回一个新的项集，其中包含附加到所有输入项的给定的相对路径。|
|`Count`|`@(MyItems->Count())`|返回项计数。|
|`DirectoryName`|`@(MyItems->DirectoryName())`|返回每个项的 `Path.DirectoryName` 等效项。|
|`Distinct`|`@(MyItems->Distinct())`|返回具有不同 `Include` 值的项。 忽略元数据。 比较不区分大小写。|
|`DistinctWithCase`|`@(MyItems->DistinctWithCase())`|返回具有不同 `itemspec` 值的项。 忽略元数据。 比较是区分大小写的。|
|`Exists`|`@(MyItems->Exists())`|筛选一组项，这些项对磁盘上实际存在的项进行筛选。|
|`GetPathsOfAllDirectoriesAbove`| `@(MyItems->GetPathsOfAllFilesAbove())`|给定一组项后，返回表示所有祖先目录的项。 不保证顺序。|
|`Reverse`|`@(MyItems->Reverse())`|按相反顺序返回项。|
|`AnyHaveMetadataValue`|`@(MyItems->AnyHaveMetadataValue("MetadataName", "MetadataValue"))` | 返回 `boolean`，指示是否有任何项具有给定的元数据名和值。 比较不区分大小写。 |
|`ClearMetadata`|`@(MyItems->ClearMetadata())` |返回清除了元数据的项。 仅保留 `itemspec`。|
|`HasMetadata`|`@(MyItems->HasMetadata("MetadataName"))`|返回具有给定元数据名的项。 比较不区分大小写。|
|`Metadata`|`@(MyItems->Metadata("MetadataName"))`|返回具有元数据名的元数据的值。|
|`WithMetadataValue`|`@(MyItems->WithMetadataValue("MetadataName", "MetadataValue"))`|返回具有给定元数据名和值的项。 比较不区分大小写。|

> [!NOTE]
> `Exists`还可在其他上下文中使用;例如，在[MSBuild 情况](msbuild-conditions.md)下， `Condition="Exists('path')"` 或在[静态属性函数](property-functions.md)中，例如 `$([System.IO.File]::Exists("path"))` 。
:::moniker-end

下面的示例显示如何使用内部项函数。

```xml
<ItemGroup>
    <TheItem Include="first">
        <Plant>geranium</Plant>
    </TheItem>
    <TheItem Include="second">
        <Plant>algae</Plant>
    </TheItem>
    <TheItem Include="third">
        <Plant>geranium</Plant>
    </TheItem>
</ItemGroup>

<Target Name="go">
    <Message Text="MetaData:    @(TheItem->Metadata('Plant'))" />
    <Message Text="HasMetadata: @(theItem->HasMetadata('Plant'))" />
    <Message Text="WithMetadataValue: @(TheItem->WithMetadataValue('Plant', 'geranium'))" />
    <Message Text=" " />
    <Message Text="Count:   @(theItem->Count())" />
    <Message Text="Reverse: @(theItem->Reverse())" />
</Target>

  <!--
  Output:
    MetaData:    geranium;algae;geranium
    HasMetadata: first;second;third
    WithMetadataValue: first;third

    Count:   3
    Reverse: third;second;first
  -->
```

## <a name="msbuild-condition-functions"></a>MSBuild 条件函数

函数 `Exists` 和 `HasTrailingSlash` 不是项函数。 它们可与 `Condition` 属性一起使用。 请参阅 [MSBuild 条件](msbuild-conditions.md)。

## <a name="see-also"></a>请参阅

你还可以使用属性对项列表执行操作，如对项元数据进行筛选;查看 [项](../msbuild/msbuild-items.md)。
