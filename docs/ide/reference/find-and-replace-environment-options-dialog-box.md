---
title: “选项”对话框 ->“环境”->“查找和替换”
description: 了解如何使用“环境”部分的“查找和替换”页来控制消息框以及查找和替换操作的其他方面。
ms.custom: SEO-VS-2020
ms.date: 12/16/2021
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.FindReplace
- VS.ToolsOptionsPages.Environment.FindandReplace
helpviewer_keywords:
- Find and Replace, Options dialog box
- Find and Replace, customizing
ms.assetid: f804d6d5-6309-46e4-8294-b83e880b5ec9
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: d999364cff0a868917eb204443f327d19f975781
ms.sourcegitcommit: d3578c384959f1b76dd06fb4b5d075fb052f8c69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2021
ms.locfileid: "135374839"
---
# <a name="find-and-replace-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“查找和替换”

使用“选项”对话框的此页，可以控制消息框及查找和替换操作的其他方面。 可以从 " **工具** " 菜单中选择 " **选项**"，展开 " **环境**"，然后选择 " **查找和替换**" 来访问此对话框。

显示信息性消息

选择此选项可以显示所有具有“始终显示此消息”选项的“查找和替换”信息性消息。 例如，如果选择不显示消息“查找已到达搜索的起始点”，则选择此选项将导致此信息性消息在使用“查找和替换”时再次出现。

如果不想看到“查找和替换”的任何信息性消息，请清除此选项。

如果对某些“查找和替换”信息性消息（但不是全部）清除“始终显示此消息”选项，“显示信息性消息”复选框将被填充，但不会被选中。 若要还原所有可选的“查找和替换”消息，请先清除此选项，然后再次选择。

> [!NOTE]
> 此选项不会影响任何未显示“始终显示此消息”选项的“查找和替换”信息性消息。

显示警告消息

选择此选项可以显示所有具有“始终显示此消息”选项的“查找和替换”警告消息。 例如，如果选择不显示“全部替换”警告消息，而此消息又在你尝试在当前未打开进行编辑的文件中进行替换时出现，则选择此选项将导致此警告消息在你尝试全部替换时再次显示。

如果不想看到“查找和替换”的任何警告消息，请清除此选项。

如果对某些“查找和替换”警告消息（但不是全部）清除“始终显示此消息”选项，“显示警告消息”复选框将被填充，但不会被选中。 若要还原所有可选的“查找和替换”消息，请先清除此选项，然后再次选择。

> [!NOTE]
> 此选项不会影响任何未显示“始终显示此消息”选项的“查找和替换”警告消息。

使用编辑器中的文本自动填充“查找内容”

如果选择此选项，从“编辑”菜单选择“查找和替换”窗口的任何视图时，可以将当前编辑器插入点任何一侧的文本粘贴到“查找内容”字段。 清除此选项可以将上次搜索的最后一个搜索模式用作“查找内容”字符串。

**自动将搜索限制为所选内容**

如果要将搜索范围设置为所选的代码，请选择此选项。

如果您不希望只搜索所选的代码，请清除此选项。

**使用 "查找所有引用" 工具窗口中的编辑器背景**

如果希望 " **查找所有引用** " 工具窗口使用与编辑器相同的背景色，请选择此选项。 如果使用深色主题或具有深色背景色的自定义主题，这会很有帮助。 有关主题的详细信息，请参阅在[Visual Studio 中更改字体、颜色和主题](../how-to-change-fonts-and-colors-in-visual-studio.md)。

::: moniker range=">=vs-2019"

**默认情况下保留搜索结果**

如果希望默认保留所有搜索结果，而不是在每次搜索后选择 " **保留结果** " 按钮，请选择此选项。 有关此功能的详细信息，请参阅 " [在文件中查找](../find-in-files.md#keep-results) " 页的 "保留结果" 部分。

::: moniker-end

## <a name="see-also"></a>请参阅

- [查找和替换文本](../finding-and-replacing-text.md)
- [在文件中查找](../find-in-files.md)
