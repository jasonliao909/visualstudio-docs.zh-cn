---
title: Visual Studio 中的 Python 教程步骤 2，编写和运行代码
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程的第 2 步，包括编辑代码和运行项目。
ms.date: 02/04/2022
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.custom: devdivchpfy22
ms.openlocfilehash: 1b7113db8659e9e4c34ed216fb068805e5fa580f
ms.sourcegitcommit: 00dcd28ca2f9940f3b7a79f2155bd1dc309c3c92
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2022
ms.locfileid: "138642776"
---
# <a name="step-2-write-and-run-code"></a>步骤 2：编写并运行代码

**上一步：[创建新的 Python 项目](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)**

虽然可以在解决方案资源管理器中管理项目文件，但处理文件内容（如源代码）通常还是在编辑器窗口进行。 编辑器在上下文上可以识别正在编辑的文件类型。 编辑器还根据文件扩展名 (识别编程语言，) 并提供适用于该语言的功能，例如使用 IntelliSense 进行语法着色和自动完成。

1. 创建新的"Python 应用程序"项目时，PythonApplication1.py 编辑器中打开名为 Visual Studio 文件。

1. 在编辑器中，开始键入`print("Hello, Visual Studio")`，并Visual Studio IntelliSense 如何显示自动完成选项。 下拉列表中加外边框的选项是按 Tab 键时使用的默认完成选项。 涉及到较长的语句或标识符时，最适合使用“完成”。

    ![IntelliSense 自动完成弹出窗口](media/vs-getting-started-python-04-IntelliSense1b.png)

1. IntelliSense 根据你使用的语句、调用的函数等显示不同的信息。 使用 `print` 函数时，在 `print` 后面键入 `(` 表示函数调用将显示该函数的完整使用情况信息。 IntelliSense 弹出窗口还用粗体显示当前参数（如此处所示的 **value**）：

    ![某函数的 IntelliSense 自动完成弹出窗口](media/vs-getting-started-python-05-IntelliSense2b.png)

1. 完成 语句，以便与以下代码匹配：

    ```python
    print("Hello, Visual Studio")
    ```

1. 注意语法着色如何区分 `print` 语句与 `"Hello Visual Studio"` 参数。 可以暂时删除字符串`"`上的最后一个 ，并注意Visual Studio语法错误的代码显示红色下划线。 最后，替换 `"` 以更正代码。

    ![IntelliSense 语法着色和错误突出显示](media/vs-getting-started-python-06-IntelliSense3b.png)

    > [!Tip]
    > 由于一个人的开发环境是件非常私人的事情，因此，Visual Studio 允许用户完全控制 Visual Studio 的外观和行为。 选择“工具” > “选项”菜单命令，浏览“环境”和“文本编辑器”选项卡下面的设置。 默认情况下，只能看到有限数量的选项;若要查看每种编程语言的所有选项，请选择 **对话框** 底部的"显示所有设置"。

1. 按 Ctrl+F5 或选择“调试” > “开始执行(不调试)”菜单项，运行到目前为止编写的代码。 如果代码中仍然存在错误，Visual Studio 会发出警告。

1. 运行程序时，控制台窗口将显示结果。 这类似于从命令行使用 *PythonApplication1.py Python 解释* 器。 按任意键关闭窗口并返回到Visual Studio编辑器。

    ![首次运行程序时的输出](media/vs-getting-started-python-07-output.png)

1. 除了完成语句和函数外，IntelliSense 还提供 Python `import` 和 `from` 语句的完成。 这些完成有助于轻松发现环境中可用的模块以及这些模块的成员。 在编辑器中，删除 `print` 行，开始键入 `import`。 键入空格时会显示模块列表：

    ![显示 import 语句的可用模块的 IntellSense](media/vs-getting-started-python-08-import1.png)

1. 通过键入或选择 `sys` 完成行。

1. 在下一行中，键入 `from` 再次查看模块列表：

    ![显示 from 语句的可用模块的 IntellSense](media/vs-getting-started-python-09-import2.png)

1. 选择或键入 `math`，然后继续键入一个空格和 `import`，将显示模块成员：

    ![显示模块成员的 IntellSense](media/vs-getting-started-python-10-import3.png)

1. 最后，导入 `sin`、 `cos`和 `radians` 成员，同时了解每个成员可用的自动完成。 完成后，代码应如下所示：

    ```python
    import sys
    from math import cos, radians
    ```

    > [!Tip]
    > 完成可处理键入时的子字符串，匹配单词的某些部分、单词开头的字母，甚至是跳过的字符。 请参阅[编辑代码 - 完成](editing-python-code-in-visual-studio.md#completions)，了解详细信息。

1. 再添加一小段代码以输出 360 度的余弦值：

    ```python
    for i in range(360):
        print(cos(radians(i)))
    ```

1. 使用 Ctrl+F5 或“调试” > “开始执行(不调试)”再次运行程序。 完成后，关闭输出窗口。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用交互式 REPL 窗口](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)

## <a name="go-deeper"></a>深入了解

- [编辑代码](editing-python-code-in-visual-studio.md)
- [格式代码](formatting-python-code.md)
- [重构代码](refactoring-python-code.md)
- [使用 PyLint](linting-python-code.md)
