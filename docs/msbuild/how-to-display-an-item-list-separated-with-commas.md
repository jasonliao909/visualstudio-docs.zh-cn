---
title: 如何：显示用逗号分隔的项列表 | Microsoft Docs
description: 了解如何使用 MSBuild 显示用逗号分隔的项列表，或为项列表指定其他分隔符字符串。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, separating items with semicolons
- MSBuild, formatting item collections
ms.assetid: 3cae844c-7c6d-4144-82dc-efad10ba458f
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 87fc8cb1870d2c99a7e654b8f9fa3ecc31773be3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093746"
---
# <a name="how-to-display-an-item-list-separated-with-commas"></a>如何：显示用逗号分隔的项列表

在 Microsoft 生成引擎 (MSBuild) 中处理项列表时，有时以易于阅读的方式显示这些项列表的内容会很有帮助。 或者，你执行的任务可能会用到以特殊的分隔符字符串分隔的项列表。 在这两种情况中，可以为项列表指定分隔符字符串。

## <a name="separate-items-in-a-list-with-commas"></a>用逗号分隔列表中的项

默认情况下，MSBuild 用分号分隔列表中的项。 例如，请看一个含有以下值的 `Message` 元素：

`<Message Text="This is my list of TXT files: @(TXTFile)"/>`

当 `@(TXTFile)` 项列表包含项 App1.txt、App2.txt 和 App3.txt 时，消息为：

`This is my list of TXT files: App1.txt;App2.txt;App3.txt`

如果要更改默认行为，可以指定自己的分隔符。 用于指定项列表分隔符的语法是：

`@(ItemListName, '<separator>')`

分隔符可以是单个字符，也可以是字符串，并且必须括在单引号中。

#### <a name="to-insert-a-comma-and-a-space-between-items"></a>在各项之间插入逗号和空格

- 使用类似下面这样的项表示法：

    `@(TXTFile, ', ')`

## <a name="example"></a>示例

在此示例中，[Exec](../msbuild/exec-task.md) 任务会运行 findstr 工具，在文件 Phrases.txt 中查找指定的文本字符串。 在 findstr 命令中，文本搜索字符串由 /c: 开关指示，因此 `@(Phrase)` 项列表中各项之间应插入分隔符 ` /c:`。

对于此示例，等效的命令行命令为：

`findstr /i /c:hello /c:world /c:msbuild phrases.txt`

```xml
<Project DefaultTargets = "Find"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <ItemGroup>
        <Phrase Include="hello"/>
        <Phrase Include="world"/>
        <Phrase Include="msbuild"/>
    </ItemGroup>

    <Target Name = "Find">
        <!-- Find some strings in a file -->
        <Exec Command="findstr /i /c:@(Phrase, ' /c:') phrases.txt"/>
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [项](../msbuild/msbuild-items.md)
