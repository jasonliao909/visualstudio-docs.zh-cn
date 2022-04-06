---
title: 使用 IntelliTest 为你的代码生成单元测试
description: IntelliTest 浏览你的 .NET 代码，以生成测试数据和单元测试套件。 了解如何运行 IntelliTest 来生成包含所有逻辑分支的智能模糊测试，查看哪些测试失败并修复它们。
ms.custom: SEO-VS-2020
ms.date: 04/04/2022
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.CreateIntelliTest
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 9bc1e9d814eae78ae060e83cc55bcf6a0c7cef5c
ms.sourcegitcommit: d9cab667735450e735622f8b93266f07b8046f3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "141402542"
---
# <a name="generate-unit-tests-for-fuzz-testing-by-using-intellitest"></a>使用 IntelliTest 生成用于模糊测试的单元测试

IntelliTest 浏览你的 .NET 代码，以生成测试数据和单元测试套件。 对于代码中的每个语句，将生成执行该语句的测试输入。 为代码中的每个条件分支执行案例分析。 例如，分析 `if` 语句、断言和可能引发异常的所有操作。 此分析用于为你的每个方法生成参数化单元测试的测试数据，从而创建具有较高代码覆盖率的单元测试。 将其视为智能模糊测试，用于修整输入和测试用例，以执行所有逻辑分支并检查是否有异常。

当你运行 IntelliTest 时，你可轻松看到哪些测试会失败，并可添加任何必要的代码来修复它们。 你可选择要保存到测试项目中的已生成测试，以提供回归套件。 当你更改代码时，重新运行 IntelliTest，以使生成的测试与你的代码更改同步。

## <a name="availability-and-extensions"></a>可用性和扩展

“创建 IntelliTest”和“运行 IntelliTest”菜单命令：

* 仅适用于 Visual Studio Enterprise 版。

* 仅支持面向 .NET Framework 的 C# 代码。

* [可扩展](#extend-framework)，支持在 MSTest、MSTest V2、NUnit 和 xUnit format 中发出测试。

* 不支持 x64 配置。

## <a name="explore-use-intellitest-to-explore-your-code-and-generate-unit-tests"></a>浏览：使用 IntelliTest 浏览代码并生成单元测试

若要生成单元测试，你的类型必须是公共类。

1. 在 Visual Studio 中打开解决方案，然后打开包含要测试的方法的类文件。

2. 右键单击一个方法并选择“运行 IntelliTest”，为方法中的代码生成单元测试。

   ::: moniker range="<=vs-2019"

   ![右键单击用于生成单元测试的方法的屏幕截图。](../test/media/vs-2019/run-pex.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   ![右键单击用于生成单元测试的方法的屏幕截图。](../test/media/vs-2022/run-pex.png)

   ::: moniker-end

   IntelliTest 使用不同的输入多次运行你的代码。 每次运行都会在表中表示出来，显示输入测试数据以及产生的输出或异常。

   ::: moniker range="<=vs-2019"

   !["浏览结果"窗口的屏幕截图。](../test/media/vs-2019/pex-exploration-results.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   !["浏览结果"窗口的屏幕截图。](../test/media/vs-2022/pex-exploration-results.png)

   ::: moniker-end

要为一个类中的所有公共方法生成单元测试，只需右键单击类而不是特定的方法，然后选择“运行 IntelliTest”。 使用“浏览结果”窗口中的下拉列表，显示类中每个方法的单元测试和输入数据。

::: moniker range="<=vs-2019"

![要从列表中查看的测试结果的屏幕截图。](../test/media/vs-2019/select-pex-test.png)

::: moniker-end

::: moniker range=">=vs-2022"

![要从列表中查看的测试结果的屏幕截图。](../test/media/vs-2022/select-pex-test.png)

::: moniker-end

对于通过的测试，检查结果列中报告的结果是否与你对代码的预期要求匹配。 对于失败的测试，根据需要修复你的代码。 然后重新运行 IntelliTest 来验证修复。

## <a name="persist-save-the-unit-tests-as-a-regression-suite"></a>保留：将单元测试保存为回归套件

1. 选择你要与参数化单元测试一同保存到测试项目中的数据行。

     ::: moniker range="<=vs-2019"

     ![保存测试结果的屏幕截图。](../test/media/vs-2019/save-pex-tests.png)

     ::: moniker-end

     ::: moniker range=">=vs-2022"

     ![保存测试结果的屏幕截图。](../test/media/vs-2022/save-pex-tests.png)

     ::: moniker-end

     你可以查看已创建的测试项目和参数化单元测试，单个单元测试（对应于每个行）保存在测试项目的 .g.cs 文件中，参数化单元测试保存在其对应的 .cs 文件中。 可以从测试资源管理器运行这些单元测试并查看结果，正如手动创建的任何单元测试一样。

     ::: moniker range="<=vs-2019"

     ![解决方案资源管理器中保存的测试的屏幕截图。](../test/media/vs-2019/test-method-pex.png)

     ::: moniker-end

     ::: moniker range=">=vs-2022"

     ![解决方案资源管理器中保存的测试的屏幕截图。](../test/media/vs-2022/test-method-pex.png)

     ::: moniker-end

     此外，还向测试项目添加了必要的引用。

     如果方法代码已更改，则重新运行 IntelliTest，以使单元测试与更改同步。

## <a name="assist-use-intellitest-to-focus-code-exploration"></a>帮助：使用 IntelliTest 聚焦代码浏览

1. 如果有更复杂的代码，IntelliTest 可以帮助你聚焦对代码的浏览。 例如，如果你的一个方法包含作为参数的接口，并且有多个类实现该接口，则 IntelliTest 将发现这些类并报告警告。

     查看警告，确定后续操作。

     ::: moniker range="<=vs-2019"

     ![查看警告的屏幕截图。](../test/media/vs-2019/pex-view-warning.png)

     ::: moniker-end

     ::: moniker range=">=vs-2022"

     ![查看警告的屏幕截图。](../test/media/vs-2022/pex-view-warning.png)

     ::: moniker-end

2. 调查代码并了解要测试的内容后，可修复警告，以选择要用于测试该接口的类。

     ::: moniker range="<=vs-2019"

     ![修复警告的屏幕截图。](../test/media/vs-2019/pex-fix-warning.png)

     ::: moniker-end

     ::: moniker range=">=vs-2022"

     ![修复警告的屏幕截图。](../test/media/vs-2022/pex-fix-warning.png)

     ::: moniker-end

     此选择会添加到 PexAssemblyInfo.cs 文件中。

     `[assembly: PexUseType(typeof(Camera))]`

3. 现在，你可重新运行 IntelliTest，以生成参数化单元测试并使用已修复的类测试数据。

     ::: moniker range="<=vs-2019"

     ![修复后重新运行 IntelliTest 的屏幕截图。](../test/media/vs-2019/pex-warnings-fixed.png)

     ::: moniker-end

     ::: moniker range=">=vs-2022"

     ![修复后重新运行 IntelliTest 的屏幕截图。](../test/media/vs-2022/pex-warnings-fixed.png)

     ::: moniker-end

## <a name="specify-use-intellitest-to-validate-correctness-properties-that-you-specify-in-code"></a>指定：使用 IntelliTest 来验证在代码中指定的正确性属性

指定需要生成的单元测试来验证的输入和输出之间的常规关系。 此规范封装在一个方法中，该方法看似为测试方法，但已被全称量词化。 这就是参数化单元测试方法，并且你所做的任何断言都必须保留 IntelliTest 可以生成的所有可能输入值。

## <a name="q--a"></a>问题解答

### <a name="q-can-you-use-intellitest-for-unmanaged-code"></a>问：是否可以对非托管代码使用 IntelliTest？

**答：** 不可以，IntelliTest 仅适用于托管代码。

### <a name="q-when-does-a-generated-test-pass-or-fail"></a>问：生成的测试在什么情况下通过，什么情况下失败？

**答：** 与其他单元测试相同，如果没有异常产生即通过。 如果有任何断言失败，或者测试的代码引发未处理的异常，则失败。

如果你的一个测试可在引发特定异常的情况下通过，则可根据你在测试方法、测试类或程序集级别的要求设置以下属性之一：

- **PexAllowedExceptionAttribute**

- **PexAllowedExceptionFromTypeAttribute**

- **PexAllowedExceptionFromTypeUnderTestAttribute**

- **PexAllowedExceptionFromAssemblyAttribute**

### <a name="q-can-i-add-assumptions-to-the-parameterized-unit-test"></a>问：我能否将假设添加到参数化单元测试？

**答：** 可以，使用假设指定特定方法的单元测试不需要的测试数据。 使用 <xref:Microsoft.Pex.Framework.PexAssume> 类添加假设。 例如，你可以添加类似于以下形式的`lengths`变量不为 null 的假设：

`PexAssume.IsNotNull(lengths);`

如果添加了假设并重新运行 IntelliTest，则将删除不再相关的测试数据。

### <a name="q-can-i-add-assertions-to-the-parameterized-unit-test"></a>问：我能否将断言添加到参数化单元测试？

**答：** 可以，IntelliTest 将在运行单元测试时检查你在语句中的断言内容是否正确。 使用 <xref:Microsoft.Pex.Framework.PexAssert> 类或测试框架附带的断言 API 来添加断言。 例如，可添加两个变量相等的断言。

`PexAssert.AreEqual(a, b);`

如果添加了断言并重新运行 IntelliTest，将检查断言的有效性；如果断言无效，则测试失败。

### <a name="q-can-i-generate-parameterized-unit-tests-without-running-intellitest-first"></a><a name="NoRun"></a> 问：是否可以无需首先运行 IntelliTest 便生成参数化单元测试？

**答：** 可以，在类或方法中单击右键，然后选择 **创建 IntelliTest**。

::: moniker range="<=vs-2019"

![创建 IntelliTest 的屏幕截图。](../test/media/vs-2019/pex-create-intellitest.png)

::: moniker-end

::: moniker range=">=vs-2022"

![创建 IntelliTest 的屏幕截图。](../test/media/vs-2022/pex-create-intellitest.png)

::: moniker-end

接受默认格式以生成测试，或更改项目和测试的命名方式。 你可以创建新的测试项目或将你的测试保存到现有项目。

::: moniker range="<=vs-2019"

![使用 MSTest 默认值创建 IntelliTest 的屏幕截图。](../test/media/vs-2019/pex-create-intellitest-mstest.png)

::: moniker-end

::: moniker range=">=vs-2022"

![使用 MSTest 默认值创建 IntelliTest 的屏幕截图。](../test/media/vs-2022/pex-create-intellitest-mstest.png)

::: moniker-end

<a name="extend-framework"></a>
### <a name="q-can-i-use-other-unit-test-frameworks-with-intellitest"></a>问：是否可以将其他单元测试框架用于 IntelliTest？

**答：** 可以，请按照下列步骤 [查找和安装其他框架](../test/install-third-party-unit-test-frameworks.md)。
Visual Studio Marketplace 中也提供了测试框架扩展，例如 [NUnit T测试生成器](https://marketplace.visualstudio.com/items?itemName=NUnitDevelopers.TestGeneratorNUnitextension-18371)。

重新启动 Visual Studio 并重新打开你的解决方案后，在类或方法中单击右键，然后选择 **创建 IntelliTest**。 请在此处选择已安装的框架：

::: moniker range="<=vs-2019"

![选择 IntelliTest 的其他单元测试框架的屏幕截图。](../test/media/vs-2019/pex-create-intellitest-extensions.png)

::: moniker-end

::: moniker range=">=vs-2022"

![选择 IntelliTest 的其他单元测试框架的屏幕截图。](../test/media/vs-2022/pex-create-intellitest-extensions.png)

::: moniker-end

然后，运行 IntelliTest 以在其相应的 .g.cs 文件中生成单个单元测试。

### <a name="q-can-i-learn-more-about-how-the-tests-are-generated"></a>问：是否可以了解有关如何生成测试的详细信息？

**答：** 可以，要获取高级概述，请阅读此 [博客文章](https://devblogs.microsoft.com/devops/intellitest-one-test-to-rule-them-all/)。
