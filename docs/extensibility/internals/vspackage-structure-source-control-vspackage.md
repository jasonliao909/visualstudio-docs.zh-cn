---
title: VSPackage 结构 (源代码管理 VSPackage) |Microsoft Docs
description: 了解源代码管理包 SDK，它为 VSPackage 提供与源代码管理实现程序集成Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b95c382342675d79c0c6e854b5fc087d495827e2
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898817"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 结构（源代码管理 VSPackage）

源代码管理包 SDK 提供了创建 VSPackage 的准则，该 VSPackage 允许源代码管理实现者将其源代码管理功能与 Visual Studio环境集成。 VSPackage 是 COM 组件，通常由 Visual Studio 集成开发环境 (IDE) 基于包在其注册表项中播发的服务按需加载。 每个 VSPackage 都必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 。 VSPackage 通常使用 Visual Studio IDE 提供的服务，并提供自己的一些服务。

VSPackage 声明其菜单项，通过 .vsct 文件建立默认项状态。 IDE Visual Studio显示此状态中的菜单项，直到加载 VSPackage。 随后，将调用 VSPackage 的 方法实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 来启用或禁用菜单项。

## <a name="source-control-package-characteristics"></a>源代码管理包特征

源代码管理 VSPackage 已深度集成到 Visual Studio。 VSPackage 语义包括：

- 作为接口接口的 VSPackage 实现 (`IVsPackage` 接口) 

- UI 命令 (.vsct 文件和 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口接口的) 

- 将 VSPackage 注册到 Visual Studio。

源代码管理 VSPackage 必须与以下其他Visual Studio通信：

- 项目

- 编辑器

- 解决方案

- Windows

- 正在运行的文档表

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>Visual Studio使用的环境服务

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

SVsRegisterScciProvider 服务

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>实现和调用的 VSIP 接口

源代码管理包是一个 VSPackage，因此它可以直接与注册到 VISUAL STUDIO 的其他 VSPackage 交互。 为了提供全面源代码管理功能，源代码管理 VSPackage 可以处理项目或 shell 提供的接口。

要识别 Visual Studio IDE 中的项目，必须实现 Visual Studio <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> 项目。 但是，此接口的专用性不足以进行源代码管理。 应受源代码管理的项目实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 。 源代码管理 VSPackage 使用此接口来查询项目的内容，并提供其字形和绑定信息 (这些信息用于在受源代码管理) 的项目的服务器位置和磁盘位置之间建立连接。

源代码管理 VSPackage 实现 ，这反过来又允许项目自行注册源代码管理并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 检索其状态字形。

有关源代码管理 VSPackage 必须考虑的接口的完整列表，请参阅 [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)。

## <a name="see-also"></a>另请参阅

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
