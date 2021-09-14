---
title: Visual StudioShell |Microsoft Docs
description: Visual Studio shell 是 Visual Studio 集成的主要代理，提供基本功能并支持 VSPackage 之间的交叉通信。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- shell, Visual Studio
- Visual Studio, shell
ms.assetid: cb124ef4-1a6b-4bfe-bfbf-295ef9c07f36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7f57defce4eb9b46185f0d266822b5f4a0d2e719
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600844"
---
# <a name="visual-studio-shell"></a>Visual Studio Shell
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]shell 是 中集成的主要代理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 shell 提供必要的功能，使 VSPackage 能够共享公用服务。 由于 的体系结构目标是将主要功能托管在 VSPackage 中，因此 shell 是一个框架，用于提供基本功能并支持其组件 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 之间的交叉通信。

## <a name="shell-responsibilities"></a>Shell 职责
 shell 具有以下关键职责：

- 支持 (COM 接口) 用户界面用户界面 (元素) 。 其中包括默认菜单和工具栏、文档窗口框架或多文档界面 (MDI) 子窗口、工具窗口框架和停靠支持。

- 维护正在运行的文档表 (RDT) 中当前打开的所有文档的运行列表，以便协调文档的持久性，并保证不能以多种方式或不兼容的方式打开一个文档。

- 支持命令路由和命令处理接口 `IOleCommandTarget` 。

- 在适当的时间加载 VSPackage。 延迟加载 VSPackage 是提高 shell 性能所必需的。

- 管理提供基本 shell 功能的某些共享服务（如 ）和 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> （提供基本的窗口功能）。

- 管理解决方案 (.sln) 文件。 解决方案包含相关项目组，类似于工作区 (.dsw) 6.0 Visual C++文件。

- 跟踪 shell 范围的选择、上下文和货币。 shell 跟踪以下类型的项：

  - 当前项目

  - 当前项目项或当前项 ID <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>

  - "属性"窗口 **的当前选择** 或 `SelectionContainer`

  - 用于控制命令、菜单和工具栏可见性的 UI 上下文 ID 或 CmdUIGuid

  - 当前活动元素，例如活动窗口、文档和撤消管理器

  - 驱动动态帮助的用户上下文属性

  shell 还协调已安装的 VSPackage 和当前服务之间的通信。 它支持 shell 的核心功能，并使它们可用于中集成的所有 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage。 这些核心功能包括以下项：

- **关于** 对话框和初始屏幕

- **"添加新项"和"添加现有项"** 对话框

- **类视图** 窗口和 **对象浏览器**

- **"** 引用"对话框

- **"文档大纲"** 窗口

- **"动态帮助"** 窗口

- **查找** 和 **替换**

- **打开Project** 菜单 **上的**"打开文件"**对话框**

- **"** 工具"菜单上的 **"选项"** 对话框

- **"属性"** 窗口

- **解决方案资源管理器**

- **任务列表** 窗口

- **工具箱**

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>
- [VSPackages](../../extensibility/internals/vspackages.md)
