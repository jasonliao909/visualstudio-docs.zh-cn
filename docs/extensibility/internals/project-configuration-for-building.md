---
title: Project用于生成|Microsoft Docs
description: 了解如何通过新项目类型的"解决方案配置"对话框管理特定解决方案的解决方案配置列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 07112d61162f4007db1581c75188295e152e809cd733ff6b3220c5ed1ca742b3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401530"
---
# <a name="project-configuration-for-building"></a>用于生成的项目配置
给定解决方案的解决方案配置列表由"解决方案配置"对话框管理。

 用户可以创建其他解决方案配置，每个配置都有其自己的唯一名称。 当用户创建新的解决方案配置时，IDE 默认为项目中的相应配置名称;如果不存在相应的名称，则默认为"调试"。 如有必要，用户可以更改选择以满足特定要求。 此行为的唯一例外是项目支持与新解决方案配置的名称匹配的配置。 例如，假设解决方案包含 Project1 和 Project2。 Project1 具有项目配置 Debug、Retail 和 MyConfig1。 Project2 具有项目配置 Debug、Retail 和 MyConfig2。

 如果用户创建名为 MyConfig2 的新解决方案配置，Project1 会默认将其调试配置绑定到解决方案配置。 默认情况下，Project2 还会将其 MyConfig2 配置绑定到解决方案配置。

> [!NOTE]
> 绑定不区分大小写。

 当用户在配置下拉列表中选择"多个选择"项时，环境将显示一个对话框，该对话框提供可用配置的列表。

 ![多个配置](../../extensibility/internals/media/vsmultiplecfgs.gif "vsMultipleCfgs") 多个配置

 在此对话框中，用户可以选择一个或多个配置。 选择后，"属性页"对话框中显示的属性值将反映所选配置的值的交集。

 有关 [添加和](../../extensibility/internals/solution-configuration.md) 重命名解决方案和项目配置的信息，请参阅解决方案配置。

 Project依赖项和生成顺序与解决方案配置无关：也就是说，只能为解决方案中所有项目设置一个依赖关系树。 右键单击解决方案或项目，然后选择"Project **依赖项**"或 **Project"生成顺序**"选项 **Project"** 依赖项"对话框。 也可以从"打开"**菜单Project它**。

 ![Project依赖项](../../extensibility/internals/media/vsprojdependencies.gif "vsProjDependencies")Project依赖项

 Project依赖项确定项目的生成顺序。 使用对话框上的"生成顺序"选项卡可以查看解决方案中的项目生成的确切顺序，并使用"依赖项"选项卡修改生成顺序。

> [!NOTE]
> 由于 或 接口指定的显式依赖项，已添加列表中已选中其复选框但显示为灰色的项目，并且 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> 无法更改。 例如，将项目引用从项目添加到另一个项目会自动添加一个生成依赖项，该依赖项仅可通过删除引用 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 来删除。 无法选择其复选框为清除且显示为灰色的项目，因为这样做会创建依赖项循环 (例如，Project1 将依赖于 Project2，而 Project2 将依赖于 Project1) ，这将停止生成。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 生成过程包括使用单个 Build 命令调用的典型编译和链接操作。 还可以支持另外两个生成过程：用于删除以前生成的所有输出项的干净操作，以及用于确定配置中的输出项是否已更改的最新的检查。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 对象返回从 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> (返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A> 的相应) 以管理其生成过程。 若要在生成操作发生时报告其状态，配置将调用 、环境实现的接口以及任何对生成状态事件感兴趣的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback> 其他对象。

 生成后，可以使用配置设置来确定它们是否可以在调试器控制下运行。 配置实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> 以支持调试。

 实现项目依赖项后，可以通过自动化模型以编程方式操作依赖项。 在 <xref:EnvDTE.SolutionBuild.BuildDependencies%2A> 自动化模型中调用 。 没有可用的 VSIP API 级接口允许直接操作解决方案生成管理器配置及其属性。

 此外，还可以在项目依赖项窗口中提供网格。 有关详细信息，请参阅属性 [显示网格](../../extensibility/internals/properties-display-grid.md)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [用于输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)
