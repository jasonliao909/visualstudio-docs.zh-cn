---
title: 单元测试入门
description: 使用 Visual Studio 定义和运行单元测试，使代码保持正常运行并在客户之前找到错误和缺陷。
ms.custom: SEO-VS-2020
ms.date: 08/10/2021
ms.topic: tutorial
helpviewer_keywords:
- unit testing, create unit test plans
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
ms.openlocfilehash: 2465deef6d8b4c93b9e72d38bf548a001373f9e3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737267"
---
# <a name="get-started-with-unit-testing"></a>单元测试入门

使用 Visual Studio 定义和运行单元测试，使代码保持正常运行、确保代码覆盖率并在客户之前找到错误和缺陷。 经常运行单元测试，确保代码正常运行。

在本文中，代码使用 C# 和 C++，图例使用 C#，但是概念和特征适用于 .NET 语言、C++、Python、JavaScript 和 TypeScript。

## <a name="create-unit-tests"></a>创建单元测试

本节介绍了如何创建单元测试项目。

1. 在 Visual Studio 中，打开要测试的项目。

   出于演示示例单元测试的目的，本文测试一个简单的“Hello World”C# 或名为“Hello World”的 C++ 控制台项目（使用 C# 时名为“HelloWorldCore”） 。 此类项目的示例代码如下所示：

   ### <a name="net"></a>[.NET](#tab/dotnet)
   ```csharp
   namespace HelloWorldCore

      public class Program
      {
         public static void Main()
         {
            Console.WriteLine("Hello World!");
         }
      }
   ```

   ### <a name="c"></a>[C++](#tab/cpp)
   ```cpp
   #include <iostream>

   int main()
   {
      std::cout << "Hello World!\n";
   }
   ```
   ---

1. 在“解决方案资源管理器”中，选择解决方案节点。 然后，在顶部菜单栏中，选择“文件” > “添加” > “新项目”  。

1. 在新项目对话框中，找到要使用的单元测试项目。

   ::: moniker range=">=vs-2019"
   在搜索框中键入“测试”，找到要使用的测试框架的单元测试项目模板（例如 MSTest (C#) 或本机单元测试项目 (C++)），并选择它。
   ::: moniker-end
   ::: moniker range="vs-2017"
   展开“已安装”节点，选择你要用于测试项目的语言，然后选择“测试” 。
   ::: moniker-end

   从 Visual Studio 2017 14.8 版本开始，.NET 语言包括适用于 NUnit 和 xUnit 的内置模板。 对于 C++，在本示例中，选择“本机单元测试”项目，它使用 Microsoft 本机单元测试框架。 （若要使用其他 C++ 测试框架，请参阅[为 C/C++ 编写单元测试](../test/writing-unit-tests-for-c-cpp.md)）。 对于 Python，请参阅[在 Python 代码中设置单元测试](../python/unit-testing-python-in-visual-studio.md)以设置测试项目。

   > [!TIP]
   > 仅对 C# 而言，可以使用更快的方法基于代码创建单元测试项目。 有关详细信息，请参阅[创建单元测试项目和测试方法](../test/unit-test-basics.md#create-unit-test-projects-and-test-methods-c)。 若要将此方法与 .NET Core 或 .NET Standard 一起使用，需要 Visual Studio 2019。

   下图显示了 .NET 中支持的 MSTest 单元测试。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的单元测试项目模板](media/vs-2019/add-new-test-project.png)

   单击“下一步”，选择测试项目的名称，然后单击“创建”。

   ::: moniker-end

   ::: moniker range="vs-2017"

   ![Visual Studio 2019 中的单元测试项目模板](media/mstest-test-project-template.png)

   选择测试项目的名称（例如 HelloWorldTests），然后单击“确定”。

   ::: moniker-end

   项目将添加到解决方案中。

   ![解决方案资源管理器中的单元测试项目](media/vs-2019/solution-explorer.png)

1. 在单元测试项目中，右键单击“引用”或“依赖项”，然后选择“添加引用”或“添加项目引用”，添加对要测试的项目的引用   。

1. 选择包含待测试代码的项目，单击“确定”。

   ![在 Visual Studio 中添加项目引用](media/vs-2019/reference-manager.png)

1. 向单元测试方法添加代码。

   例如，你可以通过选择与测试框架匹配的正确文档选项卡来使用以下代码：MSTest、NUnit 或 xUnit（仅在 .NET 上受支持）或 C++ Microsoft 本机单元测试框架。

   ### <a name="mstest"></a>[MSTest](#tab/mstest)

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      [TestClass]
      public class UnitTest1
      {
         private const string Expected = "Hello World!";
         [TestMethod]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

   ### <a name="nunit"></a>[NUnit](#tab/nunit)

   ```csharp
   using NUnit.Framework;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      public class Tests
      {
         private const string Expected = "Hello World!";

         [SetUp]
         public void Setup()
         {
         }
         [Test]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

    ### <a name="xunit"></a>[xUnit](#tab/xunit)

    ```csharp
    using System;
    using Xunit;
    using System.IO;
    
    namespace HelloWorldTests
    {
        public class UnitTest1
        {
            private const string Expected = "Hello World!";
            [Fact]
            public void Test1()
            {
                using (var sw = new StringWriter())
                {
                    Console.SetOut(sw);
                    HelloWorldCore.Program.Main();
    
                    var result = sw.ToString().Trim();
                    Assert.Equal(Expected, result);
                }
            }
        }
    }
    ```

    ### <a name="microsoft-native-unit-test-framework"></a>[Microsoft 本机单元测试框架](#tab/msunittest)

    ```cpp
    #include "pch.h"
    #include "CppUnitTest.h"
    #include "../HelloWorldUnitTestCPP/HelloWorldUnitTestCPP.cpp"   // Update using your project name

    using namespace Microsoft::VisualStudio::CppUnitTestFramework;

    namespace HelloWorldTests
    {
       TEST_CLASS(HelloWorldTests)
       {
       public:

          TEST_METHOD(TestMethod)
          {
             std::string expected = "Hello World!\n";

             std::stringstream buffer;
             std::streambuf* sbuf = std::cout.rdbuf(); // Save cout's buffer
             std::cout.rdbuf(buffer.rdbuf()); // Redirect cout to the stringstream buffer

             // Call main() in your test
             int result = main();

             // When finished, redirect cout to the original buffer 
             std::cout.rdbuf(sbuf);
             std::cout << "std original buffer: \n";
             std::cout << buffer.get();

             // Test
             Assert::AreEqual(expected, buffer.str());
          }
       };
    }
    ```

    ---

## <a name="run-unit-tests"></a>运行单元测试

1. 打开“测试资源管理器”。[](../test/run-unit-tests-with-test-explorer.md)

   ::: moniker range=">=vs-2019"
   若要打开测试资源管理器，请选择顶部菜单栏中的“测试”>“测试资源管理器”（或按 Ctrl  + E，T）。
   ::: moniker-end
   ::: moniker range="vs-2017"
   若要打开测试资源管理器，请选择顶部菜单栏中的“测试”>“Windows”>“测试资源管理器”  。
   ::: moniker-end

1. 单击“全部运行”（或按 Ctrl  +  R，V），运行单元测试。

   ![在测试资源管理器中运行单元测试](media/vs-2019/test-explorer-run-all.png)

   测试完成后，绿色复选标记表示测试通过。 红色“x”图标表示测试失败。

   ![在测试资源管理器中查看单元测试结果](media/vs-2019/unit-test-passed.png)

> [!TIP]
> 可以使用[测试资源管理器](../test/run-unit-tests-with-test-explorer.md)从内置测试框架 (MSTest) 或第三方测试框架运行单元测试。 可以将测试分组为不同类别、筛选测试列表，以及创建、保存和运行测试播放列表。 你还可以调试测试并分析测试性能和代码覆盖率。

## <a name="view-live-unit-test-results-visual-studio-enterprise"></a>查看实时单元测试结果 (Visual Studio Enterprise)

如果在 Visual Studio 2017 或更高版本中使用 MSTest、xUnit 或 NUnit 测试框架，可查看单元测试的实时结果。

> [!NOTE]
> 要执行这些步骤，需要 Visual Studio Enterprise，以及 .NET 代码和以下测试框架之一：MSTest、xUnit 或 NUnit。

1. 选择“测试” > “Live Unit Testing” > “启动”，从“测试”菜单启用 Live Unit Testing。

   ::: moniker range="vs-2017"

   ![启用 Live Unit Testing](media/live-test-results-start.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![在 Visual Studio 2019 中启用 Live Unit Testing](media/vs-2019/start-live-unit-testing.png)

   ::: moniker-end

1. 编写和编辑代码时，请在代码编辑器窗口中查看测试的结果。

   ![查看测试的结果](media/vs-2019/live-unit-testing-results.png)

1. 单击测试结果指示器查看详细信息，例如涵盖该方法的测试的名称。

   ![选择测试结果指示符](media/vs-2019/live-unit-testing-details.png)

有关 Live Unit Testing 的详细信息，请参阅 [Live Unit Testing](../test/live-unit-testing-intro.md)。

## <a name="use-a-third-party-test-framework"></a>使用第三方测试框架

通过使用第三方测试框架（例如 NUnit、Boost 或 Google C++ 测试框架，具体取决于你的编程语言），可以在 Visual Studio 中运行单元测试。 使用第三方框架：

- 使用 NuGet 包管理器为所选框架安装 NuGet 包  。

- (.NET) 从 Visual Studio 2017 14.6 版本开始，Visual Studio 包括适用于 NUnit 和 xUnit 测试框架的预配置测试项目模板。 这些模板还包括必要的 NuGet 包以实现支持。

- (C++) 在 Visual Studio 2017 及更高版本中，已经包含了一些框架，如 Google C++ 测试框架。 有关详细信息，请参阅[在 Visual Studio 中编写适用于 C/C++ 的单元测试](../test/writing-unit-tests-for-c-cpp.md)。

添加单元测试项目：

1. 打开包含待测试代码的解决方案。

2. 右键单击“解决方案资源管理器”中的解决方案，然后选择“添加” > “新建项目”。

3. 选择单元测试项目模板。

   在本例中，选择 [NUnit](https://nunit.org/)

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的 NUnit 测试项目模板](media/vs-2019/nunit-test-project-template.png)

   单击“下一步”，为项目命名，然后单击“创建”。

   ::: moniker-end

   ::: moniker range="vs-2017"

   为项目命名，然后单击“确定”进行创建。

   ::: moniker-end

   项目模板包括对 NUnit 和 NUnit3TestAdapter 的 NuGet 引用。

   ![解决方案资源管理器中的 NUnit NuGet 依赖项](media/vs-2019/nunit-nuget-dependencies.png)

4. 将测试项目中的引用添加到包含待测试代码的项目中。

   右键单击“解决方案资源管理器”中的项目，然后选择“添加” > “引用”。 （还可以从“引用”或“依赖项”节点右键单击菜单来添加一个引用。）

5. 将代码添加到测试方法。

   ![将代码添加到单元测试代码文件](media/vs-2019/unit-test-method.png)

6. 从测试资源管理器运行测试，或右键单击测试代码并选择“运行测试”（或 Ctrl   +  R，T）。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [单元测试基础知识](../test/unit-test-basics.md)

> [!div class="nextstepaction"]
> [创建并运行托管代码的单元测试](walkthrough-creating-and-running-unit-tests-for-managed-code.md)

> [!div class="nextstepaction"]
> [编写适用于 C/C++ 的单元测试](../test/writing-unit-tests-for-c-cpp.md)
