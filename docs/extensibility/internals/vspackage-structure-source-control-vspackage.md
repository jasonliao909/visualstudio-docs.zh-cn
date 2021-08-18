---
title: VSPackage 结构 (源代码管理 VSPackage) |Microsoft Docs
description: 了解源代码管理包 SDK，它为 VSPackage 提供准则，使源代码管理实施者能够与 Visual Studio 集成。
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
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d8d0ab61556e85c1ad817dd9ee454f58645ad96e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110457"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 结构（源代码管理 VSPackage）

源代码管理包 SDK 提供了创建 VSPackage 的指导原则，使源代码管理实施者能够将其源代码管理功能与 Visual Studio 环境集成。 VSPackage 是一个 COM 组件，通常 Visual Studio 集成开发环境按需加载 (IDE) 基于其注册表项中由包播发的服务。 每个 VSPackage 都必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 。 VSPackage 通常使用 Visual Studio IDE 提供的服务，并提供自己的某些服务。

VSPackage 声明其菜单项，并通过 .vsct 文件建立默认项状态。 Visual Studio IDE 显示处于此状态的菜单项，直到加载了 VSPackage。 然后，调用方法的 VSPackage 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 来启用或禁用菜单项。

## <a name="source-control-package-characteristics"></a>源代码管理包特性

源代码管理 VSPackage 已深度集成到 Visual Studio 中。 VSPackage 语义包括：

- 要实现的接口是接口的 VSPackage (`IVsPackage`) 

- UI 命令实现 ( 的接口的 .vsct 文件和实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) 

- 将 VSPackage 注册到 Visual Studio。

源代码管理 VSPackage 必须与这些其他 Visual Studio 实体通信：

- 项目

- 编辑器

- 解决方案

- Windows

- 正在运行的文档表

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>Visual Studio可能使用的环境服务

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

SVsRegisterScciProvider 服务

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>已实现并调用 VSIP 接口

源代码管理包是一个 VSPackage，因此它可以与注册到 Visual Studio 的其他 Vspackage 直接交互。 为了提供完整的源代码管理功能，源代码管理 VSPackage 可以处理项目或 shell 所提供的接口。

Visual Studio 中的每个项目都必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> 才能在 Visual Studio IDE 中被识别为项目。 但是，此接口专用于源代码管理。 预期受源代码管理的项目将实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 。 源代码管理 VSPackage 使用此接口来查询项目的内容，并提供 it 标志符号和绑定信息 (在服务器位置与受源代码管理) 的项目的磁盘位置之间建立连接所需的信息。

源代码管理 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> ，这反过来允许项目自行注册源代码管理，并检索其状态字形。

有关源代码管理 VSPackage 必须考虑的接口的完整列表，请参阅 [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)。

## <a name="see-also"></a>请参阅

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
