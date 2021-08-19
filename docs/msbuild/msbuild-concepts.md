---
title: MSBuild 概念 | Microsoft Docs
description: 了解如何使用 MSBuild 属性、项、任务和目标来指定生成组件和过程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, concepts
ms.assetid: 083b8ba3-e4ad-45af-bb5d-3bc81d406131
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: b1da1b7af0d20d5b1f20778a2818745a42b5e33f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143152"
---
# <a name="msbuild-concepts"></a>MSBuild 概念

MSBuild 提供可用于控制生成平台如何生成软件的基本 XML 架构。 若要指定生成中的组件及其生成方式，请使用这四个 MSBuild 部件：属性、项、任务和目标。

## <a name="related-topics"></a>相关主题

| Title | 描述 |
| - | - |
| [MSBuild 属性](../msbuild/msbuild-properties.md) | 介绍属性和属性集合。 属性是可用于配置生成的键/值对。 |
| [MSBuild 项](../msbuild/msbuild-items.md) | 介绍项和项集合。 项是生成系统的输入，通常表示文件。 |
| [MSBuild 目标](../msbuild/msbuild-targets.md) | 介绍如何按特定的顺序将任务组合到一起，并允许从命令行调用生成过程的各个部分。 |
| [MSBuild 任务](../msbuild/msbuild-tasks.md) | 演示如何创建 MSBuild 可用于执行原子生成操作的可执行代码单元。 |
| [比较属性和项](../msbuild/comparing-properties-and-items.md) | 比较 MSBuild 属性和项。 二者都用于将信息传递给任务、计算条件，以及存储可在整个项目文件中引用的值。 |
| [MSBuild 特殊字符](../msbuild/msbuild-special-characters.md) | 说明如何转义 MSBuild 为在特定上下文中作特殊用途而保留的某些字符。 |
| [演练：从头创建 MSBuild 项目文件](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md) | 演示如何只使用文本编辑器以增量方式创建基本项目文件。 |
| [演练：使用 MSBuild](../msbuild/walkthrough-using-msbuild.md) | 介绍 MSBuild 的构建基块，并演示如何在不关闭 Visual Studio 集成开发环境 (IDE) 的情况下编写、操作和调试 MSBuild 项目。 |
| [MSBuild 如何生成项目](build-process-overview.md) | 介绍了 MSBuild 中使用的内部生成过程 |
| [MSBuild 参考](../msbuild/msbuild-reference.md) | 链接到包含参考信息的文档。 |
| [MSBuild](../msbuild/msbuild.md) | 概述了项目文件的 XML 架构，并演示其如何控制生成软件的过程。 |
