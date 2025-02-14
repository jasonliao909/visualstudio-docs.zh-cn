---
title: 创建单元测试方法存根
description: 了解如何使用“创建单元测试”命令，以便通过它轻松配置测试项目、测试类和其中的测试方法存根。
ms.custom: SEO-VS-2020
ms.date: 12/01/2021
ms.topic: how-to
helpviewer_keywords:
- unit testing, create unit tests
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
ms.openlocfilehash: a0252a0a2bc7ee84a8f32a75ab5c0a0b1da992aa
ms.sourcegitcommit: 5178819f49bb92995bca5c90c90e5fc5a1e04681
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2021
ms.locfileid: "134938251"
---
# <a name="create-unit-test-method-stubs-from-code"></a>从代码创建单元测试方法存根

“创建单元测试”命令创建单元测试方法存根  。 借助此功能，可以轻松地配置测试项目、测试类和其中的测试方法存根。

::: moniker range="vs-2017"
> [!NOTE]
> “创建单元测试”菜单命令仅适用于面向 .NET Framework（但不是 .NET Core 或 .NET Standard）的 C# 代码。
::: moniker-end
::: moniker range=">=vs-2019"
> [!NOTE]
> “创建单元测试”菜单命令仅适用于 C# 代码  。 若要将此方法与 .net Core 或 .NET Standard 一起使用，需要 Visual Studio 2019 或更高版本。
::: moniker-end

“创建单元测试”菜单命令可扩展，并可用于为 MSTest、MSTest V2、NUnit 和 xUnit 生成测试  。

## <a name="get-started"></a>入门

首先，在代码编辑器中选择要测试项目中的方法、类型或命名空间，右键单击，然后选择“创建单元测试”  。 “创建单元测试”对话框随即打开，可在其中配置创建测试的方式  。

::: moniker range="<=vs-2019"
![使用“创建单元测试”命令](media/createunittestcommand.png)
::: moniker-end
::: moniker range=">=vs-2022"
![使用 "创建单元测试" 命令和菜单对话框](media/vs-2022/create-unit-test-command-menu-dialog.png)
::: moniker-end

如果未显示用于 NUnit 或 xUnit 的测试框架选项，请参阅[使用第三方单元测试框架](#use-third-party-unit-test-frameworks)。

## <a name="set-unit-test-traits"></a>设置单元测试特征

如果计划在测试自动化进程中运行这些测试，可以考虑在另一个测试项目中创建测试（上述对话框中的第二个选项），并为单元测试设置单元测试特征。 这样便可更轻松地在持续集成或持续部署管道中加入或排除这些特定的测试。 如下所示，通过直接向单元测试添加元数据来设置特征。

::: moniker range="<=vs-2019"
![设置单元测试特征](media/createunittest.png)
::: moniker-end
::: moniker range=">=vs-2022"
![使用创建单元测试特征](media/vs-2022/create-unit-test-traits.png)
::: moniker-end

## <a name="use-third-party-unit-test-frameworks"></a>使用第三方单元测试框架

若要自动为 NUnit 或 xUnit 生成单元测试，请从 Visual Studio Marketplace 安装以下某个测试框架扩展：

* [适用于测试生成器的 NUnit 扩展](https://marketplace.visualstudio.com/items?itemName=NUnitDevelopers.TestGeneratorNUnitextension-18371)
* [适用于测试生成器的 xUnit.net 扩展](https://marketplace.visualstudio.com/items?itemName=YowkoTsai.xUnitnetTestGenerator)

## <a name="when-should-i-use-this-feature"></a>应何时使用此功能？

只要需要创建单元测试就可使用此功能，但在测试代码覆盖率很小或没有覆盖率且没有任何文档的现有代码时尤其适用。 换而言之，在代码说明有限或不存在代码说明的情况下适用。 它有效地实现了类似于 [IntelliTest](generate-unit-tests-for-your-code-with-intellitest.md) 的方法，该方法反映了代码的观察行为。

但此功能同样适用于以下情况：开发人员在开始时编写代码，然后使用该代码启动单元测试。 在编码流程中，开发人员可能想要为特定的一段代码快速创建一个单元测试方法存根（包含合适的测试类和合适的测试项目）。

## <a name="see-also"></a>请参阅

- [IntelliTest 入门](generate-unit-tests-for-your-code-with-intellitest.md)
- [单元测试博客文章](https://devblogs.microsoft.com/search?query=unit+testing)
