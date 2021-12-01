---
title: 教程：调试 Visual Basic 代码
description: 了解 Visual Studio 调试器的功能以及如何启动调试器、逐步执行代码以及检查 Visual Basic 应用程序中的数据。
ms.custom: debug-experiment, vs-acquisition, get-started
ms.date: 09/14/2021
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- VB
helpviewer_keywords:
- debugger
ms.assetid: 62734c0d-a75a-4576-8f73-0e97c19280e1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cf02a169d775c2fb8391ee3c700f726c7462c660
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429533"
---
# <a name="tutorial-learn-to-debug-visual-basic-code-using-visual-studio"></a>教程：学习使用 Visual Studio 调试 Visual Basic 代码

本文通过分步演练介绍了 Visual Studio 调试器的功能。 如果需要更加深入地了解调试器功能，请参阅[初探调试器](../../debugger/debugger-feature-tour.md)。 当你调试应用时，通常意味着运行附带有调试器的应用程序  。 执行此操作时，调试器在运行过程中可提供许多方法让你查看代码的情况。 你可以逐步浏览代码、查看变量中存储的值、设置对变量的监视以查看值何时改变、检查代码的执行路径、查看代码分支是否正在运行等等。 如果这是你第一次尝试调试代码，可能需要在浏览本文之前阅读[零基础调试](../../debugger/debugging-absolute-beginners.md)。

虽然演示应用为 Visual Basic，但大多数功能都适用于 C#、C++、F#、Python、JavaScript 和 Visual Studio 支持的其他语言（F# 不支持“编辑并继续”。 F# 和 JavaScript 不支持“自动”窗口  ）。 屏幕截图为 Visual Basic。

在本教程中，你将：

> [!div class="checklist"]
> * 启动调试器并命中断点。
> * 了解在调试器中逐步执行代码的命令
> * 检查数据提示和调试器窗口中的变量
> * 检查调用堆栈

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"

必须安装 Visual Studio 2019 且具有“.NET Core 跨平台开发”工作负载  。

::: moniker-end
::: moniker range="vs-2017"

必须安装 Visual Studio 2017 且具有“.NET Core 跨平台开发”工作负载  。

::: moniker-end

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改”   。

::: moniker-end

::: moniker range=">=vs-2022"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 Visual Studio 安装程序启动。 选择“.NET 桌面开发”工作负载，然后选择“修改”   。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建一个 .NET Core 控制台应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

3. 在“新建项目”对话框左侧的窗格中，展开“Visual Basic”，然后选择“.NET Core”。 在中间窗格中，选择“控制台应用(.NET Core)”  。 然后将项目命名为 get-started-debugging  。

     如果看不到“控制台应用(.NET Core)”  项目模板，请选择“新建项目”  对话框左侧窗格中的“打开 Visual Studio 安装程序”  链接。

     Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

   如果开始窗口未打开，请选择“文件”>“开始窗口”   。

1. 在“开始”窗口上，选择“创建新项目”  。

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”。 接下来，从“语言”列表中选择 Visual Basic，然后从“平台”列表中选择“Windows”。 

   应用语言和平台筛选器之后，对 .NET Core 选择“控制台应用”模板，然后选择“下一步” 。

   ![显示“创建新项目”窗口的屏幕截图，其中在搜索框中输入了“控制台”，并为“语言”和“平台”筛选器分别选择了“Visual Basic”和“Windows”。 已选择“控制台应用程序”项目模板。](../visual-basic/media/vs-2019/get-started-create-console-project.png)

   > [!NOTE]
   > 如果未看到“控制台应用”模板，则可以通过“创建新项目”窗口安装该模板   。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“get-started-debugging”。 然后，选择“下一步”。

1. 选择建议的目标框架 (.NET Core 3.1) 或 .NET 5，然后选择“创建”。

   此时，Visual Studio 将打开新项目。
   
::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

   如果开始窗口未打开，请选择“文件”>“开始窗口”   。

1. 在“开始”窗口上，选择“创建新项目”  。

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”。 接下来，从“语言”列表中选择 Visual Basic，然后从“平台”列表中选择“Windows”。 

   应用语言和平台筛选器之后，对 .NET Core 选择“控制台应用程序”模板，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/get-started-create-console-project.png" alt-text="显示“创建新项目”窗口的屏幕截图，其中在搜索框中输入了“控制台”，并为“语言”和“平台”筛选器分别选择了“Visual Basic”和“Windows”。已选择了“控制台应用程序”模板。":::

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，则可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。 然后在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“get-started-debugging”。 然后，选择“下一步”。

1. 在“其他信息”窗口中，确保建议的目标框架为“(.NET 6.0)”，然后选择“创建” 。

   此时，Visual Studio 将打开新项目。
   
::: moniker-end

## <a name="create-the-application"></a>创建应用程序

1. 在 Program.cs 中，使用以下代码替换所有默认代码：

    ```vb
    Imports System

    Class ArrayExample
        Public Shared Sub Main()
            Dim letters As Char() = {"f"c, "r"c, "e"c, "d"c, " "c, "s"c, "m"c, "i"c, "t"c, "h"c}
            Dim name As String = ""
            Dim a As Integer() = New Integer(9) {}

            For i As Integer = 0 To letters.Length - 1
                name += letters(i)
                a(i) = i + 1
                SendMessage(name, a(i))
            Next

            Console.ReadKey()
        End Sub

        Private Shared Sub SendMessage(ByVal name As String, ByVal msg As Integer)
            Console.WriteLine("Hello, " & name & "! Count to " & msg)
        End Sub
    End Class
    ```

## <a name="start-the-debugger"></a>启动调试器！

::: moniker range="<=vs-2019"

1. 按 F5（“调试”>“开始调试”）或调试工具栏中的“开始调试”按钮 :::image type="icon" source="../../debugger/media/dbg-tour-start-debugging.png":::  。

     通过 **F5** 启动应用时，调试器会附加到应用进程，但现在我们还未执行任何特殊操作来检查代码。 因此应用只会加载，控制台输出如你所见。

    ```cmd
    Hello, f! Count to 1
    Hello, fr! Count to 2
    Hello, fre! Count to 3
    Hello, fred! Count to 4
    Hello, fred ! Count to 5
    Hello, fred s! Count to 6
    Hello, fred sm! Count to 7
    Hello, fred smi! Count to 8
    Hello, fred smit! Count to 9
    Hello, fred smith! Count to 10
    ```

     在本教程中，我们将使用调试器仔细查看此应用，并查看调试器功能。

2. 按红色的停止按钮 :::image type="icon" source="../../debugger/media/dbg-tour-stop-debugging.png"::: (Shift+F5) 停止调试器 。

3. 在控制台窗口中，按某个键来关闭控制台窗口。

::: moniker-end

::: moniker range=">=vs-2022"

1. 按 F5（“调试”>“开始调试”），或在调试工具栏中选择绿色的“开始调试”按钮  。

    :::image type="content" source="media/vs-2022/debug-toolbar-start-button.png" alt-text="显示调试工具栏的屏幕截图，其中突出显示了绿色的“开始调试”按钮。":::

    通过 **F5** 启动应用时，调试器会附加到应用进程，但现在我们还未执行任何特殊操作来检查代码。 因此应用只会加载，控制台输出如你所见。

    ```cmd
    Hello, f! Count to 1
    Hello, fr! Count to 2
    Hello, fre! Count to 3
    Hello, fred! Count to 4
    Hello, fred ! Count to 5
    Hello, fred s! Count to 6
    Hello, fred sm! Count to 7
    Hello, fred smi! Count to 8
    Hello, fred smit! Count to 9
    Hello, fred smith! Count to 10
    ```

    在本教程中，我们将使用调试器仔细查看此应用，并查看调试器功能。

2. 按 Shift+F5 停止调试器，或在调试工具栏中选择红色的“停止调试”按钮  。

    :::image type="content" source="media/vs-2022/debug-toolbar-stop-button.png" alt-text="显示调试工具栏的屏幕截图，其中突出显示了红色的“停止调试”按钮。":::

3. 在控制台窗口中，按某个键来关闭控制台窗口。

::: moniker-end
## <a name="set-a-breakpoint-and-start-the-debugger"></a>设置断点并启动调试器

::: moniker range="<=vs-2019"

1. 在 `Main` 函数的 `For` 循环中，通过单击以下代码行的左边距来设置断点：

    `name += letters(i)`

    设置断点的位置会出现一个红圈 :::image type="icon" source="../../debugger/media/dbg-breakpoint.png":::。

    断点是可靠调试的最基本和最重要的功能之一。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

2. 按 F5 或“开始调试”按钮 :::image type="icon" source="../../debugger/media/dbg-tour-start-debugging.png":::，应用随即启动，调试器将运行到在其中设置了断点的代码行 。

    ![显示 Visual Studio 代码编辑器窗口的屏幕截图，其中，执行已在断点处停止。](../visual-basic/media/get-started-hit-breakpoint-vb.png)

    黄色箭头表示调试器暂停处的语句，它还在同一点上暂停应用执行（此语句尚未执行）。

     如果应用尚未运行，则按 F5 会启动调试器并在第一个断点处停止  。 否则，按 F5 将继续运行应用至下一个断点  。

    当你知道要详细检查的代码行或代码段时，断点功能非常有用。 有关可设置的不同类型断点（如条件断点）的信息，请参阅[使用断点](../../debugger/using-breakpoints.md)。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在 `Main` 函数的 `For` 循环中，通过单击以下代码行的左边距来设置断点：

    `name += letters(i)`

    设置断点的位置会出现一个红色圆圈。

    断点是可靠调试的最基本和最重要的功能之一。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

2. 按 F5（“调试”>“开始调试”）或调试工具栏中的“开始调试”按钮，应用随即启动，调试器将运行到在其中设置了断点的代码行  。

    :::image type="content" source="media/vs-2022/get-started-hit-breakpoint-vb.png" alt-text="显示 Visual Studio 代码编辑器窗口的屏幕截图，其中，执行已在断点处停止。":::

    黄色箭头表示调试器暂停处的语句，它还在同一点上暂停应用执行（此语句尚未执行）。

    如果应用尚未运行，则按 F5 会启动调试器并在第一个断点处停止  。 否则，按 F5 将继续运行应用至下一个断点  。

    当你知道要详细检查的代码行或代码段时，断点功能非常有用。 有关可设置的不同类型断点（如条件断点）的信息，请参阅[使用断点](../../debugger/using-breakpoints.md)。

::: moniker-end
## <a name="navigate-code-in-the-debugger-using-step-commands"></a>使用单步执行命令在调试器中导航代码

::: moniker range="<=vs-2019"

大多数情况下，我们使用键盘快捷方式，因为这是在调试器中快速执行应用的好方法（括号中显示了等效的命令，如菜单命令）。

1. 在 `Main` 方法中的 `For` 循环中暂停时，按两次 F11（或选择“调试”>“单步执行”）前进到 `SendMessage` 方法调用 。

     按两次 F11 后，应位于以下代码行：

     `SendMessage(name, a(i))`

1. 再按一次 F11 单步执行到 `SendMessage` 方法  。

     黄色指针会前进到 `SendMessage` 方法。

     ![显示在单步执行“SendMessage”方法后 Visual Studio 代码编辑器中的调试会话的屏幕截图，其中，执行已暂停。](../visual-basic/media/get-started-f11-vb.png)

     F11 是“单步执行”命令，每按一次，应用就执行下一个语句  。 F11 是一种以最详尽方式检查执行流的好方法。 （为了更快地浏览代码，我们还向你展示一些其他选项。）默认情况下，调试器会跳过非用户代码（如果需要更多详细信息，请参阅[仅我的代码](../../debugger/just-my-code.md)）。

     假设你已完成了对 `SendMessage` 方法的检查，并且希望退出该方法但保持位于调试器中。 可使用“单步跳出”命令执行此操作  。

1. 按 Shift+F11（或选择“调试”>“单步跳出”）  。

     此命令将恢复应用执行（并使调试器前进），直到当前方法或函数返回。

     你应当回到 `Main` 方法的 `For` 循环，在 `SendMessage` 方法调用处暂停。

1. 多按几次 F11，直到再次返回到 `SendMessage` 方法调用。

1. 在方法调用处暂停时，按一次 F10（或选择“调试”>“单步跳过”）。

     ![显示在单步跳过“SendMessage”方法调用后 Visual Studio 代码编辑器中的调试会话的屏幕截图，其中，执行已暂停。](../visual-basic/media/get-started-step-over-vb.png)

     请注意，这次调试器不会单步执行 `SendMessage` 方法。 按 F10 将使调试器前进，但不会单步执行应用代码中的函数或方法（代码仍将执行）。 通过在进行 `SendMessage` 方法调用时按“F10”（而不是“F11”），我们跳过了 `SendMessage` 的实现代码（我们现在可能对此不感兴趣）。 有关在代码中进行移动的不同方法的详细信息，请参阅[浏览调试器中的代码](../../debugger/navigating-through-code-with-the-debugger.md)。

::: moniker-end

::: moniker range=">=vs-2022"

在本文中，我们使用了键盘快捷方式，因为这是在调试器中快速执行应用的好方法（括号中显示了等效的命令，如菜单命令）。

1. 在 `Main` 方法中的 `For` 循环中暂停时，按两次 F11（或选择“调试”>“单步执行”）前进到 `SendMessage` 方法调用 。

     按两次 F11 后，应位于以下代码行：

     `SendMessage(name, a(i))`

1. 再按一次 F11 单步执行到 `SendMessage` 方法  。

     黄色指针会前进到 `SendMessage` 方法。

    :::image type="content" source="media/vs-2022/get-started-f11-vb.png" alt-text="显示在单步执行“SendMessage”方法后 Visual Studio 代码编辑器中的调试会话的屏幕截图，其中，执行已暂停。":::

     F11 是“单步执行”命令，每按一次，应用就执行下一个语句 。 F11 是一种以最详尽方式检查执行流的好方法。 （为了更快地浏览代码，我们还向你展示一些其他选项。）默认情况下，调试器会跳过非用户代码（如果需要更多详细信息，请参阅[仅我的代码](../../debugger/just-my-code.md)）。

     假设你已完成了对 `SendMessage` 方法的检查，并且希望退出该方法但保持位于调试器中。 可使用“单步跳出”命令执行此操作  。

1. 按 Shift+F11（或选择“调试”>“单步跳出”）  。

     此命令将恢复应用执行（并使调试器前进），直到当前方法或函数返回。

     你应当回到 `Main` 方法的 `For` 循环，在 `SendMessage` 方法调用处暂停。

1. 多按几次 F11，直到再次返回到 `SendMessage` 方法调用。

1. 在方法调用处暂停时，按一次 F10（或选择“调试”>“单步跳过”）。

    :::image type="content" source="media/vs-2022/get-started-step-over-vb.png" alt-text="显示在单步跳过“SendMessage”方法调用后 Visual Studio 代码编辑器中的调试会话的屏幕截图，其中，执行已暂停。":::

     请注意，这次调试器不会单步执行 `SendMessage` 方法。 按 F10 将使调试器前进，但不会单步执行应用代码中的函数或方法（代码仍将执行）。 通过在进行 `SendMessage` 方法调用时按“F10”（而不是“F11”），我们跳过了 `SendMessage` 的实现代码（我们现在可能对此不感兴趣）。 有关在代码中进行移动的不同方法的详细信息，请参阅[浏览调试器中的代码](../../debugger/navigating-through-code-with-the-debugger.md)。

::: moniker-end

## <a name="navigate-code-using-run-to-click"></a>使用“运行时单击”导航代码

::: moniker range="<=vs-2019"

1. 按 F5 再次前进到断点  。

1. 在代码编辑器中向下滚动，并将鼠标悬停在 `SendMessage` 方法中的 `Console.WriteLine` 方法上，直到左侧出现绿色的“运行到单击处”按钮 :::image type="icon" source="../../debugger/media/dbg-tour-run-to-click.png":::。 按钮的工具提示显示“将执行运行到此处”。

   ![显示“运行到单击处”按钮的屏幕截图，其中代码编辑器窗口左侧突出显示了工具提示。](../visual-basic/media/get-started-run-to-click-vb.png)

   > [!NOTE]
   > “运行时单击”是 [!include[vs_dev15](../../misc/includes/vs_dev15_md.md)] 中的新增按钮  。 （如果未看到绿色箭头按钮，请在此示例中改为使用 F11 以使调试器前进到正确的位置。  ）

2. 单击“运行到单击处”按钮 :::image type="icon" source="../../debugger/media/dbg-tour-run-to-click.png":::。

    调试器会前进到 `Console.WriteLine` 方法。

    使用此按钮类似于设置临时断点。 “运行时单击”对于快速到达应用代码的可见区域十分方便（你可在任何打开的文件中单击）  。

::: moniker-end

::: moniker range=">=vs-2022"

1. 按 F5 再次前进到断点  。

1. 在代码编辑器中向下滚动，并将鼠标悬停在 `SendMessage` 方法中的 `Console.WriteLine` 方法上，直到左侧出现绿色的“运行到单击处”按钮。 按钮的工具提示显示“将执行运行到此处”。

   :::image type="content" source="media/vs-2022/get-started-run-to-click-vb.png" alt-text="显示“运行到单击处”按钮的屏幕截图，其中代码编辑器窗口左侧突出显示了工具提示。":::

2. 选择“运行到单击处”按钮。

    调试器会前进到 `Console.WriteLine` 方法。

    使用此按钮类似于设置临时断点。 “运行时单击”对于快速到达应用代码的可见区域十分方便（你可在任何打开的文件中单击）  。

::: moniker-end

## <a name="restart-your-app-quickly"></a>快速重启应用

::: moniker range="<=vs-2019"

在调试工具栏中单击“重启”按钮 :::image type="icon" source="../../debugger/media/dbg-tour-restart.png"::: (Ctrl+Shift+F5)   。

当你按下“重启”时，与停止应用并重启调试器相比，它节省了时间  。 调试器在执行代码命中的第一个断点处暂停。

调试器再次在你之前在 `For` 循环上设置的断点处停止。

::: moniker-end

::: moniker range=">=vs-2022"

若要重启应用，请按 Ctrl + Shift + F5 组合键，与停止应用并重启调试器相比，这样可以节省时间  。 调试器在执行代码命中的第一个断点处暂停。

调试器再次在你之前在 `For` 循环上设置的断点处停止。

::: moniker-end

## <a name="inspect-variables-with-data-tips"></a>使用数据提示检查变量

::: moniker range="<=vs-2019"

允许你检查变量的功能是调试器最有用的功能之一，并且有不同的方法来执行此操作。 通常，当尝试调试问题时，你试图找出变量是否存储了你期望它们在特定时间具有的值。

1. 在暂停于 `name += letters[i]` 语句时，将鼠标悬停在 `letters` 变量上，此时你会看到其默认值，即数组中第一个元素的值 `"f"c`。

1. 接下来，将鼠标悬停在 `name` 变量上，会看到其当前值为空字符串。

1. 多按几次 F5（或“调试”>“继续”），通过 `For` 循环执行多次循环访问，再次在断点处暂停，每次都将鼠标悬停在 `name` 变量上以检查其值  。

     ![显示已在代码编辑器中停止调试执行的屏幕截图，其中突出显示了“name”变量，数据提示显示值为“fre”。](../visual-basic/media/get-started-data-tip-vb.png)

     变量的值随 `For` 循环的每次迭代而更改，显示的值依次为 `f`、`fr`、`fre`，依此类推。

     通常情况下，在调试时，需要快速检查变量的属性值，以查看它们是否存储了你希望它们存储的值，可根据数据提示执行此操作。

::: moniker-end

::: moniker range=">=vs-2022"

允许你检查变量的功能是调试器最有用的功能之一，并且有不同的方法来执行此操作。 通常，当尝试调试问题时，你试图找出变量是否存储了你期望它们在特定时间具有的值。

1. 在暂停于 `name += letters[i]` 语句时，将鼠标悬停在 `letters` 变量上，此时你会看到其默认值，即数组中第一个元素的值 `"f"c`。

1. 接下来，将鼠标悬停在 `name` 变量上，会看到其当前值为空字符串。

1. 多按几次 F5（或“调试”>“继续”），通过 `For` 循环执行多次循环访问，再次在断点处暂停，每次都将鼠标悬停在 `name` 变量上以检查其值  。

     :::image type="content" source="media/vs-2022/get-started-data-tip-vb.png" alt-text="显示已在代码编辑器中停止调试执行的屏幕截图，其中突出显示了“name”变量，数据提示显示值为“fre”。":::

     变量的值随 `For` 循环的每次迭代而更改，显示的值依次为 `f`、`fr`、`fre`，依此类推。

     通常情况下，在调试时，需要快速检查变量的属性值，以查看它们是否存储了你希望它们存储的值，可根据数据提示执行此操作。

::: moniker-end

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>使用“自动”和“局部变量”窗口检查变量

::: moniker range="<=vs-2019"

1. 查看代码编辑器底部的“自动”窗口  。

    如果该窗口已关闭，请在调试器中处于暂停状态时，选择“调试”>“窗口”>“自动变量”将其打开  。

    在“自动”窗口中，可看到变量及其当前值  。 “自动”窗口显示当前行或前一行使用的所有变量（检查文档中特定于语言的行为）  。

1. 接下来，我们来看看“自动”窗口旁边的选项卡中的“局部变量”窗口   。

1. 展开 `letters` 变量以显示其包含的元素。

     ![显示“局部变量”窗口的屏幕截图，其中展开了“letters”变量以显示它包含的元素的值和类型。](../visual-basic/media/get-started-locals-window-vb.png)

    “局部变量”窗口显示当前[作用域](https://www.wikipedia.org/wiki/Scope_(computer_science))中的变量，即当前执行上下文  。

::: moniker-end

::: moniker range=">=vs-2022"

1. 查看代码编辑器底部的“自动”窗口  。

    如果该窗口已关闭，请在调试器中处于暂停状态时，选择“调试”>“窗口”>“自动变量”将其打开  。

    在“自动”窗口中，可看到变量及其当前值  。 “自动”窗口显示当前行或前一行使用的所有变量（检查文档中特定于语言的行为）  。

1. 接下来，我们来看看“自动”窗口旁边的选项卡中的“局部变量”窗口   。

1. 展开 `letters` 变量以显示其包含的元素。

    :::image type="content" source="media/vs-2022/get-started-locals-window-vb.png" alt-text="显示“局部变量”窗口的屏幕截图，其中展开了“letters”变量以显示它包含的元素的值和类型。":::

    “局部变量”窗口显示当前[作用域](https://www.wikipedia.org/wiki/Scope_(computer_science))中的变量，即当前执行上下文  。

::: moniker-end

## <a name="set-a-watch"></a>设置监视

1. 在主代码编辑器窗口中，右键单击 `name` 变量，然后选择“添加监视”  。

    “监视”窗口将在代码编辑器的底部打开  。 可使用“监视”窗口指定要关注的变量（或表达式）  。

    现在，你在 `name` 变量上设置好了监视，当你在调试器中移动时，可看到其值发生变化。 与其他变量窗口不同，“监视”窗口始终显示你正在监视的变量（当超出作用域时，它们会变灰）  。

## <a name="examine-the-call-stack"></a>检查调用堆栈

::: moniker range="<=vs-2019"

1. 在 `For` 循环中暂停时，单击“调用堆栈”窗口，默认情况下，该窗口在右下方窗格中打开  。

    如果该窗口已关闭，请在调试器中处于暂停状态时，选择“调试”>“窗口”>“调用堆栈”将其打开  。

2. 单击多次 F11，直至看到调试器在 `SendMessage` 方法中暂停  。 查看“调用堆栈”窗口  。

    ![显示 Visual Studio“调用堆栈”窗口的屏幕截图，顶部行中突出显示了 SendMessage 方法调用。](../visual-basic/media/get-started-call-stack-vb.png)

    “调用堆栈”窗口显示方法和函数被调用的顺序  。 最上面一行显示当前函数（此应用中的 `SendMessage` 方法）。 第二行显示 `SendMessage` 是从 `Main` 方法调用的，依此类推。

   > [!NOTE]
   > “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图  。

    调用堆栈是检查和理解应用执行流的好方法。

    可双击代码行来查看该源代码，这也会更改调试器正在检查的当前作用域。 此操作不会使调试器前进。

    还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作  。 例如，你可将断点插入到指定的函数中，使用“运行到光标处”推进调试器，然后检查源代码  。 有关详细信息，请参阅[如何：检查调用堆栈](../../debugger/how-to-use-the-call-stack-window.md)。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在 `For` 循环中暂停时，单击“调用堆栈”窗口，默认情况下，该窗口会在右下方窗格中打开。

    如果该窗口已关闭，请在调试器中处于暂停状态时，选择“调试”>“窗口”>“调用堆栈”将其打开  。

2. 单击多次 F11，直至看到调试器在 `SendMessage` 方法中暂停  。 查看“调用堆栈”窗口  。

    :::image type="content" source="media/vs-2022/get-started-call-stack-vb.png" alt-text="显示 Visual Studio“调用堆栈”窗口的屏幕截图，顶部行中突出显示了 SendMessage 方法调用。":::

    “调用堆栈”窗口显示方法和函数被调用的顺序  。 最上面一行显示当前函数（此应用中的 `SendMessage` 方法）。 第二行显示 `SendMessage` 是从 `Main` 方法调用的，依此类推。

   > [!NOTE]
   > “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图  。

    调用堆栈是检查和理解应用执行流的好方法。

    可双击代码行来查看该源代码，这也会更改调试器正在检查的当前作用域。 此操作不会使调试器前进。

    还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作  。 例如，你可将断点插入到指定的函数中，使用“运行到光标处”推进调试器，然后检查源代码  。 有关详细信息，请参阅[如何：检查调用堆栈](../../debugger/how-to-use-the-call-stack-window.md)。

::: moniker-end

## <a name="change-the-execution-flow"></a>更改执行流

1. 按两次 F11 以运行 `Console.WriteLine` 方法  。

1. 在 `SendMessage` 方法调用中暂停调试器后，使用鼠标抓取左侧的黄色箭头（执行指针），将其向上移动一行，返回到 `Console.WriteLine`。

1. 按下 F11  。

    调试器将重新运行 `Console.WriteLine` 方法（你会在控制台窗口输出中看到）。

    通过更改执行流，你可以进行测试不同代码执行路径或重新运行代码等操作，而无需重启调试器。

    > [!WARNING]
    > 通常你需要小心使用此功能，工具提示中会出现警告。 你也可能会看到其他警告。 移动指针无法将应用程序还原到更早的应用状态。

1. 按 F5 继续运行应用  。

    恭喜你完成本教程！

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解了如何启动调试器、逐步执行代码以及检查变量。 你可能会希望更深入地了解调试器功能以及查看指向更多信息的链接。

> [!div class="nextstepaction"]
> [初探调试器](../../debugger/debugger-feature-tour.md)
