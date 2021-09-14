---
title: 禁用旧代码分析
ms.date: 10/04/2019
description: 了解如何在 Visual Studio 中启用和关闭二进制代码Visual Studio。 请参阅如何在托管代码项目中配置此功能。
ms.custom: SEO-VS-2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.openlocfilehash: c687a8c2fd1293913670af4489dfb5c9663344c1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601304"
---
# <a name="how-to-enable-and-disable-binary-code-analysis-for-managed-code"></a>如何：为托管代码启用和禁用二进制代码分析

可以配置旧版代码分析 (二进制) 生成托管代码项目后运行。 还可以针对每个生成配置使用不同的设置，例如调试和发布。

> [!NOTE]
> 旧版分析不适用于较新的项目类型，例如 .NET Core 和 .NET Standard应用。 这些项目使用[基于.NET Compiler Platform](roslyn-analyzers-overview.md)分析器实时和生成时分析代码。 有关在这些项目中禁用源代码分析的信息，请参阅 [如何禁用源代码分析](disable-code-analysis.md)。

启用或禁用旧代码分析：

1. 在 **解决方案资源管理器** 中，选择并按住 (或右键单击) ，然后选择"属性 **"。**

2. 在项目的"属性"对话框中，转到 **"Code Analysis选项卡**。

3. 在"配置"中 **指定生成类型，** 在"平台"中指定 **目标平台**。  (Non-.NET Core/.NET Standard projects.) 

::: moniker range="vs-2017"

4. 若要启用或禁用自动代码分析，请选中或清除"在生成 **Code Analysis启用** 代码分析"复选框。

::: moniker-end

::: moniker range=">=vs-2019"

4. 若要启用或禁用自动代码分析，请在"二进制分析器"部分选中或清除"生成时 **运行"** 复选框。

   ![在生成选项中运行二进制代码Visual Studio](media/run-on-build-binary-analyzers.png)

::: moniker-end

> [!NOTE]
> 对生成禁用二进制代码分析不会影响基于[](roslyn-analyzers-overview.md).NET Compiler Platform分析器，如果将它们作为一个包安装为 NuGet分析器，则这些分析器始终在生成时执行。 有关从这些分析器禁用分析的信息，请参阅 [如何禁用源代码分析](disable-code-analysis.md)。
