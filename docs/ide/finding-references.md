---
title: 在代码中查找引用
description: 了解“查找所有引用”命令，以便查找代码中对特定代码元素的引用。
ms.custom: SEO-VS-2020
ms.date: 09/26/2017
ms.topic: conceptual
helpviewer_keywords:
- code editor, find all references
- find all references
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 2a942755238a356032f41e7cff9e5a462196275c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737120"
---
# <a name="find-references-in-your-code"></a>在代码中查找引用

可以使用“查找所有引用”命令在整个代码库中查找引用特定码位元素的位置  。 在你想要查找其引用的元素的上下文（右键单击）菜单中可以使用“查找所有引用”命令  。 或者，如果使用键盘，请按 Shift + F12  。

结果显示在名为 \<element> references 的工具窗口中，其中 element 是要搜索的项名称。 使用“引用”窗口里的工具栏，可以： 
- 在下拉列表框中更改搜索的范围。 选择仅在已更改的文档中进行查找，一直到查找完整个解决方案。
- 通过选择“复制”  按钮，复制引用的选定项。
- 通过选择按钮转到列表中的下一或上一位置，或按 F8 和 Shift + F8 键来完成此操作   。
- 选择“清除所有筛选器”  按钮，清除返回结果上的所有筛选器。
- 选择“分组依据:”下拉列表框中的设置，更改返回项的分组方式  。
- 选择“保留结果”  按钮，保留当前的搜索结果窗口。 选择此按钮后，当前的搜索结果会继续保留在此窗口中，而新的搜索结果则会显示在新的工具窗口中。
- 在“搜索查找所有引用”文本框中输入文本，在搜索结果中搜索字符串  。

还可以将鼠标悬停在任一搜索结果之上，从而查看引用预览。

![“查找所有引用”工具窗口](../ide/media/vside_findallreferences.png)

## <a name="navigate-to-references"></a>转到引用
可以使用以下方法导航到“引用”窗口中的引用： 

- 按 F8 转到下一个引用，或者按 Shift + F8 转到上一个引用   。
- 对引用按 Enter 键，或双击引用在代码中转到此引用  。
- 在引用的右键单击菜单（关联菜单）中，选择“转到上一位置”  或“转到下一位置”  命令。
- 选择向上箭头和向下箭头键（如果已在“选项”对话框中启用）    。 要启用此功能，请在菜单栏上依次选择“工具” > “选项” > “环境” > “选项卡和窗口” > “预览选项卡”，然后选中“允许在预览选项卡中打开新文件”和“在查找结果中预览选定的文件”框。

## <a name="change-reference-groupings"></a>更改引用分组
默认情况下，引用是先按项目进行分组，然后再按定义进行分组。 不过，可以更改工具栏上“分组依据:”下拉列表框中的设置，从而更改此分组顺序  。 例如，可以将其从默认设置“先按项目，然后按定义”更改为“先按定义，然后按项目”，也能更改为其他设置   。

虽然“定义”  和“项目”  是默认使用的两个分组，但可以在选定项的右键单击菜单或关联菜单中选择“分组”  命令，从而添加其他分组。 如果解决方案有许多文件和路径，那么添加其他分组将会很有帮助。

## <a name="filter-by-reference-type-in-net"></a>在 .NET 中按引用类型进行筛选
在 C# 或 Visual Basic 中，“查找引用”窗口有“类型”列，其中列出了找到的引用类型。 通过单击将鼠标悬停在列标题上方时显示的筛选器图标，可以使用此列按引用类型进行筛选。 可以按读取、写入、引用、名称、命名空间和类型筛选引用。

![“查找引用窗口类型”列 ](../ide/media/vside_findallreferencesKind.png)

## <a name="see-also"></a>另请参阅

- [导航代码](../ide/navigating-code.md)
