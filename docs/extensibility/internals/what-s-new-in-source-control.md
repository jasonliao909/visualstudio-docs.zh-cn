---
title: Visual Studio 2015 SDK 的源代码管理中的新增功能 |Microsoft Docs
description: 了解源代码管理 Vspackage 的功能并查看实现步骤的概述。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a289c15bd0e89b0d7106d2206a9858a8fe9a3763
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139550697"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK 的源代码管理的新增功能

[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]在中，可以通过实现源控件 VSPackage，提供深度集成的源代码管理解决方案。 本部分介绍源代码管理 Vspackage 的功能，并概述实现步骤。

## <a name="the-source-control-vspackage"></a>源代码管理 VSPackage

Visual Studio 支持两种类型的源代码管理解决方案。 在所有版本的 Visual Studio 中，仍可以集成源代码管理插件基于 API 的插件。 你还可以为源代码管理创建 VSPackage， [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 它提供了一个适用于需要高级别复杂和自治的源代码管理解决方案的深度集成。

VSPackage 可以将几乎任何类型的功能添加到 Visual Studio。 源代码管理 VSPackage 为 Visual Studio 提供了一个完整的源代码管理功能，从向用户显示的 UI 到与源代码管理系统的后端通信。

实现源代码管理 VSPackage 需要 "全部或无" 策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现一些源代码管理接口和新的 UI 元素 (对话框、菜单和工具栏) ，以涵盖整个源代码管理功能，以及任何包与 Visual Studio 成功集成所需的接口。

以下步骤概述了实现源代码管理包所需的操作。 有关详细信息，请参阅 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。

1. 创建提供专用源代码管理服务的 VSPackage。

2. 实现源控件相关服务中的接口，这些服务由 Visual Studio 的提供 (例如， <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> 接口) 。

3. 注册源代码管理 VSPackage。

4. 实现所有源代码管理 UI，包括菜单项、对话框、工具栏和上下文菜单。

5. 当事件处于活动状态且必须由 VSPackage 处理时，所有与源代码管理相关的事件均会传递到源代码管理 VSPackage。

6. 源代码管理 VSPackage 必须侦听事件（例如实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> 接口的事件），并跟踪 Project 文档 (TPD) 事件 (，如接口) 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 并执行必要的操作。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
