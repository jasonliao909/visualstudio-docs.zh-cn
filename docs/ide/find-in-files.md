---
title: 在文件中查找
description: 了解“在文件中查找”功能，并了解如何使用此功能搜索特定的一组文件。
ms.custom: SEO-VS-2020
ms.date: 07/23/2021
ms.topic: conceptual
f1_keywords:
- vs.findinfiles
helpviewer_keywords:
- objects [Visual Studio], finding
- text searches, replacing text
- objects [Visual Studio], searching for
- Find and Replace window, Find in Files tab
- text searches, Find and Replace window
- documents, searching
- files, searching
- Find in Files tab, Find and Replace window
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bffb7e2f8866ccd2371f8e501788672cb55c03f8
ms.sourcegitcommit: fdba1b294b94e1f6a8e897810646873422393fff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2021
ms.locfileid: "114680180"
---
# <a name="find-in-files"></a>在文件中查找

“在文件中查找”可用于搜索指定的一组文件。 Visual Studio 找到的匹配项在 IDE 中的“查找结果”窗口中列出。 结果的显示方式取决于在你“查找和替换”对话框的“在文件中查找”选项卡上选择的选项。 

::: moniker range=">=vs-2019"

:::image type="content" source="media/find-files-vs2019.png" alt-text="Visual Studio 2019 中“查找和替换”对话框的屏幕截图，其中打开了“在文件中查找”选项卡。":::

> [!IMPORTANT]
> 如果使用 Visual Studio 2019 [版本 16.6](/visualstudio/releases/2019/release-notes-v16.6/) 或更早的版本，则“查找和替换”对话框可能与此处显示的不同。 切换到本页的 [Visual Studio 2017](find-in-files.md?view=vs-2017&preserve-view=true) 版本，查看与屏幕上显示的内容相匹配的说明。

::: moniker-end

::: moniker range="vs-2017"

:::image type="content" source="media/find-files-vs2017.png" alt-text="Visual Studio 2017 中“查找和替换”对话框的屏幕截图，其中打开了“在文件中查找”选项卡。":::

::: moniker-end

## <a name="how-to-display-find-in-files"></a>如何显示“在文件中查找”

使用以下步骤打开“查找和替换”对话框，或按 Ctrl +Shift+F。

1. 在菜单栏中，选择“编辑” > “查找和替换” 。

1. 从弹出菜单中选择“在文件中查找”。

若要取消“查找”操作，请按 Ctrl+Break 。

> [!NOTE]
> “查找和替换”工具不会搜索具有 `Hidden` 或 `System` 属性的目录。

::: moniker range="vs-2017"

## <a name="find-what"></a>查找内容：

若要搜索一个新的文本字符串或表达式，请在“查找内容”框中进行指定。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="search-box"></a>搜索框

若要搜索一个新的文本字符串或表达式，请在“搜索”框中进行指定。 若要搜索最近搜索的 20 条字符串中的任意一条，请打开下拉列表并选择字符串。

可以选择或清除以下一个或多个选项：

- **匹配大小写**  - 如果选择此选项，“查找结果”搜索将区分大小写。
- **全字匹配**  - 如果选择此选项，“查找结果”窗口将仅返回全字匹配项。
- **使用正则表达式**  - 选中后，可以在“搜索”框中（或“替换”文本框中）使用特殊表示法来定义要匹配的文本。 有关这些表示法的列表，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

    > [!Important]
    > 仅当选中“使用正则表达式”复选框后，“表达式生成器”按钮才会显示在“搜索”框旁边。 
    >
    > :::image type="content" source="media/find-files-expression-builder-vs-2019.png" alt-text="“在文件中查找”对话框的屏幕截图，其中包含“表达式生成器”按钮和“使用正则表达式”复选框，其周围带有边框。":::

## <a name="look-in"></a>查找范围

从“查找范围”下拉列表中选择的选项确定“在文件中查找”是搜索整个工作区、整个解决方案、当前项目、当前目录、所有打开的文档还是当前文档。 

还可使用相邻的“浏览(...)”按钮找到要搜索的位置。

此外，还可以选中或清除“包括外部项”复选框和/或“包括杂项文件”复选框。 

## <a name="file-types"></a>文件类型

“文件类型”选项指示要在“查找范围”目录中搜索的文件类型。  选择列表中的任意项以输入预配置的搜索字符串，该字符串将查找那些特定类型的文件。 还可以排除文件。 为此，请以“！”字符作为任何路径或文件类型的前缀，以将其从搜索中排除。

### <a name="append-results"></a>附加结果

使用此选项将当前搜索的结果追加到上次的搜索结果中。

::: moniker-end

::: moniker range="vs-2017"

### <a name="expression-builder"></a>表达式生成器

如果要在搜索字符串中使用正则表达式，请选择搜索框旁相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

> [!NOTE]
> 只有在“查找选项”下选择了“使用正则表达式”后，才会启用“表达式生成器”按钮  。

## <a name="look-in"></a>查找范围:

从“查找范围”下拉列表中选择的选项将确定“在文件中查找”是仅在当前活动文件中搜索，还是在特定文件夹内存储的所有文件中搜索。

从列表中选择搜索范围，或单击“浏览(...)”按钮以显示“选择搜索文件夹”对话框并输入自己的目录集。 也可以直接在“查找范围”框中键入路径。

> [!WARNING]
> 如果选择“整个解决方案”或“当前项目”选项，可不搜索项目和解决方案文件 。 如果想要在项目文件进行查找，请选择搜索文件夹。

> [!NOTE]
> 如果使用“查找范围”选项会搜索已从源代码管理中签出的文件，则只会找到已下载到本机计算机的文件版本。

::: moniker-end

::: moniker range="vs-2017"

## <a name="include-subfolders"></a>包括子文件夹

指定将搜索“查找范围”文件夹的子文件夹。

## <a name="find-options"></a>查找选项

可以展开或折叠“查找选项”部分。 可以选择或清除以下选项：

可以选择或清除以下一个或多个选项：

**匹配大小写**

如果选择此选项，“查找结果”搜索将区分大小写

**全字匹配**

如果选择此选项，“查找结果”窗口将仅返回全字匹配项。

**使用正则表达式**

如果选中此复选框，则可以使用特殊表示法在“查找内容”或“替换为”文本框中定义要匹配的文本模式。 有关这些表示法的列表，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

**查找以下文件类型**

此列表指示要在“查找范围”目录中搜索的文件类型。 如果此字段为空白，则将搜索“查找范围”目录中的所有文件。

选择列表中的任意项以输入预配置的搜索字符串，该字符串将查找那些特定类型的文件。

## <a name="result-options"></a>结果选项

可以展开或折叠“结果选项”部分。 可以选中或清除“在以下位置列出结果”下的以下选项：

**“查找结果 1”窗口**

如果选择此选项，当前的搜索结果将替换“查找结果 1”窗口中的内容。 此窗口将自动打开，以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 1”  。

**“查找结果 2”窗口**

如果选择此选项，当前的搜索结果将替换“查找结果 2”窗口中的内容。 此窗口将自动打开，以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 2”。

> [!TIP]
> 可以通过按 Alt+1 或Alt+2 在结果窗口之间进行切换。

**查找结果表**

以表格式而不是文本列表显示搜索结果。

**附加结果**

从搜索的结果追加到以前的搜素结果。

**只显示文件名**

显示包含搜索匹配项的文件列表，而不显示搜索匹配项本身。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [在文件中替换](../ide/replace-in-files.md)
- [查找和替换文本](../ide/finding-and-replacing-text.md)
- [Visual Studio 命令](../ide/reference/visual-studio-commands.md)