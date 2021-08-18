---
title: 解决方案概述
description: 了解解决方案的内部机制，适用于想要在扩展中处理Visual Studio开发人员。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6ea779481103042241821086d04e874d10d2ced2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028717"
---
# <a name="solutions-overview"></a>解决方案概述

解决方案是一组一个或多个项目，这些项目协同工作以创建应用程序。 与解决方案相关的项目和状态信息存储在两个不同的解决方案文件中。 [解决方案 (.sln) ](solution-dot-sln-file.md)文件基于文本，可以置于源代码控制之下，并可在用户之间共享。 解决方案 [用户选项 (.suo) 是](solution-user-options-dot-suo-file.md) 二进制文件。 因此，.suo 文件不能放置在源代码控制下，并且包含特定于用户的信息。

任何 VSPackage 都可以写入任一类型的解决方案文件。 由于文件的性质，实现了两个不同的接口来写入它们。 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> 将文本信息写入 .sln 文件，接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 将二进制流写入 .suo 文件。

> [!NOTE]
> 项目无需将自身的条目显式写入解决方案文件中;环境为项目处理该操作。 因此，除非要专门将其他内容添加到解决方案文件，否则不需要以这种方式注册 VSPackage。

每个支持解决方案持久性的 VSPackage 都使用三个接口：接口（由环境实现，由 VSPackage 调用）和 和 （这两个接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> `IVsPersistSolutionProps` `IVsPersistSolutionOpts` 都由 VSPackage 实现）。 只有在 VSPackage 将私有信息写入 .suo 文件时，才需要实现 `IVsPersistSolutionOpts` 接口。

打开解决方案时，将发生以下过程。

1. 环境读取解决方案。

2. 如果环境找到 `CLSID` ，它将加载相应的 VSPackage。

3. 如果加载了 VSPackage，则环境会 `QueryInterface` 为 VSPackage 所需的接口调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 接口。

   - 从 .sln 文件读取时，环境会调用 `QueryInterface` `IVsPersistSolutionProps` 。

   - 从 .suo 文件读取时，环境会调用 `QueryInterface` `IVsPersistSolutionOpts` 。

   有关使用这些文件的特定信息，请参阅解决方案[ (。Sln) 文件和](../../extensibility/internals/solution-dot-sln-file.md)[解决方案用户选项 (。Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

> [!NOTE]
> 如果要创建包含两个项目配置的新解决方案配置，并且从生成中排除第三个项目配置，则需要使用属性页 UI 或自动化。 不能直接更改解决方案生成管理器配置及其属性，但可以在自动化模型中使用 DTE 中的 类操作 `SolutionBuild` 解决方案生成管理器。 有关配置解决方案的更多信息，请参阅 [解决方案配置](../../extensibility/internals/solution-configuration.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
