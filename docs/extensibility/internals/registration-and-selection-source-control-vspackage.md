---
title: 注册和选择 (源代码管理 VSPackage) |Microsoft Docs
description: 了解如何将源代码管理 VSPackage 注册到 Visual Studio以及如何选择要从多个已注册的源代码管理包加载的包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3b2c64584eb550aba9bc0ea6240fccdeed79bb614001ca62235fface5d3635f9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275263"
---
# <a name="registration-and-selection-source-control-vspackage"></a>注册和选择（源代码管理 VSPackage）
必须注册源代码管理 VSPackage，以将其公开给 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 如果注册了多个源代码管理 VSPackage，用户可以选择在适当的时间加载哪个 VSPackage。 有关 VSPackage 以及如何注册 VSPackage 的详细信息，请参阅[VSPackages。](../../extensibility/internals/vspackages.md)

## <a name="registering-a-source-control-package"></a>注册源代码管理包
 已注册源代码管理包，以便 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 环境可以找到它并查询其支持的功能。 这符合延迟加载方案，在此方案中，只有在需要或显式请求包的功能或命令时，才创建包的实例。

 VSPackages 将信息放在特定于版本的注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *X.Y* 中，其中 *X* 是主版本号 *，Y* 是次版本号。 这种做法提供了支持并行安装多个版本的 的能力 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 UI (用户界面) 支持从多个已安装的源代码管理插件 (源代码管理包) 以及源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackages 进行选择。 一次只能有一个活动的源代码管理插件或 VSPackage。 但是，如下所述，IDE 允许通过基于解决方案的包交换机制在源代码管理插件和 VSPackage 之间切换。 源代码管理 VSPackage 有一些要求来启用此选择机制。

### <a name="registry-entries"></a>注册表项
 源代码管理包需要三个专用 GUID：

- 包 GUID：这是包的主 GUID，其中包含源代码管理实现 (在本部分ID_Package中称为) 。

- 源代码管理 GUID：这是用于向 Visual Studio 源代码管理存根注册的源代码管理 VSPackage 的 GUID，还用作命令 UI 上下文 GUID。 源代码管理服务 GUID 在源代码管理 GUID 下注册。 在示例中，源代码管理 GUID 称为 ID_SccProvider。

- 源代码管理服务 GUID：这是本部分中名为 Visual Studio (的SID_SccPkgService GUID) 。 除此之外，源代码管理包还需要为 VSPackage、工具窗口等定义其他 GUID。

  以下注册表项必须由源代码管理 VSPackage 创建：

| 项名称 | 项 |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` |  (默认值) = rg_sz：{ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` |  (默认值) = rg_sz：\<Friendly name of Package><br /><br /> Service = rg_sz：{SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` |  (默认值) = rg_sz：#\<Resource ID for localized name><br /><br /> Package = rg_sz：{ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br />  (请注意，键名称 已由 使用，不能用作 `SourceCodeControl` [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] \<PackageName> .)  |  (默认值) = rg_sz：{ID_Package} |

## <a name="selecting-a-source-control-package"></a>选择源代码管理包
 多个基于源代码管理插件 API 的插件和源代码管理 VSPackage 可以同时注册。 选择源代码管理插件或 VSPackage 的过程必须确保在适当的时间加载插件或 VSPackage，并可以延迟加载不必要的组件，直到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 需要它们。 此外， 必须从其他非活动 VSPackage（包括菜单项、对话框和工具栏）中删除所有 UI，并显示活动 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 的 UI。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 执行以下任一操作时加载源代码管理 VSPackage：

- 解决方案在 (源代码管理下时打开) 。

   打开源代码管理下的解决方案或项目时，IDE 会导致加载为该解决方案指定的源代码管理 VSPackage。

- 执行源代码管理 VSPackage 的任何菜单命令。

  源代码管理 VSPackage 应仅在实际使用所需的任何组件时加载它们 (也称为延迟加载) 。

### <a name="automatic-solution-based-vspackage-swapping"></a>基于解决方案的自动 VSPackage 交换
 可以通过"源代码管理"类别下的"选项" [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 对话框手动 **交换源代码管理 VSPackage。** 基于解决方案的自动包交换意味着，为特定解决方案指定的源代码管理包在打开该解决方案时自动设置为活动。 每个源代码管理包都应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 处理实现源代码管理插件 API (和源代码管理 VSPackages 的) 插件之间的切换。

 源代码管理适配器包用于切换到任何基于源代码管理插件 API 的插件。 切换到中间源代码管理适配器包并确定必须将哪个源代码管理插件设置为活动或不活动的过程对用户是透明的。 当任何源代码管理插件处于活动状态时，适配器包始终处于活动状态。 在两个源代码管理插件之间切换，只需加载和卸载插件 DLL。 但是，切换到源代码管理 VSPackage 涉及与 IDE 交互以加载相应的 VSPackage。

 打开任何解决方案且 VSPackage 的注册表项位于解决方案文件中时，将调用源代码管理 VSPackage。 打开解决方案时， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 查找注册表值并加载相应的源代码管理 VSPackage。 所有源代码管理 VSPackage 都必须具有上述注册表项。 源代码管理下的解决方案标记为与特定源代码管理 VSPackage 相关联。 源代码管理 VSPackage 必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 才能启用基于解决方案的自动 VSPackage 交换。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>Visual Studio用于包选择和切换的 UI
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在"源代码管理"类别下的"选项"对话框中为源代码管理 VSPackage 和插件 **选择提供** UI。  它允许用户选择活动源代码管理插件或 VSPackage。 下拉列表包括：

- 所有已安装的源代码管理包

- 所有已安装的源代码管理插件

- 禁用源代码控制的"无"选项

  只有活动源代码管理选择的 UI 可见。 VSPackage 选择隐藏上一个 VSPackage 的 UI，并显示新 VSPackage 的 UI。 按用户选择活动 VSPackage。 如果用户有多个并发打开的 副本 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，则每个副本可能使用不同的活动 VSPackage。 如果多个用户登录到同一台计算机，则每个用户都可以有单独的打开实例，每个实例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 具有不同的活动 VSPackage。 当用户关闭 的多个实例时，上次打开解决方案处于活动状态的源代码管理 VSPackage 将成为默认源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage，在重启时设置为活动状态。

  与 早期版本不同 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，IDE 重启不再是切换源代码管理 VSPackage 的唯一方法。 VSPackage 选择是自动的。 切换包需要Windows用户权限 (管理员或 Power User) 。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [功能](../../extensibility/internals/source-control-vspackage-features.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
