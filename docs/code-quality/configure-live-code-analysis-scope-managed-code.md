---
title: 配置 .NET 的实时代码分析范围
ms.date: 05/13/2022
description: 了解 Visual Studio 中的背景分析。 了解如何将分析范围限制为可见文档、所有打开的文档或所有文件和项目。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 4720a456c28b3ff639df9f70819220a44ee71589
ms.sourcegitcommit: b86afb55321ec393bd29afffc2574772f36f94bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2022
ms.locfileid: "145148981"
---
# <a name="configure-live-code-analysis-for-net"></a>配置 .NET 的实时代码分析

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

Visual Studio在编辑器中编辑源文件时分析代码。 这称为 *后台分析*。 若要获得可接受的 Visual Studio IDE 编辑体验，有些分析是必需的最少分析。 有些是为了提升 IDE 功能的响应能力。 而有一些是为了启用其他 IDE 功能，例如 Roslyn 分析器中的诊断和代码修复。 根据功能，这些分析可以按如下方式进行分组：

- **诊断的后台计算**：用于计算源文件中的错误、警告和建议的分析。 这些诊断以条目形式显示在错误列表中，以波形曲线显示在编辑器中。 它们可分为两类：
  - C# 和 Visual Basic 编译器诊断
  - Roslyn 分析器诊断，其中包括：

    - 用于代码样式建议的内置 IDE 分析器
    - 用于代码质量建议的内置 CA 分析器
    - 为当前解决方案中的项目[安装](./install-roslyn-analyzers.md)的第三方分析器包。

- **其他后台分析**：用于提升 IDE 功能的响应能力和 Visual Studio 交互的分析。 下面是此类分析的一些示例：
  - 后台分析打开的文件。
  - 后台编译已打开文件的项目来实现符号，从而提升某些 IDE 功能的响应能力。
  - 生成语法和符号缓存。
  - 检测源文件（如窗体和控件）的设计器关联。

## <a name="default-analysis-scope"></a>默认分析范围

默认情况下，编译器诊断在所有打开的文档上运行，Visual Studio 2022 及更高版本中，Roslyn 分析器诊断仅在当前活动文档上运行。 前面提到的一些 _其他后台分析_ 针对至少有一个打开文件的所有项目执行。 针对整个解决方案执行一些后台分析。

## <a name="custom-analysis-scope"></a>自定义分析范围

每个后台分析的默认范围已针对大多数客户方案和解决方案优化用户体验、功能和性能。 但是，在某些情况下，客户可能需要自定义此范围以减少或增加后台分析。 例如：

- 省电模式：如果在笔记本电脑电池上运行，则可能希望最大程度地减少耗电量，以延长电池使用时间。 在此方案中，需要最大程度地减少后台分析。
- 按需代码分析：如果希望在需要时关闭实时分析器执行并手动运行代码分析，则需要最大程度地减少后台分析。 请参阅[操作指南：按需手动运行代码分析](./how-to-run-code-analysis-manually-for-managed-code.md)。
- 完整解决方案分析：你可能希望在解决方案中的所有文件中查看所有诊断，无论它们是否在编辑器中打开。 在此方案中，你需要将后台分析范围最大化到整个解决方案。

从 2019 Visual Studio 开始，可以针对 C# 和Visual Basic项目显式自定义所有实时代码分析的范围，包括诊断计算。 可用的分析范围包括：

::: moniker range=">=vs-2022"

| 选项 | 说明 |
| - | - |
| 无 | 禁用所有分析器和相应的代码修复。<br/><br/>所有 *打开* 的文档上都启用了编译器诊断和相应的代码修复。 |
| 当前文档 (默认)  | 所有分析器仅在当前活动文档上运行。<br/><br/>在所有 *打开* 的文档上都启用编译器诊断。 |
| 打开文档 | 所有打开的文档上都启用了 *所有* 分析器和编译器诊断。 |
| 整个解决方案 | 解决方案 *中的所有* 文档（无论是打开还是关闭）上都启用了所有分析器和编译器诊断。 |

::: moniker-end

::: moniker range="<=vs-2019"

- **当前文档**：最小化实时代码分析范围，以仅对编辑器中的当前文件或可见文件执行。
- **打开文档**：实时代码分析范围包括所有打开的文档。 这是默认值。
- **整个解决方案**：最大化实时代码分析范围，以对整个解决方案中的所有文件和项目执行。

::: moniker-end

可以通过以下步骤在 **“选项** ”中选择上述自定义分析范围之一：

1. 要打开“选项”对话框，请在 Visual Studio 中的菜单栏上依次选择“工具” > “选项”  。

2. 在“**选项**”对话框中，选择 **“文本编辑器** > **C#** (”或 **Visual Basic) >****“高级**”。

3. 选择所需的“后台分析范围”以自定义分析范围。 完成后选择“确定”。

::: moniker range=">=vs-2022"

![Visual Studio中的后台代码分析范围选项的屏幕截图。](./media/background-analysis-scope.png)

::: moniker-end

::: moniker range="<=vs-2019"

![Visual Studio中的后台代码分析范围选项的屏幕截图。](./media/vs-2019/background-analysis-scope.png)

::: moniker-end

> [!NOTE]
> 在 2019 Visual Studio 之前，可以使用 **“工具** > **选项** > **文本编辑器** > **C (#** ”中的 **“启用完整解决方案分析**”复选框自定义诊断计算的分析范围，或 **Visual Basic) >****“高级**”选项卡。不支持在以前的Visual Studio版本中最小化后台分析范围。

## <a name="automatically-minimize-live-code-analysis-scope"></a>自动最小化实时代码分析范围

如果 Visual Studio 检测到可用的系统内存为 200 MB 或更少，它会自动将实时代码分析范围最小化为“当前文档”。 如果发生这种情况，则会显示一条警报，通知你 Visual Studio 已禁用某些功能。 有关详细信息，请参阅 [自动功能挂起](automatic-feature-suspension.md)。

![最小化分析范围的警报文本](./media/fsa_alert.png)

## <a name="see-also"></a>另请参阅

- [自动功能挂起](./automatic-feature-suspension.md)
- [节能模式功能请求](https://github.com/dotnet/roslyn/issues/38429)
