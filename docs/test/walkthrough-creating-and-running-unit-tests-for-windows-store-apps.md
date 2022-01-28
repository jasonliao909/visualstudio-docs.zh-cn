---
title: 为通用 Windows 平台 (UWP) 应用创建并运行单元测试
description: '了解 Visual Studio 中的单元测试 UWP 应用，并使用测试驱动开发来创建 c # UWP 应用并对其进行单元测试。'
ms.custom: SEO-VS-2020
ms.date: 01/20/2022
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests
- unit tests, UWP apps
- unit tests, running
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- uwp
author: mikejo5000
ms.openlocfilehash: 60a8e08afd93d633b3492646f6d31a17d088264e
ms.sourcegitcommit: abd19232659447bc9bf946692a5de49130416bad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2022
ms.locfileid: "137831396"
---
# <a name="walkthrough-create-and-run-unit-tests-for-uwp-apps"></a>演练：创建并运行 UWP 应用的单元测试

本文介绍如何在 Visual Studio 中通用 Windows 平台 (UWP) 应用进行单元测试。 Visual Studio 提供适用于 c #、Visual Basic 和 c + + 的 UWP 单元测试项目模板。 有关开发 UWP 应用的详细信息，请参阅 [UWP 应用入门](/windows/uwp/get-started/)。

本文逐步讲解如何在 UWP 应用中创建 c # 类并对其进行单元测试。 该示例使用 [测试驱动开发](quick-start-test-driven-development-with-test-explorer.md) 来编写验证特定行为的测试，然后编写通过测试的代码。

## <a name="create-and-run-a-unit-test-project"></a>创建并运行单元测试项目

下面的过程介绍如何创建和运行 UWP 应用的单元测试项目。

### <a name="create-a-uwp-unit-test-project"></a>创建 UWP 单元测试项目

::: moniker range=">=vs-2022"

1. 在 Visual Studio **开始**"窗口中，选择"**创建新项目**"。

1. 在 " **创建新项目** " 页面上的搜索框中输入 " *单元测试* "。 模板列表筛选器到单元测试项目。

1. 针对 C# 或 Visual Basic，选择“单元测试应用(通用 Windows)”模板，然后选择“下一步”。

   :::image type="content" source="media/vs-2022/new-uwp-unit-test-app.png" alt-text="显示在 Visual Studio 中创建新 UWP 单元测试应用的屏幕截图。":::

1. （可选）更改项目或解决方案的名称和位置，然后选择“创建”。

1. （可选）更改目标和最低平台版本，然后选择“确定”。

Visual Studio 创建测试项目并在 Visual Studio **解决方案资源管理器** 中将其打开。

:::image type="content" source="media/vs-2022/uwp-unit-test-project-solution-explorer.png"  alt-text="在解决方案资源管理器中显示 UWP 单元测试项目的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2019"

1. 在 Visual Studio **开始**"窗口中，选择"**创建新项目**"。

1. 在 " **创建新项目** " 页面上的搜索框中输入 " *单元测试* "。 模板列表筛选器到单元测试项目。

1. 针对 C# 或 Visual Basic，选择“单元测试应用(通用 Windows)”模板，然后选择“下一步”。

   :::image type="content" source="media/vs-2019/new-uwp-unit-test-app.png" alt-text="显示在 Visual Studio 中创建新 UWP 单元测试应用的屏幕截图。":::

1. （可选）更改项目或解决方案的名称和位置，然后选择“创建”。

1. （可选）更改目标和最低平台版本，然后选择“确定”。

Visual Studio 创建测试项目并在 Visual Studio **解决方案资源管理器** 中将其打开。

:::image type="content" source="media/vs-2019/uwp-unit-test-project-solution-explorer.png"  alt-text="在解决方案资源管理器中显示 UWP 单元测试项目的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2017"

1. 从 **“文件”** 菜单中选择 **“新建项目”**。

   此时将显示“新建项目”对话框。

2. 在“模板”之下，选择要用以创建单元测试的编程语言，然后选择关联的 Windows 通用单元测试库。 例如，选择“Visual C#”，选择“Windows 通用”，然后选择“单元测试库(通用 Windows)”。

3. （可选）在“名称”文本框中，输入要用于项目的名称。

4. （可选）通过在“位置”文本框中输入路径，或通过选择“浏览”按钮，修改项目的创建路径。

5. （可选）在 **“解决方案”** 名称文本框中，输入要用于解决方案的名称。

6. 保持选中 **“创建解决方案的目录”** 选项并选择 **“确定”** 按钮。

   :::image type="content" source="media/unit_test_win8_1.png" alt-text="显示定制的单元测试库的屏幕截图。":::

解决方案资源管理器中会填充 UWP 单元测试项目，代码编辑器中显示标题为“UnitTest1”的默认单元测试。

:::image type="content" source="media/unit_test_win8_unittestexplorer_newprojectcreated.png" alt-text="显示新定制的单元测试项目的屏幕截图。":::

::: moniker-end

### <a name="edit-the-projects-application-manifest"></a>编辑项目的应用程序清单

1. 在 **解决方案资源管理器** 中，右键单击 *appxmanifest.xml* 文件并选择 " **打开**"。

1. 在清单设计器中，选择 " **功能** " 选项卡。

1. 在 " **功能** " 列表中，选择代码和单元测试所需的功能。 例如，如果您的代码及其单元测试需要访问 internet，请选择 " **internet** " 复选框。

仅选择单元测试正常运行所需的功能。

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/unit-test.png" alt-text="显示单元测试清单的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2019"

:::image type="content" source="media/vs-2019/unit-test.png" alt-text="显示单元测试清单的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2017"

:::image type="content" source="media/unit-test.png" alt-text="显示单元测试清单的屏幕截图。":::

::: moniker-end

### <a name="add-code-to-unit-test-the-uwp-app"></a>添加代码以对 UWP 应用进行单元测试

在 Visual Studio 代码编辑器中，编辑单元测试代码文件以添加测试所需的断言和逻辑。 有关示例，请参阅本文后面的对 [c # 类进行单元测试](#unit-test-a-c-class) 。

### <a name="run-the-unit-test-with-test-explorer"></a>在测试资源管理器中运行单元测试

::: moniker range=">=vs-2022"

使用 **测试资源管理器** 生成解决方案并运行单元测试。

1. 在 Visual Studio **测试**"菜单上，选择"**测试资源管理器**"。 此时将打开“测试资源管理器”窗口。

1. 在 **测试资源管理器** 中，选择 " **全部运行** " 图标。 必须使用 " **全部运行** " 来发现 UWP 项目中的测试。

   :::image type="content" source="media/vs-2022/test-explorer.png" alt-text="显示 &quot;测试资源管理器全部运行&quot; 图标的屏幕截图。":::

解决方案将生成并运行单元测试。 测试运行后，测试将显示在 **测试资源管理器** 测试列表中，其中包含有关结果和持续时间的信息。

:::image type="content" source="media/vs-2022/test-explorer-run.png" alt-text="显示具有已完成测试信息的测试资源管理器的屏幕截图。":::

此外，在 " **测试资源管理器**" 中，可以选择单个测试，然后右键单击以 **运行** 或 **调试** 测试，或选择 " **开始测试** " 以打开测试代码。 在顶部菜单中，可以对测试进行分组、将测试添加到播放列表或打开测试选项。

:::image type="content" source="media/vs-2022/test-explorer-done.png" alt-text="显示测试资源管理器上下文菜单的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2019"

使用 **测试资源管理器** 生成解决方案并运行单元测试。 

1. 在 Visual Studio **测试**"菜单上，选择"**测试资源管理器**"。 此时将打开“测试资源管理器”窗口。

1. 在 **测试资源管理器** 中，选择 " **全部运行** " 图标。 必须使用 " **全部运行** " 来发现 UWP 项目中的测试。

   :::image type="content" source="media/vs-2019/test-explorer.png" alt-text="显示 &quot;测试资源管理器全部运行&quot; 图标的屏幕截图。":::

解决方案将生成并运行单元测试。 测试运行后，测试将显示在 **测试资源管理器** 测试列表中，其中包含有关结果和持续时间的信息。

:::image type="content" source="media/vs-2019/test-explorer-run.png" alt-text="显示具有已完成测试信息的测试资源管理器的屏幕截图。":::

此外，在 " **测试资源管理器**" 中，可以选择单个测试，然后右键单击以 **运行** 或 **调试** 测试，或选择 " **开始测试** " 以打开测试代码。 在顶部菜单中，可以对测试进行分组、将测试添加到播放列表或打开测试 **选项**。

:::image type="content" source="media/vs-2019/test-explorer-done.png" alt-text="显示测试资源管理器上下文菜单的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2017"

生成解决方案并在测试资源管理器中运行单元测试：

1. 在 "Visual Studio **测试**" 菜单上，选择 " **Windows**"，然后选择 "**测试资源管理器**"。 此时将打开“测试资源管理器”窗口。

1. 从 **“生成”** 菜单中选择 **“生成解决方案”** 。  现在，你的单元测试将显示在 **测试资源管理器** 中。

   > [!NOTE]
   > 必须生成解决方案，才能在 " **测试资源管理器**" 中更新单元测试列表。

1. 在 **测试资源管理器** 中，选择你创建的单元测试，然后选择 " **全部运行**"。

   :::image type="content" source="media/unit-test-run.png" alt-text="显示 &quot;测试资源管理器全部运行&quot; 命令的屏幕截图。":::

解决方案将生成并运行单元测试。 测试运行后，测试将显示在 **测试资源管理器** 测试列表中，其中包含有关结果和持续时间的信息。

:::image type="content" source="media/unit-test-done.png" alt-text="显示具有已完成测试信息的测试资源管理器的屏幕截图。":::

> [!TIP]
> 可以选择测试资源管理器中列出的一个或多个单元测试，然后右击并选择“运行选定测试”。
>
> 还可以选择 **调试选定的测试**， **打开测试**，并使用 **Properties** 选项。
>
> :::image type="content" source="media/unit-test-context-menu.png" alt-text="显示测试资源管理器上下文菜单的屏幕截图。":::

::: moniker-end

## <a name="unit-test-a-c-class"></a>对 c # 类进行单元测试

一组稳定的良好单元测试可提高你在更改代码时未引入 bug 的置信度。 下面的示例演示了一种为 UWP 应用中的 c # 类创建单元测试的方法。 该示例使用 *测试驱动开发* 来编写验证特定行为的测试，然后编写通过测试的代码。

在示例 **Maths** 代码项目中， **Rooter** 类实现了一个函数，该函数计算数字的估计平方根。 **RooterTests** 项目单元测试 **Rooter** 类。

### <a name="create-the-solution-and-projects"></a>创建解决方案和项目

创建 UWP 应用项目：

1. 在 Visual Studio **文件**"菜单上，选择"**新建 Project**"。
1. 在 "**创建新项目**" 页面上的 "搜索" 框中输入 *空白应用*，然后选择 c #**空白应用 (通用 Windows)** 项目模板。
1. 在 " **配置新项目** " 页上，将项目命名为 *Maths*，然后选择 " **创建**"。
1. （可选）更改目标和最低平台版本，然后选择“确定”。 Visual Studio 创建项目并在 **解决方案资源管理器** 中打开它。

创建单元测试项目：

1. 在 **解决方案资源管理器** 中，右键单击 **Maths** 解决方案，然后选择 "**添加**" "  >  **新建 Project**"。
1. 在 "**添加新项目**" 页上，在 "搜索" 框中输入 "*单元测试*"，然后选择 "c #**单元测试应用 (通用 Windows)** 项目模板。
1. 将测试项目命名为 *RooterTests*，然后选择 " **创建**"。
1. （可选）更改目标和最低平台版本，然后选择“确定”。 **RooterTests** 项目显示在 "**解决方案资源管理器** 中的 **Maths** 解决方案下。

### <a name="verify-that-tests-run-in-test-explorer"></a>验证测试是否在测试资源管理器中运行

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 类提供了几个可以用来验证测试方法结果的静态方法。

::: moniker range=">=vs-2019"

1. 在 **解决方案资源管理器** 中，选择 **RooterTests** 项目中的 *UnitTest* 文件。

1. 将以下代码插入到中 `TestMethod1` ：

   ```csharp
   [TestMethod]
   public void TestMethod1()
   {
       Assert.AreEqual(0, 0);
   }
   ```

1. 在 **测试资源管理器** 中，选择 " **运行所有测试**"。

1. 测试项目将生成并运行，测试显示在 " **通过的测试**" 下。 右侧的 " **组摘要** " 窗格提供有关测试的详细信息。

::: moniker-end

::: moniker range="vs-2017"


1. 在 **解决方案资源管理器** 中，选择 **RooterTests** 项目中的 *UnitTest* 文件。

1. 将以下代码插入到中 `TestMethod1` ：

   ```csharp
   [TestMethod]
   public void TestMethod1()
   {
       Assert.AreEqual(0, 0);
   }
   ```

1. 在“测试”菜单中，选择“运行”>“所有测试”。

将生成并运行测试项目。 此时将显示 " **测试资源管理器** " 窗口，并在 " **通过的测试**" 下显示测试。 窗口底部的 "摘要" 窗格提供有关所选测试的更多详细信息。


::: moniker-end

### <a name="add-a-class-to-the-app-project"></a>向应用程序项目添加类

::: moniker range=">=vs-2022"

1. 在 **解决方案资源管理器** 中，右键单击 **Maths** 项目，然后选择 " **添加** > **类**"。

1. 将该类文件命名为 *Rooter*，然后选择 " **添加**"。

1. 在代码编辑器中，将以下代码添加到 `Rooter` *Rooter* 文件中的类：

   ```csharp
   public Rooter()
   {
   }
   
   // estimate the square root of a number
   public double SquareRoot(double x)
   {
       return 0.0;
   }
   ```

   `Rooter` 类声明一个构造函数和 `SquareRoot` estimator 方法。 `SquareRoot`方法是测试基本测试设置的最小实现。

1. `internal` `public` 在类声明中将关键字更改为 `Rooter` ，以便测试代码能够访问它。

   ```csharp
   public class Rooter
   ```
::: moniker-end

::: moniker range="<=vs-2019"

1. 在 **解决方案资源管理器** 中，右键单击 **Maths** 项目，然后选择 " **添加** > **类**"。

1. 将该类文件命名为 *Rooter*，然后选择 " **添加**"。

1. 在代码编辑器中，将以下代码添加到 `Rooter` *Rooter* 文件中的类：

   ```csharp
   public Rooter()
   {
   }
   
   // estimate the square root of a number
   public double SquareRoot(double x)
   {
       return 0.0;
   }
   ```

   `Rooter` 类声明一个构造函数和 `SquareRoot` estimator 方法。 `SquareRoot`方法是测试基本测试设置的最小实现。

1. 将 `public` 关键字添加到 `Rooter` 类声明，以便测试代码能够访问它。

   ```csharp
   public class Rooter
   ```
::: moniker-end

### <a name="add-a-reference-from-the-test-project-to-the-app-project"></a>向应用程序项目添加对测试项目的引用

::: moniker range=">=vs-2022"

1. 在 **解决方案资源管理器** 中，右键单击 **RooterTests** 项目，然后选择 " **添加** > **引用**"。

1. 在 " **引用管理器-RooterTests** " 对话框中，展开 " **项目**"，然后选择 " **Maths** " 项目。

   :::image type="content" source="media/vs-2022/add-reference.png" alt-text="屏幕截图，显示添加对 Maths 项目的引用。":::

1. 选择“确定”  。

1. 将以下 `using` 语句添加到 *UnitTest* 中的以下 `using Microsoft.VisualStudio.TestTools.UnitTesting;` 行：

   ```csharp
   using Maths;
   ```
::: moniker-end

::: moniker range="vs-2019"

1. 在 **解决方案资源管理器** 中，右键单击 **RooterTests** 项目，然后选择 " **添加** > **引用**"。

1. 在 " **引用管理器-RooterTests** " 对话框中，展开 " **项目**"，然后选择 " **Maths** " 项目。

   :::image type="content" source="media/ute_cs_windows_addreference.png" alt-text="屏幕截图，显示添加对 Maths 项目的引用。":::

1. 选择“确定”  。

1. 将以下 `using` 语句添加到 *UnitTest* 中的以下 `using Microsoft.VisualStudio.TestTools.UnitTesting;` 行：

   ```csharp
   using Maths;
   ```
::: moniker-end

::: moniker range="vs-2017"


1. 在 **解决方案资源管理器** 中，右键单击 **RooterTests** 项目，然后选择 " **添加** > **引用**"。

1. 在 " **引用管理器-RooterTests** " 对话框中，展开 " **项目**"，然后选择 " **Maths** " 项目。

   :::image type="content" source="media/add-reference.png" alt-text="屏幕截图，显示添加对 Maths 项目的引用。":::

1. 选择“确定”  。

1. 将以下 `using` 语句添加到 *UnitTest* 中的以下 `using Microsoft.VisualStudio.TestTools.UnitTesting;` 行：

   ```csharp
   using Maths;
   ```
::: moniker-end

### <a name="add-a-test-that-uses-the-app-function"></a>添加使用应用函数的测试

1. 将以下测试方法添加到 *UnitTest*：

   ```csharp
   [TestMethod]
   public void BasicTest()
   {
       Maths.Rooter rooter = new Rooter();
       double expected = 0.0;
       double actual = rooter.SquareRoot(expected * expected);
       double tolerance = .001;
       Assert.AreEqual(expected, actual, tolerance);
   }
   ```

   新测试将显示在 "**测试资源管理器**" 的 "**未运行的测试**" 节点中 **解决方案资源管理器** 和。

1. 若要避免 "负载包含两个或多个具有相同目标路径的文件" 错误，请在 **解决方案资源管理器** 中展开 " **Maths** " 项目下的 "**属性**" 节点，并删除 *Default.rd.xml* 文件。

1. 保存所有文件。

### <a name="run-the-tests"></a>运行测试

::: moniker range=">=vs-2022"

在 **测试资源管理器** 中，选择 " **运行所有测试** " 图标。 解决方案生成，测试运行并通过。

:::image type="content" source="media/vs-2022/test-explorer-uwp-app.png" alt-text="在测试资源管理器中显示基本测试的屏幕截图":::


::: moniker-end

::: moniker range="vs-2019"

在 **测试资源管理器** 中，选择 " **运行所有测试** " 图标。 解决方案生成，测试运行并通过。

:::image type="content" source="media/vs-2019/test-explorer-uwp-app.png" alt-text="在测试资源管理器中显示基本测试的屏幕截图":::


::: moniker-end

::: moniker range="vs-2017"

在“测试资源管理器”中，选择“全部运行”。 解决方案生成，测试运行并通过。

:::image type="content" source="media/ute_cpp_testexplorer_basictest.png" alt-text="在测试资源管理器中显示 BasicTest 的屏幕截图":::


::: moniker-end

你已设置测试和应用项目，并已验证可运行测试（调用应用项目中的函数）。 现在可以编写真实测试和代码。

### <a name="add-tests-and-make-them-pass"></a>添加测试并使它们通过

最好不要更改已通过的测试。 改为添加新测试。 通过一次添加一个测试来开发代码，并确保所有测试在每次迭代后都通过。

::: moniker range=">=vs-2022"

1. 将名为的新测试添加 `RangeTest` 到 *UnitTest*：

   ```csharp
   [TestMethod]
   public void RangeTest()
   {
       Rooter rooter = new Rooter();
       for (double v = 1e-6; v < 1e6; v = v * 3.2)
       {
           double expected = v;
           double actual = rooter.SquareRoot(v*v);
           double tolerance = expected/1000;
           Assert.AreEqual(expected, actual, tolerance);
       }
   }
   ```

1. 运行 RangeTest 测试并验证它是否失败。

   :::image type="content" source="media/vs-2022/test-explorer-rangetest-fail.png" alt-text="在测试资源管理器中显示 Rangetest 未通过失败的屏幕截图。":::

   > [!TIP]
   > 在测试驱动的开发中，您可以在编写测试后立即运行测试。 这种做法有助于避免编写从不失败的测试的简单错误。

1. 修复应用程序代码，以便新测试通过。 在 *Rooter* 中，按如下所示更改 `SquareRoot` 函数：

   ```csharp
   public double SquareRoot(double x)
   {
       double estimate = x;
       double diff = x;
       while (diff > estimate / 1000)
       {
           double previousEstimate = estimate;
           estimate = estimate - (estimate * estimate - x) / (2 * estimate);
           diff = Math.Abs(previousEstimate - estimate);
       }
       return estimate;
   }
   ```

1. 在 **测试资源管理器** 中，选择 " **运行所有测试** " 图标。 现在所有三个测试都将通过。

::: moniker-end

::: moniker range="vs-2019"

1. 将名为的新测试添加 `RangeTest` 到 *UnitTest*：

   ```csharp
   [TestMethod]
   public void RangeTest()
   {
       Rooter rooter = new Rooter();
       for (double v = 1e-6; v < 1e6; v = v * 3.2)
       {
           double expected = v;
           double actual = rooter.SquareRoot(v*v);
           double tolerance = expected/1000;
           Assert.AreEqual(expected, actual, tolerance);
       }
   }
   ```

1. 运行 RangeTest 测试并验证它是否失败。

   :::image type="content" source="media/vs-2019/test-explorer-rangetest-fail.png" alt-text="在测试资源管理器中显示 Rangetest 未通过失败的屏幕截图。":::

   > [!TIP]
   > 在测试驱动的开发中，您可以在编写测试后立即运行测试。 这种做法有助于避免编写从不失败的测试的简单错误。

1. 修复应用程序代码，以便新测试通过。 在 *Rooter* 中，按如下所示更改 `SquareRoot` 函数：

   ```csharp
   public double SquareRoot(double x)
   {
       double estimate = x;
       double diff = x;
       while (diff > estimate / 1000)
       {
           double previousEstimate = estimate;
           estimate = estimate - (estimate * estimate - x) / (2 * estimate);
           diff = Math.Abs(previousEstimate - estimate);
       }
       return estimate;
   }
   ```

1. 在 **测试资源管理器** 中，选择 " **运行所有测试** " 图标。 现在所有三个测试都将通过。

::: moniker-end

::: moniker range="vs-2017"

1. 将名为的新测试添加 `RangeTest` 到 *UnitTest*：

   ```csharp
   [TestMethod]
   public void RangeTest()
   {
       Rooter rooter = new Rooter();
       for (double v = 1e-6; v < 1e6; v = v * 3.2)
       {
           double expected = v;
           double actual = rooter.SquareRoot(v*v);
           double tolerance = expected/1000;
           Assert.AreEqual(expected, actual, tolerance);
       }
   }
   ```

1. 运行 RangeTest 测试并验证它是否失败。

   :::image type="content" source="media/range-test-fail.png" alt-text="在测试资源管理器中显示 Rangetest 未通过失败的屏幕截图。":::

   > [!TIP]
   > 在测试驱动的开发中，您可以在编写测试后立即运行测试。 这种做法有助于避免编写从不失败的测试的简单错误。

1. 修复应用程序代码，以便新测试通过。 在 *Rooter* 中，按如下所示更改 `SquareRoot` 函数：

   ```csharp
   public double SquareRoot(double x)
   {
       double estimate = x;
       double diff = x;
       while (diff > estimate / 1000)
       {
           double previousEstimate = estimate;
           estimate = estimate - (estimate * estimate - x) / (2 * estimate);
           diff = Math.Abs(previousEstimate - estimate);
       }
       return estimate;
   }
   ```

1. 在“测试资源管理器”中，选择“全部运行”。 现在所有三个测试都将通过。

::: moniker-end

### <a name="refactor-the-code"></a>重构代码

在本部分，你将重构应用和测试代码，然后重新运行测试以确保它们仍然通过。

#### <a name="simplify-the-square-root-estimation"></a>简化平方根估算

1. 在 *Rooter.cs* 中，通过更改以下行来简化函数 `SquareRoot` 中的中心计算：

   `estimate = estimate - (estimate * estimate - x) / (2 * estimate);`

   如果

   `estimate = (estimate + x/estimate) / 2.0;`

1. 运行所有测试，确保尚未引入回归。 测试应全部通过。

#### <a name="remove-duplicate-test-code"></a>删除重复的测试代码

`RangeTest`方法对传递给 方法的 `tolerance` 变量的分母进行 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 硬编码。 如果计划添加更多使用相同公差计算的测试，则多个位置使用硬编码值会使代码更难维护。 相反，可以将专用帮助程序方法添加到 类以计算 `UnitTest1` 公差值，然后从 调用该方法 `RangeTest` 。

若要添加帮助程序方法，在 *UnitTest.cs 中：*

1. 将以下方法添加到 `UnitTest1` 类：

   ```csharp
   private double ToleranceHelper(double expected)
   {
   return expected / 1000;
   }
   ```

1. 在 `RangeTest` 中，更改以下行：

   `double tolerance = expected/1000;`

   如果

   `double tolerance = ToleranceHelper(expected);`

1. 运行 **RangeTest** 测试以确保它仍然通过。

> [!TIP]
> 如果将帮助程序方法添加到测试类，并且不希望帮助程序方法出现在测试资源管理器的列表中，请不要将 属性添加到 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 方法。

## <a name="next-steps"></a>后续步骤

- [单元测试工具和任务](../test/unit-test-your-code.md)
- [演练：创建并运行托管代码的单元测试](walkthrough-creating-and-running-unit-tests-for-managed-code.md)
- [演练：通过测试资源管理器进行测试驱动开发](quick-start-test-driven-development-with-test-explorer.md)
