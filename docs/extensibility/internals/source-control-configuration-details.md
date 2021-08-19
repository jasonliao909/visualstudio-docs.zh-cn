---
title: 源代码管理配置详细信息|Microsoft Docs
description: 了解如何在 Visual Studio 中实现项目类型的源代码管理，这涉及到将项目系统或编辑器配置为请求权限。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], configuration details
ms.assetid: adbee9fc-7a2e-4abe-a3b8-e6615bcd797f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 22b4cccf05fb3f18b809d3d76cade14c57ea0188
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102344"
---
# <a name="source-control-configuration-details"></a>源代码管理配置详细信息
若要实现源代码管理，需要正确配置项目系统或编辑器以执行以下操作：

- 请求转换为已更改状态的权限

- 请求保存文件的权限

- 请求在项目中添加、删除或重命名文件的权限

## <a name="request-permission-to-transition-to-changed-state"></a>请求转换为已更改状态的权限
 项目或编辑器必须通过调用 来请求转换为 (状态) 更改的权限 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 。 实现 的每个编辑器都必须调用 并接收批准，才能在返回 之前从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 环境 `True` 更改文档 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData.IsDocDataDirty%2A> 。 项目实质上是项目文件的编辑器，因此，对项目文件实现更改状态跟踪的责任与文本编辑器对项目文件执行更改状态跟踪的责任相同。 环境处理解决方案的已更改状态，但必须处理解决方案引用但不存储的任何对象的更改状态，如项目文件或其项。 一般情况下，如果项目或编辑器负责管理项的持久性，则它负责实现更改状态跟踪。

 为了响应 `IVsQueryEditQuerySave2::QueryEditFiles` 调用，环境可以执行以下操作：

- 拒绝对更改的调用，在这种情况下，编辑器或项目必须保持未更改 (保持) 状态。

- 指示应重新加载文档数据。 对于项目，环境将重新加载项目的数据。 编辑器必须通过其实现从磁盘重新加载 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> 数据。 在任一情况下，重新加载数据时，项目或编辑器中的上下文都可以更改。

  将适当的调用放大到现有代码库是一 `IVsQueryEditQuerySave2::QueryEditFiles` 项复杂而困难的任务。 因此，应在创建项目或编辑器期间集成这些调用。

## <a name="request-permission-to-save-a-file"></a>请求保存文件的权限
 在项目或编辑器保存文件之前，它必须调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> 。 对于项目文件，解决方案会自动完成这些调用，解决方案知道何时保存项目文件。 编辑器负责进行这些调用，除非 的编辑器实现 `IVsPersistDocData2` 使用帮助程序函数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 。 如果编辑器按 `IVsPersistDocData2` 此方式实现，则调用 `IVsQueryEditQuerySave2::QuerySaveFile` 或 `IVsQueryEditQuerySave2::QuerySaveFiles` 。

> [!NOTE]
> 始终提前进行这些调用，即，在编辑器能够接收取消时。

## <a name="request-permission-to-add-remove-or-rename-files-in-the-project"></a>请求在文件中添加、删除或重命名Project
 在项目可以添加、重命名或删除文件或目录之前，它必须调用相应的方法来 `IVsTrackProjectDocuments2::OnQuery*` 从环境请求权限。 如果授予了权限，则项目必须完成该操作，然后调用相应的方法来通知 `IVsTrackProjectDocuments2::OnAfter*` 环境该操作已完成。 项目必须为所有文件调用 接口的方法 (例如，特殊) <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 文件，而不只是父文件。 文件调用是必需的，但目录调用是可选的。 如果项目具有目录信息，则它应调用相应的方法，但如果该项目没有此信息，则环境 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 将推断目录信息。

 项目不应在项目打开或关闭 `IVsTrackProjectDocuments2` 时调用 的方法。 在启动时需要此信息的侦听器可以等待事件并浏览解决方案以 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A> 查找所需的信息。 关闭时，不需要此信息。 `IVsTrackProjectDocuments2` 从 提供 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> 。

 对于每个添加、重命名和删除操作，都有 `OnQuery*` 一个 方法和 `OnAfter*` 一个 方法。 调用 `OnQuery*` 方法以请求添加、重命名或删除文件或目录的权限。 在添加、重命名或删除文件或目录并且项目状态反映新状态后调用 `OnAfter*` 方法。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
