---
title: RegPkg 实用工具|Microsoft Docs
description: 了解 RegPkg.exe 实用工具如何向 Visual Studio 注册 VSPackage 并为部署做好准备。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ed91788526177392901a6fd8aa03f139f9267827
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664316"
---
# <a name="regpkg-utility"></a>RegPkg 实用工具
> [!NOTE]
> 在文件中注册包的首选Visual Studio是使用 .pkgdef 文件。 这样，无需访问系统注册表即可进行扩展部署，这是 VSIX 部署的要求。 Pkgdef 文件是使用 [CreatePkgDef 实用工具 创建的](../../extensibility/internals/createpkgdef-utility.md)。 有关包部署Visual Studio，请参阅[Shipping Visual Studio Extensions。](../../extensibility/shipping-visual-studio-extensions.md)

 该RegPkg.exe实用工具向 注册 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage，并准备该 VSPackage 进行部署。 此实用工具在 VSPackage 开发期间在后台使用。 它作为生成过程的一部分运行，以便可以在实验性配置单元中生成和运行 VSPackage。

 RegPkg 可以生成多种格式的系统注册表脚本。 可以将这些脚本合并到部署项目中，例如.msi或Windows安装程序 XML 工具集文件。

 RegPkg.exe通常位于 \<*Visual Studio SDK installation path*>\VisualStudioIntegration\Tools\Bin\RegPkg.exe。 RegPkg 遵循以下语法：

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 /root：root 在指定的根下执行 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 注册。

 /regfile：FileName 创建 .reg 文件，而不是更新注册表。  不能与 /vrgfile、/rgsfile 或 /wixfile 一起使用。

 /rgsfile：FileName 创建 .rgs 文件，而不是更新注册表。  不能与 /vrgfile、/regfile 或 /wixfile 一起使用。

 /vrgfile：FileName 创建 .vrg 文件，而不是更新注册表。  不能与 /regfile、/rgsfile 或 /wixfile 一起使用。

 /rgm 除了创建 rgs 文件外，还创建 .rgm 文件。  必须与 /rgsfile 结合使用。

 /wixfile：FileName 创建Windows安装程序 XML 工具集兼容的文件，而不是更新注册表。  不能与 /regfile、/rgsfile 或 /vrgfile 一起使用。

 /codebase 强制注册 CodeBase 而不是程序集。

 /assembly 强制注册到程序集而不是 CodeBase。

 /unregister 取消注册此包。  无法使用

 使用 /regfile 或 /vrgfile 或 /rgsfile 或 /wixfile。

## <a name="see-also"></a>另请参阅
- [VSPackages](../../extensibility/internals/vspackages.md)
- [RegPkg 包注册疑难解答](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
