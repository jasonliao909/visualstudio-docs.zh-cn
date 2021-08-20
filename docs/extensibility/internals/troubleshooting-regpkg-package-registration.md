---
title: RegPkg 包注册疑难解答|Microsoft Docs
description: 使用此信息对注册表中的 RegPkg 包注册进行Visual Studio。 使用适用于包的 RegPkg 版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 103e04bbfb32000e5e3a533988e6727f4323fcda
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124524"
---
# <a name="troubleshooting-regpkg-package-registration"></a>RegPkg 包注册疑难解答
> [!NOTE]
> 在文件中注册包的首选Visual Studio是使用 .pkgdef 文件。 这样，无需访问系统注册表即可进行扩展部署。 Pkgdef 文件是使用 [CreatePkgDef 实用工具 创建的](../../extensibility/internals/createpkgdef-utility.md)。

 若要在 中使用 RegPkg 注册包，必须使用适用于包的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] RegPkg 版本。

## <a name="regpkg-versions-related-to-package-versions"></a>与包版本相关的 RegPkg 版本
 有两个版本的 RegPkg。 一个版本包含在 中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 使用此版本注册已使用以下程序集之一构建的包：

1. Microsoft.VisualStudioShell.9.0.dll

2. Microsoft.VisualStudioShell.10.0.dll

3. Microsoft.VisualStudioShell.11.0.dll

   它无法注册使用早期版本的程序集Microsoft.VisualStudio.Shell.dll包。

   早期版本的 RegPkg 可以注册已通过使用程序集生成Microsoft.VisualStudio.Shell.dll包。 但是，它无法注册使用该程序集的更高版本构建的包。

## <a name="see-also"></a>请参阅
- [VSPackages](../../extensibility/internals/vspackages.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
