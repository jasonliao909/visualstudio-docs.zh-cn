---
title: 在共享 VSPackage 和版本控制 VSPackage 之间|Microsoft Docs
description: 了解通过共享或版本控制策略并行安装 VSPackage，以及多个版本的 Visual Studio 和 .NET Framework。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 34bd5db7f02b69c5f2f3e9b017f7cccbabbf175cfe70ba70af0efb835f7ecc4f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434940"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>在共享 VSPackage 和版本控制 VSPackage 之间选择
不同版本的 Visual Studio可以共存于同一计算机上。 VSPackage 可以支持任何版本的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 组合。

 可以通过共享策略或版本控制策略这两种策略之一来启用 VSPackage 的并行安装。 这两种版本都适用于多个版本的 和关联的版本 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .NET Framework。

 在共享策略中，注册了一个 VSPackage 以在多个版本的 中使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 在版本控制策略中，将安装多个 VSPackage DLL，每个支持 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的版本各有一个。

## <a name="shared-vspackages"></a>共享 VSPackage
 在多个版本的 中使用相同的 VSPackage 时，使用共享 VSPackage 是合适的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 若要实现共享 VSPackage，必须执行以下步骤：

- 使 VSPackage 与多个版本的 兼容 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 有两种方法可用：

  - 将 VSPackage 限制为仅使用所支持的 的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 最早版本的功能。

  - 对 VSPackage 进行编程，使其适应 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 运行它的 版本。 然后，如果对较新服务的查询失败，则 VSPackage 可以提供旧版本中支持的其他服务 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

- 正确注册 VSPackage。 有关详细信息，请参阅[VSPackage 注册和](../extensibility/internals/vspackage-registration.md)[托管 VSPackage 注册](/previous-versions/bb166783(v=vs.100))。

- 正确注册文件扩展名。 有关详细信息，请参阅为并行 [部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 创建一个安装程序，用于为 的适当版本部署 VSPackage。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 有关详细信息，请参阅使用安装程序和组件Windows安装[VSPackage。](../extensibility/internals/component-management.md) [](../extensibility/internals/installing-vspackages-with-windows-installer.md)

- 解决注册冲突问题。 有关详细信息，请参阅 [VSPackage 注册](../extensibility/internals/vspackage-registration.md)。

- 确保共享文件和版本控制文件都遵守引用计数，以允许安全安装和删除多个版本。 有关详细信息，请参阅 [组件管理](../extensibility/internals/component-management.md)。

## <a name="versioned-vspackages"></a>版本控制 VSPackage
 在版本控制 VSPackage 策略下，为支持的每个版本创建 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 一个 VSPackage。 当你希望利用的更高版本提供的服务时，这样做是合适的，因为每个 VSPackage 都可以在不影响其他 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage 的情况下发展。 不过，从单个代码库或多个独立代码库创建多个二进制文件的版本控制策略可能需要比共享策略更多的初始开发。 此外，可能需要执行其他安装工作，因为必须为每个版本创建单独的安装程序，或者创建一个安装程序来检测已安装的 版本以及 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage 支持的版本。

## <a name="binary-compatibility"></a>二进制兼容性
 通常，二进制兼容性允许使用早期版本的 Visual Studio 开发的本机代码 VSPackage 在更高版本的 Visual Studio。 但是，有三个重要的例外：

- 如果 VSPackage 依赖于公共语言运行时的特定版本，则它必须确定运行它的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 哪个版本。

- VSPackage 可能依赖于另一个 VSPackage 或其他产品的特定功能。 因此，VSPackage 只能在满足依赖项时运行。

- VSPackage 可能受 Service Pack 或更高版本的安全修复 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的影响 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 在这种情况下，在应用安全修补程序后，使用 早期版本开发的 VSPackage 可能无法在 版本中 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 运行。 但是，可以使用更高版本重新生成包，并且它还在早期版本中运行。

  必须使用 与 目标版本匹配的 和 版本生成 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 托管 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] VSPackage。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]

  除了规划 VSPackage 二进制文件的二进制兼容性之外，还应考虑解决方案和项目文件格式。 如果 VSPackage 创建了一个新的项目类型，则必须确定它是否可以在一个版本或多个版本的 中运行 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅 [升级自定义项目](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)。

## <a name="see-also"></a>请参阅
- [使用安装程序安装 VSPackage Windows](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [组件管理](../extensibility/internals/component-management.md)