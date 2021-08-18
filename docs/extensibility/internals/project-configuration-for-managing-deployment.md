---
title: Project用于管理部署的配置 |Microsoft Docs
description: 了解如何部署到所需的调试和安装位置，以及两种 Visual Studio 支持支持部署的项目的方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fdd15349522c1bf49f379551825a773b676f6196
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094641"
---
# <a name="project-configuration-for-managing-deployment"></a>用于管理部署的项目配置
部署是指以物理方式将输出项从生成过程移动到预期位置以便进行调试和安装的操作。 例如，Web 应用程序可以在本地计算机上生成，然后放在服务器上。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持以下两种方法来部署项目：

- 作为部署过程的主题。

- 作为部署过程的管理者。

  在部署解决方案之前，必须首先添加部署项目以配置部署选项。 如果 "部署" 项目尚不存在，则会询问你是否要在从 "**生成**" 菜单中选择 "**部署解决方案**" 时创建一个项目，或右键单击该解决方案。 单击 **"是"** 将打开 "**添加新 Project** " 对话框，其中选择了 "**远程部署向导**" 项目。

  远程部署向导要求你提供应用程序类型 (Windows 或 Web) 、要包含的项目输出组、要包括的任何其他文件以及要部署到的远程计算机。 向导的最后一页显示所选选项的摘要。

  作为部署过程的主题的项目将生成必须移动到备用环境的输出项。 这些输出项被描述为接口的参数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> ，其主要用途是为了允许项目对输出进行分组。 有关的实现的详细信息 `IVsProjectCfg2` ，请参阅[Project 的输出配置](../../extensibility/internals/project-configuration-for-output.md)。

  用于管理部署过程的部署项目，启用此命令并在选择此命令时做出响应。 部署项目实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 接口以执行部署，并调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback> 接口以报告部署状态事件。

  配置可以指定影响其生成或部署操作的依赖项。 生成或部署依赖项是在生成或部署配置之前或之后必须生成或部署的项目。 项目之间的生成依赖项与接口一起说明 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> ，并部署与接口的依赖关系 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> 。 有关详细信息，请参阅[用于生成的 Project 配置](../../extensibility/internals/project-configuration-for-building.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
