---
title: VSPackage 注册|Microsoft Docs
description: 了解 VSPackage 注册，其中包Visual Studio建议安装它们，并且应该通过写入注册表中的信息来加载它们。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f0257eb175dff65a28cc942ef4854cfdff437d5c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117626"
---
# <a name="vspackage-registration"></a>VSPackage 注册
VSPackage 必须 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 建议它们已安装并且应加载。 此过程是通过在注册表中写入信息完成的。 这是安装程序的典型作业。

> [!NOTE]
> 在 VSPackage 开发过程中，使用自我注册是一种接受的做法。 但是 [!INCLUDE[vsipprvsip](../../extensibility/includes/vsipprvsip_md.md)] ，合作伙伴无法在安装过程中使用自注册来发货。

 安装程序包中的注册表Windows项通常在 Registry 表中创建。 还可以在 Registry 表中注册文件扩展名。 但是，Windows安装程序通过编程标识符提供内置支持， (ProgId) 、类、扩展和谓词表。 有关详细信息，请参阅数据库 [表](/windows/desktop/Msi/database-tables)。

 请确保注册表项与适用于所选并行策略的组件相关联。 例如，共享文件的注册表项应与该文件的安装程序组件Windows相关联。 同样，特定于版本的文件的注册表项应与该文件的 组件相关联。 否则，安装或卸载的一个版本的 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可能会中断其他版本中的 VSPackage。 有关详细信息，请参阅支持多个[版本的 Visual Studio。](../../extensibility/supporting-multiple-versions-of-visual-studio.md)

> [!NOTE]
> 管理注册的最简单方法是在同一文件中使用相同的数据进行开发人员注册和安装时注册。 例如，某些安装程序开发工具可以在生成时使用 .reg 格式的文件。 如果开发人员维护 .reg 文件进行自己的日常开发和调试，则这些相同的文件可以自动包含在安装程序中。 如果无法自动共享注册数据，必须确保安装程序的注册数据副本是最新的。

## <a name="registering-unmanaged-vspackages"></a>注册非托管 VSPackage
 非托管 VSPackages (包括由 Visual Studio 包模板生成的) 使用 ATL 样式的 .rgs 文件来存储注册信息。 .rgs 文件格式特定于 ATL，通常不能按安装创作工具使用。 必须单独维护 VSPackage 安装程序的注册信息。 例如，开发人员可以将 .reg 格式的文件与 .rgs 文件更改保持同步。 .reg 文件可以与 RegEdit 合并以用于开发工作，也可以由安装程序使用。

## <a name="registering-managed-vspackages"></a>注册托管 VSPackage
 RegPkg 工具从托管 VSPackage 读取注册属性，并可以将信息直接写入注册表或写入安装程序可以使用的 .reg 格式文件。

> [!NOTE]
> RegPkg 工具不可再发行，不能用于在用户的系统中注册 VSPackage。

## <a name="why-vspackages-should-not-self-register-at-install-time"></a>为什么在安装时不应Self-Register VSPackage
 VSPackage 安装程序不应依赖于自我注册。 初看起来，仅将 VSPackage 的注册表值保留于 VSPackage 本身似乎是一个不错的想法。 鉴于开发人员需要可用于其日常工作和测试的注册表值，避免在安装程序中维护注册表数据的单独副本是有意义的。 安装程序可以依赖于 VSPackage 本身来写入注册表值。

 虽然从理论上讲，自我注册有几个缺陷，因此不适合 VSPackage 安装：

- 正确支持安装、卸载、安装回滚和卸载回滚要求你为通过调用 RegPkg 自行注册的每个托管 VSPackage 创作四个自定义操作。

- 并行支持的方法可能要求你创作四个自定义操作，这些操作针对每个支持的 版本调用 RegSvr32 或 RegPkg。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]

- 无法安全地回滚具有自注册模块的安装，因为无法告知自注册密钥是否由其他功能或应用程序使用。

- 自注册 DLL 有时链接到不存在或版本错误的辅助 DLL。 相反，Windows安装程序可以使用注册表表注册 DLL，而不需要依赖于系统的当前状态。

- 如果组件同时指定为"从源运行"并列在 SelfReg 表中，则可拒绝自注册代码访问网络资源（如类型库）。 这可能会导致在管理安装过程中组件的安装失败。

## <a name="see-also"></a>请参阅
- [Windows Installer](/windows/desktop/Msi/windows-installer-portal)
- [托管包注册](/previous-versions/bb166783(v=vs.100))