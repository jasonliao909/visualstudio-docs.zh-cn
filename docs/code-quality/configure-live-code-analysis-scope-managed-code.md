---
title: 为 .NET 配置实时代码分析范围
ms.date: 09/01/2020
description: 了解 Visual Studio 中的背景分析。 了解如何将分析限制为可见文档、所有打开的文档或所有文件和项目。
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
ms.openlocfilehash: 0e02ea853f402cfcad1d36547e747add2e5a3265930d34561f9d84a7797bd0b2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121312334"
---
# <a name="configure-live-code-analysis-for-net"></a>为 .NET 配置实时代码分析

Visual Studio编辑器中编辑源文件时，会执行一系列实时代码分析（也称为后台分析）。  对于可接受的 IDE 编辑体验，其中一Visual Studio分析是必需的。 其中一些功能用于改进 IDE 功能的响应能力。 虽然其中一些功能是启用其他 IDE 功能，例如 Roslyn 分析器中的诊断和代码修复。 根据功能，这些分析可以按如下方式分组：

- **诊断的背景计算**：分析以计算源文件中的错误、警告和建议。 这些诊断在错误列表中显示为条目，在编辑器中显示为一个锯齿。 它们可分为两类：
  - C# Visual Basic编译器诊断
  - Roslyn 分析器诊断，其中包括：

    - 用于代码样式建议的内置 IDE 分析器
    - 用于代码质量建议的内置 CA 分析器
    - 为当前解决方案 [中的](./install-roslyn-analyzers.md) 项目安装的第三方分析器包。

- **其他背景分析**：用于改进 IDE 功能的响应Visual Studio交互的分析。 此类分析的一些示例包括：
  - 打开的文件的背景分析。
  - 使用打开的文件对项目进行后台编译，以实现符号以提高某些 IDE 功能的响应能力。
  - 生成语法和符号缓存。
  - 检测源文件（如窗体、控件等）的设计器关联。

## <a name="default-analysis-scope"></a>默认分析范围

默认情况下，对诊断的背景计算执行实时代码分析，分析所有在 Visual Studio。  上面提到的 _其他背景分析_ 很少针对所有项目执行，这些项目至少有一个打开的文件。 虽然几乎不为整个解决方案执行背景分析。

## <a name="custom-analysis-scope"></a>自定义分析范围

每个背景分析的默认范围已针对大多数客户方案和解决方案优化了最佳用户体验、功能和性能。 但是，在某些情况下，客户可能需要自定义此范围以减少或增加背景分析。 例如：

- 省电模式：如果用户在笔记本电脑电池上运行，他们可能需要将功耗降至最低，延长电池使用时间。 在此方案中，他们希望最大程度地减少后台分析。
- 按需代码分析：如果用户更喜欢关闭实时分析器执行并按需手动运行代码分析，则他们希望最大程度地减少后台分析。 请参阅 [如何：手动按需运行代码分析](./how-to-run-code-analysis-manually-for-managed-code.md)。
- 完整解决方案分析：如果用户希望始终在解决方案的所有文件中查看所有诊断，无论它们是否在编辑器中打开。 在此方案中，他们希望将后台分析范围最大化为整个解决方案。

从 Visual Studio 2019 版本 16.5 开始，用户可以显式自定义 C# 和 Visual Basic 项目的所有实时代码分析（包括诊断计算）的范围。 可用的分析范围包括：

- **当前文档**：将实时代码分析范围最小化为仅对编辑器中的当前文件或可见文件执行。
- **打开文档**：默认实时代码分析范围，如上一部分所述。
- **整个解决方案**：最大化实时代码分析范围，以针对整个解决方案中所有文件和项目执行。

可以按照以下步骤在"工具选项"对话框中选择上述自定义分析范围之一：

1. 若要打开"**选项"** 对话框，请选择"工具选项"Visual Studio **菜单**  >  **栏上**。

2. 在"**选项"** 对话框中，选择"**文本编辑器**  >  **C#"或**"**基本高级**  >  **"。**

3. 选择所需的 **"背景分析范围"** 以自定义分析范围。 完成后 **，** 选择"确定"。

![分析范围。](./media/background-analysis-scope.png)

> [!NOTE]
> 在 Visual Studio 2019 版本 16.5 之前，用户可以使用"工具选项""文本编辑器  >    >    >  **C#"**  >  或"基本高级"选项卡中的"启用完整解决方案分析"复选框，自定义诊断计算的分析范围到整个解决方案。不支持在早期版本中最小化后台分析Visual Studio范围。

## <a name="automatically-minimize-live-code-analysis-scope"></a>自动最小化实时代码分析范围

如果Visual Studio检测到 200 MB 或更少的系统内存可用，则会自动将实时代码分析范围最小化为"当前文档"。 如果发生这种情况，则会出现一条警报，Visual Studio禁用某些功能。 如果需要，可以使用按钮切换回以前的分析范围。

![警报文本最小化分析范围](./media/fsa_alert.png)

## <a name="see-also"></a>另请参阅

- [自动功能挂起](./automatic-feature-suspension.md)
- [电源保存模式功能请求](https://github.com/dotnet/roslyn/issues/38429)
