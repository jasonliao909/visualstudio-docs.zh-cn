---
title: 注册和选择 (源控件 VSPackage) |Microsoft Docs
description: 了解如何将源代码管理 VSPackage 注册到 Visual Studio，以及如何选择要从多个已注册源代码管理包中加载的包。
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
ms.openlocfilehash: 23a64b0432c5a77f764ae7ef83e1c0ed9d604c2f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042109"
---
# <a name="registration-and-selection-source-control-vspackage"></a>注册和选择（源代码管理 VSPackage）
必须注册源代码管理 VSPackage，才能将其公开给 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 如果注册了多个源代码管理 VSPackage，则用户可以选择要在适当的时间加载的 VSPackage。 有关更多详细信息，请参阅 [vspackage](../../extensibility/internals/vspackages.md) 和注册方式。

## <a name="registering-a-source-control-package"></a>注册源代码管理包
 已注册源代码管理包，以便 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 环境可以找到它并查询其支持的功能。 这取决于延迟加载方案，在此方案中，仅当包的一个实例是必需的或显式请求时，才会创建包的实例。

 Vspackage 将信息放在特定于版本的注册表项中 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *x. Y*，其中 *X* 是主要版本号， *Y* 是次版本号。 这种做法提供支持并行安装多个版本的的功能 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]用户界面 (UI) 支持从多个已安装的源代码管理插件 (通过源代码管理适配器包) 以及源代码管理 vspackage 进行选择。 一次只能有一个活动源代码管理插件或 VSPackage。 但是，如下所述，IDE 允许通过基于解决方案的自动包交换机制在源代码管理插件和 Vspackage 之间切换。 对于源代码管理 VSPackage 的部分，需要满足一些要求，才能启用此选择机制。

### <a name="registry-entries"></a>注册表项
 源代码管理包需要三个专用 Guid：

- 包 GUID：这是包的主要 GUID，其中包含此部分)  (调用的源代码管理实现 ID_Package。

- 源代码管理 GUID：这是用于注册 Visual Studio 源代码管理存根的源控件 VSPackage 的 GUID，也用作命令 UI 上下文 GUID。 源代码管理服务 GUID 是在源代码管理 GUID 下注册的。 在此示例中，源代码管理 GUID 称为 ID_SccProvider。

- 源代码管理服务 guid：这是 Visual Studio (本部分) 中称为 SID_SccPkgService 的专用服务 guid。 除此之外，源代码管理包还需要为 Vspackage、工具窗口等定义其他 Guid。

  以下注册表项必须由源代码管理 VSPackage 生成：

| 项名称 | 项 |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` |  (默认值) = rg_sz： {ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` |  (默认值) = rg_sz：\<Friendly name of Package><br /><br /> 服务 = rg_sz： {SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` |  (默认值) = rg_sz：#\<Resource ID for localized name><br /><br /> Package = rg_sz： {ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br />  (请注意，键名称 `SourceCodeControl` 已被使用， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 并且不能作为的选择 \<PackageName> 。 )  |  (默认值) = rg_sz： {ID_Package} |

## <a name="selecting-a-source-control-package"></a>选择源代码管理包
 可以同时注册多个源代码管理插件基于 API 的插件和源代码管理 Vspackage。 选择源代码管理插件或 VSPackage 的过程必须确保 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 将插件或 VSPackage 加载到适当的时间，并在需要时延迟加载不必要的组件。 此外， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必须从其他不活动的 vspackage 中删除所有 UI，包括菜单项、对话框和工具栏，并显示活动 VSPackage 的 ui。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 当执行以下任一操作时，加载源代码管理 VSPackage：

- 当解决方案处于源代码管理) 下时 (打开解决方案。

   当打开源代码管理下的解决方案或项目时，IDE 将导致为该解决方案指定的源代码管理 VSPackage。

- 将执行源代码管理 VSPackage 的任何菜单命令。

  源代码管理 VSPackage 应仅在实际使用时才加载它所需的任何组件 (也称为延迟加载) 。

### <a name="automatic-solution-based-vspackage-swapping"></a>自动基于解决方案的 VSPackage 交换
 可以通过 " [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **源代码管理**" 类别下的 "**选项**" 对话框手动交换源代码管理 vspackage。 自动基于解决方案的包交换意味着在打开该解决方案时，已为特定解决方案指定的源代码管理包将自动设置为 "活动"。 每个源代码管理包应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在两个源代码管理插件之间处理开关 (实现源代码管理插件 API) 和源代码管理 Vspackage。

 源代码管理适配器包用于切换到任何源代码管理插件基于 API 的插件。 切换到中间源代码管理适配器包并确定必须设置为活动或非活动状态的过程对用户是透明的。 当任何源代码管理插件处于活动状态时，适配器包始终处于活动状态。 在两个源代码管理插件之间切换，只是加载和卸载插件 DLL。 但是，切换到源代码管理 VSPackage 涉及到与 IDE 的交互，以便加载相应的 VSPackage。

 当打开任何解决方案，并且 VSPackage 的注册表项位于解决方案文件中时，将调用源代码管理 VSPackage。 打开解决方案后， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 查找注册表值并加载相应的源代码管理 VSPackage。 所有源代码管理 Vspackage 都必须包含上述注册表项。 受源代码管理的解决方案将标记为与特定的源控件 VSPackage 相关联。 源代码管理 Vspackage 必须实现， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 才能启用基于解决方案的自动 VSPackage 交换。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>Visual Studio用于选择和切换包的 UI
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在 "**源代码管理**" 类别下的 "**选项**" 对话框中为源代码管理 VSPackage 和插件选择提供 UI。 它允许用户选择活动源代码管理插件或 VSPackage。 下拉列表包括：

- 所有已安装的源代码管理包

- 所有已安装的源代码管理插件

- "无" 选项，用于禁用源代码管理

  仅活动源代码管理选项的 UI 可见。 VSPackage 选择将隐藏上一个 VSPackage 的 UI，并显示新的 UI。 将在每个用户的基础上选择活动 VSPackage。 如果用户同时打开多个副本 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，每个副本可能会使用不同的活动 VSPackage。 如果多个用户登录到同一台计算机，则每个用户都可以打开单独的实例 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，每个实例都有不同的活动 VSPackage。 当某个用户关闭多个实例时 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，针对最后打开的解决方案处于活动状态的源代码管理 VSPackage 将成为默认的源代码管理 VSPackage，以在重新启动时设置为活动状态。

  与的早期版本不同 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，IDE 重新启动不再是切换源代码管理 vspackage 的唯一方法。 VSPackage 选择是自动的。 切换包需要 Windows 的用户特权 (不是管理员或超级用户) 。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [功能](../../extensibility/internals/source-control-vspackage-features.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
