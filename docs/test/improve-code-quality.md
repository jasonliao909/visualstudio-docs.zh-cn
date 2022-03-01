---
title: 单元测试工具
description: 了解 Visual Studio 测试工具如何帮助你和你的团队达到并保持高标准的代码卓越性。
ms.custom: SEO-VS-2020
ms.date: 08/19/2021
ms.topic: conceptual
helpviewer_keywords:
- testing tools [Visual Studio]
- unit tests [Visual Studio]
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 4f1aec397a930e6aeca95d9c8eb62ac04c0ca92c
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138148461"
---
# <a name="first-look-at-testing-tools-in-visual-studio"></a>首先介绍 Visual Studio 中的测试工具

Visual Studio 测试工具可帮助你和你的团队达到并保持高标准的代码卓越性。

> [!NOTE]
> Visual Studio 的所有版本均提供单元测试。 其他测试工具（例如 Live Unit Testing 和 IntelliTest）仅可在 Visual Studio Enterprise 版本中可用。 有关版本的详细信息，请参阅[比较 Visual Studio IDE](https://visualstudio.microsoft.com/vs/compare/)。

## <a name="test-explorer"></a>测试资源管理器

“测试资源管理器”窗口可帮助开发人员创建、管理和运行单元测试  。 可以使用 Microsoft 单元测试框架或若干第三方和开源框架之一。

::: moniker range="vs-2017"
![Visual Studio 测试资源管理器](media/devtest-testexplorer.png)
::: moniker-end

::: moniker range=">=vs-2019"
![Visual Studio 测试资源管理器 16.2](media/vs-2019/test-explorer-16-2.PNG)
::: moniker-end

* [单元测试入门](unit-test-your-code.md)
* [单元测试基础知识](unit-test-basics.md)
* [使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)
* [测试资源管理器常见问题解答](test-explorer-faq.md)
* [安装第三方单元测试框架](install-third-party-unit-test-frameworks.md)

Visual Studio 也可扩展，并支持第三方单元测试适配器，如 NUnit 和 xUnit.net。 此外，通过帮助识别在语义上类似的代码块（这可能是常见 bug 修复或重构的备选项），代码克隆功能还同时可以获得高质量的软件。

![第三方测试集成](media/devtest-thirdparty.png)

## <a name="live-unit-testing"></a>Live Unit Testing

[Live Unit Testing](../test/live-unit-testing.md) 会自动在后台运行单元测试，并在 Visual Studio 代码编辑器中以图形方式显示代码覆盖率和测试结果。

> [!NOTE]
> Live Unit Testing 仅在企业版中提供，并且仅支持 .NET 代码。

## <a name="intellitest"></a>IntelliTest

IntelliTest 会自动为托管代码生成单元测试和测试数据。 IntelliTest 提高了覆盖率且大大减少了创建和维护新代码或现有代码的单元测试的工作量。

![操作中的 IntelliTest](media/devtest-intellitest.png)

> [!NOTE]
> 只有企业版提供 IntelliTest。 面向 .NET Framework 的 C# 代码支持它。 当前不支持 .NET Core 和 .NET Standard。

* [使用 IntelliTest 为代码生成单元测试](generate-unit-tests-for-your-code-with-intellitest.md)
* [IntelliTest – One test to rule them all](https://devblogs.microsoft.com/devops/intellitest-one-test-to-rule-them-all/)（IntelliTest - 一个测试掌控所有情况）
* [IntelliTest 参考手册](intellitest-manual/index.md)

## <a name="code-coverage"></a>代码覆盖率

[代码覆盖率](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)确定正在由编码的测试（例如单元测试）实际进行测试的项目代码的比例。 若要有效防止 Bug，测试应作用于或“覆盖”你的大部分代码。

> [!NOTE]
> 只有企业版中提供代码覆盖率。

可将代码覆盖率分析应用于托管和非托管（本机）代码。

代码覆盖率是使用测试资源管理器运行测试方法时的一个选项。 结果表将显示在各个程序集、类和方法中运行的代码的百分比。 此外，源代码编辑器会显示已测试的代码。

* [使用代码覆盖率确定正在测试的代码量](using-code-coverage-to-determine-how-much-code-is-being-tested.md)
* [使用 Visual Studio（实验室）进行单元测试、代码覆盖率分析和代码克隆分析](https://azuredevopslabs.com/labs/devopsserver/liveunittesting)
* [自定义代码覆盖率分析](customizing-code-coverage-analysis.md)

## <a name="microsoft-fakes"></a>Microsoft Fakes

[Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md) 将应用程序的其余部分替换为存根或填充码，有助于隔离受测代码。

> [!NOTE]
> Microsoft Fakes 仅在企业版中提供，并且仅支持 .NET 代码。

## <a name="user-interface-testing-with-coded-ui-and-selenium"></a>通过编码的 UI 和 Selenium 进行用户界面测试

编码的 UI 测试提供了一种方法来创建完全自动化的测试，用来验证应用程序用户界面的功能和行为。 它们可在各种技术（包括基于 XAML 的 UWP 应用、浏览器应用和 SharePoint 应用）中自动进行 UI 测试。

> [!NOTE]
> 编码的 UI 是已弃用的功能。

无论选择最适用的编码 UI 测试还是使用 Selenium 进行的基于泛型浏览器的 UI 测试，Visual Studio 均提供所有所需的工具。

![使用编码的 UI 进行 UI 测试](media/devtest-codeduitest.png)

* [使用 UI 自动化来测试代码](use-ui-automation-to-test-your-code.md)
* [创建、编辑和维护编码的 UI 测试入门](walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
* [使用编码的 UI 测试来测试 UWP 应用](test-uwp-app-with-coded-ui-test.md)
* [使用 Visual Studio Enterprise（实验室）进行编码的 UI 测试简介](https://azuredevopslabs.com/labs/tfs/codedui)

## <a name="related-scenarios"></a>相关方案

* [探索和手动测试 (Azure Test Plans)](/azure/devops/test/index?view=vsts&preserve-view=true)
* [负载测试（Azure Test Plans）](/azure/load-testing/)
* [代码分析工具](../code-quality/code-analysis-for-managed-code-overview.md)
