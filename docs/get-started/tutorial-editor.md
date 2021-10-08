---
title: 代码编辑器中的编辑功能简介
description: 了解如何使用 Visual Studio 中的代码编辑器向文件添加代码，以及如何编写代码、导航到代码和重构代码。
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: tutorial
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 7a82b65bb3d0c02c5c6240f414d23ca90a702b85
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128432189"
---
# <a name="learn-to-use-the-code-editor"></a>了解如何使用代码编辑器

在这个 10 分钟的 Visual Studio 代码编辑器简介中，我们会向文件添加代码，了解 Visual Studio 编写、导航和了解代码的简便方法。

::: moniker range="vs-2017"

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

> [!TIP]
> 如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

::: moniker range=">=vs-2022"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

本文假定你已熟悉编程语言。 如果不熟悉，则建议首先查看其中一个编程快速入门，如使用 [Python](../ide/quickstart-python.md) 或 [C#](../get-started/csharp/tutorial-aspnet-core.md) 创建 Web 应用，或使用 [Visual Basic](../ide/quickstart-visual-basic-console.md) 或 [C++](/cpp/get-started/tutorial-console-cpp) 创建控制台应用。

::: moniker range=">=vs-2022"

> [!TIP]
> 若要继续执行本文中的操作，请确保为 Visual Studio 选择了 C# 设置。 有关为集成开发环境 (IDE) 选择设置的信息，请参阅[选择环境设置](csharp/visual-studio-ide.md#select-environment-settings)。

::: moniker-end

## <a name="create-a-new-code-file"></a>创建新代码文件

先创建一个新文件并向其添加一些代码。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

1. 在菜单栏上的“文件”菜单中，选择“新建”>“文件”  。

1. 在“新建文件”对话框的“常规”类别中，选择“Visual C# 类”，然后选择“打开”   。

   编辑器中将打开主干为 C# 类的新文件。 （请注意，我们无需创建完整的 Visual Studio 项目来获取代码编辑器提供的某些益处，仅需一个代码文件即可！）

   ![Visual Studio 中 C# 代码文件的屏幕截图。](media/tutorial-editor.png)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。 按 Esc  或单击“开始”窗口中的“继续但无需代码”以打开开发环境。

1. 在菜单栏上的“文件”菜单中，选择“新建”>“文件”  。

1. 在“新建文件”对话框的“常规”类别中，选择“Visual C# 类”，然后选择“打开”   。

   编辑器中将打开主干为 C# 类的新文件。 （请注意，我们无需创建完整的 Visual Studio 项目来获取代码编辑器提供的某些益处，仅需一个代码文件即可！）

   ![Visual Studio 中 C# 代码文件的屏幕截图。](media/tutorial-editor.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。 选择 Esc 键或选择“开始”窗口中的“继续但无需代码”以打开开发环境。

1. 在菜单栏上的“文件”菜单中，选择“新建”>“文件”，或选择 Ctrl+N     键。

1. 在“新建文件”对话框的“常规”类别中，选择“Visual C# 类”，然后选择“打开”   。

   编辑器中将打开主干为 C# 类的新文件。

   :::image type="content" source="media/vs-2022/tutorial-editor.png" alt-text="Visual Studio 2022 中 C# 代码文件的屏幕截图。":::

::: moniker-end

## <a name="use-code-snippets"></a>使用代码片段

Visual Studio 提供了实用的代码片段，可用于快速方便地生成常用代码块。 [代码片段](../ide/code-snippets.md)可用于不同编程语言，包括 C#、Visual Basic 和 C++。

我们将 C# `void Main` 代码片段添加到文件。

::: moniker range="<=vs-2019"

1. 将光标停在文件中最后的结束括号 } 的上方，并键入字符 `svm`。 （`svm` 代表 `static void Main`；[Main()](/dotnet/csharp/programming-guide/main-and-command-args/) 方法是 C# 应用程序的入口点。）

   随即将出现一个弹出对话框，其中包含有关 `svm` 代码片段的信息。

   ![Visual Studio 中代码片段的 IntelliSense 弹出项的屏幕截图。](media/tutorial-intellisense-snippet.png)

1. 按 Tab 两次，插入代码片段。

   你会看到 `static void Main()` 方法签名被添加到文件。

对于不同编程语言，可用的代码片段不同。 依次选择“编辑” > “IntelliSense” > “插入代码片段”，然后选择语言的文件夹，即可查看该语言的可用代码片段  。 对于 C#，该列表如下所示：

![C# 代码片段列表的 IntelliSense 弹出项的屏幕截图。](media/tutorial-code-snippet-list.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 将光标停在文件中最后的结束括号 **`}`** 的上方，并键入字符 `svm`。

   随即将出现一个弹出对话框，其中包含有关 `svm` 代码片段的信息。

   :::image type="content" source="media/vs-2022/tutorial-intellisense-snippet.png" alt-text="Visual Studio 2022 中代码片段的 IntelliSense 弹出项的屏幕截图。":::

1. 选择 Tab 键两次，插入代码片段。

   你会看到 `static void Main()` 方法签名被添加到文件。 [Main()](/dotnet/csharp/programming-guide/main-and-command-args/) 方法是 C# 应用程序的入口点。

对于不同编程语言，可用的代码片段不同。 依次选择“编辑” > “IntelliSense” > “插入代码片段”，或选择 Ctrl+K、Ctrl+X 键，然后选择编程语言的文件夹，即可查看该语言的可用代码片段      。 对于 C#，代码片段列表如下所示：

:::image type="content" source="media/vs-2022/tutorial-code-snippet-list.png" alt-text="C# 代码片段列表的 IntelliSense 弹出项的屏幕截图。":::

::: moniker-end

该列表包含用于创建[类](/dotnet/csharp/fundamentals/types/classes)、[构造函数](/dotnet/csharp/programming-guide/classes-and-structs/constructors)、[for](/dotnet/csharp/language-reference/statements/iteration-statements#the-for-statement) 循环、[if](/dotnet/csharp/language-reference/statements/selection-statements#the-if-statement) 或 [switch](/dotnet/csharp/language-reference/statements/selection-statements#the-switch-statement) 语句等的代码片段。

## <a name="comment-out-code"></a>为代码添加注释

::: moniker range="<=vs-2019"

工具栏是 Visual Studio 菜单栏下的一行按钮，有助于提高编码效率。 例如，可以切换 IntelliSense 完成模式（[IntelliSense](../ide/using-intellisense.md) 是一种编码辅助工具，可显示匹配方法列表以及其他内容），增加或减少行缩进，或标注出不想编译的代码。 在本部分中，我们将标注出部分代码。

![Visual Studio 中“编辑器”工具栏的屏幕截图。](media/tutorial-editor-toolbar.png)

1. 将以下代码粘贴到 `Main()` 方法主体中。

    ```csharp
    // _words is a string array that we'll sort alphabetically
    string[] _words = {
        "the",
        "quick",
        "brown",
        "fox",
        "jumps"
    };

    string[] morewords = {
        "over",
        "the",
        "lazy",
        "dog"
    };

    IEnumerable<string> query = from word in _words
                                orderby word.Length
                                select word;
    ```

1. 我们现在没有使用 `morewords` 变量，但稍后可能会用到，所以我们不想彻底删除它。 那我们就来为这些行加上注释。 选择整个 `morewords` 定义直到结束分号，然后选择工具栏上的“为选定行添加注释”。 如果想要使用键盘，请按 Ctrl+K, Ctrl+C   。

   ![Visual Studio 中“编辑器”工具栏的“注释禁止”按钮的屏幕截图。](media/tutorial-comment-out.png)

   C# 注释字符 `//` 添加到了每个所选行的开始处，从而为代码添加注释。

::: moniker-end

::: moniker range=">=vs-2022"

文本编辑器工具栏是 Visual Studio 菜单栏下的一行按钮，有助于提高编码效率。 例如，可以切换到 [IntelliSense](../ide/using-intellisense.md) 完成模式、增加或减少缩进，或者注释掉不想编译的代码。

:::image type="content" source="media/vs-2022/tutorial-editor-toolbar.png" alt-text="Visual Studio 2022 中“文本编辑器”工具栏的屏幕截图。":::

让我们注释掉一些代码。

1. 将以下代码粘贴到 `Main()` 方法主体中。

    ```csharp
    // someWords is a string array.
    string[] someWords = {
        "the",
        "quick",
        "brown",
        "fox",
        "jumps"
    };

    string[] moreWords = {
        "over",
        "the",
        "lazy",
        "dog"
    };

    // Alphabetically sort the words.
    IEnumerable<string> query = from word in someWords
                                orderby word
                                select word;
    ```

1. 我们现在没有使用 `moreWords` 变量，但稍后可能会用到，所以我们不想删除它。 那我们就来注释掉这些行。 选择整个 `moreWords` 定义直到结束分号，然后选择文本编辑器工具栏上的“注释掉选定行”。 如果想要使用键盘，请选择 Ctrl+E、C  。

   :::image type="content" source="media/vs-2022/tutorial-comment-out.png" alt-text="Visual Studio 2022 中“文本编辑器”工具栏的“注释禁止”按钮的屏幕截图。":::

   C# 注释字符 `//` 添加到了每个所选行的开始处，从而为代码添加注释。

如果要注释掉行，可以选择它们，然后选择文本编辑器工具栏上的“注释掉所选行”按钮。 如果想要使用键盘，请选择 Ctrl+E、U  。

:::image type="content" source="media/vs-2022/tutorial-uncomment.png" alt-text="Visual Studio 2022 中“文本编辑器”工具栏的“注释禁止”按钮的屏幕截图。":::

::: moniker-end

## <a name="collapse-code-blocks"></a>折叠代码块

::: moniker range="<=vs-2019"

我们不想看到生成的 `Class1` 的空[构造函数](/dotnet/csharp/programming-guide/classes-and-structs/constructors)，所以为了让代码更整洁，我们将其折叠。 在构造函数第一行的边距中选择内部带有减号的小灰色框。 如果首选使用键盘，也可将光标置于构造函数代码中的任意位置，然后按 Ctrl+M、Ctrl+M   。

![Visual Studio 中“文本编辑器”工具栏的“大纲显示折叠”按钮的屏幕截图。](media/tutorial-collapse.png)

代码块折叠到第一行，后跟省略号 (`...`)。 若要再次展开代码块，请单击现在带有加号的相同灰色框，或者再次按 Ctrl+M，Ctrl+M   。 此功能被称为[大纲显示](../ide/outlining.md)，在折叠长方法或整个类时特别有用。

::: moniker-end

::: moniker range=">=vs-2022"

我们不想看到生成的 `Class1` 的空[构造函数](/dotnet/csharp/programming-guide/classes-and-structs/constructors)，所以为了让代码更整洁，我们将其折叠。 在构造函数第一行的边距中选择内部带有减号的小灰色框。 如果首选使用键盘，也可将光标置于构造函数代码中的任意位置，然后选择 Ctrl+M、Ctrl+M    键。

:::image type="content" source="media/vs-2022/tutorial-collapse.png" alt-text="Visual Studio 2022 中“文本编辑器”工具栏的“大纲显示折叠”按钮的屏幕截图。":::

代码块折叠到第一行，后跟省略号 (`...`)。 若要再次展开代码块，请选择现在带有加号的相同灰色框，或者再次选择 Ctrl+M，Ctrl+M   。 此功能被称为[大纲显示](../ide/outlining.md)，在折叠长方法或整个类时特别有用。

::: moniker-end

## <a name="view-symbol-definitions"></a>查看符号定义

::: moniker range="<=vs-2019"

通过 Visual Studio 编辑器可轻松查看类型、方法等的定义。一种方法是导航到包含定义的文件，例如通过选择“转到定义”，转到引用符号的任何位置。 使用“[速览定义](../ide/go-to-and-peek-definition.md#peek-definition)”速度更快，不会干扰你处理文件。 我们来快速查看一下 `string` 类型的定义。

1. 右键单击出现的任意 `string`，然后选择内容菜单上的“速览定义”。 或者，按 Alt+F12 。

   此时会出现一个弹出窗口，其中包含 `String` 类的定义。 可在弹出窗口中滚动，甚至还可从速览的代码中查看另一类型的定义。

   ![Visual Studio 中的“速览定义”窗口的屏幕截图。](media/tutorial-peek-definition.png)

1. 选择弹出窗口右上方的“x”小框，关闭“速览定义”窗口。

::: moniker-end

::: moniker range=">=vs-2022"

通过 Visual Studio 编辑器，可轻松查看类型、方法或变量的定义。 一种方法是转到包含定义的任何文件，例如通过选择“转到定义”或选择“F12”键，转到引用符号的任何位置 。 使用“[速览定义](../ide/go-to-and-peek-definition.md#peek-definition)”速度更快，不会干扰你处理代码。

我们来快速查看一下 `string` 类型的定义。

1. 右键单击出现的任意 `string`，然后选择内容菜单上的“速览定义”。 或者，选择 Alt+F12 键 。

   此时会出现一个弹出窗口，其中包含 `String` 类的定义。 可在弹出窗口中滚动，甚至还可从速览的代码中查看另一类型的定义。

   :::image type="content" source="media/vs-2022/tutorial-peek-definition.png" alt-text="Visual Studio 2022 中的“速览定义”窗口的屏幕截图。":::

1. 选择弹出窗口右上方的“x”小框，关闭“速览定义”窗口。

::: moniker-end

## <a name="use-intellisense-to-complete-words"></a>使用 IntelliSense 完成单词

::: moniker range="<=vs-2019"

编写代码时，[IntelliSense](../ide/using-intellisense.md) 是非常宝贵的资源。 它可显示某个类型的可用成员信息，或某个方法不同重载的参数详情。 还可用于完成单词，从而在输入大量字符后消除字符带来的歧义。 添加代码行，将有序字符串呈现到控制台窗口，这是程序输出的标准位置。

1. 在 `query` 变量下，开始键入以下代码：

   ```csharp
   foreach (string str in qu
   ```

   IntelliSense 会显示有关 `query` 符号的“快速信息”。

   ![Visual Studio 中 IntelliSense 文字自动完成弹出项的屏幕截图。](media/tutorial-intellisense-completion-list.png)

1. 若要使用 IntelliSense 文字自动完成功能插入单词 `query` 的剩余部分，请按 Tab。

1. 完成后，代码块如以下代码所示。 你甚至可以通过输入 `cw`，然后按 Tab 两次来生成 `Console.WriteLine` 代码，再次练习使用代码片段。

   ```csharp
   foreach (string str in query)
   {
      Console.WriteLine(str);
   }
   ```

::: moniker-end

::: moniker range=">=vs-2022"

编写代码时，[IntelliSense](../ide/using-intellisense.md) 是非常宝贵的资源。 它可显示某个类型的可用成员信息，或某个方法不同重载的参数详情。 还可用于完成单词，从而在输入大量字符后消除字符带来的歧义。

添加代码行，将有序字符串呈现到控制台窗口，这是程序输出的标准位置。

1. 在 `query` 变量下，开始键入以下代码：

   ```csharp
   foreach (string str in qu
   ```

   此时会看到一个 IntelliSense 弹出项，其中包含有关 `query` 符号的相关信息。

   :::image type="content" source="media/vs-2022/tutorial-intellisense-completion-list.png" alt-text="Visual Studio 2022 中 IntelliSense 文字自动完成弹出项的屏幕截图。":::

1. 若要使用 IntelliSense 文字自动完成插入单词 `query` 的剩余部分，请选择 Tab 键。

1. 完成后，代码块如以下代码所示。 你可以通过输入 `cw`，然后选择 Tab 两次来生成 `Console.WriteLine` 语句，从而进一步练习代码片段。

   ```csharp
   foreach (string str in query)
   {
      Console.WriteLine(str);
   }
   ```

::: moniker-end

## <a name="refactor-a-name"></a>重构名称

::: moniker range="<=vs-2019"

没有谁能一次就得到正确的代码，代码中可能必须要更改的一项内容是变量或方法的名称。 我们来试试 Visual Studio 的[重构](../ide/refactoring-in-visual-studio.md)功能，将 `_words` 变量重命名为 `words`。

1. 将光标置于 `_words` 变量的定义上，然后从右键菜单或上下文菜单中选择“重命名”，或按 Ctrl+R，Ctrl+R    。

   此时编辑器右上角会弹出一个“重命名”对话框。

1. 输入所需名称“words”。 请注意，查询中对 `words` 的引用也会自动重命名。 在按 Enter 前，请在“重命名”弹出框中选中“包含注释”复选框  。

   ![Visual Studio 中“重命名”对话框的屏幕截图。](media/tutorial-rename.png)

1. 按 **Enter**。

   出现的两处 `words` 均被重命名，代码注释中对 `words` 的引用也被重命名。

::: moniker-end

::: moniker range=">=vs-2022"

没有谁能一次就得到正确的代码，代码中可能必须要更改的一项内容是变量或方法的名称。 我们来试试 Visual Studio 的[重构](../ide/refactoring-in-visual-studio.md)功能，将 `someWords` 变量重命名为 `unsortedWords`。

1. 将光标置于 `someWords` 变量的定义上，然后从右键菜单或上下文菜单中选择“重命名”，或选择 F2 键。 

   此时编辑器右上角会出现一个“重命名”对话框。

   :::image type="content" source="media/vs-2022/tutorial-rename-start.png" alt-text="Visual Studio 2022 编辑器内“重命名”弹出项的屏幕截图。":::

1. 输入所需名称“unsortedWords”。 你会看到查询中对 `query` 赋值语句中 `unsortedWords` 的引用也会自动重命名。 请在“重命名”弹出框中选中“包含注释”复选框，然后选择 Enter 键或选择“应用”   。

   :::image type="content" source="media/vs-2022/tutorial-rename.png" alt-text="Visual Studio 2022 中“重命名”弹出框的屏幕截图。":::

1. 选择 Enter 键，或在“重命名组”对话框中选择“应用”。  

   代码中出现的两处 `someWords` 均被重命名，代码注释中的文本 `someWords` 也被重命名。

::: moniker-end

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [了解项目和解决方案](../get-started/tutorial-projects-solutions.md)

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)
- [导航代码](../ide/navigating-code.md)
- [大纲显示](../ide/outlining.md)
- [转到定义和速览定义](../ide/go-to-and-peek-definition.md)
- [重构](../ide/refactoring-in-visual-studio.md)
- [使用 IntelliSense](../ide/using-intellisense.md)
