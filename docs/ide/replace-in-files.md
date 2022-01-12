---
title: 在文件中替换
description: 了解“在文件中替换”功能，以及如何使用该功能在一组指定文件的代码中搜索某个字符串或表达式，并更改找到的部分或全部匹配项。
ms.custom: SEO-VS-2020
ms.date: 01/04/2022
ms.topic: conceptual
f1_keywords:
- vs.findreplace.replaceinfiles
- vs.replaceinfiles
helpviewer_keywords:
- text searches, replacing text
- find and replace
- replace in files
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: cd864bb7423e95694ae63643ffd1f1be75224a72
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135804481"
---
# <a name="replace-in-files"></a>在文件中替换

借助“在文件中替换”功能，可以在一组指定文件的代码中搜索某个字符串或表达式，并更改一部分或全部的匹配项。 找到的匹配项与所执行的操作在“结果选项”中选择的“查找结果”窗口中列出 。

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/find-replace-files.png" alt-text="Visual Studio 2022 中的 &quot;查找和替换&quot; 对话框的屏幕截图，其中打开了 &quot;在文件中替换&quot; 选项卡。":::

::: moniker-end

::: moniker range="vs-2019"

:::image type="content" source="media/vs-2019/find-replace-files.png" alt-text="Visual Studio 2019 中的 &quot;查找和替换&quot; 对话框的屏幕截图，其中打开了 &quot;在文件中替换&quot; 选项卡。":::

> [!IMPORTANT]
> 如果使用 Visual Studio 2019 [版本 16.6](/visualstudio/releases/2019/release-notes-v16.6/) 或更早的版本，则“查找和替换”对话框可能与此处显示的不同。 切换到本页的 [Visual Studio 2017](find-in-files.md?view=vs-2017&preserve-view=true) 版本，查看与屏幕上显示的内容相匹配的说明。

::: moniker-end

::: moniker range="vs-2017"

:::image type="content" source="media/find-replace-files.png" alt-text="Visual Studio 2017 中的 &quot;查找和替换&quot; 对话框的屏幕截图，其中打开了 &quot;在文件中替换&quot; 选项卡。":::

::: moniker-end

可以使用以下任一方法在“查找和替换”窗口中显示“在文件中替换”，或使用 Ctrl + Shift + H。

## <a name="to-display-replace-in-files"></a>显示“在文件中替换”

::: moniker range=">=vs-2019"

1. 按 Ctrl + Q，然后在屏幕顶部的搜索框中输入“替换”。

1. 在结果列表中选择“在文件中替换”。

   — 或 —

::: moniker-end

1. 在“编辑”菜单上展开“查找和替换”。

2. 选择“在文件中替换”。

   — 或 —

   如果已经打开“查找和替换”窗口，则在工具栏上选择“在文件中替换”。

> [!NOTE]
> “查找和替换”工具不会搜索具有 `Hidden` 或 `System` 属性的目录。

" **在文件中替换** " 选项与 "在 **[文件中查找](find-in-files.md)** " 选项相同，但有两个例外：对话框底部有其他替换操作按钮。 而且，对话框中提供了以下替换选项。

::: moniker range=">=vs-2019"

## <a name="replace-textbox"></a>替换文本框

若要将“查找”文本框中的字符串实例替换为其他字符串，请在“替换”文本框中输入替换字符串。 若要删除“查找”文本框中的字符串实例，则保留此字段为空。 打开列表以显示最近搜索的字符串。 若要在替换字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

::: moniker-end

::: moniker range="vs-2017"

## <a name="replace-with"></a>替换为

若要将“查找内容”框中的字符串实例替换为其他字符串，请在“替换为”框中输入替换字符串。 若要删除“查找内容”框中的字符串实例，则保留该字段为空。 打开列表，显示最近搜索的 20 个字符串。 若要在替换字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

## <a name="display-file-names-only"></a>只显示文件名

如果选中此复选框，则“查找结果”窗口将列出所有包含搜索字符串的文件的完整名称和路径。 但是，结果不包含显示字符串的代码行。 此复选框仅可用于“在文件中查找”。

::: moniker-end

## <a name="keep-modified-files-open-after-replace-all"></a>全部替换后保持将已修改的文件打开

选中此选项后，此选项会将已进行替换的所有文件保留为打开状态，以便您可以撤消或保存更改。 内存方面的制约可能会限制在替换操作之后可以保持打开的文件数。

> [!CAUTION]
> 只能对保持打开状态以供编辑的文件使用 **“撤消”** 选项。 如果未选择此选项，则尚未打开以供编辑的文件继续处于关闭状态，并且在这些文件中 **“撤消”** 选项不可用。

::: moniker range=">=vs-2022"

> [!NOTE]
> 从 Visual Studio 2022 开始，搜索性能得到了优化，在显示最终结果之前，会显示部分结果，如来自预索引文件的结果。 不过，在执行替换操作时，这种性能优势不适用，因为替换操作只有在返回完整搜索结果后才会开始。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [查找和替换文本](../ide/finding-and-replacing-text.md)
- [在文件中查找](../ide/find-in-files.md)
- [Visual Studio 命令](../ide/reference/visual-studio-commands.md)
