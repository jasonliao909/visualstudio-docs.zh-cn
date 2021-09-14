---
title: 解决方案配置|Microsoft Docs
description: 了解如何实现项目类型支持的解决方案配置，这些配置将引导"启动" (F5) 和"生成"命令的行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solution configurations
ms.assetid: f22cfc75-3e31-4e0d-88a9-3ca99539203b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ecd5d2fc6fba5d42b2c9435f47b371dd5ca346f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600862"
---
# <a name="solution-configuration"></a>解决方案配置
解决方案配置存储解决方案级属性。 它们指示"启动" ( F5) 生成 **命令的行为。** 默认情况下，这些命令生成并启动调试配置。 这两个命令在解决方案配置的上下文中执行。 这意味着用户可以期望 F5 启动并生成通过设置配置的任何活动解决方案。 环境旨在优化解决方案，而不是构建和运行项目。

 标准Visual Studio工具栏“开始”按钮左侧的一个解决方案配置下拉列表“开始”按钮。 此列表允许用户选择在按下 F5 时要启动的配置、创建自己的解决方案配置或编辑现有配置。

> [!NOTE]
> 没有用于创建或编辑解决方案配置的扩展性接口。 您必须使用 `DTE.SolutionBuild`。 但是，有一些扩展性 API 用于管理解决方案生成。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>。

 下面是如何实现项目类型支持的解决方案配置：

- Project

   显示在当前解决方案中找到的项目的名称。

- 配置

   若要提供项目类型支持的配置列表并显示在属性页中，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> 。

   "配置"列显示要在此解决方案配置中生成的项目配置的名称，并列出单击箭头按钮时的所有项目配置。 环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A> 方法以填充此列表。 如果 方法指示项目支持配置编辑，则"配置"标题下也会显示"新建"或"编辑 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> "选项。 每个选择都启动对话框，这些对话框调用 接口 `IVsCfgProvider2` 的方法以编辑项目的配置。

   如果项目不支持配置，则"配置"列将显示"无"并处于禁用状态。

- 平台

   显示所选项目配置生成针对的平台，并列出单击箭头按钮时项目的所有可用平台。 环境调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A> 方法以填充此列表。 如果 方法指示项目支持平台编辑，则"平台"标题下也会显示"新建"或" <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> 编辑"选项。 每个选择都启动对话框，这些对话框调用 `IVsCfgProvider2` 方法来编辑项目的可用平台。

   如果项目不支持平台，则该项目的平台列将显示"无"并处于禁用状态。

- 构建

   指定项目是否由当前解决方案配置生成。 调用解决方案级生成命令时，不会生成未选择的项目，尽管它们包含任何项目依赖项。 未选择生成的项目仍包括在解决方案的调试、运行、打包和部署中。

- 部署

   指定当"启动"或"部署"命令与所选解决方案生成配置一同使用时，是否部署项目。 如果项目支持通过在其 对象上实现 接口进行部署，则此字段的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 复选框将可用。

  添加新的解决方案配置后，用户可以从标准工具栏上的"解决方案配置"下拉列表框中选择它，以生成和/或启动该配置。

## <a name="see-also"></a>另请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
