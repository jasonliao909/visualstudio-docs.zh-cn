---
title: MSBuild 17.0 中的新增功能 | Microsoft Docs
description: 了解已针对 MSBuild 17.0 更改和更新的功能和属性，并链接到发行说明。
ms.date: 10/25/2021
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 5ca502169d2c238be7871ca19cc9372e91f4207a
ms.sourcegitcommit: abfcccf63234819c75a61bf2c4c7f710a9d23cdb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2021
ms.locfileid: "132250590"
---
# <a name="whats-new-in-msbuild-170"></a>MSBuild 17.0 中的新增功能

本文介绍 MSBuild 17.0 中的重要更新。 有关详细的发行说明，请参阅 [MSBuild 17.0.0](https://github.com/dotnet/msbuild/releases/tag/v17.0.0)。

随 [Visual Studio 2022](../ide/whats-new-visual-studio-2022.md) 和 [.NET 6.0](/dotnet/) 一起提供的 MSBuild 17.0。

## <a name="changed-path"></a>更改的路径

 MSBuild 安装在每版 Visual Studio 下的 \Current  文件夹中，可执行文件位于 \Bin  子文件夹中。 例如，与 Visual Studio 2022 Community 一起安装的 MSBuild.exe 的路径为 C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe。你也可以使用以下 PowerShell 模块来定位 MSBuild：[vssetup.powershell](https://github.com/Microsoft/vssetup.powershell) 。

## <a name="changed-properties"></a>更改的属性

 下列 MSBuild 属性已因新版本号而更新。

- 此版工具的 `MSBuildToolsVersion` 保留为“Current”。 程序集版本与 Visual Studio 2017 和 Visual Studio 2019 中的程序集版本相同，为 15.1.0.0。

- 此版工具的 `VisualStudioVersion` 为“17.0”

## <a name="64-bit"></a>64 位

MSBuild.exe 以前有 32 位和 64 位版本，但现在默认为 64 位版本。 Visual Studio 2022 对所有生成使用 64 位版本的 MSBuild。 32 位版本仍可用，但建议将所有生成切换到 64 位版本。

对于任务所有者，这意味着当 MSBuild 加载任务时，它将尝试在 64 位进程中加载它。 建议考虑将任务更新为在 64 位进程中运行，但为了实现兼容性，可告知 MSBuild 你的任务仅在其 [UsingTask](../msbuild/how-to-configure-targets-and-tasks.md) 中以 32 位运行。

## <a name="performance-improvements"></a>性能改进

MSBuild 速度更快了！ 此版本的重点是提高许多常见场景的性能。 MSBuild 17.0 可更快地生成更大的项目。

## <a name="net-versions"></a>.NET 版本

MSBuild（和 Visual Studio）现面向 .NET Framework 4.7.2 和 .NET 6.0。 若想要使用新的 MSBuild API 功能，必须升级程序集，但现有代码将继续工作。

## <a name="logs"></a>日志

二进制日志较小，包含更多信息。

## <a name="breaking-changes"></a>中断性变更

- 无法再在属性函数中调用方法 `GetType()`。
- 适用于 .NET 的 MSBuild 面向 .NET 6。

## <a name="other-behavior-changes"></a>其他行为变更

- `MSBuildCopyContentTransitively` 现在默认启用，确保了增量生成的输出文件夹中的一致性。

有关此版本中的更多更改，请参阅详细的发行说明。

## <a name="see-also"></a>另请参阅

- [MSBuild](../msbuild/msbuild.md)
