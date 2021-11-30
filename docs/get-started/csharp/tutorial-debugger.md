---
title: 教程：调试 C# 代码
description: 了解 Visual Studio 调试器的功能，以及如何启动调试器、单步调试代码并检查 C# 应用程序中的数据。
ms.custom: debug-experiment, vs-acquisition, get-started
ms.date: 09/14/2020
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- CSharp
helpviewer_keywords:
- debugger
ms.assetid: 62734c0d-a75a-4576-8f73-0e97c19280e1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b872043a5e8b200f6f5678857aa1c4e67c53945b
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133257044"
---
# <a name="tutorial-learn-to-debug-c-code-using-visual-studio"></a>教程：了解如何使用 Visual Studio 调试 C# 代码

本文通过分步演练介绍了 Visual Studio 调试器的功能。 如果需要更加深入地了解调试器功能，请参阅[初探调试器](../../debugger/debugger-feature-tour.md)。 当你调试应用时，通常意味着运行附带有调试器的应用程序  。 执行此操作时，调试器在运行过程中可提供许多方法让你查看代码的情况。 你可以逐步浏览代码、查看变量中存储的值、设置对变量的监视以查看值何时改变、检查代码的执行路径、查看代码分支是否正在运行等等。 如果这是你第一次尝试调试代码，可能需要在浏览本文之前阅读[零基础调试](../../debugger/debugging-absolute-beginners.md)。

虽然演示应用为 C#，但大多数功能都适用于 C++、Visual Basic、F#、Python、JavaScript 和 Visual Studio 支持的其他语言（F# 不支持“编辑并继续”。 F# 和 JavaScript 不支持“自动”窗口  ）。 屏幕截图为 C#。

在本教程中，你将：

> [!div class="checklist"]
> * 启动调试器并命中断点。
> * 了解在调试器中逐步执行代码的命令
> * 检查数据提示和调试器窗口中的变量
> * 检查调用堆栈

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2022"

须安装 Visual Studio 2022 且具有“.NET 桌面开发”工作负载。

::: moniker-end

::: moniker range="vs-2019"

必须安装 Visual Studio 2019 且具有“.NET Core 跨平台开发”工作负载  。

::: moniker-end

::: moniker range="vs-2017"

必须安装 Visual Studio 2017 且具有“.NET Core 跨平台开发”工作负载  。

::: moniker-end

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

::: moniker range="<=vs-2019"

如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改”   。

::: moniker-end

::: moniker range=">=vs-2022"

如果你已有 Visual Studio 但未安装“.NET 桌面开发”工作负载，请转到“工具” > “获取工具和功能...”，随即会启动 Visual Studio 安装程序  。 在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载，然后选择“修改” 。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建一个 .NET Core 控制台应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

1. 在“新建项目”  对话框的左窗格中，展开“C#”  ，然后选择“.NET Core”  。 在中间窗格中，选择“控制台应用(.NET Core)”  。 然后将项目命名为 get-started-debugging  。

     如果看不到“控制台应用(.NET Core)”  项目模板，请选择“新建项目”  对话框左侧窗格中的“打开 Visual Studio 安装程序”  链接。

     Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

   如果开始窗口未打开，请选择“文件”>“开始窗口”   。

1. 在“开始”窗口上，选择“创建新项目”  。

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择 C#，然后从“平台”列表中选择 Windows 。 

   应用语言和平台筛选器之后，对 .NET Core 选择“控制台应用程序”模板，然后选择“下一步” 。

   ![控制台应用的 C# 模板的屏幕截图。](../csharp/media/vs-2019/get-started-create-console-project.png)

   > [!NOTE]
   > 如果未看到“控制台应用”模板，则可以通过“创建新项目”窗口安装该模板   。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“GetStartedDebugging”    。 然后，选择“下一步”。

1. 选择 "推荐的目标框架" ( ".NET Core 3.1 (长期支持) ) 或 .NET 5.0 (" 当前) "，然后选择" **创建**"。

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio。

   如果“开始”窗口未打开，请选择“文件”>“启动窗口” 。

1. 在“开始”窗口上，选择“创建新项目”  。

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择 C#，然后从“平台”列表中选择 Windows 。 

   应用语言和平台筛选器之后，选择“控制台应用程序”模板，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/get-started-create-console-project.png" alt-text="Visual Studio 2022 的“创建新项目”窗口中“控制台应用程序”模板的屏幕截图。":::

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。 然后在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“GetStartedDebugging”    。 然后，选择“下一步”。

1. 在 "**附加信息**" 窗口中，确保在 "**框架**" 下拉菜单中选择 " **.net 6.0 (长期支持")** ，然后选择 "**创建**"。

    此时，Visual Studio 将打开新项目。

::: moniker-end

## <a name="create-the-application"></a>创建应用程序

在 Program.cs 中，将所有默认代码替换为以下代码：

```csharp
using System;

class ArrayExample
{
    static void Main()
    {
        char[] letters = { 'f', 'r', 'e', 'd', ' ', 's', 'm', 'i', 't', 'h'};
        string name = "";
        int[] a = new int[10];
        for (int i = 0; i < letters.Length; i++)
        {
            name += letters[i];
            a[i] = i + 1;
            SendMessage(name, a[i]);
        }
        Console.ReadKey();
    }

    static void SendMessage(string name, int msg)
    {
        Console.WriteLine("Hello, " + name + "! Count to " + msg);
    }
}
```

## <a name="start-the-debugger"></a>启动调试器！

::: moniker range="<=vs-2019"

1. 按 F5（“调试”>“开始调试”），或者按“开始调试”按钮 ![“开始调试”按钮的插图。](../../debugger/media/dbg-tour-start-debugging.png "开始调试")   （在“调试”工具栏中）。

     通过 **F5** 启动应用时，调试器会附加到应用进程，但现在我们还未执行任何特殊操作来检查代码。 因此应用就会加载，并且你会看到此控制台输出。

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

1. 按红色的停止按钮 ![“停止调试”按钮的插图。](../../debugger/media/dbg-tour-stop-debugging.png "停止调试") (Shift + F5) 停止调试器 。

1. 在控制台窗口中，按某个键来关闭控制台窗口。

::: moniker-end

::: moniker range=">=vs-2022"

此处我们主要使用的是键盘快捷方式，因为这样可以快速执行调试器命令。 等效的命令（例如工具栏或菜单命令）也会注明。

1. 若要启动调试器，请按 F5，或者在“标准”工具栏中选择“调试目标”按钮，或者在“调试”工具栏中选择“开始调试”按钮，或者从菜单栏中选择“调试”>“开始调试”    。

    :::image type="content" source="media/vs-2022/dbg-tour-start-debugging.png" alt-text="Visual Studio 2022 的“标准”工具栏中“调试目标”按钮的屏幕截图。":::

    按 F5 会启动应用，并且调试器会附加到应用进程。 由于我们尚未执行任何特殊操作来检查代码，因此应用将一直运行到完成为止，并且你会看到控制台输出。

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

1. 若要停止调试器，请按 Shift+F5，或者在“调试”工具栏中选择“停止调试”按钮，或者从菜单栏中选择“调试”>“停止调试”   。

    :::image type="content" source="media/vs-2022/dbg-tour-stop-debugging.png" alt-text="Visual Studio 2022 的“调试”工具栏中“停止调试”按钮的屏幕截图。":::

1. 在控制台窗口中，按任意键关闭控制台窗口。

::: moniker-end

## <a name="set-a-breakpoint-and-start-the-debugger"></a>设置断点并启动调试器

::: moniker range="<=vs-2019"

1. 在 `Main` 函数的 `for` 循环中，通过单击以下代码行的左边距来设置断点：

    `name += letters[i];`

    一个红圈 ![断点的插图。](../../debugger/media/dbg-breakpoint.png "断点") 会出现在设置断点的位置。

    断点是可靠调试的最基本和最重要的功能之一。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

1. 按 F5 或“开始调试”按钮 ![“开始调试”按钮的屏幕截图。](../../debugger/media/dbg-tour-start-debugging.png "开始调试")，应用随即启动，调试器将运行到在其中设置了断点的代码行 。

    ![设置并命中断点](../csharp/media/get-started-set-breakpoint.gif)

    黄色箭头表示调试器暂停处的语句，它还在同一点上暂停应用执行（此语句尚未执行）。

     如果应用尚未运行，则按 F5 会启动调试器并在第一个断点处停止  。 否则，按 F5 将继续运行应用至下一个断点  。

    当你知道要详细检查的代码行或代码段时，断点功能非常有用。 有关可设置的不同类型断点（如条件断点）的信息，请参阅[使用断点](../../debugger/using-breakpoints.md)。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在 `Main` 函数的 `for` 循环中，通过单击以下代码行的左边距来设置断点：

    `name += letters[i];`

    设置断点的位置会出现一个红色圆圈。

    :::image type="content" source="media/vs-2022/dbg-tour-breakpoint.png" alt-text="Visual Studio 2022 中的断点的屏幕截图。"::: 

    断点是执行可靠调试所不可或缺的一项功能。 你可以设置断点，以便 Visual Studio 在你设置的断点处暂停正在运行的代码，这样你就可以查看变量值或内存行为，或者确定代码的分支是否已运行。

1. 若要开始调试，请按 F5，或者在“标准”工具栏中选择“调试目标”按钮，或者在“调试”工具栏中选择“开始调试”按钮，或者从菜单栏中选择“调试” > “开始调试”    。 应用随即启动，调试器将运行到你设置了断点的代码行。

    :::image type="content" source="media/vs-2022/get-started-set-breakpoint.png" alt-text="显示 Visual Studio 2022 代码编辑器中的断点的屏幕截图，代码执行已在断点处暂停。":::

    黄色箭头指向调试器暂停时所在的语句。 应用执行将在同一位置暂停，此处的语句尚未执行。

    当应用未运行时，按 F5 会启动调试器。调试器将持续运行该应用，直至到达第一个断点。 如果应用在某个断点处暂停，则按 F5 会继续运行该应用，直至到达下一个断点。

    如果你知道自己要详细检查的代码行或代码段，则断点功能非常有用。 有关可设置的各种断点（例如条件断点）的详细信息，请参阅[使用断点](../../debugger/using-breakpoints.md)。

::: moniker-end

## <a name="navigate-code-and-inspect-data-by-using-data-tips"></a>使用数据提示浏览代码并检查数据

::: moniker range="<=vs-2019"

大多数情况下，我们使用键盘快捷方式，因为这是在调试器中快速执行应用的好方法（括号中显示了等效的命令，如菜单命令）。

1. 在 `name += letters[i]` 语句上暂停时，将鼠标悬停在 `letters` 变量上，会看到其默认值为数组中第一个元素的值 `char[10]`。

     允许你检查变量的功能是调试器最有用的功能之一，并且有不同的方法来执行此操作。 通常，当尝试调试问题时，你试图找出变量是否存储了你期望它们在特定时间具有的值。

1. 展开 `letters` 变量，查看其属性，其中包括变量包含的所有元素。

     ![调试器在“name+= letters[I]”语句处暂停的屏幕截图。](../csharp/media/get-started-view-data-tip.png)

1. 接下来，将鼠标悬停在 `name` 变量上，会看到其当前值为空字符串。

1. 按两次 F10（或选择“调试”>“单步跳过”）前进到 `SendMessage` 方法调用，然后再按一次 F10    。

     按 F10 将使调试器前进到下一条语句，但不会单步执行应用代码中的函数或方法（代码仍将执行）。 在进行 `SendMessage` 方法调用时，通过按 F10，我们跳过了 `SendMessage` 的实现代码（我们现在可能对此不感兴趣）。

1. 多按几次 F10（或选择“调试”>“单步跳过”），通过 `for` 循环执行多次循环访问，再次在断点处暂停，每次都将鼠标悬停在 `name` 变量上以检查其值  。

     ![Visual Studio 调试器的动画屏幕截图，其中显示在调试期间按 F10 以“单步执行”并迭代循环的效果。](../csharp/media/get-started-data-tip.gif)

     变量的值随 `for` 循环的每次迭代而更改，显示的值依次为 `f`、`fr`、`fre`，依此类推。 要在此方案中更快地前进到循环，可以按 F5 （或选择“调试器” > “继续”），此操作会使你前进到断点，而不是下一条语句    。

     通常情况下，在调试时，需要快速检查变量的属性值，以查看它们是否存储了你希望它们存储的值，可根据数据提示执行此操作。

1. 在 `Main` 方法的 `for` 循环中仍处于暂停状态时，按 F11（或选择“调试”>“单步执行”），直到在 `SendMessage` 方法调用处暂停   。

     你应该位于以下代码行：

     `SendMessage(name, a[i]);`

1. 再按一次 F11 单步执行到 `SendMessage` 方法  。

     黄色指针会前进到 `SendMessage` 方法。

     ![位于“SendMessage”方法处的执行指针的屏幕截图。](../csharp/media/get-started-f11.png "F10 单步执行")

     F11 是“单步执行”命令，每按一次，应用就执行下一个语句  。 F11 是一种以最详尽方式检查执行流的好方法。 默认情况下，调试器会跳过非用户代码（如果需要更多详细信息，请参阅[仅我的代码](../../debugger/just-my-code.md)）。

     假设你已完成了对 `SendMessage` 方法的检查，并且希望退出该方法但保持位于调试器中。 可使用“单步跳出”命令执行此操作  。

1. 按 Shift+F11（或选择“调试”>“单步跳出”）  。

     此命令将恢复应用执行（并使调试器前进），直到当前方法或函数返回。

     你应当回到 `Main` 方法的 `for` 循环，在 `SendMessage` 方法调用处暂停。 有关在代码中进行移动的不同方法的详细信息，请参阅[浏览调试器中的代码](../../debugger/navigating-through-code-with-the-debugger.md)。

::: moniker-end

::: moniker range=">=vs-2022"

1. 暂停于 `name += letters[i]` 语句处时，将鼠标悬停在 `letters` 变量上以查看显示数组大小和元素类型 `char[10]` 的数据提示。

    > [!NOTE]
    > 调试器最有用的功能之一是能够检查变量。 通常，在尝试调试某个问题时，你会试图确定变量是否具有你期望它们在特定时间具有的值。 查看数据提示是进行这种检查的好办法。

1. 展开 `letters` 变量以查看其所有数组元素以及这些元素的值。

    :::image type="content" source="media/vs-2022/get-started-view-data-tip.png" alt-text="Visual Studio 2022 中调试器数据提示的屏幕截图，其中显示了“letters”数组变量的元素值。":::

1. 将鼠标悬停在 `name` 变量上以查看其当前值（一个空字符串）。

1. 若要使调试器前进到下一条语句，请按 F10，或者在“调试”工具栏中选择“单步跳过”按钮，或者从菜单栏中选择“调试” > “单步跳过”   。 再按 F10 两次以跳过 `SendMessage` 方法调用。 

    按 F10 会使调试器前进，而不会单步执行函数或方法，不过，其代码仍会执行。 这样，就跳过了调试我们暂时不需要关注的 `SendMessage` 方法中的代码。

1. 若要迭代 `for` 循环几次，请反复按 F10。 在每次循环迭代期间，请在断点处暂停，然后将鼠标悬停在 `name` 变量上以在数据提示中检查其值。

    :::image type="content" source="media/vs-2022/get-started-data-tip.png" alt-text="Visual Studio 2022 中调试器数据提示的屏幕截图，其中显示了“name”变量的字符串值。":::

    变量的值随 `for` 循环的每次迭代而更改，显示的值依次为 `f`、`fr`、`fre`，依此类推。 若要使调试器在循环中更快前进，请按 F5，这样就会前进到断点而不是下一条语句。

1. 在 `Main` 方法的 `for` 循环中暂停时，按 F11，或者从“调试”工具栏中选择“单步执行”按钮，或者从菜单栏中选择“调试”>“单步执行”，直至到达 `SendMessage` 方法调用   。

     应在此代码行处暂停调试器：

     `SendMessage(name, a[i]);`

1. 若要单步执行 `SendMessage` 方法，请再次按 F11。

     黄色指针会前进到 `SendMessage` 方法。

     :::image type="content" source="media/vs-2022/get-started-f11.png" alt-text="显示“SendMessage”方法中的调试器执行指针的屏幕截图。":::

     按 F11 可帮助你更深入地检查代码的执行流。 若要单步执行方法调用中的方法，请按 F11。 默认情况下，调试器将跳过非用户方法的单步执行。 若要了解如何调试非用户代码，请参阅[仅我的代码](../../debugger/just-my-code.md)。

     调试完 `SendMessage` 方法后，可以返回到 `main` 方法的 `for` 循环。

1. 若要退出 `SendMessage` 方法，请按 Shift+F11，或者在“调试”工具栏中选择“单步跳出”按钮，或者从菜单栏中选择“调试”>“单步跳出”   。

     “单步跳出”将恢复应用执行并使调试器前进，直到当前方法或函数返回。

     你将在 `Main` 方法的 `for` 循环中再次看到黄色指针，该指针暂停在 `SendMessage` 方法调用处。 有关在代码中进行移动的不同方法的详细信息，请参阅[浏览调试器中的代码](../../debugger/navigating-through-code-with-the-debugger.md)。

::: moniker-end

## <a name="navigate-code-using-run-to-click"></a>使用“运行时单击”导航代码

::: moniker range="<=vs-2019"

1. 按 F5 再次前进到断点。

1. 在代码编辑器中向下滚动，并将鼠标悬停在 `SendMessage` 方法中的 `Console.WriteLine` 方法上，直到绿色的“运行到单击处”按钮 ![“运行到单击处”按钮的插图。](../../debugger/media/dbg-tour-run-to-click.png "运行时单击") 显示在左侧。 按钮的工具提示显示“将执行运行到此处”。

     ![“运行到单击处”按钮的屏幕截图。](../csharp/media/get-started-run-to-click.png "运行时单击")

   > [!NOTE]
   > “运行时单击”是 [!include[vs_dev15](../../misc/includes/vs_dev15_md.md)] 中的新增按钮  。 （如果未看到绿色箭头按钮，请在此示例中改为使用 F11 以使调试器前进到正确的位置。  ）

1. 单击“运行到单击处”按钮 ![“运行到单击处”按钮的插图。](../../debugger/media/dbg-tour-run-to-click.png "运行时单击")。

    调试器会前进到 `Console.WriteLine` 方法。

    使用此按钮类似于设置临时断点。 “运行时单击”对于快速到达应用代码的可见区域十分方便（你可在任何打开的文件中单击）  。

::: moniker-end

::: moniker range=">=vs-2022"

1. 按 F5 再次前进到断点。

1. 在代码编辑器中，将鼠标悬停在 `SendMessage` 方法中的 `Console.WriteLine` 方法调用上，直到左侧出现“运行到单击处”按钮。 按钮的工具提示显示“将执行运行到此处”。

    :::image type="content" source="media/vs-2022/get-started-run-to-click.png" alt-text="显示 Visual Studio 2022 中“运行到单击处”按钮的屏幕截图。":::

1. 选择“运行到单击处”按钮。 或者，将光标置于 `Console.WriteLine` 语句上，然后按 Ctrl+F10。 或者，右键单击 `Console.WriteLine` 方法调用，然后从上下文菜单中选择“运行到光标处”。

    调试器会前进到 `Console.WriteLine` 方法调用。

    使用“运行到单击处”按钮类似于设置临时断点，在已打开的文件的应用代码可见区域中，可以快速方便地使用这种方法。

::: moniker-end

## <a name="restart-your-app-quickly"></a>快速重启应用

::: moniker range="<=vs-2019"

在“调试”工具栏中单击“重启”![“重启应用”按钮的插图。](../../debugger/media/dbg-tour-restart.png "重启应用") 按钮 (Ctrl + Shift + F5)  。

当你按下“重启”时，与停止应用并重启调试器相比，它节省了时间  。 调试器在执行代码命中的第一个断点处暂停。

调试器再次在你之前在 `for` 循环上设置的断点处停止。

::: moniker-end

::: moniker range=">=vs-2022"

若要在调试器中从头开始重新运行应用，请按 Ctrl+Shift+F5，或者在“调试”工具栏中选择“重启”按钮，或者从菜单栏中选择“调试”>“重启”   。

:::image type="content" source="media/vs-2022/dbg-tour-restart-debugging.png" alt-text="Visual Studio 2022 的“调试”工具栏中“重启”按钮的屏幕截图。":::

“重启”将通过一个步骤停止调试器并重启调试器。 调试器重启时，将运行到第一个断点（先前在 `for` 循环中设置的断点），然后暂停。

::: moniker-end

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>使用“自动”和“局部变量”窗口检查变量

::: moniker range="<=vs-2019"

1. 查看代码编辑器底部的“自动”窗口  。

    如果该窗口已关闭，请在调试器中处于暂停状态时，选择“调试”>“窗口”>“自动变量”将其打开  。

    在“自动”窗口中，可看到变量及其当前值  。 “自动”窗口显示当前行或前一行使用的所有变量（检查文档中特定于语言的行为）  。

1. 接下来，我们来看看“自动”窗口旁边的选项卡中的“局部变量”窗口   。

1. 展开 `letters` 变量以显示其包含的元素。

     ![Visual Studio 中“局部变量”窗口的屏幕截图。](../csharp/media/get-started-locals-window.png "“局部变量”窗口")

    “局部变量”窗口显示当前[作用域](https://www.wikipedia.org/wiki/Scope_(computer_science))中的变量，即当前执行上下文  。

::: moniker-end

::: moniker range=">=vs-2022"

在调试时，“自动变量”和“局部变量”窗口会显示变量值 。 这两个窗口仅在调试会话期间才会显示。 “自动变量”窗口显示调试器所在的当前行和上一行中使用的变量。 “局部变量”窗口显示在局部范围内定义的变量，通常是当前函数或方法。

1. 在调试器处于暂停状态时，查看代码编辑器底部的“自动变量”窗口。

    如果“自动变量”窗口已关闭，请按下 Ctrl+D 和 A，或者从菜单栏中选择“调试”>“窗口”>“自动变量”    。

1. 在调试器仍处于暂停状态的情况下，在“自动变量”窗口旁边的选项卡中查看“局部变量”窗口 。

    如果“局部变量”窗口已关闭，请按下 Ctrl+D 和 L，或者从菜单栏中选择“调试”>“窗口”>“局部变量”    。

1. 在“局部变量”窗口中，展开 `letters` 变量以查看其数组元素以及这些元素的值。

     :::image type="content" source="media/vs-2022/get-started-locals-window.png" alt-text="Visual Studio 2022 中“局部变量”窗口的屏幕截图，其中的“letters”数组变量已展开。":::

有关“自动变量”和“局部变量”窗口的详细信息，请参阅[在“自动变量”和“局部变量”窗口中检查变量](/visualstudio/debugger/autos-and-locals-windows?view=vs-2022&preserve-view=true) 。

::: moniker-end

## <a name="set-a-watch"></a>设置监视

::: moniker range="<=vs-2019"

1. 在主代码编辑器窗口中，右键单击 `name` 变量，然后选择“添加监视”  。

    “监视”窗口将在代码编辑器的底部打开  。 可使用“监视”窗口指定要关注的变量（或表达式）  。

    现在，你在 `name` 变量上设置好了监视，当你在调试器中移动时，可看到其值发生变化。 与其他变量窗口不同，“监视”窗口始终显示你正在监视的变量（当超出作用域时，它们会变灰）  。

::: moniker-end

::: moniker range=">=vs-2022"

可以指定你在逐步执行代码时想要观察的变量或表达式 &mdash; 将其添加到“监视”窗口即可。

1. 当调试器处于暂停状态时，右键单击 `name` 变量并选择“添加监视”。

    “监视”窗口默认将在代码编辑器的底部打开。

1. 对 `name` 变量设置监视后，接下来请逐步执行代码，以查看 `name` 变量值在每次 `for` 循环迭代中的变化。 

    与其他变量窗口不同，“监视”窗口始终显示你正在监视的变量，不过，如果这些变量超出范围，则它们会灰显。

有关“监视”窗口的详细信息，请参阅[使用“监视”窗口监视变量](/visualstudio/debugger/watch-and-quickwatch-windows?view=vs-2022&preserve-view=true)。

::: moniker-end

## <a name="examine-the-call-stack"></a>检查调用堆栈

::: moniker range="<=vs-2019"

1. 在 `for` 循环中暂停时，单击“调用堆栈”窗口，默认情况下，该窗口在右下方窗格中打开  。

    如果该窗口已关闭，请在调试器中处于暂停状态时，选择“调试”>“窗口”>“调用堆栈”将其打开  。

1. 单击多次 F11，直至看到调试器在 `SendMessage` 方法中暂停  。 查看“调用堆栈”窗口  。

    ![Visual Studio 中“调用堆栈”窗口的屏幕截图。](../csharp/media/get-started-call-stack.png "检查调用堆栈")

    “调用堆栈”窗口显示方法和函数被调用的顺序  。 最上面一行显示当前函数（此应用中的 `SendMessage` 方法）。 第二行显示 `SendMessage` 是从 `Main` 方法调用的，依此类推。

   > [!NOTE]
   > “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图  。

    调用堆栈是检查和理解应用执行流的好方法。

    可双击代码行来查看该源代码，这也会更改调试器正在检查的当前作用域。 此操作不会使调试器前进。

    还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作  。 例如，你可将断点插入到指定的函数中，使用“运行到光标处”推进调试器，然后检查源代码  。 有关详细信息，请参阅[如何：检查调用堆栈](../../debugger/how-to-use-the-call-stack-window.md)。

::: moniker-end

::: moniker range=">=vs-2022"

“调用堆栈”显示方法和函数的调用顺序，可帮助你了解应用的执行流。

1. 当调试器在 `for` 循环中处于暂停状态时，查看“调用堆栈”窗口，该窗口默认会在代码编辑器的右下窗格中打开。

    如果“调用堆栈”窗口已关闭，请按下 Ctrl+D 和 C，或者从菜单栏中选择“调试”>“窗口”>“调用堆栈”    。

    在“调用堆栈”窗口中，你将在当前 `Main` 方法处看到黄色指针。

1. 按 F11 几次，直至看到调试器在 `SendMessage` 方法中暂停。

    “调用堆栈”窗口的第一行显示当前函数，即 `SendMessage` 方法。 第二行显示从 `Main` 方法调用的 `SendMessage` 方法。

    :::image type="content" source="media/vs-2022/get-started-call-stack.png" alt-text="Visual Studio 2022 中“调用堆栈”窗口的屏幕截图。":::

   > [!NOTE]
   > “调用堆栈”窗口类似于某些 IDE（例如 Eclipse）中的“调试”透视图。

    在“调用堆栈”窗口中，可以双击代码行转到相应的源代码，这会更改调试器正在检查的当前范围。 此操作不会使调试器前进。

    还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作  。 例如，可将断点插入到指定的函数中、使用“运行到光标处”使调试器前进，或转到源代码。 

有关“调用堆栈”的详细信息，请参阅[如何：检查调用堆栈](../../debugger/how-to-use-the-call-stack-window.md)。

::: moniker-end

## <a name="change-the-execution-flow"></a>更改执行流

::: moniker range="<=vs-2019"

1. 按两次 F11 以运行 `Console.WriteLine` 方法  。

1. 在 `SendMessage` 方法调用中暂停调试器后，使用鼠标抓住左侧的黄色箭头（执行指针），将黄色箭头向上移动一行，返回到 `Console.WriteLine`。

1. 按下 F11  。

    调试器将重新运行 `Console.WriteLine` 方法（你会在控制台窗口输出中看到）。

    通过更改执行流，你可以进行测试不同代码执行路径或重新运行代码等操作，而无需重启调试器。

    > [!WARNING]
    > 通常你需要小心使用此功能，工具提示中会出现警告。 你也可能会看到其他警告。 移动指针无法将应用程序还原到更早的应用状态。

1. 按 F5 继续运行应用  。

    恭喜你完成本教程！

::: moniker-end

::: moniker range=">=vs-2022"

在调试时，可以移动执行指针以更改应用流。

1. 当调试器暂停于 `for` 循环中的 `SendMessage` 方法调用处时，按 F11 三次以单步执行 `SendMessage` 方法，并在执行该方法后跳过 `Console.WriteLine` 方法。

    现在，调试器已暂停于 `SendMessage` 方法的最后一个右大括号处。

1. 使用鼠标抓取黄色箭头或执行指针（在左边缘中），然后将指针向上拖动一行。

    调试器现在回到了 `Console.WriteLine` 语句。

1. 按 F11。

    调试器重新运行 `Console.WriteLine` 方法，你将在控制台窗口输出中看到重复的行。

1. 按 F5 继续运行应用。

通过更改执行流，你可以进行测试不同代码执行路径或重新运行代码等操作，而无需重启调试器。

> [!WARNING]
> 请慎用此功能。 你将在执行指针的工具提示中看到一条警告，其中指出可能会出现意外的后果。 此外，还可能会看到其他警告。 移动执行指针无法将应用程序还原到以前的状态。

有关更改执行流的详细信息，请参阅[移动指针以更改执行流](/visualstudio/debugger/navigating-through-code-with-the-debugger?view=vs-2022#BKMK_Set_the_next_statement_to_execute&preserve-view=true)。

恭喜你完成本教程！

::: moniker-end

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解了如何启动调试器、逐步执行代码以及检查变量。 你可能想要大致了解调试器功能并获取指向详细信息的链接。

> [!div class="nextstepaction"]
> [初探调试器](../../debugger/debugger-feature-tour.md)
