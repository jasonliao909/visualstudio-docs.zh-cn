---
title: 教程 2：扩展 C# 控制台应用
description: 了解如何在 Visual Studio 中逐步开发 C# 控制台应用。
ms.custom: vs-acquisition, get-started
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: anandmeg
ms.author: meghaanand
manager: jmartens
monikerRange: '>=vs-2019'
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: b4b323611897a7977d906eb585f49006b54e5b9e
ms.sourcegitcommit: dc12d3d0ca2ec3601cb9de7c22e61ecf22c7c514
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132264143"
---
# <a name="tutorial-extend-c-console-app-and-debug-in-visual-studio-part-2-of-2"></a>教程：扩展 C# 控制台应用并在 Visual Studio 中调试（第 2 部分，共 2 部分）

在本教程系列的第 2 部分，你将更深入地了解日常开发所需的 Visual Studio 生成和调试功能。 这些功能包括管理多个项目、调试和引用第三方包。 你将运行在[本教程的第 1 部分](tutorial-console.md)中创建的 C# 控制台应用，并在此过程中了解 Visual Studio 集成开发环境 (IDE) 的部分功能。 本教程是由两个部分构成的系列教程的第二部分。

本教程介绍以下操作：

> [!div class="checklist"]
> * 添加第二个项目。
> * 参考库并添加包。
> * 执行更多调试。
> * 检查完整的代码。


## <a name="prerequisites"></a>先决条件

按照本文进行操作时，可以使用以下任一计算器应用：

- [本教程系列第 1 部分中的计算器控制台应用](tutorial-console.md)
- [vs-tutorial-samples 存储库](https://github.com/MicrosoftDocs/vs-tutorial-samples)中的 C# 计算器应用。 要开始，请[从存储库中打开应用](../tutorial-open-project-from-repo.md)。

## <a name="add-another-project"></a>再添加一个项目

实际代码涉及在一个解决方案中协同工作的多个项目。 你可以将类库项目添加到计算器应用，该应用提供一些计算器功能。

在 Visual Studio，可以使用菜单命令“文件” > “添加” > “新项目”来添加新项目  。 也可以右键单击“解决方案资源管理器”中的解决方案，从上下文菜单中添加项目。

::: moniker range="vs-2019"
1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新项目”  。

1. 在“添加新项目”窗口的搜索框中键入“类库”。 选择 C#“类库”项目模板，然后选择“下一步” 。

   ![“类库”项目模板选项的屏幕截图。](media/vs-2019/calculator2-add-project-dark.png)

1. 在“配置新项目”屏幕中，键入项目名称 CalculatorLibrary，然后选择“下一步”。
   
1. 系统询问时，选择 .NET 3.1。 Visual Studio 将创建新项目并将其添加到解决方案中。

   ![添加了 CalculatorLibrary 类库项目的解决方案资源管理器的屏幕截图。](media/vs-2019/calculator2-solution-explorer-with-class-library-dark2.png)

1. 将 Class1.cs 文件重命名为 CalculatorLibrary.cs 。 要重命名文件，可以在“解决方案资源管理器”中右键单击该名称，然后选择“重命名”，选择该名称并按 F2，或选择该名称，然后再次单击以键入  。

   此时可能会出现一条消息，询问你是否要重命名文件中对 `Class1` 的引用。 你可以随意回答，因为你将在后续步骤中替换该代码。

1. 现在添加项目引用，以便第一个项目可以使用新类库公开的 API。 右键单击 Calculator 项目中的“依赖项”节点，然后选择“添加项目引用”  。

   ![“添加项目引用”菜单项的屏幕截图。](media/vs-2019/calculator2-add-project-reference-dark.png)

   此时将显示“引用管理器”对话框。 在此对话框中，可以添加对项目所需的其他项目、程序集和 COM DLL 的引用。

1. 在“引用管理器”对话框中，选中 CalculatorLibrary 项目对应的复选框，然后选择“确定”  。

   ![“引用管理器”对话框的屏幕截图。](media/vs-2019/calculator2-ref-manager-dark.png)

   项目引用显示在解决方案资源管理器中的“项目”节点下 。

   ![包含项目引用的解决方案资源管理器的屏幕截图。](media/vs-2019/calculator2-solution-explorer-with-project-reference-dark2.png)

1. 在 Program.cs 中，选择 `Calculator` 类及其所有代码，然后按 Ctrl+X 进行剪切 。 然后，在 CalculatorLibrary.cs 中，将代码粘贴到 `CalculatorLibrary` 命名空间中。
   
   然后，在 Calculator 类之前添加 `public`，以在库外部公开它。

   CalculatorLibrary.cs 现在应类似于以下代码：

   ```csharp
   using System;

    namespace CalculatorLibrary
    {
        public class Calculator
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
    }
   ```

1. Program.cs 也有引用，但错误指出 `Calculator.DoOperation` 调用无法解决。 这是因为 `CalculatorLibrary` 位于其他命名空间中。 对于完全限定的引用，可以将 `CalculatorLibrary` 命名空间添加到 `Calculator.DoOperation` 调用：

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   或者，你可以尝试将 `using` 指令添加到文件的开头：

   ```csharp
   using CalculatorLibrary;
   ```

   添加 `using` 指令应该可以让你从调用站点中删除 `CalculatorLibrary` 命名空间，但现在存在歧义。 `Calculator` 是 `CalculatorLibrary` 中的类？还是 `Calculator` 是命名空间？
   
   为了解决歧义，请在 Program.cs 中将命名空间从 `Calculator` 重命名为 `CalculatorProgram`。

   ```csharp
   namespace CalculatorProgram
   ```

::: moniker-end
::: moniker range=">=vs-2022"
1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新项目”  。

1. 在“添加新项目”窗口的搜索框中键入“类库”。 选择 C#“类库”项目模板，然后选择“下一步” 。

   ![“类库”项目模板选项的屏幕截图。](media/vs-2022/calculator-add-project.png)

1. 在“配置新项目”屏幕中，键入项目名称 CalculatorLibrary，然后选择“下一步”。
   
1. 在“其他信息”屏幕上，选择 .NET 6.0。 选择“创建”  。
   
   Visual Studio 将创建新项目并将其添加到解决方案中。
   
   ![添加了 CalculatorLibrary 类库项目的解决方案资源管理器的屏幕截图。](media/vs-2022/calculator-solution-explorer-with-class-library.png)

1. 将 Class1.cs 文件重命名为 CalculatorLibrary.cs 。 要重命名文件，可以在“解决方案资源管理器”中右键单击该名称，然后选择“重命名”，选择该名称并按 F2，或选择该名称，然后再次单击以键入  。

   此时可能会出现一条消息，询问你是否要重命名文件中对 `Class1` 的引用。 你可以随意回答，因为你将在后续步骤中替换该代码。

1. 现在添加项目引用，以便第一个项目可以使用新类库公开的 API。 右键单击 Calculator 项目中的“依赖项”节点，然后选择“添加项目引用”  。

   ![“添加项目引用”菜单项的屏幕截图。](media/vs-2022/calculator-add-project-reference.png)

   此时将显示“引用管理器”对话框。 在此对话框中，可以添加对项目所需的其他项目、程序集和 COM DLL 的引用。

1. 在“引用管理器”对话框中，选中 CalculatorLibrary 项目对应的复选框，然后选择“确定”  。

   ![“引用管理器”对话框的屏幕截图。](media/vs-2022/calculator-reference-manager.png)

   项目引用显示在解决方案资源管理器中的“项目”节点下 。

   ![包含项目引用的解决方案资源管理器的屏幕截图。](media/vs-2022/calculator-solution-explorer-with-project-reference.png)

1. 在 Program.cs 中，选择 `Calculator` 类及其所有代码，然后按 Ctrl+X 进行剪切 。 然后，在 CalculatorLibrary.cs 中，将代码粘贴到 `CalculatorLibrary` 命名空间中。
   
   然后，在 Calculator 类之前添加 `public`，以在库外部公开它。

   CalculatorLibrary.cs 现在应类似于以下代码：

   ```csharp
   using System;

    namespace CalculatorLibrary
    {
        public class Calculator
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
    }
   ```

1. Program.cs 也有引用，但错误指出 `Calculator.DoOperation` 调用无法解决。 这是因为 `CalculatorLibrary` 位于其他命名空间中。 对于完全限定的引用，可以将 `CalculatorLibrary` 命名空间添加到 `Calculator.DoOperation` 调用：

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   或者，你可以尝试将 `using` 指令添加到文件的开头：

   ```csharp
   using CalculatorLibrary;
   ```

   添加 `using` 指令应该可以让你从调用站点中删除 `CalculatorLibrary` 命名空间，但现在存在歧义。 `Calculator` 是 `CalculatorLibrary` 中的类？还是 `Calculator` 是命名空间？
   
   要解决歧义，请将 Program.cs 和 CalculatorLibrary.cs 中的命名空间从 `Calculator` 重命名为 `CalculatorProgram` 。

   ```csharp
   namespace CalculatorProgram
   ```
::: moniker-end

## <a name="reference-net-libraries-write-to-a-log"></a>引用 .NET 库：写入日志

你可以使用 .NET `Trace` 类添加所有操作日志，并将其写入文本文件。 `Trace` 类对于基本的打印调试技术也很有用。 `Trace` 类位于 `System.Diagnostics` 中，并使用 `System.IO` 类（如 `StreamWriter`）。

1. 首先，在 CalculatorLibrary.cs 的顶部添加 `using` 指令：

   ```csharp
   using System.IO;
   using System.Diagnostics;
   ```

1. `Trace` 类的这种用法必须保留对该类的引用，它与文件流关联。 这意味着计算器作为一个对象的工作性能将提升，所以应在 CalculatorLibrary.cs 中的 `Calculator` 类的开头添加一个构造函数。

   此外，还应删除 `static` 关键字以将静态 `DoOperation` 方法更改为成员方法。

   ```csharp
   public Calculator()
      {
          StreamWriter logFile = File.CreateText("calculator.log");
          Trace.Listeners.Add(new TextWriterTraceListener(logFile));
          Trace.AutoFlush = true;
          Trace.WriteLine("Starting Calculator Log");
          Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
      }

   public double DoOperation(double num1, double num2, string op)
      {
   ```

1. 将日志输出添加到每个计算。 `DoOperation` 现在应如以下代码所示：

   ```csharp
   public double DoOperation(double num1, double num2, string op)
   {
        double result = double.NaN; // Default value is "not-a-number" if an operation, such as division, could result in an error.

        // Use a switch statement to do the math.
        switch (op)
        {
            case "a":
                result = num1 + num2;
                Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                break;
            case "s":
                result = num1 - num2;
                Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                break;
            case "m":
                result = num1 * num2;
                Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                break;
            case "d":
                // Ask the user to enter a non-zero divisor.
                if (num2 != 0)
                {
                    result = num1 / num2;
                    Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                }
                    break;
            // Return text for an incorrect option entry.
            default:
                break;
        }
        return result;
    }
   ```

1. 回到 Program.cs，红色波浪下划线现在标记静态调用。 要修复此问题，请通过紧邻 `while (!endApp)` 循环前方添加以下代码行来创建一个 `calculator` 变量：

   ```csharp
   Calculator calculator = new Calculator();
   ```

   此外，还应修改 `DoOperation` 调用站点以引用以小写 `calculator` 命名的对象。 代码现在是成员调用，而不是对静态方法的调用。

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

1. 再次运行应用。 完成后，右键单击 Calculator 项目节点，然后选择“在文件资源管理器中打开文件夹” 。

1. 在文件资源管理器中，导航到 bin/Debug/ 下的 output 文件夹，然后打开 calculator.log 文件 。 输出应类似于：

    ```output
    Starting Calculator Log
    Started 7/9/2020 1:58:19 PM
    1 + 2 = 3
    3 * 3 = 9
    ```

此时，CalculatorLibrary.cs 应类似于以下代码：

```csharp
using System;
using System.IO;
using System.Diagnostics;


namespace CalculatorLibrary
{
    public class Calculator
    {

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                    break;
                case "s":
                    result = num1 - num2;
                    Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                    break;
                case "m":
                    result = num1 * num2;
                    Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }
}
```

Program.cs 应类似于以下代码：

```csharp
using System;
using CalculatorLibrary;

namespace CalculatorProgram
{
   
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            Calculator calculator = new Calculator();
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
                    result = calculator.DoOperation(cleanNum1, cleanNum2, op); 
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

## <a name="add-a-nuget-package-write-to-a-json-file"></a>添加 NuGet 包：写入 JSON 文件

要以 JSON（用于存储对象数据的常用可移植格式）输出操作，可以引用 Newtonsoft.Json NuGet 包。 NuGet 包是 .NET 类库的主要分发方法。

1. 在“解决方案资源管理器”中，右键单击 CalculatorLibrary 项目的“依赖项”节点，然后选择“管理 NuGet 包”   。

   ::: moniker range="vs-2019"
   ![快捷菜单上的“管理 NuGet 包”的屏幕截图。](media/vs-2019/calculator2-manage-nuget-packages-dark2.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![快捷菜单上的“管理 NuGet 包”的屏幕截图。](media/vs-2022/calculator-manage-nuget-packages.png)
   ::: moniker-end

   “NuGet 包管理器”随即打开。

   ::: moniker range="vs-2019"
   ![NuGet 包管理器的屏幕截图。](media/vs-2019/calculator2-nuget-package-manager-dark.png)
   ::: moniker-end

1. 搜索并选择 Newtonsoft.Json 包，然后选择“安装”。

   ::: moniker range="vs-2019"
   ![NuGet 包管理器中 Newtonsoft.Json NuGet 包信息的屏幕截图。](media/vs-2019/calculator2-nuget-newtonsoft-json-dark2.png)
   
   Visual Studio 下载包并将其添加到项目。 “解决方案资源管理器”的“引用”节点中随即出现一个新条目。
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![NuGet 包管理器中的 Newtonsoft.Json NuGet 包的屏幕截图。](media/vs-2022/calculator-nuget-newtonsoft-json.png)
   如果系统提示是否接受更改，请选择“确定”。
   
   Visual Studio 下载包并将其添加到项目。 “解决方案资源管理器”的“包”节点中随即出现一个新条目 。
   ::: moniker-end

1. 在 CalculatorLibrary.cs 的开头为 `Newtonsoft.Json` 添加 `using` 指令。

   ```csharp
   using Newtonsoft.Json;
   ```

1. 创建 `JsonWriter` 成员对象，将 `Calculator` 构造函数替换为以下代码：

   ```csharp
        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }
   ```

1. 修改 `DoOperation` 方法以添加 JSON `writer` 代码：

   ```csharp
        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }
   ```

1. 用户输完操作数据后，添加一个方法来完成 JSON 语法。

   ```csharp
    public void Finish()
    {
        writer.WriteEndArray();
        writer.WriteEndObject();
        writer.Close();
    }
   ```

1. 在 Program.cs 末尾的 `return;` 之前，添加对 `Finish` 的调用：

   ```csharp
            // Add call to close the JSON writer before return
            calculator.Finish();
            return;
        }
   ```

1. 生成并运行应用，然后在输入完几个操作后，输入 n 命令关闭该应用。
   
1. 在“文件资源管理器”中打开 calculatorlog.json 文件。 你应该会看到如下所示的内容：

   ```json
   {
    "Operations": [
        {
        "Operand1": 2.0,
        "Operand2": 3.0,
        "Operation": "Add",
        "Result": 5.0
        },
        {
        "Operand1": 3.0,
        "Operand2": 4.0,
        "Operation": "Multiply",
        "Result": 12.0
        }
    ]
   }
   ```

## <a name="debug-set-and-hit-a-breakpoint"></a>调试：设置并命中断点

Visual Studio 调试器是一个功能强大的工具。 调试器可以单步执行你的代码以找到存在编程错误的确切位置。 然后，你可以了解需要进行哪些更正，并进行临时更改，以便继续运行应用。

1. 在 Program.cs 中，单击以下代码行左侧的装订线。 你也可以在该行中进行单击并选择 F9，或者右键单击并选择“断点” > “插入断点”  。

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   出现的红色圆圈表示断点。 可以使用断点来暂停应用并检查代码。 可以在任意可执行代码行上设置断点。

   ![显示设置断点的屏幕截图。](media/vs-2019/calculator-2-debug-set-breakpoint.png)

1. 构建并运行应用。 为计算输入以下值：

   - 对于第一个数字，输入 8。
   - 对于第一个数字，输入 0。
   - 对于运算符，为了增添一些趣味， 我们输入 d。

   应用在你创建断点的位置（由左侧的黄色指针和突出显示的代码表示）暂停。 突出显示的代码尚未执行。

   ![展示了如何命中断点的屏幕截图](media/vs-2019/calculator-2-debug-hit-breakpoint.png)

   现在，应用已暂停，你可以检查应用程序状态了。

## <a name="debug-view-variables"></a>调试：查看变量

1. 在突出显示的代码中，将鼠标悬停在变量（如 `cleanNum1` 和 `op`）之上。 可以在数据提示中看到这些变量的当前值（分别为 `8` 和 `d`）。

   ![显示查看数据提示的屏幕截图。](media/vs-2019/calculator-2-debug-view-datatip.png)

   调试时，检查变量是否保留了你希望它们保留的值对于修复问题通常非常关键。

2. 在下面的窗格中，查看“局部变量”窗口。 如果关闭，请依次选择“调试” > “窗口” > “局部变量”将其打开  。

   在“局部变量”窗口中，可以看到当前在范围内的每个变量及其值和类型。

   ::: moniker range="vs-2019"
   ![“局部变量”窗口的屏幕截图。](media/vs-2019/calculator-2-debug-locals-window.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![“局部变量”窗口的屏幕截图。](media/vs-2022/calculator-debug-locals-window.png)
   ::: moniker-end

3. 了解一下“自动变量”窗口。

   “自动变量”窗口类似于“局部变量”窗口，不同之处在于它显示应用暂停时所处的当前代码行前后紧跟的变量。

接下来，你将在调试器中一次执行一个语句代码，这称为“单步执行”。

## <a name="debug-step-through-code"></a>调试：单步执行代码

1. 按 F11，或选择“调试” > “单步执行”  。

   如果使用的是“单步执行”命令，应用将在执行当前语句后前进到下一个可执行语句（通常是下一个代码行）。 左侧的黄色指针始终表示当前语句。

   ![展示了“单步执行”命令的屏幕截图](media/vs-2019/calculator-2-debug-step-into.png)

   你刚刚单步执行到了 `Calculator` 类中的 `DoOperation` 方法。

1. 若要分层查看程序流，请查看“调用堆栈”窗口。 如果关闭，请依次选择“调试” > “窗口” > “局部变量”将其打开  。

   ![展示了“调用堆栈”的屏幕截图](media/vs-2019/calculator-2-debug-call-stack.png)

   此视图显示当前 `Calculator.DoOperation` 方法，由黄色指针指示。 第二行显示从 Program.cs 中的 `Main` 方法调用该方法的函数。
   
   “调用堆栈”窗口显示方法和函数被调用的顺序  。 此外，通过此窗口还可以访问许多调试器功能问，例如从其快捷菜单访问“转到源代码”。

1. 按 F10（或依次选择“调试” > “不进入子函数”）几次，直到应用在 `switch` 语句处暂停  。

   ```csharp
   switch (op)
   {
   ```

   “不进入子函数”命令与“单步执行”命令类似，不同之处在于，如果当前语句调用了函数，则调试器会运行函数中的代码，并且直到函数返回结果时才会暂停执行。 如果你对某个特定函数不感兴趣，“不进入子函数”命令会比“单步执行”快。

1. 再按一次 F10，让应用在以下代码行处暂停。

   ```csharp
   if (num2 != 0)
   {
   ```

   此代码检查是否存在除以 0 的情况。 如果应用继续运行，则会引发一般性异常（错误），但你可能想要执行其他操作，例如在控制台中查看实际返回值。 一种方法是使用称为“编辑并继续”的调试器功能对代码进行更改，然后继续调试。 但是，可以使用其他技巧来临时修改执行流。

## <a name="debug-test-a-temporary-change"></a>调试：测试临时更改

1. 选择当前在 `if (num2 != 0)` 语句处暂停的黄色指针，然后将它拖到下面的语句：

   ```csharp
   result = num1 / num2;
   ```

   将指针拖到此处会使应用完全跳过 `if` 语句，让你可以看到除以零时返回的结果。

1. 按 F10 执行代码行。

1. 如果将鼠标悬停在 `result` 变量上，则会显示“无穷大”值。 在 C# 中，“无穷大”是除以 0 的结果。

1. 按 F5，或依次选择“调试” > “继续调试”  。

   无穷大符号作为数学运算的结果显示在控制台中。

1. 输入 n 命令正确关闭应用。

## <a name="code-complete"></a>代码完成

下面是完成所有步骤后 CalculatorLibrary.cs 文件的完整代码：

```csharp
using System;
using System.IO;
using System.Diagnostics;
using Newtonsoft.Json;

namespace CalculatorLibrary
{
    public class Calculator
    {

        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }

        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }

        public void Finish()
        {
            writer.WriteEndArray();
            writer.WriteEndObject();
            writer.Close();
        }
    }
}
```

下面是 Program.cs 的代码： 

```csharp
using System;
using CalculatorLibrary;

namespace CalculatorProgram
{
   
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            Calculator calculator = new Calculator();
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
                    result = calculator.DoOperation(cleanNum1, cleanNum2, op); 
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
            calculator.Finish();
            return;
        }
    }
}
```

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 要更加深入地了解，请继续学习以下内容：

- [继续学习更多 C# 教程](/dotnet/csharp/tutorials/)。
- [快速入门：创建 ASP.NET Core Web 应用](../../ide/quickstart-aspnet-core.md)。
- [了解如何在 Visual Studio 中调试 C# 代码](tutorial-debugger.md)。
- [演练如何创建和运行单元测试](../../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)。
- [运行 C# 程序](run-program.md)。
- [了解 C# IntelliSense](../../ide/visual-csharp-intellisense.md)。
- [继续学习 Visual Studio IDE 概述](visual-studio-ide.md)。
