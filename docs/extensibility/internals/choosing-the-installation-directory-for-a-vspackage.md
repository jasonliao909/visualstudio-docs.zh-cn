---
title: 选择 VSPackage 的安装目录|Microsoft Docs
description: 了解如何使用管理还是非托管等因素为 VSPackage 及其支持文件选择安装目录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bde953b023b91c3c3e3b06fb3d50770851352da9d441b6277406ed91bbc392a5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359723"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>选择 VSPackage 的安装目录
VSPackage 及其支持文件必须位于用户的文件系统上。 位置取决于 VSPackage 是托管还是非托管、并行版本控制方案和用户选择。

## <a name="unmanaged-vspackages"></a>非托管 VSPackage
 非托管 VSPackage 是可安装在任何位置的 COM 服务器。 其注册信息必须准确反映其位置。 安装程序用户界面 (UI) 应提供默认位置作为 Windows `ProgramFilesFolder` Installer 属性值的子目录。 例如：

*&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \V1.0\\*

 应允许用户更改默认目录，以容纳保留小型启动分区并倾向于在另一个卷上安装应用程序和工具的用户。

 如果并行方案使用版本控制 VSPackage，可以使用子目录来存储不同的版本。 例如：

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \\ V1.0 \\ 2002\\*

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \\ V1.0 \\ 2003\\*

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \\ V1.0 \\ 2005\\*

## <a name="managed-vspackages"></a>托管的 VSPackage
 托管 VSPackage 还可以安装在任何位置。 但是，应考虑始终将它们安装到 GAC (全局程序集缓存) 以减少程序集加载时间。 由于托管 VSPackage 始终是强名称程序集，因此在 GAC 中安装它们意味着仅在安装时进行强名称签名验证。 在文件系统中其他位置安装的强名称程序集每次加载时都必须验证其签名。 在 GAC 中安装托管 VSPackage 时，请使用 regpkg 工具的 **/assembly** 开关写入指向程序集的强名称的注册表项。

 如果在 GAC 外的其他位置安装托管 VSPackage，请按照前面为非托管 VSPackage 提供的建议选择目录层次结构。 使用 regpkg 工具的 **/codebase** 开关编写指向 VSPackage 程序集路径的注册表项。

 有关详细信息，请参阅[注册和注销 VSPackage。](../../extensibility/registering-and-unregistering-vspackages.md)

## <a name="satellite-dlls"></a>附属 DLL
 根据约定，包含特定区域设置资源的 VSPackage 附属 DLL 位于 *VSPackage* 目录的子目录中。 子目录对应于区域设置 ID (LCID) 值。

 管理 [VSPackages](../../extensibility/managing-vspackages.md) 一文指示注册表项控制 ，其中 实际查找 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 的附属 DLL。 但是， 尝试按以下顺序在名为 的子目录中加载 LCID 值的附属 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] DLL：

1. 默认 LCID (Visual Studio LCID;例如 *，\1033* 表示英语) 

2. 具有默认子语言的默认 LCID。

3. 系统默认 LCID。

4. 具有默认子语言的系统默认 LCID。

5. 美国英语 (*.\1033* 或 *.\0x409) 。*

如果 VSPackage DLL 包含资源，而 **SatelliteDll\DllName** 注册表入口点指向它，则尝试按上述顺序 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 加载它们。

## <a name="see-also"></a>请参阅
- [在共享 VSPackage 和版本控制 VSPackage 之间选择](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [管理 VSPackage](../../extensibility/managing-vspackages.md)
- [管理包注册](/previous-versions/bb166783(v=vs.100))