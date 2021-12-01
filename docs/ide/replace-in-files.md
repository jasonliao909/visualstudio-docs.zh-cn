---
title: 在文件中查找并替换
description: 了解“在文件中替换”功能，以及如何使用该功能在一组指定文件的代码中搜索某个字符串或表达式，并更改找到的部分或全部匹配项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
ms.openlocfilehash: 3b26c84a0db97299ad7a5c0602551ba930722d00
ms.sourcegitcommit: efe1d737fd660cc9183177914c18b0fd4e39ba8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2021
ms.locfileid: "130212229"
---
# <a name="replace-in-files"></a>在文件中替换

借助“在文件中替换”功能，可以在一组指定文件的代码中搜索某个字符串或表达式，并更改一部分或全部的匹配项。 找到的匹配项与所执行的操作在“结果选项”中选择的“查找结果”窗口中列出 。

> [!NOTE]
> 显示的对话框和菜单命令可能与“帮助”中的描述不同，具体取决于现用的设置或版本。 若要更改设置，例如“常规”或“Visual C++”设置，请选择“工具” > “导入和导出设置”，再选择“重置所有设置”。

可以使用以下任一方法在“查找和替换”窗口中显示“在文件中替换”，或使用 Ctrl + Shift + H。

## <a name="to-display-replace-in-files"></a>显示“在文件中替换”

::: moniker range=">=vs-2019"

1. 按 Ctrl + Q，然后在屏幕顶部的搜索框中输入“替换”。

1. 在结果列表中选择“在文件中替换”。

或

::: moniker-end

1. 在“编辑”菜单上展开“查找和替换”。

2. 选择“在文件中替换”。

   — 或 —

   如果已经打开“查找和替换”窗口，则在工具栏上选择“在文件中替换”。

:::moniker range="vs-2017"

## <a name="find-what"></a>查找内容

:::moniker-end

:::moniker range=">=vs-2019"

## <a name="find-textbox"></a>查找文本框

::: moniker-end

若要搜索一个新的文本字符串或表达式，请在框中进行指定。 若要搜索最近搜索的 20 条字符串中的任意一条，请打开下拉列表并选择字符串。 若要在搜索字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

> [!NOTE]
> 只有在“查找选项”下选择了“使用正则表达式”后，“表达式生成器”按钮才会启用。

::: moniker range="vs-2017"

## <a name="replace-with"></a>替换为

若要将“查找内容”框中的字符串实例替换为其他字符串，请在“替换为”框中输入替换字符串。 若要删除“查找内容”框中的字符串实例，则保留该字段为空。 打开列表，显示最近搜索的 20 个字符串。 若要在替换字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

::: moniker-end
::: moniker range=">=vs-2019"

## <a name="replace-textbox"></a>替换文本框

若要将“查找”文本框中的字符串实例替换为其他字符串，请在“替换”文本框中输入替换字符串。 若要删除“查找”文本框中的字符串实例，则保留此字段为空。 打开列表，显示最近搜索的 20 个字符串。 若要在替换字符串中使用一个或多个正则表达式，请选择相邻的“表达式生成器”按钮。 有关详细信息，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。

::: moniker-end

## <a name="look-in"></a>查找范围

从“查找范围”下拉列表中选择的选项，将确定“在文件中替换”是只搜索当前活动的文件还是搜索存储在特定文件夹内的所有文件。 从列表中选择搜索范围，键入文件夹路径，或单击“浏览(...)”按钮，即可显示“选择搜索文件夹”对话框并选择要搜索的一组文件夹。 也可以直接在“查找范围”框中键入路径。

> [!NOTE]
> 如果选中“查找范围”选项会导致搜索已从源代码管理中签出的文件，则只会搜索已下载到本机计算机的文件版本。

## <a name="find-options"></a>查找选项

可以展开或折叠“查找选项”部分。 可以选择或清除以下选项：

**匹配大小写**

选中时，“查找结果”窗口将仅显示内容和大小写均匹配的搜索字符串实例。 例如，选中“区分大小写”后搜索“MyObject”会返回“MyObject”，而不会返回“myobject”或“MYOBJECT”。

**全字匹配**

选中时，“查找结果”窗口将仅显示全字匹配的搜索字符串实例。 例如，搜索“MyObject”会返回“MyObject”，而不会返回“CMyObject”或“MyObjectC”。

**使用正则表达式**

:::moniker range="vs-2017"
选中此复选框后，可以使用特殊表示法在“查找内容”或“替换为”文本框中定义文本模式。 有关这些表示法的列表，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。
:::moniker-end
:::moniker range=">=vs-2019"
选中此复选框后，可以使用特殊表示法在“查找”或“替换”文本框中定义文本模式。 有关这些表示法的列表，请参阅[在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)。
:::moniker-end

**查找以下文件类型**

此列表指示要在“查找范围”目录中搜索的文件类型。 如果此字段留空，则将搜索“查找范围”目录中的所有文件。 选择列表中的任意项以输入预配置的搜索字符串，该字符串将查找那些特定类型的文件。

## <a name="result-options"></a>结果选项

可以展开或折叠“结果选项”部分。 可以选择或清除以下选项：

**查找结果 1** 窗口

如果选择此选项，当前的搜索结果将替换“查找结果 1”窗口中的内容。 此窗口将自动打开，以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 1”。

**查找结果 2** 窗口

如果选择此选项，当前的搜索结果将替换“查找结果 2”窗口中的内容。 此窗口将自动打开，以显示搜索结果。 若要手动打开此窗口，请从“视图”菜单中选择“其他窗口”，然后选择“查找结果 2”。

**只显示文件名**

如果选中此复选框，则“查找结果”窗口将列出所有包含搜索字符串的文件的完整名称和路径。 但是，结果不包含显示字符串的代码行。 此复选框仅可用于“在文件中查找”。

**全部替换后保持将已修改的文件打开**

如果选中，则所有替换过的文件都保持打开状态，以便您可以撤消操作或保存更改。 内存方面的制约可能会限制在替换操作之后可以保持打开的文件数。

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
