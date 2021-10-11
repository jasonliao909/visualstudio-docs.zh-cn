---
title: '教程：创建一个简单的 C# 控制台应用程序 '
description: 了解如何在 Visual Studio 中分步创建 C# 控制台应用程序。
ms.custom: vs-acquisition, get-started
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: anandmeg
ms.author: meghaanand
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: e46b3ed2449972b065ac005ac83f2650cb93d03d
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128426636"
---
# <a name="tutorial-create-a-simple-c-console-app-in-visual-studio-part-1-of-2"></a>教程：在 Visual Studio 中创建一个简单的 C# 控制台应用（第 1 部分，共 2 部分）

在本教程中，你将使用 Visual Studio 创建和运行 C# 控制台应用，并探索 Visual Studio 集成开发环境 (IDE) 的部分功能。 本教程是由两个部分构成的系列教程的第一部分。

本教程介绍以下操作：

> [!div class="checklist"]
> * 创建一个 Visual Studio 项目。
> * 创建一个 C# 控制台应用。
> * 调试应用。
> * 关闭应用。
> * 检查完整的代码。

[在第 2 部分](tutorial-console-part-2.md)，你将扩展此应用以添加更多项目、了解调试技巧和引用第三方包。

## <a name="prerequisites"></a>必备条件

必须安装 Visual Studio。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

若要开始，请创建一个 C# 应用程序项目。 项目类型随附了所需的全部模板文件。

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件” > “新建” > “项目”。
   （或者，按 Ctrl+Shift+N）  。

3. 在“新建项目”对话框的左侧窗格中，展开“C#”，然后选择“.NET Core”  。 在中间窗格中，选择“控制台应用(.NET Core)”。 然后，将文件命名为“计算器”。

   ![显示 Visual Studio IDE 的“新建项目”对话框中控制台应用 (.NET Core) 项目模板的屏幕截图。](./media/new-project-csharp-calculator-console-app.png)

### <a name="add-a-workload-optional"></a>添加工作负载（可选）

如果未显示“控制台应用(.NET Core)”项目模板，可通过添加“.NET Core 跨平台开发”工作负载获取它。 操作方法如下。

#### <a name="option-1-use-the-new-project-dialog-box"></a>选项 1：使用“新建项目”对话框

1. 选择“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接。

   ![显示从“新建项目”对话框中选择“打开 Visual Studio 安装程序”链接的屏幕截图。](./media/csharp-open-visual-studio-installer-generic-dark.png)

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

   ![显示 Visual Studio 安装程序中“.NET Core 跨平台开发”工作负载的屏幕截图。](./media/dot-net-core-xplat-dev-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>选项 2：使用“工具”菜单栏

1. 取消“新建项目”对话框，再从顶部菜单栏中选择“工具”>“获取工具和功能”  。

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio，然后在“开始”窗口中选择“创建新项目”。

   ![显示“创建新项目”窗口的屏幕截图。](../../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口中，从“语言”列表中选择“C#”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“控制台”。

   应用语言、平台和项目类型筛选器之后，选择“控制台应用程序”模板，然后选择“下一步” 。

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，请选择“安装更多工具和功能” 。
   >
   > ![显示“安装更多工具和功能”链接的屏幕截图。](../../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。
   >
   > ![显示 Visual Studio 安装程序中“.NET Core 跨平台开发”工作负载的屏幕截图。](./media/dot-net-core-xplat-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“计算器”。 然后，选择“下一步”。

    :::image type="content" source="./media/vs-2019/csharp-name-your-calculator-project.png" alt-text="显示在“配置新项目”窗口中将项目命名为“Calculator”的屏幕截图。":::

1. 在“附加信息”窗口中，应已为目标框架选择“.NET Core 3.1” 。 如果未选择，则请选择“.NET Core 3.1”。 然后，选择“创建”。

    :::image type="content" source="./media/vs-2019/csharp-target-framework.png" alt-text="显示确保在“其他信息”窗口中选择“.NET Core 3.1”的屏幕截图。":::

   Visual Studio 随即打开新项目，其中包含默认的“Hello World”代码。

::: moniker-end
::: moniker range=">=vs-2022"

1. 打开 Visual Studio，然后在“开始”窗口中选择“创建新项目”。

   ![显示“创建新项目”窗口的屏幕截图。](media/vs-2022/create-new-project.png)

1. 在“创建新项目”窗口中选择“所有语言”，然后从下拉列表中选择“C#”  。 从“所有平台”列表中选择“Windows”，然后从“所有项目类型”列表中选择“控制台”   。

   应用语言、平台和项目类型筛选器之后，选择“控制台应用程序”模板，然后选择“下一步” 。

   > [!NOTE]
   > 如果未看到“控制台应用程序”模板，请选择“安装更多工具和功能” 。
   >
   > ![显示“安装更多工具和功能”链接的屏幕截图。](media/vs-2022/not-finding-what-looking-for.png)
   >
   > 在 Visual Studio 安装程序中选择“.NET 桌面开发”工作负载，然后选择“修改” 。
   >
   > ![显示 Visual Studio 安装程序中的“.NET 桌面开发”工作负载的屏幕截图。](media/vs-2022/dot-net-development-workload.png)

1. 在“配置新项目”窗口中，在“项目名称”框中键入“Calculator”，然后选择“下一步” 。

   ![显示在“配置新项目”窗口中将项目命名为“Calculator”的屏幕截图。](media/vs-2022/csharp-name-your-calculator-project.png)

1. 在“其他信息”窗口中，应已选择“.NET 6.0”作为目标框架 。 选择“创建”  。

   ![显示在“其他信息”窗口中选择了“.NET 6.0”的屏幕截图。](media/vs-2022/csharp-target-framework.png)

   Visual Studio 随即打开新项目，其中包含默认的“Hello World”代码。

::: moniker-end

## <a name="create-the-app"></a>创建应用

本部分的操作：

- 探索 C# 中的一些基本整数数学运算。
- 添加代码以创建一个基本计算器应用。
- 调试该应用，以查找并修复错误。
- 优化代码，使其更高效。

### <a name="explore-integer-math"></a>探索整数数学运算

首先在 C# 中进行一些基本的整数数学运算。

::: moniker range="<=vs-2019"
1. 在代码编辑器中，删除默认“Hello World”代码。

    ![显示从新的计算器应用中删除默认 Hello World 代码的屏幕截图。](./media/csharp-console-calculator-deletehelloworld.png)

   具体而言，删除显示 `Console.WriteLine("Hello World!");` 的行。

1. 在其原位置，键入以下代码：

    ```csharp
            int a = 42;
            int b = 119;
            int c = a + b;
            Console.WriteLine(c);
            Console.ReadKey();
    ```

    请注意，执行此操作时，Visual Studio 中的 IntelliSense 功能会提供自动完成该项的选项。

    > [!NOTE]
    > 以下动画并非旨在复制前面的代码。 它仅用于显示自动完成功能的工作方式。

    ![显示 Visual Studio IDE 中 IntelliSense 自动完成功能的整数数学运算代码动画。](./media/integer-math-intellisense.gif)

1. 选择“计算器”旁的绿色“开始”按钮以生成并运行程序，或按“F5”。

   ![显示从工具栏中选择“Calculator”按钮以运行应用的屏幕截图。](./media/csharp-console-calculator-button.png)

   随即会打开控制台窗口，显示 42 + 119 的总和，即 161。

    ![显示包含整数数学运算结果的控制台窗口的屏幕截图。](./media/csharp-console-integer-math.png)

1. （可选）可以更改运算符来更改结果。 例如，可以将 `int c = a + b;` 代码行中的 `+` 运算符更改为 `-` 进行减法运算，更改为 `*` 进行乘法运算，或更改为 `/` 进行除法运算。 然后，运行该程序时，结果也会改变。

1. 关闭控制台窗口。
::: moniker-end

::: moniker range=">=vs-2022&quot;
1. 在“解决方案资源管理器”的右侧窗格中选择“Program.cs”，以在代码编辑器中显示该文件 

1. 在代码编辑器中，替换显示了 `Console.WriteLine(&quot;Hello World!");` 的默认“Hello World”代码。

    ![显示要在 program 文件中替换的行的屏幕截图。](media/vs-2022/csharp-console-calculator-delete-hello-world.png)

   将该行替换为以下代码：

   ```csharp
       int a = 42;
       int b = 119;
       int c = a + b;
       Console.WriteLine(c);
       Console.ReadKey();
   ```

    如果你键入代码，则 Visual Studio IntelliSense 功能将提供用于自动完成输入的选项。

    > [!NOTE]
    > 以下动画并非旨在演示前面的代码，而只是演示 IntelliSense 的工作原理。

    ![显示 Visual Studio IDE 中 IntelliSense 自动完成功能的整数数学运算代码动画。](media/integer-math-intellisense.gif)

1. 若要生成并运行应用，请按 F5，或者在顶部工具栏中选择名称“Calculator”旁边的绿色箭头 。

   ![显示从“调试”工具栏中选择“Calculator”按钮以运行应用的屏幕截图。](media/vs-2022/csharp-console-calculator-button.png)

   随即会打开控制台窗口，其中显示了 42 + 119 的总和，即 161。

    ![显示整数数学运算结果的控制台窗口的屏幕截图。](media/vs-2022/csharp-console-integer-math.png)

1. 关闭控制台窗口。

1. （可选）可以更改运算符来更改结果。 例如，可以将 `int c = a + b;` 代码行中的 `+` 运算符更改为 `-` 进行减法运算，更改为 `*` 进行乘法运算，或更改为 `/` 进行除法运算。 运行应用时，结果会相应地更改。

::: moniker-end

### <a name="add-code-to-create-a-calculator"></a>添加代码以创建计算器

向项目添加一组更复杂的计算器代码以继续操作。

1. 在代码编辑器中，将 program.cs 中的所有代码替换为以下新代码：

    ```csharp
    using System;

    namespace Calculator
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Declare variables and then initialize to zero.
                int num1 = 0; int num2 = 0;

                // Display title as the C# console calculator app.
                Console.WriteLine("Console Calculator in C#\r");
                Console.WriteLine("------------------------\n");

                // Ask the user to type the first number.
                Console.WriteLine("Type a number, and then press Enter");
                num1 = Convert.ToInt32(Console.ReadLine());

                // Ask the user to type the second number.
                Console.WriteLine("Type another number, and then press Enter");
                num2 = Convert.ToInt32(Console.ReadLine());

                // Ask the user to choose an option.
                Console.WriteLine("Choose an option from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                // Use a switch statement to do the math.
                switch (Console.ReadLine())
                {
                    case "a":
                        Console.WriteLine($"Your result: {num1} + {num2} = " + (num1 + num2));
                        break;
                    case "s":
                        Console.WriteLine($"Your result: {num1} - {num2} = " + (num1 - num2));
                        break;
                    case "m":
                        Console.WriteLine($"Your result: {num1} * {num2} = " + (num1 * num2));
                        break;
                    case "d":
                        Console.WriteLine($"Your result: {num1} / {num2} = " + (num1 / num2));
                        break;
                }
                // Wait for the user to respond before closing.
                Console.Write("Press any key to close the Calculator console app...");
                Console.ReadKey();
            }
        }
    }
    ```

1. 选择“Calculator”按钮或按 F5 运行应用 。

   控制台窗口即会打开。

1. 在控制台窗口中，按照提示将数字 42 和 119 相加 。

   应用应如以下屏幕快照所示：

    ![控制台窗口的屏幕截图，其中显示了 Calculator 应用和提示。](media/csharp-console-calculator.png)

### <a name="add-decimal-functionality"></a>添加小数运算功能

现在调整代码以添加更多功能。

当前的计算器应用仅接受并返回整数。 例如，如果运行该应用，将数字 42 除以数字 119，则结果为 0，这并不精确。

![控制台窗口的屏幕截图，其中显示了 Calculator 应用返回不精确的整数作为结果。](./media/csharp-console-calculator-nodecimal.png)

若要修复代码以通过处理小数来提高精度，请执行以下操作：

1. 在 Visual Studio 编辑器中的 program.cs 内，按 Ctrl+H 打开“查找和替换”控件  。

1. 在该控件中键入“int”，在“替换”字段中键入“float” 。

1. 在该控件中选择“匹配大小写”和“全字匹配”对应的图标，或者按 Alt+C 和 Alt+W     。

1. 选择“全部替换”图标或按 Alt+A 运行搜索和替换  。

    ![显示如何将 int 变量更改为 float 的“查找和替换”控件动画。](media/find-replace-control-animation.gif)

1. 再次运行计算器应用，将数字 42 除以数字 119 。

   该应用现在返回的是小数而不是 0。

    ![“控制台”窗口的屏幕截图，其中显示了 Calculator 应用现在返回小数作为结果。](media/csharp-console-calculator-decimal.png)

现在，应用可以生成小数结果。 对代码再做一些调整，使应用也可以计算小数。

1. 使用“查找和替换”控件将 `float` 变量的每个实例更改为 `double`，并将 `Convert.ToInt32` 方法的每个实例更改为 `Convert.ToDouble`。

1. 运行计算器应用，将数字 42.5 除以数字 119.75 。

   该应用现在接受小数值，并返回更长的小数作为结果。

    ![“控制台”窗口的屏幕截图，其中显示了 Calculator 应用现在接受小数，并返回更长的小数结果。](media/csharp-console-calculator-usedecimals.png)

   在[修改代码](#revise-the-code)部分，你将减少结果中的小数位数。

## <a name="debug-the-app"></a>调试应用

你已改进了基本计算器应用，但该应用目前还不能处理异常，例如用户输入错误。 例如，如果用户尝试除以零或者输入意外的字符，则应用可能会停止工作、返回错误或返回意外的非数值结果。

现在来演练一些常见的用户输入错误，在调试程序中找到它们（若其出现），并在代码中修复它们。

> [!TIP]
> 有关调试器及其工作原理的详细信息，请参阅[初步了解 Visual Studio 调试器](../../debugger/debugger-feature-tour.md)。

### <a name="fix-the-divide-by-zero-error"></a>修复“被零除”错误

如果你尝试将数字除以零，则控制台应用可能会冻结，并在代码编辑器中显示哪些内容是错误的。

   ![Visual Studio 代码编辑器的屏幕截图，其中以黄色突出显示了一行，并显示了“尝试除以零”的“未经处理的异常”错误。](./media/csharp-console-calculator-dividebyzero-error.png)

> [!NOTE]
> 有时，应用不会冻结且调试器不会显示“被零除”错误。 相反，应用可能会返回意外的非数字结果，如无穷符号。 以下代码修复仍然适用。

若要更改代码以处理此错误，请执行以下操作：

1. 在 program.cs 中，将 `case "d":` 和显示了 `// Wait for the user to respond before closing` 的注释之间的代码替换为以下代码：

   ```csharp
            // Ask the user to enter a non-zero divisor until they do so.
                while (num2 == 0)
                {
                    Console.WriteLine("Enter a non-zero divisor: ");
                    num2 = Convert.ToInt32(Console.ReadLine());
                }
                Console.WriteLine($"Your result: {num1} / {num2} = " + (num1 / num2));
                break;
        }
    ```

   替换代码后，包含 `switch` 语句的部分应如以下屏幕截图所示：

   ![显示 Visual Studio 代码编辑器中修改后的 switch 部分的屏幕截图。](media/csharp-console-calculator-switch-code.png)

现在，将任意数字除以零时，该应用会要求输入另一个数字，并且在你提供非零数字之前，它会不断地要求你这样做。

   ![控制台窗口的屏幕截图，其中显示应用反复提示输入非零数字。](media/csharp-console-calculator-dividebyzero.png)

### <a name="fix-the-format-error"></a>修复“格式”错误

如果在应用要求输入数字字符时你输入了字母字符，应用将会冻结。 Visual Studio 将显示代码编辑器中的哪些内容是错误的。

   ::: moniker range="<=vs-2019"
   ![显示 Visual Studio 代码编辑器中未经处理的格式错误的屏幕截图。](media/csharp-console-calculator-format-error.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![显示 Visual Studio 代码编辑器中未经处理的格式错误的屏幕截图。](media/vs-2022/csharp-console-calculator-format-error.png)
   ::: moniker-end

若要防止此异常，可以重构先前输入的代码。

#### <a name="revise-the-code"></a>修改代码

可将应用分为两个类：`Calculator` 和 `Program`，而不是依赖于 `program` 类来处理所有代码。

`Calculator` 类处理大量的计算工作，而 `Program` 类则会处理用户界面和错误处理工作。

现在就开始吧。

1. 在 program.cs 中，删除 `Calculator` 命名空间中左大括号和右大括号之间的所有内容：

    ```csharp
    using System;

    namespace Calculator
    {

    }
    ```

1. 在大括号之间添加以下新的 `Calculator` 类：

    ```csharp
    class Calculator
    {
        public static double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    break;
                case "s":
                    result = num1 - num2;
                    break;
                case "m":
                    result = num1 * num2;
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }

    ```

1. 另外还添加新的 `Program` 类，如下所示：

    ```csharp
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
    ```

1. 选择“Calculator”按钮或按 F5 运行应用 。

1. 按照提示，用数字 42 除以数字 119 。 结果应类似于以下屏幕截图：

   ::: moniker range="<=vs-2019"
   ![控制台窗口的屏幕截图，其中显示了已重构的 Calculator 应用。](media/csharp-console-calculator-refactored.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![控制台窗口的屏幕截图，其中显示了已重构的 Calculator 应用。](media/vs-2022/csharp-console-calculator-refactored.png)
   ::: moniker-end

   现在可以输入更多算式，直到选择关闭控制台应用。 结果中的小数位数也会减少。 如果输入错误的字符，则会得到相应的错误响应。

## <a name="close-the-app"></a>关闭应用程序

1. 如果尚未关闭计算器应用，现在请将其关闭。

1. 关闭 Visual Studio 中的输出窗格。

   ![显示关闭 Visual Studio 中的“输出”窗格的屏幕截图。](media/csharp-calculator-close-output-pane.png)

1. 在 Visual Studio 中，按 Ctrl+S 保存应用 。

[!INCLUDE[../includes/git-source-control.md](../includes/git-source-control.md)]

## <a name="review-code-complete"></a>查看：代码完成

在本教程中，你对计算器应用做出了许多更改。 该应用现在可以更高效地处理计算资源，并可处理大多数的用户输入错误。

以下是完整代码，全部显示在同一个位置：

```csharp

using System;

namespace Calculator
{
    class Calculator
    {
        public static double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    break;
                case "s":
                    result = num1 - num2;
                    break;
                case "m":
                    result = num1 * num2;
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
}

```

## <a name="next-steps"></a>后续步骤

:::moniker range="vs-2017"

继续学习更多教程：

> [!div class="nextstepaction"]
> [C# 教程](/dotnet/csharp/tutorials)

> [!div class="nextstepaction"]
> [学习 Visual Studio IDE 教程](../visual-studio-ide.md)

:::moniker-end

:::moniker range=">=vs-2019"

继续学习本教程的第二部分：

> [!div class="nextstepaction"]
> [教程第 2 部分：扩展和调试 C# 控制台应用](tutorial-console-part-2.md)
:::moniker-end
