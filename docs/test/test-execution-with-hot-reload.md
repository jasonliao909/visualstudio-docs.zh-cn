---
title: 使用热重载的测试执行
description: 了解如何通过测试资源管理器在 Visual Studio 中使用热重载。 本主题介绍如何启用使用热重载的测试执行，支持使用热重载的情况，以及使用时应采取的操作。
ms.date: 10/15/2021
ms.topic: how-to
author: vritant24
ms.author: vrbhardw
manager: manishj
ms.technology: vs-ide-test
ms.workload:
- VB
- CSharp
ms.openlocfilehash: 358f55acf7bc54059a2f21624b26c45021815c64
ms.sourcegitcommit: 0257750be796cc46e01cebd8976f637743d29417
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2021
ms.locfileid: "130290598"
---
# <a name="test-execution-with-hot-reload"></a>使用热重载的测试执行

Visual Studio 中的测试运行涉及到在使用[测试平台](https://github.com/microsoft/vstest/)执行你的测试之前，生成项目以更新磁盘上的二进制文件。 Visual Studio 内部的生成时间会根据对代码的[更改类型](https://github.com/dotnet/roslyn/blob/296e0fada42f241d338b169c3c6c6189101ef0b7/docs/wiki/EnC-Supported-Edits.md)而有所不同。 对于较大的解决方案，生成可能是测试运行中成本最高的部分。 在 Visual Studio 2022 及更高版本中，可以启用使用热重载的测试执行，通过跳过支持场景的生成来以加速测试执行。

## <a name="what-is-supported"></a>支持的场景
- 面向 .NET 6.0 和更高版本的 C# 和 VB 项目
- 为调试配置生成的测试项目
- Visual Studio 2022 及更高版本

## <a name="enable-test-execution-with-hot-reload"></a>启用使用热重载的测试执行
通过选择“测试” > “选项”“(实验性)为面向 .NET 6 及更高版本的 C# 和 VB 测试项目启用使用热重载的测试运行” > 来启用此功能。
![Visual Studio“测试选项”页上的“启用使用热重载的测试运行”按钮的屏幕截图。 选择此选项后，测试执行将对支持的场景使用热重载](./media/test-execution-hot-reload-option.png)

## <a name="why-is-it-experimental"></a>为什么会标记为“实验性”？
这是一种新的测试执行方法，我们改变了验证代码的一种广泛使用的路径。 随着我们收到更多的用户反馈，我们也期望围绕这一功能的用户体验会到改变。 出于这两个原因，我们目前已将此功能标记为“实验性”。

## <a name="how-it-works"></a>工作原理
启用此选项后，测试资源管理器将自动使用启用热重载的测试执行。 如果无法使用热重载，它将回退到生成并运行测试的常规行为。 作为运行测试的用户，无需对工作流进行任何更改（即可以继续编辑代码并运行测试）。

在后台，我们使用与新发布的[用于在运行时编辑 C#/VB 代码的热重载体验](https://devblogs.microsoft.com/dotnet/introducing-net-hot-reload/)中提供的[编辑和继续](../debugger/edit-and-continue.md)基础结构相同的基础结构来确定所做的更改。 出于此原因，我们只有在没有“强制编辑”时才会使用热重载，在这种情况下，我们会在执行测试之前回退到生成测试。 有关支持的编辑的更多详细信息，请参阅[编辑并继续文档](https://github.com/dotnet/roslyn/blob/296e0fada42f241d338b169c3c6c6189101ef0b7/docs/wiki/EnC-Supported-Edits.md)

## <a name="how-much-faster-will-the-test-execution-be"></a>测试执行速度要快多少？
在估计此功能可为你节省多少时间时，有许多可变因素。 例如：
- 项目生成所花费的时间。
- 进行了哪种编辑。
- 进行编辑的文件有多大。
- 进行编辑的位置（是否为叶项目）。

最终，速度改进将与该特定测试运行中发生的生成时间直接相关。

### <a name="notes"></a>注释
- 启用选项或打开 Visual Studio 后的第一次第一次测试运行将进行项目生成。
- 运行测试时，编辑器中的文件可能不会进行保存。 若要解决这些问题，请在签入之前，确保执行完整生成 (Ctrl+Shift+B)。
- 发生使用热重载的测试执行时，磁盘上的二进制文件不会更新。
- 使用热重载的测试执行在测试资源管理器中的“测试” > “运行所有测试”、“在视图中运行所有测试”中不起作用，在解决方案资源管理器的解决方案节点的“运行所有测试”中也不起作用。 此功能不适用于这些命令，因为它们目前保证能生成整个解决方案。
- 当使用不受支持的目标框架（版本低于 .NET 6.0）的测试运行时，将进行项目生成。
- 如果磁盘上的内容与测试资源管理器显示的内容之间存在任何不一致，请考虑使用 Ctrl+Shift+B 生成解决方案/项目，然后运行测试。 任何显式生成都会将热重载测试结果替换为常规的完整生成测试结果。

## <a name="known-issues"></a>已知问题
- 在以下场景中，不会发生使用热重载的测试执行：
  - 代码覆盖率
  - Live Unit Testing
  - 分析
  - 调试
- 如果存在无法读取的令牌，可能无法读取堆栈跟踪。 我们正在[此处](https://github.com/dotnet/runtime/issues/56335)跟踪此问题，计划在 .NET 7.0 中修复
  - 在这种情况下，建议的解决方法是生成项目并重新运行测试。

## <a name="your-feedback-matters"></a>你的反馈很重要
如前所述，要完成此实验性功能，我们需要你提供反馈。 如果你有关于体验的建议，或遇到任何问题，请花点时间向我们报告问题。 只有通过你的反馈，我们才能确保关键问题得到解决，并根据你的输入确定将来的决策的优先级。

若要联系我们，请使用 [Visual Studio 反馈机制](https://developercommunity.visualstudio.com/home)。
