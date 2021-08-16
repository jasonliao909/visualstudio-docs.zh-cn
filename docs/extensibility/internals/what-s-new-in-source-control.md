---
title: Visual Studio 2015 SDK | 中的源代码管理新增功能Microsoft Docs
description: 了解源代码管理 VSPackage 的功能，并查看实现步骤的概述。
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
ms.openlocfilehash: 9f828aa153ddba9fcc0bb6db07084277b48b7c862447bd2b8fc4e6681123ab44
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431729"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK 源代码管理中的新增功能

在 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 中，可以通过实现源代码管理 VSPackage 来提供深度集成的源代码管理解决方案。 本部分介绍源代码管理 VSPackage 的功能，并概述实现步骤。

## <a name="the-source-control-vspackage"></a>源代码管理 VSPackage

Visual Studio支持两种类型的源代码管理解决方案。 在所有版本的 Visual Studio 中，仍可以集成基于源代码管理插件 API 的插件。 还可以为源代码管理创建 VSPackage，该源代码管理提供适用于需要高度复杂性和自治的源代码管理解决方案的深层 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 集成路径。

VSPackage 几乎可以将任何类型的功能添加到Visual Studio。 源代码管理 VSPackage 为Visual Studio提供完整的源代码管理功能，从呈现给用户的 UI 到与源代码管理系统的后端通信。

实现源代码管理 VSPackage 需要"全部或无"策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现大量源代码管理接口和新的 UI 元素 (对话框、菜单和工具栏) ，以涵盖整个源代码管理功能，以及任何包成功与 Visual Studio 集成所需的接口。

以下步骤概述了实现源代码管理包所需的内容。 有关详细信息，请参阅 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。

1. 创建提供专用源代码管理服务的 VSPackage。

2. 实现源代码管理相关服务中的接口，这些接口由 Visual Studio (，例如 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> 接口) 。

3. 注册源代码管理 VSPackage。

4. 实现所有源代码管理 UI，包括菜单项、对话框、工具栏和上下文菜单。

5. 所有与源代码管理相关的事件在活动时传递给源代码管理 VSackage，并且必须由 VSPackage 处理。

6. 源代码管理 VSPackage 必须侦听事件，例如实现 接口的事件，以及跟踪 Project 文档 (TPD) 事件 (（由接口) 实现）并执行必要的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> 操作。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
