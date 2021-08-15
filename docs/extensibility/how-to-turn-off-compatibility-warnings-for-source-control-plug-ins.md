---
title: 关闭源代码管理插件的警告
description: 在使用源代码管理时，用户可能会看到多个兼容性Visual Studio。 了解如何禁用这些警告。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- source control plug-ins, turning off compatibility warnings
- compatibility warnings, turning off
ms.assetid: ba318e12-921b-4b7a-a8c2-12c712be1dbf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 94ed8d8357ae9b95d538a5bef39c96e2e1662b9711b6da423183ee52f2113774
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448268"
---
# <a name="how-to-turn-off-compatibility-warnings-for-source-control-plug-ins"></a>如何：关闭源代码管理插件的兼容性警告

在 中使用源代码管理时，用户可能会看到多个兼容性警告 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 显示警告取决于源代码管理插件的功能，可以在此处详细禁用。

### <a name="to-disable-the-warning-to-ensure-optimal-source-control-integration-with-visual-studio"></a>禁用警告："确保与源代码管理的最佳Visual Studio"

- 设置以下注册表项 (在必要时添加值) ：

   **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\DontDisplayCheckDotNETCompatible = dword：00000001**

   对于所有非插件， [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] 将显示此警告。

### <a name="to-disable-the-warning-the-installed-source-control-provider-does-not-support-all-the-capabilities"></a>禁用警告："已安装的源代码管理提供程序不支持所有功能"

- 设置以下两个注册表值 (在必要时添加) ：

     **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\WarnedOldMSSCCIProvider = dword：000000000**

    **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl\UseOldSCC = dword：00000001**

     如果源代码管理插件未显式支持多个项目的重新 (即，如果一次只能签入一个文件和项目，则会显示此) 。

     最好支持重新 (功能 `SCC_CAP_REENTRANT`) ;这样做会删除此警告。 但是，如果无法提供此支持，可以设置这些注册表项。

## <a name="see-also"></a>另请参阅

- [功能标志](../extensibility/capability-flags.md)
