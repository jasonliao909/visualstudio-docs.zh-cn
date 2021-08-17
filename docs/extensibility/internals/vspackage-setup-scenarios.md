---
title: VSPackage 安装方案 |Microsoft Docs
description: 了解有关支持并行安装 Visual Studio 的最佳实践，以及 VSPackage 的共享或并行安装。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e75851e8a2775fda80a4bcb6ffefa93558c4f786
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122069619"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage 安装方案

设计 VSPackage 安装程序以获得灵活性，这一点很重要。 例如，你可能需要在未来发布安全修补程序，或者可以更改需要完全并行版本控制支持的业务策略。

在[支持 Visual Studio 的多个版本](../../extensibility/supporting-multiple-versions-of-visual-studio.md)中，你可以了解支持的并行安装的优点和问题，其中包括 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 的共享或并行安装。 简而言之，并行 Vspackage 为你提供了支持的新功能的最大灵活性 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

本主题中讨论的方案并不是您唯一的选择，但将作为建议的最佳实践提供。

## <a name="components-privacy-and-sharing"></a>组件、隐私和共享

### <a name="make-your-components-independent"></a>使组件独立

标识并填充组件后，分配并 `GUID` 部署组件，无法更改其组合。 如果更改了组件的组合，则生成的组件必须是新的包含新组件的组件 `GUID` 。 考虑到这些事实，通过使每个组件独立于独立的单元，实现最大版本的灵活性。 有关控制组件规则的详细信息，请参阅 [更改组件代码](/windows/desktop/Msi/changing-the-component-code) 和 [如果组件规则损坏会发生什么情况？](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)。

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>不要将共享资源和专用资源混合到组件中

引用计数发生在组件级别上。 因此，将共享资源和专用资源混合到一个组件中，无法更新专用资源（如可执行文件），也不会覆盖共享资源。 此方案会创建向后兼容性问题，并限制你创建并行功能。

例如，用于注册 VSPackage 的注册表值 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 应保留在单独的组件中，用于将 VSPackage 注册到 Visual Studio。 共享的文件或注册表值还会出现在另一个组件中。

## <a name="scenario-1-shared-vspackage"></a>方案1：共享 VSPackage

在这种情况下，共享 VSPackage (单个二进制文件，该二进制文件支持 Visual Studio 的多个版本，并随附 Windows Installer 包。 使用 Visual Studio 的每个版本进行注册都是由用户选择的功能控制的。 这也意味着，当分配给不同的功能时，可以单独选择每个组件以进行安装或卸载，使用户能够控制将 VSPackage 集成到不同版本的中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。  (参阅[Windows Installer 功能](/windows/desktop/Msi/windows-installer-features)，以获取有关在 Windows Installer 包中使用功能的详细信息 ) 

![VS Shared VSPackage 安装程序](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

如图所示，共享组件成为 Feat_Common 功能的一部分，该功能始终是安装的。 通过使 Feat_VS2002 和 Feat_VS2003 功能可见，用户可以在安装时选择要将 VSPackage 集成到其中的 Visual Studio 版本。 用户还可以使用 Windows Installer 维护模式来添加或删除功能，在这种情况下，会在不同版本的 Visual Studio 中添加或删除 VSPackage 注册信息。

> [!NOTE]
> 将功能的显示列设置为0会隐藏该功能。 较低级别的列值（例如1）可确保始终安装该值。 有关详细信息，请参阅 [INSTALLLEVEL 属性](/windows/desktop/Msi/installlevel) 和 [功能表](/windows/desktop/Msi/feature-table)。

## <a name="scenario-2-shared-vspackage-update"></a>方案2：共享的 VSPackage 更新

在此方案中，将提供方案1中 VSPackage 安装程序的更新版本。 为了进行讨论，更新添加了对 Visual Studio 的支持，但它也可能是更简单的安全修补程序或 bug 修复 Service Pack。 Windows安装程序安装更新的规则需要系统上已有的未更改组件重新复制。 在这种情况下，版本为1.0 的系统将覆盖更新的组件 Comp_MyVSPackage.dll 并让用户选择添加新功能 Feat_VS2005 及其组件 Comp_VS2005_Reg。

> [!CAUTION]
> 每当在多个版本的中共享 VSPackage 时 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，VSPackage 的后续版本都必须保持与 Visual Studio 以前版本的向后兼容性。 如果你不能维护向后兼容性，则必须使用并行的私有 Vspackage。 有关详细信息，请参阅[支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)。

![VS 共享 VS 包更新安装程序](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

此方案提供了一个新的 VSPackage 安装程序，利用 Windows Installer 对次要升级的支持。 用户只需安装版本1.1，版本1.0。 但是，系统不需要安装版本1.0。 同一安装程序将在没有版本1.0 的系统上安装版本1.1。 以这种方式提供小升级的优点是不需要完成开发升级安装程序和完整产品安装程序的工作。 一个安装程序将执行两个作业。 安全修补程序或 Service Pack 可能会改用 Windows Installer 修补程序。 有关详细信息，请参阅 [修补和升级](/windows/desktop/Msi/patching-and-upgrades)。

## <a name="scenario-3-side-by-side-vspackage"></a>方案3：并行 VSPackage

此方案提供了两个 VSPackage 安装程序-每个版本的 Visual Studio .net 2003 和 Visual Studio。 每个安装程序都安装了一种并行或专用的 VSPackage (一个专门为 Visual Studio) 的特定版本构建和安装的安装程序。 每个 VSPackage 都在其自己的组件中。 因此，每个可以单独提供修补程序或维护版本。 因为 VSPackage DLL 现在是特定于版本的，所以在与 DLL 相同的组件中包含其注册信息是安全的。

![VS 并行 VS 包安装程序](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

每个安装程序还包括在两个安装程序之间共享的代码。 如果共享代码已安装到常见位置，则同时安装这两个 .msi 文件将只安装一次共享代码。 第二个安装程序只会递增组件上的引用计数。 引用计数可确保在卸载其中一个 Vspackage 时，共享代码仍适用于其他 VSPackage。 如果同时卸载第二个 VSPackage，则将删除共享代码。

## <a name="scenario-4-side-by-side-vspackage-update"></a>方案4：并行 VSPackage 更新

在这种情况下，你 Visual Studio 的 VSPackage 会受到安全漏洞的影响，并且你需要发出更新。 例如，在方案2中，你可以创建一个新的 .msi 文件，用于更新现有的安装以包含安全修补程序，以及部署已存在的安全修补程序的新安装。

在这种情况下，VSPackage 是安装在全局程序集缓存中的托管 VSPackage (GAC) 。 重新生成它以包括安全修补程序时，必须更改程序集版本号的修订号部分。 新程序集版本号的注册信息将覆盖以前的版本，从而导致 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 加载固定程序集。

![VS 并行 VS 包更新安装程序](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

有关部署并行程序集的详细信息，请参阅[使用 .NET Framework 简化部署和解决 DLL Hell](/previous-versions/dotnet/articles/ms973843(v=msdn.10))。

## <a name="see-also"></a>请参阅

- [Windows Installer](/windows/desktop/Msi/windows-installer-portal)
- [支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)