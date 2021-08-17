---
title: 相关服务和界面（源代码管理 VSPackage）
titleSuffix: ''
description: 了解 VISUAL STUDIO SDK 中与源代码管理 VSPackage 相关的接口。 包实现一些接口，并使用其他接口进行源代码管理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control packages, interfaces
- interfaces, source control packages
ms.assetid: 3e96e838-5675-46bb-99cf-40d420086038
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a51c5894234aba9b0689ee5ff940720ebab4c3e6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042070"
---
# <a name="related-services-and-interfaces-source-control-vspackage"></a>相关服务和界面（源代码管理 VSPackage）

本部分列出了 中与 VSPackage 相关的所有源代码管理接口 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。 源代码管理 VSPackage 实现其中一些接口，并使用其他接口来完成源代码管理任务。

## <a name="interfaces-implemented-by-and-for-source-control-vspackages"></a>由 和 为源代码管理 VSPackage 实现的接口

 在 中介绍了以下接口，源代码管理 VSPackage 根据所需的功能集实现 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 其中一部分接口。 某些接口标记为必需，必须由每个源代码管理 VSPackage 实现。

 对于包未实现这些接口， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供默认实现。 请注意，默认实现适用于未注册 VSPackage 且未控制任何项目的情况。 正确编写的源代码管理 VSPackage 实现所有必要的接口，而不是将其保留为这些接口的默认实现。

 源代码管理 VSPackage 必须实现封装以下部分或所有接口的专用服务。

 接口包括：

- 必需：源代码 (VSPackage、源代码管理存根、项目) 实现 接口。

- 建议：实体应实现此接口;否则，源代码管理功能可能会受到限制。

- 可选：实体可以实现此接口以提供更丰富的功能集。

| 接口 | 用途 | 实现者 | 实现？ |
| - | - |--------------------------|-------------|
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | 编辑器在修改或保存文件之前调用此接口。 如果签出失败，源代码管理 VSPackage 可以签出文件或拒绝操作。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | 此接口为项目提供基本的源代码管理功能，例如向源代码管理注册和注销项目，以及提供对基本源代码管理字形的支持。 | 源代码管理 VSPackage | 必需 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> | 此接口是使用 函数从 获取的，或者 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:System.Runtime.InteropServices.Marshal.QueryInterface%2A> 只是将实现 的对象强制转换 `IVsHierarchy` 到 `IVsSccProject2` 。 它用于获取项目中源代码管理下的文件，或通知项目当前源代码管理状态或位置。 | Project | 必需 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> | 集成模块使用此接口设置当前活动 VSPackage。 | 源代码管理 VSPackage | 必需 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> | 此接口基于订阅模型。 任何 VSPackage 都可以表明它想要接收文档事件，并且 shell 会就即将发生的事件提供建议。 它由 实现并处理，这反过来又将实现 的事件 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] `IVsTrackProjectDocumentsEvents2` 传递给 VSPackage。 | 源代码管理存根 | 必需 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | 此接口提供批处理、同步读/写操作和高级 `OnQueryAddFiles` 方法。 | 源代码管理存根 | 必需 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> | **解决方案资源管理器** 将新文件添加到项目中，或者重命名或删除项目的文件和文件夹时，项目和项目将调用此接口。 源代码管理 VSPackage 可以签出项目文件或取消操作。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents3> | **解决方案资源管理器** 和项目调用此接口，以响应对 IVstrackProjectDocuments3 接口的方法的调用。 源代码管理 VSPackage 可以跟踪批处理操作、同步读/写操作，以及使用更高级 `OnQueryAddFiles` 的方法。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccEnlistmentPathTranslation> | 此接口为 Web 项目提供登记管理支持。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManagerTooltip> | 此接口用于检索项目中源代码管理的文件的工具提示。 | 源代码管理 VSPackage | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccOpenFromSourceControl> | 此接口提供命名空间扩展支持。 | 源代码管理 VSPackage | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccControlNewSolution> | VSPackage 使用此接口将命名空间扩展集成到" **新建**"、" **打开**"或" **保存"** 对话框中。 因此，项目可以在创建时自动添加到源代码管理中，或在保存操作生效时添加到源代码管理中。 | 源代码管理 VSPackage | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> | VSPackage 使用此接口将其他字形定义为中节点的源代码管理 **解决方案资源管理器。** | 源代码管理 VSPackage | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccAddWebProjectFromSourceControl> | Web **项目的** "添加"对话框使用此接口。 它提供用于浏览源代码管理位置和打开以前添加到该位置的源代码管理存储库中的 Web 项目的方法。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> | 此接口支持异步 (后台) 从源代码管理加载项目。 | 源代码管理 VSPackage | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromSccProjectEvents> | 此接口允许项目监视 由 发起的异步加载的进度 <xref:Microsoft.VisualStudio.Shell.Interop.IVsAsynchOpenFromScc> 。 | Project | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | 此接口允许 IDE 查询活动源代码管理 VSPackage。 即使未注册活动源代码管理 VSPackage，IDE 也查询具有含义的源代码管理设置的值。 此接口由 实现并处理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 | 源代码管理存根 | 必需 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider> | 此接口用于注册源代码管理 VSPackage。 | 源代码管理存根 | 必需 |
| <xref:EnvDTE.SourceControl> | 此接口用于自动化。 因此，它只公开可在不显示任何 UI 的情况下执行的函数。 | 源代码管理 VSPackage | 可选 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> | 此接口用于将源代码管理设置保存在解决方案 (.sln) 文件中。 这些设置包括源代码管理位置和源代码管理状态标志。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> | 此接口用于将源代码管理设置保存在解决方案选项 (.suo) 文件中。 这可能包括特定于用户的源代码管理设置，例如当前用户的登记位置。 | 源代码管理 VSPackage | 建议 |
| <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> | 此接口用于监视事件，以便执行一些操作，例如，在关闭解决方案之前签入项目文件，或在打开项目时从源代码管理获取新文件。 | 源代码管理 VSPackage | 建议 |

## <a name="see-also"></a>请参阅
- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
