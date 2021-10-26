---
title: 配置任务 | Microsoft Docs
description: 通过 MSBuild 配置要在进程外运行的 MSBuild 任务，以便面向当前运行所在的上下文之外的上下文。
ms.custom: SEO-VS-2020
ms.date: 10/19/2021
ms.topic: conceptual
ms.assetid: 9aabe67a-1720-4bbf-80d3-822b3ccf75c0
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 6c29e1a6a2b2e4544c94fe4837076a3d2dbbe3c3
ms.sourcegitcommit: efe1d737fd660cc9183177914c18b0fd4e39ba8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2021
ms.locfileid: "130213235"
---
# <a name="configure-tasks"></a>配置任务

通过 MSBuild 可以配置要在进程外运行的 MSBuild 目标和任务，以便在当前运行整体生成所在的上下文之外的上下文中运行任务。 当运行与 64 位 MSBuild 不兼容的任务时，以及面向不同版本的 .NET Framework 时，这可能很有用。 

例如，当开发计算机运行 64 位的 .NET Framework 4.5 操作系统时，可面向 32 位 NET Framework 2.0 应用程序。 还可以面向运行 .NET Framework 4 或更早版本的计算机。 32 或 64 位与特定 .NET Framework 版本的组合称为“目标上下文”。

## <a name="tasks"></a>任务

 MSBuild 在进程外运行特定的生成任务，以面向更大的上下文集合。  例如，32 位 MSBuild 可在 64 位进程中运行生成任务。 这是由 `UsingTask` 实参和 `Task` 形参控制的。 .NET Framework 4.5 安装的目标将设置这些自变量和参数，无需进行任何更改即可生成适用于各种目标上下文的应用程序。

 如果要创建自己的目标上下文，必须正确设置这些实参和形参。 有关示例，请参阅 .NET Framework 4.5 Microsoft.Common.targets 文件和 Microsoft.Common.Tasks 文件 。  有关如何创建可用于多个目标上下文的自定义任务或如何修改现有任务的信息，请参阅[如何：配置目标和任务](../msbuild/how-to-configure-targets-and-tasks.md)。

## <a name="errors-arising-from-incorrect-configuration"></a>因配置不正确而导致出现的错误

配置中存在错误可能导致任务失败，并出现 [MSB4018](../msbuild/errors/msb4018.md) 或 [MSB4062](../msbuild/errors/msb4062.md) 错误。

## <a name="see-also"></a>请参阅

- [多定向](../msbuild/msbuild-multitargeting-overview.md)
