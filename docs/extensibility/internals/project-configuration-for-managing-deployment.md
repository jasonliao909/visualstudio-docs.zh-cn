---
title: 用于管理部署项目|Microsoft Docs
description: 了解部署到预期位置进行调试和安装，以及支持Visual Studio项目的两种方法。
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
ms.workload:
- vssdk
ms.openlocfilehash: 3c6077665ccc3bbe5f87b91a1d2fc5636e08539d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899896"
---
# <a name="project-configuration-for-managing-deployment"></a>用于管理部署的项目配置
部署是在物理上将输出项从生成过程移动到预期位置进行调试和安装的行为。 例如，Web 应用程序可能构建在本地计算机上，然后放置在服务器上。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持在部署中涉及项目的两种方式：

- 作为部署过程的主题。

- 作为部署过程的经理。

  在部署解决方案之前，必须先添加部署项目以配置部署选项。 如果部署项目不存在，当从"生成"菜单中选择"部署解决方案"或右键单击解决方案时，会询问是否要创建一个。 单击 **"是** " **将** 打开"添加新项目"对话框，并选中 **"远程部署向导"** 项目。

  远程部署向导会要求你提供应用程序类型 (Windows 或 Web) 、要包括的项目输出组、要包含的其他任何文件以及要部署到的远程计算机。 向导的最后一页显示所选选项的摘要。

  作为部署过程主题的项目将生成必须移动到备用环境的输出项。 这些输出项被描述为 接口的参数，如果允许项目对输出进行分组，则其主要 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 用途为 。 有关 的实现详细信息，请参阅 `IVsProjectCfg2` [输出 的项目配置](../../extensibility/internals/project-configuration-for-output.md)。

  管理部署过程的部署项目会启用"部署"命令，在选择此命令时做出响应。 部署项目实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 接口来执行部署，并调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback> 接口以报告部署状态事件。

  配置可以指定影响其生成或部署操作的依赖关系。 生成或部署依赖项是必须在生成或部署配置本身之前或之后生成或部署的项目。 使用 接口描述项目之间的生成依赖 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> 关系，然后使用 接口部署 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> 依赖项。 有关详细信息，请参阅用于 [生成 的项目配置](../../extensibility/internals/project-configuration-for-building.md)。

## <a name="see-also"></a>另请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
