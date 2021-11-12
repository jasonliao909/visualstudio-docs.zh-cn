---
title: 配置 .NET 的实时代码分析范围
ms.date: 09/01/2020
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
ms.openlocfilehash: 664d24c2732ee2c63475ac986fa9bbab78831493
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601332"
---
# <a name="configure-live-code-analysis-for-net"></a>配置 .NET 的实时代码分析

当你在编辑器中编辑源文件时，Visual Studio 会执行大量实时代码分析（也称为后台分析）。 若要获得可接受的 Visual Studio IDE 编辑体验，有些分析是必需的最少分析。 有些是为了提升 IDE 功能的响应能力。 而有一些是为了启用其他 IDE 功能，例如 Roslyn 分析器中的诊断和代码修复。 根据功能，这些分析可以按如下方式进行分组：

- **诊断的后台计算**：用于计算源文件中的错误、警告和建议的分析。 这些诊断以条目形式显示在错误列表中，以波形曲线显示在编辑器中。 它们可分为两类：
  - C# 和 Visual Basic 编译器诊断
  - Roslyn 分析器诊断，其中包括：

    - 提供代码样式建议的内置 IDE 分析器
    - 提供代码质量建议的内置 CA 分析器
    - 为当前解决方案中的项目[安装](./install-roslyn-analyzers.md)的第三方分析器包。

- **其他后台分析**：用于提升 IDE 功能的响应能力和 Visual Studio 交互的分析。 下面是此类分析的一些示例：
  - 后台分析打开的文件。
  - 后台编译已打开文件的项目来实现符号，从而提升某些 IDE 功能的响应能力。
  - 生成语法和符号缓存。
  - 检测源文件（如窗体、控件等）的设计器关联。

## <a name="default-analysis-scope"></a>默认分析范围

默认情况下，对 Visual Studio 中打开的所有文件执行诊断后台计算的实时代码分析。 上面提到的其他后台分析很少对至少有一个打开的文件的所有项目执行。 而几乎不对整个解决方案执行后台分析。

## <a name="custom-analysis-scope"></a>自定义分析范围

为提供最佳用户体验、功能和性能，每个后台分析的默认范围已针对大多数客户方案和解决方案进行了优化。 但是，在某些情况下，客户可能需要自定义此范围以减少或增加后台分析。 例如：

- 节能模式：如果用户使用笔记本电脑电池运行，他们可能需要将功耗降至最低，以延长电池使用时间。 在这种情况下，他们可能希望最大程度地减少后台分析。
- 按需代码分析：如果用户更喜欢关闭实时分析器执行并按需手动运行代码分析，他们可能希望最大程度地减少后台分析。 请参阅[操作指南：按需手动运行代码分析](./how-to-run-code-analysis-manually-for-managed-code.md)。
- 完整解决方案分析：如果用户希望始终看到解决方案的所有文件中的所有诊断，无论它们是否在编辑器中打开。 在这种情况下，他们可能希望将后台分析范围最大化为整个解决方案。

从 Visual Studio 2019 版本 16.5 开始，用户可以显式自定义 C# 和 Visual Basic 项目的所有实时代码分析（包括诊断计算）的范围。 可用的分析范围包括：

- **当前文档**：最小化实时代码分析范围，以仅对编辑器中的当前文件或可见文件执行。
- **打开的文档**：默认实时代码分析范围，如上一部分所述。
- **整个解决方案**：最大化实时代码分析范围，以对整个解决方案中的所有文件和项目执行。

可以按照以下步骤在“工具选项”对话框中选择上述自定义分析范围之一：

1. 要打开“选项”对话框，请在 Visual Studio 中的菜单栏上依次选择“工具” > “选项”  。

2. 在“选项”对话框中，依次选择“文本编辑器” > “C#”或“Basic” > “高级”    。

3. 选择所需的“后台分析范围”以自定义分析范围。 完成后选择“确定”。

![分析范围。](./media/background-analysis-scope.png)

> [!NOTE]
> 在 Visual Studio 2019 版本 16.5 之前，用户可以使用“工具” > “选项” > “文本编辑器” > “C#”或“Basic” > “高级”选项卡中的“启用完整解决方案分析”复选框，将诊断计算的分析范围自定义为整个解决方案。在以前的 Visual Studio 版本中，不支持最小化后台分析范围      。

## <a name="automatically-minimize-live-code-analysis-scope"></a>自动最小化实时代码分析范围

如果 Visual Studio 检测到可用的系统内存为 200 MB 或更少，它会自动将实时代码分析范围最小化为“当前文档”。 如果发生这种情况，则会显示一条警报，通知你 Visual Studio 已禁用某些功能。 如果需要，可以使用按钮切换回以前的分析范围。

![最小化分析范围的警报文本](./media/fsa_alert.png)

## <a name="see-also"></a>另请参阅

- [自动功能挂起](./automatic-feature-suspension.md)
- [节能模式功能请求](https://github.com/dotnet/roslyn/issues/38429)
