---
title: 工作区中的工作区文件Visual Studio |Microsoft Docs
description: 了解实现 IFileContextProvider 接口以支持对打开文件夹工作区的见解的文件上下文提供程序。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 92658912e6910f21c6e79f779dff66b6c8b85a04b55f138a0971903789d4c8a2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121374580"
---
# <a name="workspace-file-contexts"></a>工作区文件上下文

对打开文件夹工作区 [的所有](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) 见解都由实现 接口的"文件上下文提供程序" <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> 生成。 这些扩展可能会查找文件夹或文件中的模式、读取 MSBuild 文件和生成文件、检测包依赖项等，以便累积定义文件上下文所需的见解。 文件上下文本身不执行任何操作，而是提供其他扩展插件随后可以处理的数据。

<xref:Microsoft.VisualStudio.Workspace.FileContext>每个 都有 `Guid` 一个与之关联的 ，用于标识它所携带的数据类型。 工作区稍后 `Guid` 会使用它来匹配通过 属性使用数据的 <xref:Microsoft.VisualStudio.Workspace.FileContext.Context> 扩展。 导出文件上下文提供程序时，会使用元数据来标识可能生成数据 `Guid` 的文件上下文。

定义后，文件上下文可以与工作区中任意数目的文件或文件夹相关联。 给定的文件或文件夹可以与任意数量的文件上下文相关联。 这是一种多对多关系。

文件上下文的最常见方案与生成、调试和语言服务相关。 有关详细信息，请参阅与这些方案相关的其他主题。

## <a name="file-context-lifecycle"></a>文件上下文生命周期

的生命周期 `FileContext` 是不确定的。 组件随时都可以异步请求某些上下文类型集。 将查询支持某些请求上下文类型的子集的提供程序。 实例 `IWorkspace` 通过 方法充当使用者和提供程序之间的中间 <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> 人。 使用者可能会请求上下文，并基于上下文执行一些短期操作，而其他使用者可能会请求上下文并维护长期引用。

文件可能会发生更改，导致文件上下文过时。 提供程序可以在 上发送事件 `FileContext` ，以通知使用者更新。 例如，如果为某些文件提供了生成上下文，但磁盘上更改使该上下文无效，则原始生成者可以调用 事件。 任何使用者仍引用 `FileContext` ，然后可以重新查询新的 `FileContext` 。

>[!NOTE]
>没有向使用者推送模型。 使用者在请求后不会收到提供程序的新 `FileContext` 通知。

## <a name="expensive-file-context-computations"></a>昂贵的文件上下文计算

从磁盘读取文件内容可能很昂贵，尤其是在提供程序需要解决文件之间的关系时。 例如，可以查询提供程序获取某些源文件的文件上下文，但文件上下文依赖于项目文件的元数据。 分析项目文件或使用项目文件MSBuild成本高昂。 相反，扩展可以导出 以 `IFileScanner` 在 `FileDataValue` 工作区索引编制期间创建数据。 现在，当系统询问文件上下文时， `IFileContextProvider` 可以快速查询该索引数据。 有关索引的详细信息，请参阅 [工作区索引主题](workspace-indexing.md) 。

>[!WARNING]
>请谨慎考虑其他 `FileContext` 计算成本可能很高的方式。 某些 UI 交互是同步的，依赖于大量 `FileContext` 请求。 示例包括打开编辑器选项卡和 **打开解决方案资源管理器上下文** 菜单。 这些操作会提出许多生成上下文类型请求。

## <a name="file-context-related-apis"></a>与文件上下文相关的 API

- <xref:Microsoft.VisualStudio.Workspace.FileContext> 保存数据和元数据。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> 和 <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider`1> 创建文件上下文。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextProviderAttribute> 导出文件上下文提供程序。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> 用于使用者获取文件上下文。
- <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> 定义打开文件夹将消耗的生成上下文类型。

## <a name="file-context-actions"></a>文件上下文操作

虽然 本身只是有关某些文件 (数据) ，但 是一种表示和操作 `FileContext` <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> 该数据的方法。 `IFileContextAction` 在用法上非常灵活。 其中两个最常见的情况是生成和调试。

## <a name="reporting-progress"></a>报告进度

<xref:Microsoft.VisualStudio.Workspace.IFileContextActionBase.ExecuteAsync%2A>方法被传递 `IProgress<IFileContextActionProgressUpdate>` ，但参数不应用作该类型。 `IFileContextActionProgressUpdate` 为空接口，调用 `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` 可能会引发 `NotImplementedException` 。 相反， `IFileContextAction` 必须在必要时将参数强制转换到另一种类型。

有关应用程序提供的类型Visual Studio，请参阅相应方案的文档。

## <a name="file-context-action-related-apis"></a>与文件上下文操作相关的 API

- <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> 基于 执行某些行为 `FileContext` 。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextActionProvider> 创建 的实例 `IFileContextAction` 。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextActionProviderAttribute> 导出类型 `IWorkspaceProviderFactory<IFileContextActionProvider>` 。

## <a name="file-watching"></a>文件监视

工作区侦听文件更改通知，并可通过 提供 <xref:Microsoft.VisualStudio.Workspace.IFileWatcherService> <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> 。 与"ExcludedItems"设置匹配的文件不会生成文件通知事件。 事件之间的阈值用于简化通知和重复减少。 需要响应文件更改时，应订阅此服务。

>[!TIP]
>默认情况下， [工作区的索引服务](workspace-indexing.md) 订阅文件事件。 文件添加和修改将导致针对 `IFileScanner` 该文件的新数据调用相关的 事件。 文件删除将删除索引数据。 无需订阅文件观察 `IFileScanner` 程序服务。

## <a name="next-steps"></a>后续步骤

* [索引](workspace-indexing.md) - 工作区索引收集并保存有关工作区的信息。
* [工作区](workspaces.md) - 查看工作区概念和设置存储。
