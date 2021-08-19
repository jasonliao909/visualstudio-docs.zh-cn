---
title: 了解如何使用实时单元测试测试代码
description: 通过创建面向 .NET Standard 的简单类库了解 Live Unit Testing 的用法，并通过创建面向 .NET Core 的 MSTest 项目对其进行测试。
ms.custom: SEO-VS-2020
ms.date: 04/03/2020
ms.topic: how-to
helpviewer_keywords:
- Live Unit Testing
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- dotnet
ms.openlocfilehash: 2041845ab82ec539ccaec0befd3275aeab7c0493
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148462"
---
# <a name="get-started-with-live-unit-testing"></a>Live Unit Testing 入门

在 Visual Studio 解决方案中启用 Live Unit Testing 后，它可以直观描述测试覆盖率和测试状态。 Live Unit Testing 还会在你每次修改代码时动态执行测试，并在更改导致测试失败时立即发出通知。

Live Unit Testing 可用于测试针对 .NET Framework 或 .NET Core 的解决方案。 本教程将通过创建面向 .NET Standard 的简单类库来说明 Live Unit Testing 的用法，并创建面向 .NET Core 的 MSTest 项目来对其进行测试。

可从 GitHub 上的 [MicrosoftDocs/visualstudio-docs](https://github.com/MicrosoftDocs/visualstudio-docs/tree/master/docs/test/samples/csharp/UtilityLibraries/) 存储库下载完整的 C# 解决方案。

## <a name="prerequisites"></a>先决条件

本教程需要已安装具有 .NET Core 跨平台开发工作负载的 Visual Studio Enterprise Edition  。

## <a name="create-the-solution-and-the-class-library-project"></a>创建解决方案和类库项目

首先，创建名为 UtilityLibraries 的 Visual Studio 解决方案，其中包含单个 .NET Standard 类库项目 StringLibrary。

解决方案只是一个可以存储一个或多个项目的容器。 要创建空白解决方案，请打开 Visual Studio 并执行以下操作：

1. 从顶级的 Visual Studio 菜单中依次选择“文件” > “新建” > “项目”    。

1. 在模板搜索框中键入“解决方案”，然后选择“空白解决方案”模板   。 将该项目命名为“UtilityLibraries”  。

   ::: moniker range="vs-2017"

   ![“新建项目”对话框](./media/lut-start/new-solution.png)

   ::: moniker-end

1. 完成解决方案的创建。

现在已创建解决方案，接下来需要创建一个名为 StringLibrary 的类库，其中包含大量用于处理字符串的扩展方法。

1. 在“解决方案资源管理器”中，右键单击 UtilityLibraries 解决方案，然后选择“添加” > “新建项目”    。

::: moniker range="vs-2017"

2. 在“添加新项目”对话框中，选择 C# 节点，然后选择“.NET Standard”   。

   > [!NOTE]
   > 由于我们的库是针对 .NET Standard，而不是特定的 .NET 实现，因此可以从支持此 .NET Standard 的任何 .NET 实现对其进行调用。 有关详细信息，请参阅 [.NET Standard](/dotnet/standard/net-standard)。

3. 在右窗格中选择“类库(.NET Standard)”模板，然后在“名称”文本框中输入“StringLibrary”，如下图所示    ：

   ![“添加新项目”对话框](./media/lut-start/add-project-cs.png)

4. 选择“确定”创建项目  。

::: moniker-end

::: moniker range=">=vs-2019"

2. 在模板搜索框中键入“类库”，然后选择“类库(.NET Standard)”模板   。 单击 **“下一步”** 。

   > [!NOTE]
   > 由于我们的库是针对 .NET Standard，而不是特定的 .NET 实现，因此可以从支持此 .NET Standard 的任何 .NET 实现对其进行调用。 有关详细信息，请参阅 [.NET Standard](/dotnet/standard/net-standard)。

3. 将该项目命名为“StringLibrary”  。

4. 单击“创建”以创建项目  。

::: moniker-end

5. 将代码编辑器中的所有现有代码替换为以下代码：

   ```csharp
   using System;

   namespace UtilityLibraries
   {
       public static class StringLibrary
       {
           public static bool StartsWithUpper(this string s)
           {
               if (String.IsNullOrWhiteSpace(s))
                   return false;

               return Char.IsUpper(s[0]);
           }

           public static bool StartsWithLower(this string s)
           {
               if (String.IsNullOrWhiteSpace(s))
                   return false;

               return Char.IsLower(s[0]);
           }

           public static bool HasEmbeddedSpaces(this string s)
           {
               foreach (var ch in s.Trim())
               {
                   if (ch == ' ')
                       return true;
               }
               return false;
           }
       }
   }
   ```

   StringLibrary 有三种静态方法：

   - 如果字符串以大写字符开头，则 `StartsWithUpper` 返回 `true`；否则返回 `false`。

   - 如果字符串以小写字符开头，则 `StartsWithLower` 返回 `true`；否则返回 `false`。

   - 如果字符串包含嵌入的空格字符，则 `HasEmbeddedSpaces` 返回 `true`；否则返回 `false`。

6. 从顶级 Visual Studio 菜单中依次选择“生成” > “生成解决方案”   。 生成应该成功。

## <a name="create-the-test-project"></a>创建测试项目

下一步是创建单元测试项目，以测试 StringLibrary 库。 通过执行以下步骤创建单元测试：

1. 在“解决方案资源管理器”中，右键单击 UtilityLibraries 解决方案，然后选择“添加” > “新建项目”    。

::: moniker range="vs-2017"

2. 在“添加新项目”对话框中，选择 C# 节点，然后选择“.NET Core”   。

   > [!NOTE]
   > 不需要使用与类库相同的语言编写单元测试。

3. 在右窗格中选择“单元测试项目(.NET Core)”模板，然后在“名称”文本框中输入“StringLibraryTests”，如下图所示    ：

   ![单元测试项目的“添加新项目”对话框](./media/lut-start/add-unit-test-cs.png)

4. 选择“确定”创建项目  。

   > [!NOTE]
   > 此入门教程使用 Live Unit Testing 的 MSTest 测试框架。 还可使用 xUnit 和 NUnit 测试框架。

::: moniker-end

::: moniker range=">=vs-2019"

2. 在模板搜索框中键入“单元测试”，选择“C#”作为语言，然后对 .NET Core 选择“单元测试项目”模板  。 单击“下一步”  。

   > [!NOTE]
   > 从 Visual Studio 2019 版本 16.9 开始，MSTest 项目模板名称已从“MSTest 单元测试项目(.NET Core)”更改为“单元测试项目”。

3. 将项目命名为“StringLibraryTests”，然后单击“下一步”。

4. 选择建议的目标框架 (.NET Core 3.1) 或 .NET 5，然后选择“创建”。

   > [!NOTE]
   > 此入门教程使用 Live Unit Testing 的 MSTest 测试框架。 还可使用 xUnit 和 NUnit 测试框架。

::: moniker-end

5. 单元测试项目无法自动访问它正在测试的类库。 可以通过添加对类库项目的引用来提供测试库访问权限。 为此，请右键单击 `StringLibraryTests` 项目，然后依次选择“添加” > “引用”   。 在“引用管理器”对话框中，确保“解决方案”选项卡处于选中状态，然后选择 StringLibrary 项目，如下图所示   。

   ![“引用管理器”对话框](./media/lut-start/add-reference.png)

6. 将模板提供的样本单元测试代码替换为以下代码：

   ```csharp
   using System;
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using UtilityLibraries;

   namespace StringLibraryTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestStartsWithUpper()
           {
               // Tests that we expect to return true.
               string[] words = { "Alphabet", "Zebra", "ABC", "Αθήνα", "Москва" };
               foreach (var word in words)
               {
                   bool result = word.StartsWithUpper();
                   Assert.IsTrue(result,
                                 $"Expected for '{word}': true; Actual: {result}");
               }
           }

           [TestMethod]
           public void TestDoesNotStartWithUpper()
           {
               // Tests that we expect to return false.
               string[] words = { "alphabet", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                                  "1234", ".", ";", " " };
               foreach (var word in words)
               {
                   bool result = word.StartsWithUpper();
                   Assert.IsFalse(result,
                                  $"Expected for '{word}': false; Actual: {result}");
               }
           }

           [TestMethod]
           public void DirectCallWithNullOrEmpty()
           {
               // Tests that we expect to return false.
               string[] words = { String.Empty, null };
               foreach (var word in words)
               {
                   bool result = StringLibrary.StartsWithUpper(word);
                   Assert.IsFalse(result,
                                  $"Expected for '{(word == null ? "<null>" : word)}': " +
                                  $"false; Actual: {result}");
               }
           }
       }
   }
   ```

7. 通过选择工具栏上的“保存”图标来保存你的项目  。

   由于单元测试代码包含一些非 ASCII 字符，因此将显示以下对话框来进行警告，如果以其默认的 ASCII 格式保存文件，某些字符将会丢失。

8. 选择“以其他编码保存”按钮  。

   ![选择文件编码](media/lut-start/ascii-encoding.png)

9. 在“高级保存选项”对话框的“编码”下拉列表中，选择“Unicode (UTF-8 无签名) - 代码页 65001”，如下图所示    ：

   ![选择 UTF-8 编码](media/lut-start/utf8-encoding.png)

10. 从顶级 Visual Studio 菜单中选择“生成” > “重新生成解决方案”，编译单元测试项目   。

已创建一个类库并为其编写了几个单元测试。 现在已完成使用 Live Unit Testing 所需的预备工作。

## <a name="enable-live-unit-testing"></a>启用 Live Unit Testing

到目前为止，尽管已为 StringLibrary 类库编写测试，但尚未执行。 启用 Live Unit Testing 后，就会自动执行这些测试。 为此，请执行以下操作：

1. 选择包含 StringLibrary 代码的代码编辑器窗口（可选）。 可以是 C# 项目的 Class1.cs，或者 Visual Basic 项目的 Class1.vb   。 （启用 Live Unit Testing 后，通过此步骤可直观检查测试结果和代码覆盖率的范围。）

1. 从顶级 Visual Studio 菜单中依次选择“测试” > “Live Unit Testing” > “启动”    。

1. Visual Studio 启动 Live Unit Testing，使其自动运行所有测试。

::: moniker range="vs-2017"
完成运行测试后，“测试资源管理器”显示整体结果和各个测试的结果  。 此外，代码编辑器窗口以图形方式显示测试代码覆盖率和测试结果。 如下图所示，三项测试均已成功执行。 它还显示测试中已覆盖 `StartsWithUpper` 方法中的所有代码路径，并已成功执行这些测试（用绿色复选标记“✓”指示）。 最后，显示 StringLibrary 中的其他方法都没有代码覆盖率（用蓝线“➖”指示）。

![启动 Live Unit testing 后的测试资源管理器和代码编辑器窗口](media/lut-start/lut-results-cs.png)
::: moniker-end
::: moniker range=">=vs-2019"
运行完测试后，Live Unit Testing 同时显示总体结果和各个测试的结果  。 此外，代码编辑器窗口以图形方式显示测试代码覆盖率和测试结果。 如下图所示，三项测试均已成功执行。 它还显示测试中已覆盖 `StartsWithUpper` 方法中的所有代码路径，并已成功执行这些测试（用绿色复选标记“✓”指示）。 最后，显示 StringLibrary 中的其他方法都没有代码覆盖率（用蓝线“➖”指示）。

![启动 Live Unit testing 后的实时测试资源管理器和代码编辑器窗口](media/lut-start/vs-2019/lut-results-cs.png)
::: moniker-end

还可通过在代码编辑器窗口中选择一个特定的代码覆盖率图标来获得有关测试覆盖率和测试结果的更多详细信息。 若要查看此详细信息，请执行以下操作：

1. 单击 `StartsWithUpper` 方法中写着 `if (String.IsNullOrWhiteSpace(s))` 的行上的绿色复选标记。 如下图所示，Live Unit Testing 指示三个测试均覆盖该代码行，并且都已成功执行。

   ![`if` 条件语句的代码覆盖率](media/lut-start/code-coverage-cs1.png)

1. 单击 `StartsWithUpper` 方法中写着 `return Char.IsUpper(s[0])` 的行上的绿色复选标记。 如下图所示，Live Unit Testing 指示只有两个测试均覆盖该代码行，并且都已成功执行。

   ![return 语句的代码覆盖率](media/lut-start/code-coverage-cs2.png)

Live Unit Testing 标识的主要问题是代码覆盖率不完整。 此问题将在下一部分得以解决。

## <a name="expand-test-coverage"></a>展开测试覆盖率

此部分将把单元测试扩展到 `StartsWithLower` 方法。 执行此操作时，Live Unit Testing 将以动态方式继续测试代码。

若要将代码覆盖率扩展到 `StartsWithLower` 方法，请执行以下操作：

1. 将以下 `TestStartsWithLower` 和 `TestDoesNotStartWithLower` 添加到项目的测试源代码文件中：

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/unittest2.cs" id="Snippet1":::

1. 在调用 [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsFalse`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.isfalse) 方法之后，立即添加以下代码来修改 `DirectCallWithNullOrEmpty` 方法。

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/unittest2.cs" id="Snippet2":::

1. 在你修改源代码时，Live Unit Testing 将自动执行新增的和修改后的测试。 如下图所示，所有测试（包括已添加的两个测试和已修改的测试）都已成功。

   ::: moniker range="vs-2017"
   ![展开测试覆盖率之后的测试资源管理器](media/lut-start/test-dynamic.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![展开测试覆盖率之后的实时测试资源管理器](media/lut-start/vs-2019/test-dynamic.png)
   ::: moniker-end

1. 切换到包含 StringLibrary 类源代码的窗口。 Live Unit Testing 现在显示代码覆盖率已扩展到 `StartsWithLower` 方法。

    ![StartsWithLower 方法的代码覆盖率](media/lut-start/lut-extended-cs.png)

在某些情况下，“测试资源管理器”中的成功测试可能会灰显  。指示某个测试当前正在执行，或测试没有再次运行，因为测试自上次执行之后不会受到任何代码更改带来的影响。

到目前为止，所有测试都已成功。 在接下来的部分中，我们将讨论如何处理测试失败的问题。

## <a name="handle-a-test-failure"></a>处理测试失败

此部分将介绍如何使用 Live Unit Testing 标识、故障排除并解决测试失败的问题。 需要将测试覆盖率扩展到 `HasEmbeddedSpaces` 方法来执行此操作。

1. 将以下方法添加到测试文件：

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/unittest2.cs" id="Snippet3":::

1. 测试执行时，Live Unit Testing 指示 `TestHasEmbeddedSpaces` 方法失败，如下图所示：

   ::: moniker range="vs-2017"
   ![报告失败的测试的测试资源管理器](media/lut-start/test-failure.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![报告失败测试的实时测试资源管理器](media/lut-start/vs-2019/test-failure.png)
   ::: moniker-end

1. 选择显示库代码的窗口。 Live Unit Testing 已将代码覆盖率扩展到 `HasEmbeddedSpaces` 方法。 它还报告测试失败，方法是将一个红色“🞩”添加到被失败的测试覆盖的行。

1. 将鼠标悬停在有 `HasEmbeddedSpaces` 方法签名的行上。 Live Unit Testing 会显示一个工具提示，报告该方法被某个测试覆盖，如下图所示：

   ![关于失败的测试的 Live Unit Testing 信息](media/lut-start/test-failure-info-cs.png)

1. 选择失败的“TestHasEmbeddedSpaces”测试  。 Live Unit Testing 提供了几个选项，如运行所有测试和调试所有测试，如下图所示：

   ::: moniker range="vs-2017"
   ![失败的测试的 Live Unit Testing 选项](media/lut-start/test-failure-options.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![失败的测试的 Live Unit Testing 选项](media/lut-start/vs-2019/test-failure-options.png)
   ::: moniker-end

1. 选择“全部调试”，调试失败的测试  。

1. Visual Studio 在调试模式下执行测试。

   测试将数组中的每个字符串分配给名为 `phrase` 的变量，并将其传递给 `HasEmbeddedSpaces` 方法。 程序执行暂停，并在断言表达式第一次为 `false` 时调用调试程序。 下图显示了 [`Microsoft.VisualStudio.TestTools.UnitTesting.Assert.IsTrue`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert.istrue) 方法调用中的意外值导致的异常对话框。

   ![Live Unit Testing 异常对话框](media/lut-start/exception-dialog-cs.png)

   此外，Visual Studio 提供的所有调试工具均可帮助我们对失败的测试进行故障排除，如下图所示：

   ![Visual Studio 调试工具](media/lut-start/debugging-tools-cs.png)

   请注意，在“自动”窗口中，`phrase` 变量的值是“Name\tDescription”，它是数组的第二个元素  。 测试方法需要 `HasEmbeddedSpaces` 在传递该字符串时返回 `true`；而它返回 `false`。 显然，这是因为它无法将制表符“\t”识别为嵌入的空格。

1. 请依次选择“调试” > “继续”，按 F5 或单击单击工具栏上的“继续”按钮，继续执行该测试程序     。 由于出现未经处理的异常，测试终止。
本文提供对 bug 进行初步调查的足够信息。 `TestHasEmbeddedSpaces`（测试例程）进行了错误的假设，或者 `HasEmbeddedSpaces` 无法正确识别所有嵌入的空格。

1. 若要诊断并更正问题，请从 `StringLibrary.HasEmbeddedSpaces` 方法开始。 查看 `HasEmbeddedSpaces` 方法中的比较。 它认为嵌入的空格是U + 0020。 但是，Unicode 标准包含许多其他空格字符。 这表明库代码对空格字符进行了错误的测试。

1. 将相等比较替换为对 <xref:System.Char.IsWhiteSpace%2A?displayProperty=fullName> 方法的调用：

   :::code language="csharp" source="../test/samples/snippets/csharp/lut-start/program2.cs" id="Snippet1":::

1. Live Unit Testing 会自动重新运行失败的测试方法。

   Live Unit Testing 将显示更新后的结果，这也会显示在代码编辑器窗口中。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 Live Unit Testing](live-unit-testing.md)
- [Live Unit Testing 常见问题解答](live-unit-testing-faq.yml)
