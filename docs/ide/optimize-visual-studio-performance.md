---
title: 在 Visual Studio 速度较慢的情况下提高性能
titleSuffix: ''
description: 如果发现其运行速度缓慢，了解如何提高Visual Studio性能。
ms.custom: SEO-VS-2020
ms.date: 04/12/2022
ms.topic: conceptual
helpviewer_keywords:
- performance [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
f1_keywords:
- vs.performancecenter
ms.workload:
- multiple
ms.openlocfilehash: 6843dd866ec5e214928eddc0f8850e9047860e0a
ms.sourcegitcommit: ad26b6583e7a3214eda233f1cbaff80879a8b5b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2022
ms.locfileid: "141674699"
---
# <a name="optimize-visual-studio-performance"></a>优化 Visual Studio 性能

如果发现 Visual Studio 运行速度缓慢，本文提供了一些建议。 有关如何提高性能的更多建议，还可以查看 [Visual Studio 性能提示和技巧](../ide/visual-studio-performance-tips-and-tricks.md)。

## <a name="upgrade-visual-studio"></a>升级 Visual Studio

如果当前使用的是早期版本的Visual Studio（例如 Visual Studio 2017 或 Visual Studio 2019），请免费下载 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads)，查看其改进的性能。 解决方案的加载速度比早期版本快得多，其他领域的性能也有所改进。 你可以在已安装 Visual Studio 早期版本或更高版本的计算机上安装 Visual Studio。 有关详细信息，请参阅[并行安装Visual Studio版本](../install/install-visual-studio-versions-side-by-side.md)。

::: moniker range="vs-2017"

如果已使用 Visual Studio 2017，请确保正在运行版本 15.6 或更高版本。 数据显示，在版本 15.6 中，解决方案的加载速度最高可提升两到三倍。 可从[此处](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)下载。 有关详细信息，请参阅[使用 Visual Studio 2017 版本 15.6 博客文章更快地加载解决方案](https://devblogs.microsoft.com/visualstudio/load-solutions-faster-with-visual-studio-2017-version-15-6/)。

::: moniker-end

## <a name="extensions-and-tool-windows"></a>扩展和工具窗口

你可能已安装扩展，Visual Studio速度缓慢。 有关管理扩展以提高性能的帮助，请参阅[更改扩展设置以提高性能](../ide/optimize-visual-studio-startup-time.md#extensions)。

同样，你可能有工具窗口Visual Studio速度缓慢。 有关管理工具窗口的帮助，请参阅[更改工具窗口设置以提高性能](../ide/optimize-visual-studio-startup-time.md#tool-windows)。

## <a name="hardware"></a>硬件

如果考虑升级硬件，固态硬盘 (SSD) 对性能的影响比额外的 RAM 或更快的 CPU 更大。

若要添加 SSD，为了获得最佳性能，应将 Windows 安装在 SSD 上，而非硬盘驱动器 (HDD)。 Visual Studio解决方案的驱动器位置似乎并不重要。

此外，不要从 U 盘运行解决方案。 请将其复制到 HDD 或 SSD。

## <a name="help-us-improve"></a>帮助我们改进

你的反馈有助于我们改进。 使用“报告问题”功能来“记录”跟踪并发送给我们。 从菜单栏中选择 **HelpSend** >  **FeedbackReport** >  a Problem。 有关详细信息，请参阅[如何报告 Visual Studio 的问题](../ide/how-to-report-a-problem-with-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [性能提示和技巧](../ide/visual-studio-performance-tips-and-tricks.md)